# OpenCLAW 飞书 API 缓存修复指南

## 问题
OpenCLAW 每分钟调用飞书 API `/open-apis/bot/v3/info` 做健康检查，1万次/月的额度当天就耗尽。

## 修复方法

### 1. 找到这个文件
```
~/.openclaw/extensions/feishu/src/probe.ts
```

### 2. 在文件开头添加缓存代码

```typescript
import { readFileSync, writeFileSync, existsSync } from "fs";

const PROBE_CACHE_TTL_MS = 24 * 60 * 60 * 1000; // 24小时缓存
const CACHE_FILE_PATH = "/root/.openclaw/extensions/feishu/probe_cache.json";

interface CacheEntry {
  result: any;
  timestamp: number;
}

function loadCache(): Map<string, CacheEntry> {
  try {
    if (existsSync(CACHE_FILE_PATH)) {
      const data = JSON.parse(readFileSync(CACHE_FILE_PATH, "utf-8"));
      return new Map(Object.entries(data));
    }
  } catch (e) {
    console.warn("[probeFeishu] Failed to load cache:", e);
  }
  return new Map();
}

function saveCache(cache: Map<string, CacheEntry>): void {
  try {
    writeFileSync(CACHE_FILE_PATH, JSON.stringify(Object.fromEntries(cache)));
  } catch (e) {
    console.warn("[probeFeishu] Failed to save cache:", e);
  }
}

const probeCache = loadCache();

function getCacheKey(cfg?: any): string {
  if (!cfg?.appId) return "no-creds";
  return `${cfg.appId}:${cfg.domain ?? "feishu"}`;
}
```

### 3. 在 probeFeishu 函数里加缓存判断

在 API 调用之前加：

```typescript
const cacheKey = getCacheKey(cfg);
const cached = probeCache.get(cacheKey);
if (cached && Date.now() - cached.timestamp < PROBE_CACHE_TTL_MS) {
  return cached.result;
}
```

在 API 调用成功之后加：

```typescript
probeCache.set(cacheKey, { result, timestamp: Date.now() });
saveCache(probeCache);
```

### 4. 重启 OpenCLAW
```bash
pkill -f openclaw && nohup openclaw > /tmp/openclaw.log 2>&1 &
```

### 5. 验证
```bash
ls -la /root/.openclaw/extensions/feishu/probe_cache.json
```

## 效果
- 修复前：1440次/天
- 修复后：1次/天

---
来自龙哥 🐉
