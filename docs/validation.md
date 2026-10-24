# 驗證紀錄與來源

## 翻譯基準

- 上游專案：[`Decryptu/pokeldn`](https://github.com/Decryptu/pokeldn)。
- 基準版本：pokeldn **0.36.0**／Plugins API **1.10**。
- 語言包版本：**1.0.4**。
- 基準 commit：[`716eb85478b7e752335f1a1f029e710d9a35a335`](https://github.com/Decryptu/pokeldn/tree/716eb85478b7e752335f1a1f029e710d9a35a335)。
- [該版本的英文範本](https://github.com/Decryptu/pokeldn/blob/716eb85478b7e752335f1a1f029e710d9a35a335/pokeldn/app/data/strings.en.toml)。
- [該版本的語言包格式說明](https://github.com/Decryptu/pokeldn/blob/716eb85478b7e752335f1a1f029e710d9a35a335/docs/plugins.md)。

2026-10-24 檢查時，上游 `main` 為上述 commit。英文快照與上游 Git blob 相符，中文對照與 `language-pack/strings.toml` 相同。來源版本及檔案雜湊見 [`reference/upstream.json`](../reference/upstream.json)。

## 本次同步範圍

- 從 pokeldn 0.35.0 的 `7d1258a04c4f777bb446ae2cc47ddfdf45a99dd5` 同步至上述 0.36.0 基準。
- 主英文表新增 7 個鍵值；沒有刪除鍵值，也沒有既有原文或格式變數變更。已補齊新增介面翻譯。
- 補上 `swsh-gift:--save-to-board` 選項說明，以及開發板資訊收集、複製、錯誤與移除禮物等 6 種應用程式訊息（2 筆原文對照、4 個動態範本）。
- 檢查變動的介面、遊戲模組、神秘禮物、工具與 Plugins API 來源；未發現現有翻譯使用的工具 ID、選項名稱或原文因移除、搬移、改名而失效。
- 語言包格式、載入與替換規則，以及 PKHeX 的 `zh-TW` 至 `zh-Hant` 對應未變。Plugins API 1.10 新增的寶可夢交換內容編輯功能不改變語言資源格式。

## 檢查結果

- 通過上游 `scripts/check_language_pack.py`：主字串缺漏 0、多餘鍵值 0、格式變數差異 0；工具說明未知鍵值 0。
- 檢查全部 1,695 個主字串的變數名稱、格式規格、轉換方式及執行期格式化。
- 通過既有 8 組訊息樣本，以及新增 6 組 `[app]` 訊息的實際替換檢查，包含裝置名稱、檔案路徑與錯誤內容的保留。
- 使用既有 PKHeX 名稱資料快照驗證術語替換（合併後 2,279 筆）；未啟動實際 PKHeX 服務。
- 通過上游封裝檢查、隔離資料目錄安裝，以及儲存語言設定後在新程序載入中文。
- 1.0.4 包內共 8 個檔案，與 `language-pack/` 逐一相同，不包含驗證報告。來源清單、參照資料與本次報告中的版本及封裝雜湊一致。
- 宣告 Plugins API 1.10 的語言包可由 pokeldn 0.36.0 載入；pokeldn 0.35.0 因僅支援 1.9 而拒絕。本版最低需求已在根目錄 README 標示。

## 已知限制

- 全部 2,168 個工具選項說明中，已翻譯 534 個，其餘 1,634 個仍使用英文。
- 未經翻譯流程的底層輸出、開發板診斷報告與原始錯誤內容仍保留英文。
- 本次未在完整圖形介面或真實 Switch／開發板上實測，也未驗證所有遊戲情境。

後續更新方式見 [maintenance.md](maintenance.md)。驗證報告供維護使用，並非語言包載入所需檔案，不隨 `.pokeplugin` 發布。
