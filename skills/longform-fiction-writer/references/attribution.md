# 借鉴来源说明

本系统在设计和实现过程中，借鉴了以下开源项目的核心思想和设计模式。

---

## webnovel-writer

**项目地址**: https://github.com/lingfengQAQ/webnovel-writer

**作者**: lingfengQAQ

**许可证**: GPL v3

### 借鉴内容

#### 1. 防幻觉三定律

| 定律 | 说明 |
|------|------|
| 大纲即法律 | 遵循大纲，不擅自发挥 |
| 设定即物理 | 遵守设定，不自相矛盾 |
| 发明需识别 | 新实体必须入库管理 |

**来源文件**: `docs/architecture.md`

#### 2. Context Agent 上下文搜集思路

- 写作前先构建"创作任务书"
- 提供本章上下文、约束和追读力策略
- 输出可被写作步骤直接消费的执行包

**来源文件**: `webnovel-writer/agents/context-agent.md`

#### 3. 六维并行审查机制

| Checker | 检查重点 |
|---------|---------|
| High-point Checker | 爽点密度与质量 |
| Consistency Checker | 设定一致性（战力/地点/时间线） |
| Pacing Checker | Strand 比例与断档 |
| OOC Checker | 人物行为是否偏离人设 |
| Continuity Checker | 场景与叙事连贯性 |
| Reader-pull Checker | 钩子强度、期待管理、追读力 |

**来源文件**: `docs/architecture.md`, `webnovel-writer/agents/*.md`

#### 4. 追读力系统

**钩子类型分类**：
- 危机钩（Crisis Hook）
- 悬念钩（Mystery Hook）
- 情绪钩（Emotion Hook）
- 选择钩（Choice Hook）
- 渴望钩（Desire Hook）

**钩子强度分级**：
- strong / medium / weak

**微兑现类型**：
- 信息兑现、关系兑现、能力兑现、资源兑现、认可兑现、情绪兑现、线索兑现

**来源文件**: `webnovel-writer/agents/reader-pull-checker.md`

#### 5. Override Contract 申诉机制

当软约束无法遵守时，可提交"覆盖合同"，记录理由和补偿计划。

**来源文件**: `webnovel-writer/agents/reader-pull-checker.md`

#### 6. 流程硬约束设计

- 禁止并步
- 禁止跳步
- 禁止临时改名
- 禁止自创模式
- 禁止自审替代

**来源文件**: `webnovel-writer/skills/webnovel-write/SKILL.md`

---

## 致谢

感谢 webnovel-writer 项目作者 lingfengQAQ 及其贡献者，他们的开源工作为长篇网文AI辅助写作提供了宝贵的设计思路和实现参考。

---

## 使用本系统的项目

如果你的项目使用了本系统，欢迎在 README 中添加以下声明：

```markdown
本项目使用 [longform-fiction-writer](https://github.com/your-repo/longform-fiction-writer) 写作流程系统，该系统借鉴了 [webnovel-writer](https://github.com/lingfengQAQ/webnovel-writer) 的核心设计。
```