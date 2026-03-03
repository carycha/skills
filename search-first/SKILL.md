---
name: search-first
description: Research-First Development Workflow. Use before starting any new implementation, adding dependencies, or building custom tools to find existing high-quality libraries (npm, PyPI, GitHub) and avoid reinventing the wheel. 「先搜尋再開發」流程。
---

# Search-First：開發前先行研究

此技能將「在實作前搜尋現有解決方案」的工作流程系統化，以避免重新造輪子，並充分利用經過驗證的社群函式庫。

## 工作流程

觸發後，請執行以下步驟：

### 1. 需求分析
- 明確定義需要什麼功能。
- 確定程式語言（如 TypeScript, Python）與框架（如 React, FastAPI）的限制。
- 使用 `grep_search` 或 `glob` 檢查專案中是否已存在類似的工具。

### 2. 並行搜尋
使用 `google_web_search` 在以下管道尋找候選方案：
- **套件註冊表**：npm, PyPI, Crates.io 等。
- **開源專案**：GitHub 儲存庫與模板。
- **生態系統工具**：MCP 伺服器或專業的 CLI 工具。

*提示：請參閱 [references/shortcuts.md](references/shortcuts.md) 取得分類搜尋關鍵字。*

### 3. 評估與決策
使用 `web_fetch` 分析候選方案的說明文件，並根據以下標準評分：
- **功能性**：是否能解決特定問題？
- **維護狀況**：最近的提交紀錄、版本歷史。
- **授權條款**：優先選擇 MIT, Apache 2.0。

| 訊號 | 行動 |
|--------|--------|
| 完全符合且維護良好 | **採用 (Adopt)** — 直接安裝並使用。 |
| 部分符合，基礎良好 | **擴展 (Extend)** — 安裝並撰寫精簡的封裝層 (Wrapper)。 |
| 多個弱符合項 | **組合 (Compose)** — 結合多個專注於單一功能的小型套件。 |
| 找不到合適方案 | **自建 (Build)** — 在參考研究結果的基礎上撰寫自定義程式碼。 |

### 4. 實作
- 安裝選定的套件（如 `npm install <package>`）。
- 若無合適套件，則運用研究過程中發現的模式來實作自定義解決方案。

## 範例

### 範例：「添加失效連結檢查」
1. **搜尋**：`google_web_search("npm markdown dead link checker")`
2. **評估**：`textlint-rule-no-dead-link` 維護良好且符合需求。
3. **行動**：`npm install textlint-rule-no-dead-link`。

## 反模式
- **直接動手寫程式**：在檢查是否存在現有工具前就開始撰寫工具類程式。
- **依賴膨脹**：為了實現一個微小功能而安裝龐大的套件。
- **過度自定義**：對函式庫進行重度封裝，導致失去其原本的優勢。
