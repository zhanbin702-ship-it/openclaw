# 章节状态表模板

保存为 `tracking/chapter-status.csv`

```csv
章节,门禁,结构复核,去AI化复核,硬检查,状态,备注,标签
V01-C001,done,pass,done,pass,draft,no,基线
V01-C002,done,pass,done,pass,draft,no,基线
V01-C003,done,pass,done,pass,draft,no,基线
V01-C004,done,pass,done,pass,draft,no,重写起点
...
```

## 字段说明

| 字段 | 说明 | 可选值 |
|------|------|--------|
| 章节 | 章节编号 | V01-C001, V02-C041 等 |
| 门禁 | 写前门禁是否完成 | done / pending |
| 结构复核 | 结构复核是否通过 | pass / fail / pending |
| 去AI化复核 | 去AI化复核是否通过 | pass / fail / pending |
| 硬检查 | 写后硬检查是否通过 | pass / fail / pending |
| 状态 | 章节当前状态 | draft / review / final |
| 备注 | 备注信息 | 自由文本 |
| 标签 | 分类标签 | 基线 / 重写起点 / 等 |