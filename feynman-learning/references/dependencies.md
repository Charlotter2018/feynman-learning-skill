# Optional visual skills

All three are optional. They only matter if the user reads their notes in Obsidian.

| Skill | What it adds | Source (license) |
|---|---|---|
| `mermaid-visualizer` | Architecture / flow / relationship diagrams from text | https://github.com/axtonliu/axton-obsidian-visual-skills (MIT) |
| `excalidraw-diagram` | Hand-drawn style memory card (`.excalidraw.md`, needs the Obsidian Excalidraw plugin to view) | https://github.com/axtonliu/axton-obsidian-visual-skills (MIT) |
| `json-canvas` | Obsidian Canvas knowledge map (`.canvas`) | https://github.com/kepano/obsidian-skills (MIT) |

## Install

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
