---
name: feynman-learning
description: |
  Feynman-technique learning coach: summarizes a source, has the user explain it back, finds blind spots, quizzes adaptively based on past mastery, and tracks progress (mastered concepts, weak areas) in a local Markdown / Obsidian knowledge base. Use whenever the user wants to learn, study, deeply understand, test their understanding of, or internalize an article, document, video transcript, or concept. Triggers: "学习", "深入学习", "费曼", "测试我", "考考我", "沉淀", "萃取", "learn", "study", "quiz me", "test my understanding", "feynman".
---

# Feynman Learning

A learning coach built on the Feynman Technique: **explain it simply → expose gaps → go back to the source → repeat until fluent**. It keeps a record of what the user has mastered and where they are weak, so every quiz gets more targeted.

## Step 0: Load or create the learning space (ALWAYS FIRST)

Look for `.feynman-learning.json` in the current directory, then in parent directories.

- **Found** → read it. All paths below (`<raw>`, `<sources>`, `<concepts>`, `<artifacts>`, `<study>`) are relative to the directory containing that file and come from its `paths` field.
- **Not found** → this is the first run. Read `references/setup.md` and run the setup flow there **before doing anything else**. Setup must get the user's explicit confirmation before creating any folder or file.

Never hard-code paths; always use the configured ones.

## Stage 0: Ingest the material

Input can be a file, a URL, pasted text, or an existing source page.

- If it is already a page in `<sources>/`, use it.
- Otherwise:
  1. Save the original into `<raw>/` (file copy, fetched article as Markdown, or pasted text as `YYYY-MM-DD 标题.md`).
  2. Create a source page `<sources>/YYYY-MM-DD 标题.md` with frontmatter (`source:` link or raw path, `created:` date, `learning_stage: 0_indexed`) and a short neutral abstract.

## Stage 1: Multi-dimensional summary [REQUIRED]

1. Read the source page and the raw material.
2. **Assess priority** and save it as `learning_priority`:
   - high: ≥5 new concepts, conflicts with what the user knows, strongly actionable, or a framework / methodology, or the user says it is important
   - medium: useful but not critical
   - low: informational, single concept, reference material
   Tell the user the level and why, and let them override.
3. **One-sentence summary**: why it matters, not just what it says.
4. **3–5 core points**.
5. **Visuals** — depends on `visual_skills` in the config:
   - `installed`: use `mermaid-visualizer` for an architecture / flow diagram → `<artifacts>/diagrams/YYYY-MM-DD-标题-架构.md`; use `excalidraw-diagram` for a hand-drawn memory card → `<artifacts>/visualizations/YYYY-MM-DD-标题-卡片.excalidraw.md`; if the content has ≥3 interconnected concepts, use `json-canvas` for a knowledge map → `<artifacts>/canvas/YYYY-MM-DD-标题.canvas`.
   - anything else: write one Mermaid diagram as a fenced ```mermaid block directly in the source page (renders in Obsidian, GitHub, VS Code). Skip the card and canvas.
6. Add to the top of the source page: the one-sentence summary and a `## 学习产出` section linking every artifact.
7. Update frontmatter:
   ```yaml
   learning_stage: 1_summarized
   learning_priority: high | medium | low
   learning_completed:
     - stage1_summary: YYYY-MM-DD
   learning_artifacts: [...]
   ```
8. Show the result right away, then offer next steps:
   ```markdown
   ## ✅ 阶段 1 完成：多维总结
   ### 📌 一句话总结
   > ...
   ### 📊 产出物
   | 类型 | 文件 |
   |------|------|
   ### 🧠 核心要点
   ...
   ### 🎯 下一步
   - ✅ 「到此为止」— 快速学习完成
   - 🟠 「深入」— 阶段 2：用你的话讲给我听
   - 🔴 「测试」— 阶段 3：考考你
   ```
   For high-priority content, recommend going deeper.

## Stage 2: Feynman rehearsal [OPTIONAL]

Trigger: "深入" / "深入学习" / auto-suggest after Stage 1 for high priority.

