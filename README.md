# 费曼学习法 Skill（feynman-learning）

一个只做一件事的 Skill：**按费曼学习法帮你真正学会一个东西。**

你用自己的话讲一遍，它对照原始材料帮你**纠偏、打分**，再**出题考你**，直到你能讲给外行听。

> 费曼学习法：选一个概念 → 讲给完全不懂的人听 → 卡住、讲错的地方回去看材料 → 用更简单的话和类比重讲。

## 怎么用

| 你说 | 它做 |
|---|---|
| 「费曼学习 + 文章 / 文件 / 链接」 | 读完材料，请你先讲一遍 |
| 「我来讲讲：……」 | 对照材料纠偏，按 4 个维度打分：准确性 40 分、完整性 25 分、通俗性 20 分、举例类比 15 分 |
| 再讲一遍 | 重新打分，显示进步（如 62 → 85） |
| 「考考我」 | 针对你讲错、讲含糊的地方出 3–5 道题，一题一题来，逐题讲解 |
| 「到此为止」 | 三行小结：已掌握 / 还薄弱 / 下次复习什么 |

没有材料也能用：只说主题（如「费曼学习 缓存击穿」），会以公认知识为依据，并会提前说明这一点。

所有纠正都会引用原文或公认事实作为依据，不凭空判断。

## 安装

只有一个文件：`feynman-learning/SKILL.md`。把 `feynman-learning` 文件夹放进你的 Agent 的 skills 目录即可。

1. 下载 [ZIP 包](https://github.com/Charlotter2018/feynman-learning-skill/archive/refs/heads/main.zip) 并解压。
2. 把里面的 `feynman-learning/` 文件夹复制到：
   - Claude Code：`~/.claude/skills/`（Windows 为 `%USERPROFILE%\.claude\skills\`）
   - 其他支持 Agent Skills 的工具：复制到它的 skills 目录
3. 重开一个会话，说「费曼学习 + 你要学的东西」。

## License

MIT
