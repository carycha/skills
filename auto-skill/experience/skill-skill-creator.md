## 🔧 技能移植與 Gemini CLI 格式優化
**日期：** 2026-03-01
**技能：** skill-creator
**情境：** 將外部 Markdown 格式的技能 (如 search-first) 移植並優化為 Gemini CLI 專屬 Agent Skill。
**解法：**
- **Trigger 轉移**：將原始 Markdown 中的 Trigger 章節移除，改寫入 YAML frontmatter 的 `description` 中，以符合 Gemini CLI 的觸發機制。
- **Progressive Disclosure**：將次要內容（如搜尋快捷關鍵字）移至 `references/` 目錄下，保持 `SKILL.md` 核心流程精簡，減少 Context 消耗。
- **工具映射**：將抽象的工作流程步驟對應到 Gemini CLI 的具體工具（如 `google_web_search`, `web_fetch`, `grep_search`）。
- **打包流程**：使用 `package_skill.cjs` 進行驗證與打包，若環境缺少 `zip` 指令，腳本會自動回退至 `tar` 處理。
- **在地化**：在翻譯 `SKILL.md` 時，同步更新 `references/` 中的檔案，確保術語與路徑引用一致。
**關鍵檔案/路徑：**
- `/home/carycha/.gemini/skills/[skill-name]/SKILL.md`
- `/home/carycha/.gemini/skills/[skill-name]/references/`
**keywords：** migration, translation, progressive-disclosure, packaging
