# 驗證紀錄與來源

## 翻譯基準

- 上游專案：[`Decryptu/pokeldn`](https://github.com/Decryptu/pokeldn)。
- 沿用 1.0.9 的基準版本：pokeldn **0.45.3**／Plugins API **1.12**。
- 語言包版本：**1.1.0**，為 1.0.9 的簽章補充版。
- 基準 commit：[`d39467c9159042b5e96f22a9054f607ecef3d6b6`](https://github.com/Decryptu/pokeldn/tree/d39467c9159042b5e96f22a9054f607ecef3d6b6)。
- 1.0.9 檢查時，上游 main 已標示 0.45.3，正式 Release 仍為 0.45.2，commit 為 `545fb1c6a10ac93c2bbda7a5a226ccf9eb313806`；依維護者確認，以 0.45.3 原始碼發佈。本次未重新查詢上游 main 或 Release，下次同步上游時再確認發佈狀態。
- [基準英文範本](https://github.com/Decryptu/pokeldn/blob/d39467c9159042b5e96f22a9054f607ecef3d6b6/pokeldn/app/data/strings.en.toml)。
- [基準語言包格式說明](https://github.com/Decryptu/pokeldn/blob/d39467c9159042b5e96f22a9054f607ecef3d6b6/docs/plugins.md)。

本次驗證日期為 2026-10-27。語言包更新前的 repo commit 為 `06c4bf710eec64f2bbce9473523c3067e3f0306f`。

## 本次範圍與基準核對

- 本次不檢查上游更新、不修改翻譯，也不升級 Plugins API；使用既有 0.45.3 基準原始碼的封裝、簽章與安裝流程。`docs/maintenance.md` 保持原樣。
- 已確認原 1.0.9 套件 SHA-256、英文與中文檔案 SHA-256 均符合原參照紀錄；原套件的七個檔案與更新前來源逐一相同。
- `plugin.toml` 只將版本由 1.0.9 改為 1.1.0，其餘設定保持原樣。五份翻譯 TOML、`LICENSE`、中英文參照快照及 `language-pack/README.md` 均保持原始位元組。
- `reference/upstream.json` 只更新 `package_version` 與 `package_sha256`；上游 commit、版本、Plugins API、檢查日期、英文 Git blob SHA、中英文 SHA-256、字串數量及其它欄位均保持不變。
- 保留既有 1.0.0 至 1.0.9 封裝檔的原始位元組，新增 `packages/pokeldn-zh-TW-1.1.0.pokeplugin`。本次跨版至 1.1.0，下一版由 **1.1.1** 開始。

## 簽章與封裝驗證

- 已確認提供的既有私鑰為 Ed25519，公開簽章指紋為 **`ZP2X-THRM-26HS-XL2C`**；未產生或更換金鑰。
- 使用既有基準的 `scripts/pack_plugin.py` 搭配 `--key` 封裝，執行時強制只讀取已存在的金鑰，禁止工具自動建立新金鑰。
- 保留 `exclude = ["README.md"]`。包內只有 `plugin.toml`、五個翻譯 TOML、`LICENSE` 與 `plugin.sig`，共 **8 個檔案**；未包含 README、驗證報告或私鑰。
- 七個來源檔案逐一與封裝內容相同；與原 1.0.9 套件比較，唯一差異是 `plugin.toml` 的版本號及新增的 `plugin.sig`，五份翻譯與授權檔完全相同。
- 透過上游套件讀取及簽章驗證函式確認 Ed25519 簽章有效、指紋一致；另確認修改翻譯檔案或版本號後，原簽章會驗證失敗。
- 套件大小為 **131,056 位元組**；`pokeldn-source.json` 的版本、Plugins API、下載網址、大小與 SHA-256，以及 `reference/upstream.json` 的套件版本與 SHA-256 均與實際封裝一致。

## 安裝與翻譯載入驗證

- 使用兩個獨立資料目錄，分別驗證全新安裝，以及先安裝未簽章的 1.0.9 再升級至 1.1.0；上游可正確辨識為更新，升級後保留已選取的語言。
- 兩種情況均確認簽章有效、安裝程式記住正確公開金鑰，之後同一套件的信任狀態為同一作者。上游安裝時驗證封裝簽章並保存公開金鑰，不會將 `plugin.sig` 留在安裝目錄。
- 兩種情況均儲存啟用及語言設定，再啟動新程序；確認載入 1.1.0／Plugins API 1.12、語系為 `zh-TW`，且所有翻譯資源與封裝來源一致。抽查「你的交換提案」與「火紅／葉綠」可正確顯示中文。
- 以既有基準、`POKELDN_PREVIEW=1` 執行 `scripts/check_language_pack.py`：主字串缺漏 0、多餘鍵值 0、格式變數名稱差異 0；未知工具說明鍵值 0。2,101 個未另設專用對照的工具說明維持原狀，未視為新增翻譯。
- 全部 1,794 個主字串通過執行期格式化；變數名稱、數量、轉換方式與格式規格一致。唯一既有例外仍為 `gts.open_until_offer_answered_3c9d1f` 的 `{value2:.0}`，另驗證 0、1、2、100 筆時不顯示多餘的 s。
- Plugins API 維持 1.12，最低可安裝版本仍為 pokeldn 0.44.0；本次實際驗證使用沿用的 0.45.3 基準，未另行測試 0.44.0。
- 本次未重新檢查上游差異、遊戲模組、文件側邊欄來源或 PKHeX 名稱資料，也未執行完整 GUI、實際硬體或外部服務測試；未將 1.0.9 的測試結果列為本次通過。

## 已知限制

以下沿用 1.0.9 的翻譯限制，本次未重新掃描相關上游來源。

- 含預覽功能在內共有 2,708 個工具選項說明，help 直接翻譯 607 個；其餘 2,101 個未另設工具專用對照，部分可使用 messages 回退，其餘顯示英文。
- 銀行能力表的 HP、Atk、Def、SpA、SpD、Spe 為上游程式碼直接定義的固定文字，未呼叫翻譯函式，因此現有語言包翻譯不會套用。目前保留英文縮寫；若上游未來支援翻譯，須再確認中文欄位標題是否能在現有寬度內完整顯示。
- PKSM 匯入摘要與版本不支援、檔案不完整等錯誤直接顯示原始文字；新增 messages 或 templates 目前不會生效。
- Showdown 匯出配置由上游產生英文，保留以供匯入使用。隨機交換紀錄的標題可以翻譯，但後面的寶可夢摘要仍取自原始資料。
- GTS 的部分交換條件、拒絕原因，以及重複提出交換時的錯誤訊息未經語言包替換。銀行批次刪除提示中的名稱與名稱排序仍使用原始資料。
- 「讀取我的資料」的遊戲名稱與日期、未接入翻譯流程的底層輸出、開發板診斷、原始錯誤，以及 `[lan]`、`[sw]` 紀錄仍有英文。
- 銀行的 `bank.file_unreadable_0fd8f4` 仍可能顯示上游傳入的英文複數字尾 s，本次未調整。
- Plugins API 1.12 新增的工具活動分類與選項組合檢查錯誤，以及 LAN 診斷日誌，直接顯示原文，未經語言包替換。
- 本次未在完整 GUI、真實 Switch 或開發板上實測，也未驗證實際 PKHeX 服務、PKSM 檔案匯入或 LAN 交換、團體戰與極巨大冒險。既有 GTS 提示與較長操作說明的排版仍待完整 GUI 確認。


後續更新方式見 [maintenance.md](maintenance.md)。驗證文件不隨 `.pokeplugin` 發布。
