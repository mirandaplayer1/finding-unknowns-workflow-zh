# Finding-Unknowns Workflow Skills

**[繁體中文版 →](zh-TW/README.md)**｜**[English →](en/README.md)**

一套讓 Claude Code「先找出未知、再動工」的工作流 skills：從粗略想法起草規格、訪談釐清模糊、掃描盲點、交付前測驗、復盤晉升——決策與教訓都落在專案檔案裡，跨對話存活。

A workflow for Claude Code that finds your unknowns before you build: draft a spec from a rough idea, interview away the ambiguity, scan for blindspots, pass a quiz before delivery, and distill lessons afterwards — with a project file layer that makes decisions survive across conversations.

## 快速開始 / Quick start

```bash
# 繁體中文版 / Traditional Chinese
cp -R zh-TW/skills/* ~/.claude/skills/

# English
cp -R en/skills/* ~/.claude/skills/
```

或用 Claude Code plugin / or as a Claude Code plugin:

```
/plugin marketplace add mirandaplayer1/finding-unknowns-workflow-zh
/plugin install finding-unknowns-zh-tw@finding-unknowns-workflow-zh   # zh-TW
/plugin install finding-unknowns-en@finding-unknowns-workflow-zh      # English
```

裝一種語言就好，兩套的 skill 同名。/ Install one language only — the two sets share skill names.

## Credit

Workflow techniques by [Thariq Shihipar](https://claude.com/blog/a-field-guide-to-claude-fable-finding-your-unknowns) (Anthropic); packaging approach partly inspired by [Neeeophytee/finding-unknowns-skills](https://github.com/Neeeophytee/finding-unknowns-skills). Original text, MIT licensed — see [LICENSE](LICENSE).
