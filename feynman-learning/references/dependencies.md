# Optional visual skills

All three are optional. They only matter if the user reads their notes in Obsidian.

| Skill | What it adds | Source (license) |
|---|---|---|
| `mermaid-visualizer` | Architecture / flow / relationship diagrams from text | https://github.com/axtonliu/axton-obsidian-visual-skills (MIT) |
| `excalidraw-diagram` | Hand-drawn style memory card (`.excalidraw.md`, needs the Obsidian Excalidraw plugin to view) | https://github.com/axtonliu/axton-obsidian-visual-skills (MIT) |
| `json-canvas` | Obsidian Canvas knowledge map (`.canvas`) | https://github.com/kepano/obsidian-skills (MIT) |

## Install

First check `git --version`.

- **git available** → use the commands below.
- **git missing** → do not try to install git yourself. Tell the user git is needed for the one-command install and recommend they set it up themselves:
  - macOS: run `xcode-select --install`, or `brew install git`
  - Windows: download from https://git-scm.com/download/win (or `winget install --id Git.Git -e`)
  - Linux: the distro package manager, e.g. `sudo apt install git`
  Then offer the no-git alternative: download the ZIPs, unzip, and copy the skill folders into the skills folder:
  - https://github.com/axtonliu/axton-obsidian-visual-skills/archive/refs/heads/main.zip → `mermaid-visualizer/`, `excalidraw-diagram/`
  - https://github.com/kepano/obsidian-skills/archive/refs/heads/main.zip → `skills/json-canvas/`
  If the user prefers to do it later, set `"visual_skills": "declined"` and continue; they can say "安装可视化 skill" any time.


Use the skills folder of the agent the user is running. Claude Code: `~/.claude/skills`. Other agents: use their documented skills folder and replace `SKILLS_DIR` below.

macOS / Linux:

```bash
SKILLS_DIR="$HOME/.claude/skills"
TMP="$(mktemp -d)"
git clone --depth 1 https://github.com/axtonliu/axton-obsidian-visual-skills "$TMP/axton"
git clone --depth 1 https://github.com/kepano/obsidian-skills "$TMP/kepano"
mkdir -p "$SKILLS_DIR"
cp -R "$TMP/axton/mermaid-visualizer" "$TMP/axton/excalidraw-diagram" "$SKILLS_DIR/"
cp -R "$TMP/kepano/skills/json-canvas" "$SKILLS_DIR/"
rm -rf "$TMP"
ls "$SKILLS_DIR"/{mermaid-visualizer,excalidraw-diagram,json-canvas}/SKILL.md
```

Windows (PowerShell):

```powershell
$SkillsDir = "$HOME\.claude\skills"
$Tmp = Join-Path $env:TEMP ("fl-" + [guid]::NewGuid())
git clone --depth 1 https://github.com/axtonliu/axton-obsidian-visual-skills "$Tmp\axton"
git clone --depth 1 https://github.com/kepano/obsidian-skills "$Tmp\kepano"
New-Item -ItemType Directory -Force $SkillsDir | Out-Null
Copy-Item -Recurse "$Tmp\axton\mermaid-visualizer","$Tmp\axton\excalidraw-diagram" $SkillsDir
Copy-Item -Recurse "$Tmp\kepano\skills\json-canvas" $SkillsDir
Remove-Item -Recurse -Force $Tmp
```

If a skill folder already exists, skip it instead of overwriting.
