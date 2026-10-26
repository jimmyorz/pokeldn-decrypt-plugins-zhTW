# 驗證紀錄與來源

## 翻譯基準

- 上游專案：[`Decryptu/pokeldn`](https://github.com/Decryptu/pokeldn)。
- 基準版本：pokeldn **0.45.3**／Plugins API **1.12**。
- 語言包版本：**1.0.9**。
- 基準 commit：[`d39467c9159042b5e96f22a9054f607ecef3d6b6`](https://github.com/Decryptu/pokeldn/tree/d39467c9159042b5e96f22a9054f607ecef3d6b6)。
- 檢查時上游 main 已標示 0.45.3，最新正式 Release 仍為 0.45.2，commit 為 `545fb1c6a10ac93c2bbda7a5a226ccf9eb313806`。依維護者確認，本次以 0.45.3 的原始碼內容發佈語言包；上游 Release 的建置延誤不改變本次採用的基準。下次同步時再確認正式 Release 的發佈狀態。
- [基準英文範本](https://github.com/Decryptu/pokeldn/blob/d39467c9159042b5e96f22a9054f607ecef3d6b6/pokeldn/app/data/strings.en.toml)。
- [基準語言包格式說明](https://github.com/Decryptu/pokeldn/blob/d39467c9159042b5e96f22a9054f607ecef3d6b6/docs/plugins.md)。

2026-10-27 準備發佈時再次確認，上游 main 仍為上述基準 commit。語言包更新前的 repo commit 為 `77b8fc447c6e4fc75cc48b91f330bfc3db0d8996`。

## 更新前的基準核對

- 原本 `reference/upstream.json` 記錄的 0.45.0 commit、英文 Git blob SHA、英文與中文 SHA-256、主字串數量及 1.0.8 套件 SHA-256 均與實際檔案一致；英文快照符合該上游 commit。
- 本次以已核對的 1.0.8 來源為起點，只追查基準之後的上游變更及相關顯示路徑，省略未變動內容的完整重掃。既有 `docs/maintenance.md` 規範保持原樣，仍執行發佈所需的格式、封裝、安裝與新程序載入檢查。
- 新增 1.0.9 套件，保留既有 1.0.0 至 1.0.8 套件的原始位元組。更新後的版本與雜湊見 [reference/upstream.json](../reference/upstream.json)。

## 本次同步範圍

- 從 0.45.0 基準 `1e26b4c6560923a9ad3ee419ec8aab717bc669d2` 比較至本次基準，共 78 個 commit、34 個變更檔案；多數為文件補充。
- 主英文表新增 3 個 GTS 鍵，總數由 1,791 增為 1,794；沒有刪除鍵，既有鍵沒有原文、格式變數、轉換方式或格式規格變更。新增內容為交換提案等待提示、「你的交換提案」及提案處理說明。
- 《火紅／葉綠》異色傳說寶可夢的操作說明由一段共用原文改為兩段：超夢須先自行交談，三聖鳥須在前情回顧結束後向上按一下再按住 B。messages 移除舊的一段對照，新增兩段對照，總數由 1,666 增為 1,667；其餘既有翻譯保持原樣。
- 新增的 GTS 重複提案錯誤 `Your offer on this listing is already waiting for the lister.` 經 `str(error)` 直接交給畫面顯示，未呼叫翻譯函式，因此本次不加入無法生效的對照。
- help 的 607 筆說明、templates 的 43 筆範本與 terms 的 110 筆術語保持原樣。既有傳說寶可夢倒數模板仍可使用；工具 ID、選項名稱與語言包顯示掛接方式未變。
- 文件側邊欄標題、父子關係與隱藏設定未變，既有 20 筆側邊欄補充翻譯完整保留。
- 語言包格式、Plugins API、載入、替換、封裝與 PKHeX 名稱語系處理的相關來源未變，Plugins API 維持 1.12。
- macOS 圖示、異色自動按鍵的底層修正、建置設定及通訊研究文件更新，不需另外翻譯。

## 檢查結果

- 在 `POKELDN_PREVIEW=1` 下執行本次基準的 `scripts/check_language_pack.py`：主字串缺漏 0、多餘鍵值 0、格式變數名稱差異 0；未知工具說明鍵值 0。
- 全部 1,794 個主字串均通過執行期格式化。另比較變數名稱、數量、轉換方式與格式規格，唯一允許的既有例外仍是 `gts.open_until_offer_answered_3c9d1f` 的 `{value2:.0}`；已檢查 0、1、2、100 筆時不顯示多餘的 s。圖鑑數字比例仍使用半形斜線。
- 3 筆新增主字串與確認稿相同，既有 1,791 筆主字串保持原樣。messages 僅替換上述操作說明；help、templates 與 terms 的檔案位元組均未改變。
- 實際呼叫本次上游的傳說寶可夢描述產生函式，確認超夢與三聖鳥兩個分支產生的完整英文，均與新 messages 鍵一致，並可正確套用確認的中文譯文。既有 20 筆側邊欄翻譯仍可套用。
- 使用本次基準對應的上游封裝工具打包，保留 `exclude = ["README.md"]`。包內只有 `LICENSE`、`plugin.toml` 與五個翻譯 TOML，共 7 個檔案，逐一與來源比對一致，沒有 README.md 或驗證報告。
- 通過隔離資料目錄安裝、儲存語言設定與新程序載入，並確認安裝後可讀取新增 GTS 字串、兩段傳說寶可夢操作說明與既有側邊欄翻譯，且沒有 README.md。
- 套件大小為 130,808 位元組；版本、Plugins API、來源清單、英文 Git blob SHA、各檔案 SHA-256 與封裝內容一致。既有套件及 `docs/maintenance.md` 均保持原始位元組。
- Plugins API 維持 1.12，最低可安裝版本仍為 pokeldn 0.44.0；本次完整翻譯基準為 0.45.3，較新功能是否存在仍取決於使用的 pokeldn 版本。
- PKHeX 相關來源未變，本次未重跑名稱資料快照測試，也未啟動實際 PKHeX 服務。

## 已知限制

- 含預覽功能在內共有 2,708 個工具選項說明，help 直接翻譯 607 個；其餘 2,101 個未另設工具專用對照，部分可使用 messages 回退，其餘顯示英文。
- 銀行能力表的 HP、Atk、Def、SpA、SpD、Spe 為上游程式碼直接定義的固定文字，未呼叫翻譯函式，因此現有語言包翻譯不會套用。目前保留英文縮寫；若上游未來支援翻譯，須再確認中文欄位標題是否能在現有寬度內完整顯示。
- PKSM 匯入摘要與版本不支援、檔案不完整等錯誤直接顯示原始文字；新增 messages 或 templates 目前不會生效。
- Showdown 匯出配置由上游產生英文，保留以供匯入使用。隨機交換紀錄的標題可以翻譯，但後面的寶可夢摘要仍取自原始資料。
- GTS 的部分交換條件、拒絕原因，以及重複提出交換時的錯誤訊息未經語言包替換。銀行批次刪除提示中的名稱與名稱排序仍使用原始資料。
- 「讀取我的資料」的遊戲名稱與日期、未接入翻譯流程的底層輸出、開發板診斷、原始錯誤，以及 `[lan]`、`[sw]` 紀錄仍有英文。
- 銀行的 `bank.file_unreadable_0fd8f4` 仍可能顯示上游傳入的英文複數字尾 s，本次未調整。
- Plugins API 1.12 新增的工具活動分類與選項組合檢查錯誤，以及 LAN 診斷日誌，直接顯示原文，未經語言包替換。
- 本次未在完整 GUI、真實 Switch 或開發板上實測，也未驗證實際 PKHeX 服務、PKSM 檔案匯入或 LAN 交換、團體戰與極巨大冒險。新增 GTS 提示與較長操作說明的排版仍待完整 GUI 確認。

後續更新方式見 [maintenance.md](maintenance.md)。驗證文件不隨 `.pokeplugin` 發布。
