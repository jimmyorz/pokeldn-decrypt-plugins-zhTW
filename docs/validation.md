# 驗證紀錄與來源

## 翻譯基準

- 上游專案：[`Decryptu/pokeldn`](https://github.com/Decryptu/pokeldn)。
- 基準版本：pokeldn **0.45.0**／Plugins API **1.12**。
- 語言包版本：**1.0.8**。
- 基準 commit：[`1e26b4c6560923a9ad3ee419ec8aab717bc669d2`](https://github.com/Decryptu/pokeldn/tree/1e26b4c6560923a9ad3ee419ec8aab717bc669d2)。
- 最新正式版 0.45.0 的 commit 為 `bd876979a75a676943b87fe05e7a1ac268dabf30`；本次 main 基準僅多了 AltStore 發行清單更新，翻譯相關內容與正式版相同。
- [基準英文範本](https://github.com/Decryptu/pokeldn/blob/1e26b4c6560923a9ad3ee419ec8aab717bc669d2/pokeldn/app/data/strings.en.toml)。
- [基準語言包格式說明](https://github.com/Decryptu/pokeldn/blob/1e26b4c6560923a9ad3ee419ec8aab717bc669d2/docs/plugins.md)。

2026-10-26 檢查時，上游 main 為上述基準 commit。語言包更新前的 repo commit 為 `65a2c302ae204cc059425aed09a8ce147fb56682`。

## 更新前的基準核對

- 原本 `reference/upstream.json` 記錄的 0.43.0 基準 commit、英文 Git blob SHA、英文與中文 SHA-256、主字串數量及 1.0.7 套件版本與 SHA-256 均與實際檔案一致；英文快照也與該上游 commit 相同。
- 1.0.7 包內七個檔案均與更新前來源相同，包含既有遊戲文件側邊欄翻譯，沒有來源與套件不同步的情況。
- 本次新增 1.0.8 套件，保留既有 1.0.0 至 1.0.7 套件的原始位元組。更新後的版本與雜湊見 [reference/upstream.json](../reference/upstream.json)。

## 本次同步範圍

- 從 0.43.0 基準 `d11d881d20306d1064c6bd0f76bf5bd1ef3fedc3` 比較至本次基準，共 14 個 commit、28 個變更檔案。
- 主英文表新增 25 個鍵，總數由 1,766 增為 1,791；沒有刪除鍵，既有鍵沒有原文、格式變數、轉換方式或格式規格變更。補齊遊戲活動分類、主機角色、連線與模式選項，以及《劍／盾》LAN 極巨團體戰與極巨大冒險的名稱、說明及操作步驟。
- 「你的主機」選項從 Switch 的角度描述：`role=host` 顯示「加入」，代表 pokeldn 開房；`role=join` 顯示「開房」，代表 pokeldn 加入。集友圈的模式沿用「藍樂活任務」與「野生寶可夢」。
- 工具由 42 增為 46 個，新增 `swsh-lan-raid-host`、`swsh-lan-raid-join`、`swsh-lan-lair-host`、`swsh-lan-lair-join`。原有工具 ID、選項名稱、啟動器與欄位識別未移除或改名。
- help 為四個新工具補上 20 筆既有 LAN 說明，另將新增的 `--lan-max-players` 說明套用至六個加入工具，共新增 26 筆，總數為 607；既有 581 筆保持原樣。四個新工具另有 48 筆既有中文說明可透過 messages 回退套用。團體戰或極巨大冒險的搜尋人數預設為 4，交換預設為 2。
- 上游工具說明鍵由 2,368 增為 2,708，新增的 340 個鍵主要來自新工具共用既有選項；去重後只有一段新原文，不能將全部新增鍵視為新寫的說明。
- messages 的 1,666 筆原文、templates 的 43 筆範本與 terms 的 110 筆術語保持原樣。各遊戲模組、神秘禮物描述及既有動態範本未出現需要替換或移除的翻譯來源；文件側邊欄標題、父子關係與隱藏設定未變。
- Plugins API 由 1.11 升至 1.12，新增工具的 `activity`、`variant` 與檢查規則；本語言包不註冊工具，不受這些新規則影響。語言包格式、載入、替換與封裝規則未變；PKHeX 的 `zh-TW` 至 `zh-Hant` 對應未變，PKHeX.Core 仍為 26.8.26。
- Android USB 燒錄、LAN 連線關閉與團體戰通訊修正，以及 CI 與 AltStore 更新，不需修改翻譯。

## 檢查結果

- 在 `POKELDN_PREVIEW=1` 下執行本次基準的 `scripts/check_language_pack.py`：主字串缺漏 0、多餘鍵值 0、格式變數名稱差異 0；未知工具說明鍵值 0。
- 全部 1,791 個主字串均通過執行期格式化。另比較變數名稱、數量、轉換方式與格式規格，唯一允許的既有例外仍是 `gts.open_until_offer_answered_3c9d1f` 的 `{value2:.0}`；已檢查 0、1、2、100 筆時不顯示多餘的 s。圖鑑數字比例仍使用半形斜線。
- 已確認 25 筆新增主字串與確認稿相同，既有 1,766 筆主字串保持原樣。messages、templates 與 terms 的檔案位元組均未改變。
- 驗證活動分類與選項顯示、主機角色方向，以及四個新增 LAN 工具的中文名稱、說明、不需開發板的設定與頻道欄位排除。
- 驗證 26 筆新增 help 與新工具的 48 筆 messages 回退翻譯可正確套用；既有 20 筆文件側邊欄翻譯仍可套用。
- 使用既有 PKHeX 名稱快照檢查 2,279 筆合併名稱對照，並抽查禮物動態描述與頭目限制訊息；未啟動實際 PKHeX 服務。
- 使用本次基準的上游封裝工具打包，保留 `exclude = ["README.md"]`。包內只有 `LICENSE`、`plugin.toml` 與五個翻譯 TOML，共 7 個檔案，逐一與來源比對一致，沒有 README.md 或驗證報告。
- 通過隔離資料目錄安裝、儲存語言設定與新程序載入，並確認安裝後可讀取新增主字串、LAN 選項說明與既有側邊欄翻譯，且沒有 README.md。
- 套件大小為 130,381 位元組；版本、Plugins API、來源清單、英文 Git blob SHA、各檔案 SHA-256 與封裝內容一致。既有套件均保持原始位元組。
- Plugins API 宣告為 1.12，最低可安裝版本改為支援該 API 的 pokeldn 0.44.0；本次完整翻譯基準為 0.45.0，較新功能是否存在仍取決於使用的 pokeldn 版本。

## 已知限制

- 含預覽功能在內共有 2,708 個工具選項說明，help 直接翻譯 607 個；其餘 2,101 個未另設工具專用對照，部分可使用 messages 回退，其餘顯示英文。
- 銀行能力表的 HP、Atk、Def、SpA、SpD、Spe 為上游程式碼直接定義的固定文字，未呼叫翻譯函式，因此現有語言包翻譯不會套用。目前保留英文縮寫；若上游未來支援翻譯，須再確認中文欄位標題是否能在現有寬度內完整顯示。
- PKSM 匯入摘要與版本不支援、檔案不完整等錯誤直接顯示原始文字；新增 messages 或 templates 目前不會生效。
- Showdown 匯出配置由上游產生英文，保留以供匯入使用。隨機交換紀錄的標題可以翻譯，但後面的寶可夢摘要仍取自原始資料。
- GTS 的部分交換條件與拒絕原因未經語言包替換。銀行批次刪除提示中的名稱與名稱排序仍使用原始資料。
- 「讀取我的資料」的遊戲名稱與日期、未接入翻譯流程的底層輸出、開發板診斷、原始錯誤，以及新增的 `[lan]`、`[sw]` 紀錄仍有英文。
- 銀行的 `bank.file_unreadable_0fd8f4` 仍可能顯示上游傳入的英文複數字尾 s，本次未調整。
- Plugins API 1.12 新增的工具活動分類與選項組合檢查錯誤，以及 LAN 診斷日誌，直接顯示原文，未經語言包替換。
- 本次未在完整 GUI、真實 Switch 或開發板上實測，也未驗證實際 PKHeX 服務、PKSM 檔案匯入或 LAN 交換、團體戰與極巨大冒險。新選項按鈕的中文寬度與換行仍待完整 GUI 確認。

後續更新方式見 [maintenance.md](maintenance.md)。驗證文件不隨 `.pokeplugin` 發布。
