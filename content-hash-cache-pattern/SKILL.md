---
name: content-hash-cache-pattern
description: Content-Hash Cache Pattern Expert. Use when the user needs to implement efficient, path-independent caching for expensive file parsing using SHA-256 hashes to prevent redundant processing. 「內容雜湊快取模式」
---

# Content-Hash File Cache Pattern

此模式指導如何使用 SHA-256 內容雜湊作為快取鍵，來快取昂貴的檔案處理結果（如 PDF 轉換、OCR 或圖像分析）。與基於路徑的快取不同，此方法在檔案移動、重命名後仍可命中快取，並在內容更改時自動失效。

## 核心模式 (The Pattern)

1.  **內容雜湊快取鍵**：使用檔案內容（而非路徑）生成雜湊值，確保唯一性與一致性。
2.  **不可變快取條目 (Frozen Dataclass)**：使用具備槽位 (slots) 的不可變資料類別，確保快取資料的結構穩定。
3.  **基於檔案的儲存**：每個快取條目儲存為 `{hash}.json`，免去維護全域索引檔的複雜性。
4.  **服務層包裝 (SRP)**：將快取邏輯與處理邏輯分離，保持核心處理函數的純淨性。

## 何時啟動

- **檔案處理管線**：如 PDF 轉 Markdown、大型圖片 OCR。
- **高成本重複運算**：運算成本遠高於磁碟讀取成本時。
- **CLI 工具擴展**：需要實作 `--cache` 或 `--no-cache` 選項。

## 最佳實踐

- **對檔案分塊 (Chunking)**：雜湊大型檔案時應使用分塊讀取（例如 64KB），避免佔用過多記憶體。
- **錯誤優雅降級**：若快取損毀，應回傳 `None` 並視為快取未命中，而非讓系統崩潰。
- **雜湊截斷日誌**：在日誌中列印截斷後的雜湊值 (如前 12 位元) 以方便調試。

## 參考資料

- **具體 Python 實作**：[implementation.md](references/implementation.md)
- **設計決策與反模式分析**：[design.md](references/design.md)
