# Agent 技能優化最佳實踐

此分類記錄提升 Gemini CLI 技能 (Agent Skills) 觸發率、精準度及維護品質的最佳實踐。

---

## 🔧 高效技能描述 (Skill Description) 撰寫指南
**日期：** 2026-03-03
**情境：** 當技能很少自動發動或觸發不精準時。
**最佳實踐：**
- **採用「專家角色」開頭**：描述開頭應明確指定角色，例如 "REST API Design Expert" 或 "PostgreSQL Architect"，這能引導模型以該領域專家的身份介入。
- **使用「意圖導向」觸發句型**：標準化使用 `Use when the user asks to [action]...`。
- **加入具體技術動詞**：在描述中明確包含行為動詞，如 `design`, `review`, `troubleshoot`, `optimize`, `refactor`, `implement` 等。
- **多國語言語義強化**：針對中文環境，在英文描述後加入中文關鍵字（如：`「迭代檢索」模式`），協助跨語言語義匹配。
- **保持精煉 (Keep it Short)**：將描述字數維持在 2-3 句內 (100-200 字元)，減少 Token 消耗並維持核心意圖清晰。
- **排除模糊術語**：避免使用過於籠統的字眼如 "Help with data"，應改為 "Process large datasets (CSV/Parquet) for high-performance analysis"。
