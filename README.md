# 费曼学习法 Skill（feynman-learning）

让 AI 当你的费曼学习教练：**你先讲 → 它找盲点、纠错 → 出题考你 → 记下你掌握了什么、哪里还薄弱**，下次按你的掌握程度出题。

适用于 Claude Code，以及其他支持 Agent Skills（`SKILL.md`）的工具。

## 它能做什么

| 阶段 | 你说 | 它做 |
|---|---|---|
| 1 多维总结（必做） | 「学习 xxx」 | 一句话总结 + 3–5 个要点 + 架构图，自动判断这份材料值不值得深学 |
| 2 费曼复述 | 「深入」 | 让你用自己的话讲给外行听，揪出含糊、跳步和误解，追问到你讲清楚 |
| 3 自适应测验 | 「测试」「考考我」 | 先读你的历史学习记录：掌握的不考定义、考应用；薄弱点换个角度再考 |
| 4 沉淀输出 | 「沉淀」 | 引导你写出自己的理解，关联已有知识 |
| 随时 | 「到此为止」 | 收口，更新学习进度 |

所有记录都是本地 Markdown 文件：每份素材一页来源页（学习阶段、盲点、测验结果写在 frontmatter 里），另有知识卡片墙、学习仪表盘和学习日志。用 Obsidian 打开体验最好，不用 Obsidian 也能用。

## 安装

macOS / Linux：

```bash
git clone --depth 1 https://github.com/Charlotter2018/feynman-learning-skill /tmp/feynman-learning-skill
mkdir -p ~/.claude/skills
cp -R /tmp/feynman-learning-skill/feynman-learning ~/.claude/skills/
```

Windows（PowerShell）：

```powershell
git clone --depth 1 https://github.com/Charlotter2018/feynman-learning-skill "$env:TEMP\feynman-learning-skill"
New-Item -ItemType Directory -Force "$HOME\.claude\skills" | Out-Null
Copy-Item -Recurse "$env:TEMP\feynman-learning-skill\feynman-learning" "$HOME\.claude\skills\"
```

其他 Agent 工具：把 `feynman-learning/` 文件夹放进对应的 skills 目录即可。

## 第一次使用

在你想存放学习笔记的文件夹（比如 Obsidian 仓库）里打开 Claude Code，说「学习 <文章链接或文件>」。第一次会先做初始化，**每一步都会先问你**：

1. **确认目录**：给出一套推荐目录结构（素材、来源页、概念页、产出物、学习进度），你确认或改名后才创建；已有同类目录会直接沿用，不会覆盖。配置写在根目录的 `.feynman-learning.json`。
2. **可选的可视化 Skill**：只有检测到你装了 Obsidian，才会问你要不要装下面三个 Skill；不装也能正常学习，架构图会直接以 Mermaid 代码块写进笔记。

| Skill | 作用 | 地址 |
|---|---|---|
| mermaid-visualizer | 架构图、流程图 | https://github.com/axtonliu/axton-obsidian-visual-skills |
| excalidraw-diagram | 手绘风认知卡片 | https://github.com/axtonliu/axton-obsidian-visual-skills |
| json-canvas | Obsidian Canvas 知识地图 | https://github.com/kepano/obsidian-skills |

默认目录结构：

```
<学习根目录>/
├── .feynman-learning.json
├── raw/                 原始素材
├── wiki/sources/        来源页（每份素材一页）
├── wiki/concepts/       概念页
├── artifacts/           架构图、认知卡片、Canvas、你的输出
└── study/               学习进度：卡片、日志、卡片墙、仪表盘
```

## 文件说明

```
feynman-learning/
├── SKILL.md                    主流程（阶段 0–5 + 进度追踪）
└── references/
    ├── setup.md                首次初始化流程
    ├── dependencies.md         可选 Skill 的地址和安装命令
    └── templates.md            仪表盘、卡片墙、日志、卡片模板
```

## License

MIT
