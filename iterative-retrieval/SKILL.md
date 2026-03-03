---
name: iterative-retrieval
description: Codebase Context Retrieval Expert. Use when the user needs a deep understanding of a codebase, or when a sub-agent fails due to missing context. Implements a 4-phase refined search (Dispatch-Evaluate-Refine-Loop) for high-precision file discovery. 「迭代檢索」模式。
---

# Iterative Retrieval Pattern

此技能指導如何在多 Agent 工作流中，透過「派發-評估-精煉-循環」四階段，逐步獲取高品質且精準的代碼上下文。

## 核心流程 (The 4-Phase Loop)

請遵循以下步驟進行上下文檢索，最多執行 3 次循環：

### Phase 1: DISPATCH (派發)

執行初步的廣度搜尋。利用 `grep_search` 或 `glob` 搜尋潛在相關文件。
- **目標**：獲取候選檔案清單。
- **技巧**：不要一開始就過度精確。

```bash
# 範例：搜尋認證相關模式
grep_search(pattern: 'authentication|user|session', include: 'src/**/*.ts')
```

### Phase 2: EVALUATE (評估)

對檢索出的檔案內容進行評分 (0.0 - 1.0)。
- **High (0.8-1.0)**：直接實作目標功能。
- **Medium (0.5-0.7)**：包含相關模式或類型定義。
- **Low (0.2-0.4)**：僅略微相關。
- **None (0-0.2)**：不相關，應排除。

### Phase 3: REFINE (精煉)

根據評估結果更新搜尋標準。
- **新增關鍵字**：從評分高的檔案中提取新術語 (例如：發現 codebase 使用 `throttle` 而非 `rate-limit`)。
- **更新排除路徑**：將確認不相關的路徑加入 `exclude_pattern`。
- **鎖定缺口**：識別當前上下文仍缺少的邏輯或依賴。

### Phase 4: LOOP (循環)

若尚未獲得足夠上下文（通常為 3 個以上 High 分數檔案且無關鍵缺口），則帶入新條件回到 Phase 1。**上限為 3 次循環**。

## 最佳實踐

1. **從廣到窄**：第一輪通常用來了解專案的術語慣例 (Terminology)。
2. **識別缺口**：明確指出「我現在還缺什麼」，這能驅動下一輪的高效檢索。
3. **見好就收**：獲得 3 個高相關性檔案通常優於 10 個中等相關檔案。
4. **排除信心**：勇敢排除低相關性文件，避免 Context 污染。

## 參考資料

- 查看具體案例 (Bug Fix & Feature Implementation): [examples.md](references/examples.md)
- 涉及子 Agent 派發邏輯：請參考 `codebase_investigator` 工具。
