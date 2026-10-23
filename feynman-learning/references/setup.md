# First-run setup

Run this only when no `.feynman-learning.json` exists in the current directory or its parents. Do the steps in order, and **do not create anything before the user confirms in step 3**.

## 1. Pick the learning root

- If the current directory, or a parent, contains a `.obsidian/` folder → that folder is an Obsidian vault; propose its root as the learning root.
- Otherwise propose the current directory, and mention the user can name any other folder.

## 2. Detect Obsidian

Obsidian counts as installed if any of these is true:
- the learning root (or a parent) contains `.obsidian/`
- macOS: `/Applications/Obsidian.app` or `~/Applications/Obsidian.app` exists
- Windows: `%LOCALAPPDATA%\Programs\Obsidian` or `%LOCALAPPDATA%\Obsidian` exists
- Linux: `obsidian` is on PATH, or `flatpak list` shows `md.obsidian.Obsidian`, or an Obsidian AppImage is in `~/Applications`

Remember the result for step 5.

## 3. Propose the folder layout and get confirmation

Show the proposed tree with the actual root path, and ask the user to confirm or rename any folder. Example:

```
<learning root>/
├── .feynman-learning.json   配置文件（记录下面各目录的位置）
├── raw/                     原始素材：文章、PDF、视频文稿
├── wiki/
│   ├── sources/             来源页：每份素材一页，学习进度写在这里
│   └── concepts/            概念页：跨素材的知识点
├── artifacts/
│   ├── diagrams/            架构图 / 关系图（Mermaid）
│   ├── visualizations/      认知卡片（Excalidraw）
│   ├── canvas/              知识地图（Canvas）
│   └── writings/            你自己的输出
└── study/                   学习进度
    ├── cards/               每个知识点一张卡片
    ├── log/                 学习日志（按月）
    ├── domains/             按领域归类
    ├── 知识卡片墙.md
    └── 学习仪表盘.md
```

Rules:
- If some of these folders already exist, reuse them; never overwrite existing files.
- If the user already has an equivalent structure (e.g. `wiki/来源/`), map to it instead of creating a parallel one.
- Ask once, wait for a clear yes (or a list of changes). No folders before that.

## 4. Create the structure

After confirmation:
1. Create the folders.
2. Create `<study>/学习仪表盘.md`, `<study>/知识卡片墙.md` and the current month's `<study>/log/YYYY-MM.md` from `references/templates.md`.
3. Write `.feynman-learning.json` in the learning root:

```json
{
  "version": 1,
  "created": "YYYY-MM-DD",
  "obsidian": true,
  "visual_skills": "pending",
  "paths": {
    "raw": "raw",
    "sources": "wiki/sources",
    "concepts": "wiki/concepts",
    "artifacts": "artifacts",
    "study": "study"
  }
}
```

`paths` are relative to the folder containing the config file; use whatever names the user confirmed.

## 5. Optional visual skills (only if Obsidian is installed)

- **Obsidian not installed** → set `"visual_skills": "not_applicable"`. Stage 1 will put diagrams inline as Mermaid code blocks. Do not mention the other skills.
- **Obsidian installed** → check whether `json-canvas`, `mermaid-visualizer` and `excalidraw-diagram` are already available (listed in your available skills, or present in the agent's skills folder, e.g. `~/.claude/skills/<name>/SKILL.md`).
  - All present → `"visual_skills": "installed"`.
  - Some missing → ask the user **once** whether to install them, showing the table and commands from `references/dependencies.md`. They are optional: without them learning still works, just without the hand-drawn card and Canvas map.
    - Yes → run the install commands, verify each `SKILL.md` exists, set `"installed"`. Tell the user the new skills take effect in a new session; until then use the inline-Mermaid fallback.
    - No → set `"declined"` and do not ask again. If they later say "安装可视化 skill", run step 5 again.

## 6. Report and continue

Tell the user what was created (tree + config path), then continue with the material they originally asked to learn (Stage 0).
