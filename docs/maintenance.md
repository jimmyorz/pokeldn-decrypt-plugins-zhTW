# 更新參照

## 基準與可編輯來源

`reference/upstream.json` 記錄目前英文基準的來源 commit 與檔案雜湊。`reference/strings.en.toml` 是該 commit 的快照，並不會自動跟隨上游更新。

`language-pack/` 保存可重新打包的完整來源。`reference/strings.zh-TW.toml` 是主字串的備用對照；修改 `language-pack/strings.toml` 時也應同步更新此副本，以免兩份內容分歧。

`docs/validation.md` 記錄目前語言包的檢查結果、檢查範圍與限制。此文件供維護使用，pokeldn 不會讀取，也不應放入 `language-pack/` 或封裝進 `.pokeplugin`。報告只記錄實際執行的檢查，不保留臨時測試包標記，也不沿用舊版本的檢查結果。

正式發行版與翻譯基準 commit 的差異（例如已翻譯但尚未正式發布的功能）集中記錄在 `docs/validation.md`，兩份 README 不重複這類暫時性說明。下次同步上游時，先確認這些功能是否已納入正式版，再更新該紀錄；`reference/upstream.json` 仍記錄實際採用的基準 commit。

| 檔案 | 對照方式 |
| --- | --- |
| `strings.toml` | 依上游英文表的完整鍵值配對 |
| `messages.toml` | 英文原文 → 中文，部分與主字串重疊 |
| `help.toml` | `工具 ID:選項名稱` → 中文說明 |
| `terms.toml` | 完整英文術語 → 中文術語 |
| `templates.toml` | 含具名變數的英文範本 → 中文範本 |

## 更新流程

1. 先確認 `reference/upstream.json` 記錄的 commit、英文檔案雜湊與 `reference/strings.en.toml` 一致；不一致時先回報，不可直接覆蓋基準。取得新版上游原始碼，記錄版本、Plugins API 與 commit，再比較新版英文表。除了新增與刪除鍵值，也要檢查同一鍵值的英文內容、格式變數、轉換方式及格式規格是否變更。
2. 更新 `language-pack/strings.toml`。保留所有鍵值、格式變數名稱、轉換方式及格式規格，例如 `{value0}`、`{name!r}`、`{value0:02X}`。唯一已確認的格式規格例外是 `gts.open_until_offer_answered_3c9d1f` 的 `{value2:.0}`：此變數只承載英文複數字尾，保留變數但不顯示內容；驗證時須另外檢查 0、1、多筆的結果，不可放寬其他字串。斜線兩側均為中文時使用全形 `／`，英文字母或數字之間使用半形 `/`；格式變數須確認實際代入內容。
3. 依新版原始碼檢查補充資源。`messages.toml` 與 `templates.toml` 依賴原文字面內容，`help.toml` 依賴工具 ID 與選項名稱；它們不能只靠主英文表判斷是否仍有效。範圍包含介面訊息、各遊戲模組、神秘禮物內容、動態描述與工具選項，不限於先前檢查過的固定檔案。另確認語言包格式、Plugins API、載入與替換規則，以及 PKHeX 名稱語系處理有無改變；提高 API 宣告前須確認最低可安裝的 pokeldn 版本。

   文件側邊欄標題取自上游 `docs/*.md` 的 `title` 欄位，透過 `i18n.message()` 查詢 `messages.toml`，不會自動套用 `terms.toml`。僅翻譯遊戲主分類標題及其子頁面標題，其它文件分類、子頁面與文件內文均保留上游英文。新增的遊戲文件標題翻譯統一放在 `language-pack/messages.toml` 底部的 `# 文件側邊欄－遊戲標題與子頁面` 區塊，既有翻譯不搬移或重複新增。新增前須核對上游文件的 `title`、`parent` 與 `nav_exclude` 欄位，只補充正常顯示於側邊欄且尚未翻譯的遊戲相關標題；英文鍵值必須與上游原文完全一致，包含大小寫、標點與空白，不得自行建立原文變體。每次同步上游時，須檢查遊戲相關文件標題是否新增、刪除、更名或調整父子關係，並同步維護翻譯；若上游修改文件標題的翻譯處理方式，須重新確認是否仍需透過 `messages.toml` 提供對照。

4. 在已安裝依賴的上游原始碼目錄執行下列檢查，將路徑換成此儲存庫的實際位置。

   ```sh
   POKELDN_PREVIEW=1 python scripts/check_language_pack.py /path/to/pokeldn-decrypt-plugins-zhTW/language-pack
   ```

   此工具只在格式變數不符時回傳失敗；仍須檢查列出的缺漏、多餘鍵值及未翻譯說明，並保留變數的格式規格與轉換方式。
5. 同步中英文參照及文件：根目錄 README 的翻譯對應版本、更新日期、語言包版本、Plugins API、最低版本與下載連結；`language-pack/README.md` 的涵蓋數量與來源連結；`CHANGELOG.md` 的中文更新內容。README 不放本地測試過程或臨時測試包資訊。下載標籤維持「下載最新 pokeldn 繁體中文（台灣）語言包」，只更新連結中的版本。
6. 產出新版時，提高 `plugin.toml` 的版本，使用對應上游的 `scripts/pack_plugin.py` 打包至 `packages/`。保留 `plugin.toml` 的 `exclude = ["README.md"]`；確認包內只有 `plugin.toml`、五個翻譯 TOML 與 `LICENSE`，逐一比對來源內容，且沒有 README.md 或驗證報告，再同步 `pokeldn-source.json` 的版本、Plugins API、下載 URL、檔案大小與 SHA-256。
7. 在隔離資料目錄驗證安裝、選取語言及新程序載入；能操作圖形介面與硬體時再抽查實際畫面及功能。將實際檢查結果寫入 `docs/validation.md`，未執行的項目須明確記錄，不能沿用舊版的通過狀態。
8. 最後更新 `reference/upstream.json` 的上游版本、commit、Plugins API、檢查日期、英文 Git blob SHA 與 SHA-256，並從本次檔案重新計算 `chinese_sha256`、`package_sha256`、`package_version` 及字串數量。確認它們與中文對照、封裝檔、來源清單及驗證報告一致。這些資料不會因重新打包而自動更新；即使經使用者同意覆寫相同版本，也必須同步更新。

## 版本保存方式

既有 `packages/` 封裝檔保留原始位元組；1.0.6 包內七個檔案均與 `language-pack/` 的對應來源相同。README.md 保留在儲存庫，透過 `plugin.toml` 的 `exclude` 排除；驗證報告也不放入封裝。後續修改請使用新版本號，只有使用者明確要求時才覆寫既有版本。

原分支的簽章指紋及發佈腳本不適用於本語言包，已移除。本儲存庫直接保存可下載的包並提供 `pokeldn-source.json`，不需要沿用原本的版本發佈流程。
