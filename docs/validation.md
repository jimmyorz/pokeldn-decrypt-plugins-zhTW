# 驗證紀錄與來源

## 翻譯基準

- 上游專案：[`Decryptu/pokeldn`](https://github.com/Decryptu/pokeldn)。
- 基準版本：pokeldn **0.39.1**／Plugins API **1.11**。
- 語言包版本：**1.0.5**。
- 基準 commit：[`a3e6f5be826d00ca8f9202a8c73ceb77d20f8ee0`](https://github.com/Decryptu/pokeldn/tree/a3e6f5be826d00ca8f9202a8c73ceb77d20f8ee0)。
- [該版本的英文範本](https://github.com/Decryptu/pokeldn/blob/a3e6f5be826d00ca8f9202a8c73ceb77d20f8ee0/pokeldn/app/data/strings.en.toml)。
- [該版本的語言包格式說明](https://github.com/Decryptu/pokeldn/blob/a3e6f5be826d00ca8f9202a8c73ceb77d20f8ee0/docs/plugins.md)。

2026-10-25 檢查時，上游 `main` 為上述 commit。英文快照與上游 Git blob 相符，中文對照與 `language-pack/strings.toml` 相同。來源版本及檔案雜湊見 [`reference/upstream.json`](../reference/upstream.json)。

## 本次同步範圍

- 從 pokeldn 0.36.0 的 `716eb85478b7e752335f1a1f029e710d9a35a335` 同步至上述 0.39.1 基準。
- 主英文表新增 12 個鍵、移除 2 個鍵，其中兩組為原文改寫後更換鍵值；其餘既有原文與格式變數未變。已補齊「讀取我的資料」、頭目寶可夢及《火紅／葉綠》獨立配信的介面翻譯，並同步替換兩筆舊原文對照。
- 補上 `frlg-gift:--save-to-board` 與 `rse-gift:--save-to-board` 的選項說明；後者是預覽功能共用啟動器的選項。
- 補上異色傳說寶可夢強化的名稱、操作及倒數說明，以及強化組合的顯示衝突與容量不足訊息。
- 補上頭目摘要標記，以及 PKHeX 服務新增的頭目限制與條件不符訊息。
- 已比較 40 個工具的 ID、啟動器及選項；除新增的兩個選項說明外，未發現既有工具 ID、選項名稱或說明因移除、搬移、改名而失效。
- 語言包格式、載入與替換規則，以及 PKHeX 的 `zh-TW` 至 `zh-Hant` 對應未變。PKHeX.Core 版本仍為 26.8.26。

## 檢查結果

- 通過上游 `scripts/check_language_pack.py`：主字串缺漏 0、多餘鍵值 0、格式變數差異 0；工具說明未知鍵值 0。
- 檢查全部 1,705 個主字串的變數名稱、格式規格、轉換方式及執行期格式化；保留 `{name!r}` 等轉換方式。
- 通過既有 14 組訊息樣本、新增 10 組模組文字與動態訊息樣本，以及 5 組頭目錯誤訊息樣本。倒數說明使用上游實際產生的文字，並檢查兩項、三項強化衝突及容量不足的情況。
- 確認摘要中的異色與頭目標記能同時顯示中文。訓練家紀錄保留 `trainer=`、`TID=`、`SID=`，已驗證上游可遮蔽中文訓練家名稱及 ID。
- 使用既有 PKHeX 名稱資料快照驗證術語替換（合併後 2,279 筆），並檢查道具名稱未被局部改寫；未啟動實際 PKHeX 服務。
- 通過上游封裝檢查、隔離資料目錄安裝，以及儲存語言設定後在新程序載入中文。
- 1.0.5 包內共 8 個檔案，與 `language-pack/` 逐一相同，不包含驗證報告。來源清單與參照資料中的版本、檔案大小及封裝雜湊一致。
- 本版宣告 Plugins API 1.11，已在 0.39.1 原始碼上驗證載入。[0.39.0 的 API 宣告](https://github.com/Decryptu/pokeldn/blob/v0.39.0/pokeldn/plugins.py) 已為 1.11，因此 README 標示最低版本為 0.39.0；只支援較舊 API 的版本無法安裝本包。

## 已知限制

- 全部 2,170 個工具選項說明中，已翻譯 536 個，其餘 1,634 個仍使用英文。
- 「讀取我的資料」的結果與紀錄直接插入 `console_trainer.title()` 的英文遊戲名稱，未先套用術語翻譯；日期使用固定的 `%d %b %Y` 格式。這些部分需由上游提供在地化處理，僅新增語言包對照不會生效。
- 未經翻譯流程的底層輸出、開發板診斷報告與原始錯誤內容仍保留英文。
- 本次未在完整圖形介面或真實 Switch／開發板上實測，也未驗證所有遊戲情境。上游調整過面板寬度與欄位排列，窄視窗及手機顯示仍需抽查。

後續更新方式見 [maintenance.md](maintenance.md)。驗證報告供維護使用，並非語言包載入所需檔案，不隨 `.pokeplugin` 發布。