1. Ask: 「请用你自己的话，向一个外行解释 [核心概念]。」 Let the user answer freely.
2. Find blind spots: vague words (大概、可能、应该是), logic jumps (A → C without B), and misunderstandings.
3. Probe each one: 「你刚才说 X，能具体说说为什么吗？」「这和你前面说的 Y 是什么关系？」
4. Correct with quotes from the source, the "why", and an analogy or example.
5. Ask for a re-explanation until it is clear and accurate.
6. Record in the source page:
   ```markdown
   ## 学习记录
   ### 盲点与纠正
   - [盲点]: [纠正]
   ### 关键洞察
   - ...
   ```
   ```yaml
   learning_stage: 2_rehearsed
   learning_notes:
     blind_spots: [...]
     key_insights: [...]
   ```
7. Sync progress (see "Progress tracking").

## Stage 3: Adaptive testing [OPTIONAL]

Trigger: "测试" / "考考我" / "quiz me" / auto-suggest after Stage 2.

1. **Build the user's knowledge model first**: read every page in `<sources>/` that has `learning_notes` or `learning_quiz`, and collect `key_insights`, `weak_areas`, `mastered_concepts` (≥80% accuracy) and past `test_level`. Note concepts shared with earlier sources.
2. **3–5 questions, quality over quantity**:
   - already mastered → no definition questions; ask application (「在你的场景里怎么用 X？」), synthesis (「X 和 Y 的本质区别？」) or trade-off questions (「只能保留三个要素，选哪三个，为什么？」)
   - new concepts → foundational understanding and mechanism
   - weak areas → targeted review from a different angle than last time
3. Ask one question at a time and wait for the answer.
4. Give feedback immediately: confirm and deepen if right; if wrong or incomplete, explain why and cite the source.
5. Score it and update frontmatter:
   ```yaml
   learning_stage: 3_tested
   learning_quiz:
     questions_total: 5
     questions_correct: 4
     accuracy: 80%
     weak_areas: [...]
     mastered_concepts: [...]
     test_level: basic | intermediate | advanced
   ```
6. Sync progress.

## Stage 4: Internalization [OPTIONAL]

Trigger: "沉淀" / "internalize" / auto-suggest after a good quiz.

1. Reflection prompts: 「这和你之前的认知有什么联系？」「能用它解决什么实际问题？」「如果要教别人，你会怎么组织？」
2. The user writes the output (summary, connection map, or action plan); help organize it. If `visual_skills` is `installed`, `mermaid-visualizer` can draw the connection map.
3. Save to `<artifacts>/writings/YYYY-MM-DD-标题-我的理解.md`.
4. If the insight adds value, append a `## 个人洞察` section to the related page in `<concepts>/` (create the concept page if missing).
5. `learning_stage: 4_internalized`; sync progress.

## Stage 5: Done

When the user says "到此为止" or finishes the stages they want: set `learning_stage: 5_completed` with the date, and sync progress.

## Progress tracking

Folder: `<study>/` (created during setup; layout in `references/setup.md`).

**When to sync** (required): after Stage 2 corrections, after a Stage 3 quiz, and when the user says "到此为止". After Stage 1 only, it is enough to add one log line and mark the card `learning`.

**What to write**:
1. `<study>/cards/<知识点>.md` — frontmatter `type: learning-card`, `domain`, `status` (`todo | learning | practiced | mastered`), `updated`, `sources`, `artifacts`. Body: one-sentence summary / links to the source page and artifacts / corrected misconceptions / how to apply it. Do **not** copy the full source content — a card is progress + corrections + links.
2. Prepend one line to `<study>/log/YYYY-MM.md` (newest first).
3. Refresh `<study>/知识卡片墙.md` and `<study>/domains/<领域>.md`: each card shows only the concept name plus a small date or 「待学习」.
4. Update counts and recent log lines in `<study>/学习仪表盘.md`.

## Rules

- Respect the user's pace: stop whenever they say "到此为止"; jump directly to a stage if asked (e.g. "只要测试").
- Show results in the conversation; never update files silently.
- Before any quiz, always read the learning history first.
- Never create folders or install anything without the user's confirmation.
