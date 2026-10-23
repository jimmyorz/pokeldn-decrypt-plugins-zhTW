# 更新參照

## 基準與可編輯來源

`reference/upstream.json` 記錄目前英文基準的來源 commit 與檔案雜湊。`reference/strings.en.toml` 是該 commit 的快照，並不會自動跟隨上游更新。

`language-pack/` 保存可重新打包的完整來源。`reference/strings.zh-TW.toml` 是主字串的備用對照；修改 `language-pack/strings.toml` 時也應同步更新此副本，以免兩份內容分歧。

| 檔案 | 對照方式 |
| --- | --- |
| `strings.toml` | 依上游英文表的完整鍵值配對 |
| `messages.toml` | 英文原文 → 中文，部分與主字串重疊 |
| `help.toml` | `工具 ID:選項名稱` → 中文說明 |
| `terms.toml` | 完整英文術語 → 中文術語 |
| `templates.toml` | 含具名變數的英文範本 → 中文範本 |

## 更新流程

1. 取得新版上游原始碼，記錄 commit，先比較舊 `reference/strings.en.toml` 與新版英文表。除了新增與刪除鍵值，也要檢查同一鍵值的英文內容是否變更。
2. 更新 `language-pack/strings.toml`。保留所有鍵值、格式變數名稱、轉換方式及格式規格，例如 `{value0}`、`{name!r}`、`{value0:02X}`。
3. 依新版原始碼檢查補充資源。`messages.toml` 與 `templates.toml` 依賴原文字面內容，`help.toml` 依賴工具 ID 與選項名稱；它們不能只靠主英文表判斷是否仍有效。
4. 在已安裝依賴的上游原始碼目錄執行下列檢查，將路徑換成此儲存庫的實際位置。

   ```sh
   python scripts/check_language_pack.py /path/to/pokeldn-decrypt-plugins-zhTW/language-pack
   ```

   此工具只在格式變數不符時回傳失敗；仍須檢查列出的缺漏、多餘鍵值及未翻譯說明，並保留變數的格式規格與轉換方式。
5. 同步中英文參照、`reference/upstream.json`、README 中的翻譯對應版本、更新日期與涵蓋數量，以及驗證紀錄。若產出新版，先提高 `plugin.toml` 的版本，使用上游 `scripts/pack_plugin.py` 打包至 `packages/`，再同步來源清單的版本、下載 URL、檔案大小與 SHA-256。
6. 在隔離資料目錄安裝新版，選取 App language，完整重開程式並抽查介面。主介面可翻譯不代表每個動態訊息與遊戲情境都已驗證。

## 版本保存方式

`packages/pokeldn-zh-TW-1.0.0.pokeplugin` 保留最初交付檔案的原始位元組；目前 `language-pack/` 的九個檔案與 1.0.1 包的解壓內容逐一相同。請以新版本號提供之後修改的包，不要用不同內容覆寫既有版本。

原分支的簽章指紋及發佈腳本不適用於本語言包，已移除。本儲存庫直接保存可下載的包並提供 `pokeldn-source.json`，不需要沿用原本的版本發佈流程。
