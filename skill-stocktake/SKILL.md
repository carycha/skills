---
name: skill-stocktake
description: Skill Library Auditor. Use for periodic auditing and optimization of the Gemini CLI skill library (Quick Scan or Full Stocktake) to ensure quality and remove redundancy. 「技能庫盤點與優化」
---

# skill-stocktake

此技能用於審核 `~/.gemini/skills/` 下的所有 Agent Skills，透過 AI 的整體判斷 (Holistic Judgment) 確保技能庫的精簡與效能。

## 執行模式

- **快速掃描 (Quick Scan)**：當 `results.json` 存在時，僅針對上次審核後有異動的檔案進行評估 (5–10 min)。
- **全面盤點 (Full Stocktake)**：執行完整審核，重新評估所有技能 (20–30 min)。

## 審核流程 (Workflow)

### Phase 1: 庫存清點 (Inventory)

執行腳本獲取候選清單：
```bash
bash scripts/scan.sh
```
若為 Quick Scan，改用：
```bash
bash scripts/quick-diff.sh scripts/results.json
```

### Phase 2: 品質評估 (Quality Evaluation)

讀取每一項技能，並對照 [評估指南](references/evaluation-guide.md) 進行評分。
- **Chunk 處理**：建議每批次處理 20 個技能，以維持 Context 精準度。
- **中間結果**：每批次結束後執行 `save-results.sh` 存檔。

### Phase 3: 總結報告

產生摘要表格，列出所有技能的 Verdict (Keep/Improve/Update/Retire/Merge) 與原因。

### Phase 4: 整合建議

根據 Verdict 執行以下操作（需經用戶確認）：
- **Retire/Merge**：具體說明重疊之處並建議移除或合併。
- **Improve/Update**：提供具體的修改建議。

## 注意事項

- **緩存路徑**：`scripts/results.json` (或位於技能目錄下)。
- **技術驗證**：若涉及過時的 API 或工具，必須使用 `google_web_search` 進行核實。
- **精簡原則**：若 `GEMINI.md` 或 `MEMORY.md` 已經涵蓋該內容，應優先建議 Retire。
