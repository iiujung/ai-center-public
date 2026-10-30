# 共用/

## 放什麼
各公司都用得到的東西。目前只有 Skill：`工具/技能/<名字>/`。內建兩個：`kb-setup`（從零訪談建庫）、`kb-migrate`（搬舊知識庫進來）。

## Skill 怎麼放、怎麼用
- 實體只有一份，在 `~/AI-Center/ai-company/共用/工具/技能/<名字>/SKILL.md`。名字用小寫英文、數字和單個連字符；`SKILL.md` 開頭寫 frontmatter，至少兩項：`name`（和資料夾名一樣）、`description`（什麼時候用）。
- 哪家公司要用，就在那家公司的資料夾掛相對路徑軟連結（在 `~/AI-Center/ai-company` 執行）：
  - Claude Code 讀：`ln -s ../../../共用/工具/技能/<名字> <公司>/.claude/skills/<名字>`
  - Codex、Gemini 等其他 AI 讀：`ln -s ../../../共用/工具/技能/<名字> <公司>/.agents/skills/<名字>`
  - 用相對路徑，整個 `AI-Center` 搬到哪，連結照樣有效。
- Windows 建不了軟連結時：先試開「開發人員模式」再用 `New-Item -ItemType SymbolicLink`；還是不行就用目錄接合點（junction，`New-Item -ItemType Junction`，記的是完整路徑，搬家後要重建，並把 `.claude/skills/`、`.agents/skills/` 寫進 `.gitignore`）。
- 只想給一家公司用的 Skill，也放這裡，只在那家公司掛連結就好。
- 改 Skill 只改這裡的實體，掛連結的地方不用動；改之前想一下別家公司也在用，不要寫死某家公司的路徑。需要分公司的地方，寫成「所在公司的…」並列出各家的位置。
- 腳本找金鑰：`REPO_ROOT = SKILL_DIR.parents[3]`，也就是 repo 根的 `.env`。

## 不放什麼
不放某家公司自己的資料、品牌規範、最佳實踐（放回各公司的 `工具/最佳實踐/`）。
