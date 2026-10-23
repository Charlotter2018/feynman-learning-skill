# Starter templates

Replace `YYYY-MM-DD` / `YYYY-MM` with real dates. Use Obsidian wiki links (`[[...]]`); they still read fine as plain text elsewhere.

## `<study>/学习仪表盘.md`

```markdown
---
type: learning-dashboard
updated: YYYY-MM-DD
---

# 学习仪表盘

| 状态 | 数量 |
|------|------|
| 待学习 todo | 0 |
| 学习中 learning | 0 |
| 已练习 practiced | 0 |
| 已掌握 mastered | 0 |

## 薄弱点（来自测验）

- （暂无）

## 最近学习

- （暂无，学习后自动更新）

入口：[[知识卡片墙]] · 日志在 `log/`
```

## `<study>/知识卡片墙.md`

```markdown
---
type: learning-card-wall
updated: YYYY-MM-DD
---

# 知识卡片墙

每张卡片只显示知识点名称 + 日期（或「待学习」），点进去看详情。

## 学习中

## 已掌握

## 待学习
```

## `<study>/log/YYYY-MM.md`

```markdown
# 学习日志 YYYY-MM

<!-- 最新在上：- YYYY-MM-DD [[知识点]] 阶段 N · 一句话收获 -->
```

## `<study>/cards/<知识点>.md`

```markdown
---
type: learning-card
domain: 领域
status: learning
updated: YYYY-MM-DD
sources: ["[[来源页]]"]
artifacts: []
---

# 知识点

**一句话**：...

**来源**：[[来源页]]

## 纠正过的认知

- 原来以为 ... → 实际上 ...

## 怎么用

- ...
```
