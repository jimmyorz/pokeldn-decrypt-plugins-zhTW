# 更新參照 / Maintenance reference

## 基準與可編輯來源 / Baseline and editable sources

`reference/upstream.json` 記錄目前英文基準的來源 commit 與檔案雜湊。`reference/strings.en.toml` 是該 commit 的快照，並不會自動跟隨上游更新。

`reference/upstream.json` records the English baseline's commit and hashes. `reference/strings.en.toml` is a snapshot of that commit and does not update automatically.

`language-pack/` 保存可重新打包的完整來源。`reference/strings.zh-TW.toml` 是主字串的備用對照；修改 `language-pack/strings.toml` 時也應同步更新此副本，以免兩份內容分歧。

`language-pack/` contains the complete sources for rebuilding. `reference/strings.zh-TW.toml` is a reference copy of the main translations; synchronize it whenever `language-pack/strings.toml` changes.

| 檔案 / File | 對照方式 / Matching rule |
| --- | --- |
| `strings.toml` | 依上游英文表的完整鍵值配對 / Match exact keys in the upstream English table |
| `messages.toml` | 英文原文 → 中文，部分與主字串重疊 / Literal English → Chinese, with some overlap with the main table |
| `help.toml` | `工具 ID:選項名稱` → 中文說明 / `tool ID:option` → Chinese help |
| `terms.toml` | 完整英文術語 → 中文術語 / English term → Chinese term |
| `templates.toml` | 含具名變數的英文範本 → 中文範本 / English templates with named fields → Chinese templates |

## 更新流程 / Update workflow

1. 取得新版上游原始碼，記錄 commit，先比較舊 `reference/strings.en.toml` 與新版英文表。除了新增與刪除鍵值，也要檢查同一鍵值的英文內容是否變更。
   Obtain the new upstream checkout and record its commit. Compare the old reference with the new English table, checking added/removed keys as well as changed English values under existing keys.
2. 更新 `language-pack/strings.toml`。保留所有鍵值、格式變數名稱、轉換方式及格式規格，例如 `{value0}`、`{name!r}`、`{value0:02X}`。
   Update the translations while preserving keys, field names, conversions, and format specifications such as `{value0}`, `{name!r}`, and `{value0:02X}`.
3. 依新版原始碼檢查補充資源。`messages.toml` 與 `templates.toml` 依賴原文字面內容，`help.toml` 依賴工具 ID 與選項名稱；它們不能只靠主英文表判斷是否仍有效。
   Review supplementary resources against the new source. Messages and templates depend on literal English text; help entries depend on tool IDs and option names. The main English table alone cannot validate them.
4. 在已安裝依賴的上游原始碼目錄執行下列檢查，將路徑換成此 repo 的實際位置。
   Run the following check from an upstream checkout with its dependencies installed, replacing the path with this repository's actual location.

   ```sh
   python scripts/check_language_pack.py /path/to/pokeldn-decrypt-plugins-zhTW/language-pack
   ```

   此工具只在格式變數不符時回傳失敗；仍須檢查列出的缺漏、多餘鍵值及未翻譯說明，並保留變數的格式規格與轉換方式。
   This checker exits with failure only for placeholder mismatches. Also review missing/extra keys and untranslated help, and preserve field format specifications and conversions.
5. 同步中英文參照、`reference/upstream.json`、涵蓋數量與驗證紀錄。若產出新版，先提高 `plugin.toml` 的版本，使用上游 `scripts/pack_plugin.py` 打包至 `packages/`，再同步來源清單的版本、下載 URL、檔案大小與 SHA-256。
   Synchronize both reference tables, provenance, coverage counts, and validation records. For a new package, bump the manifest version, use upstream `scripts/pack_plugin.py` to build into `packages/`, and update the source listing's version, URL, byte size, and SHA-256.
6. 在隔離資料目錄安裝新版，選取 App language，完整重開程式並抽查介面。主介面可翻譯不代表每個動態訊息與遊戲情境都已驗證。
   Install into an isolated data directory, select the app language, restart completely, and check the interface. Working interface translations do not establish coverage of every dynamic message or gameplay scenario.

## 版本保存方式 / Version preservation

`packages/pokeldn-zh-TW-1.0.0.pokeplugin` 保留最初交付檔案的原始位元組；目前 `language-pack/` 的九個檔案與 1.0.1 包的解壓內容逐一相同。請以新版本號提供之後修改的包，不要用不同內容覆寫既有版本。

The 1.0.0 package retains the exact bytes originally delivered. All nine files in `language-pack/` match the extracted 1.0.1 archive. Use a new version number for subsequent changes instead of overwriting an existing version with different content.

原 fork 的簽章指紋及發佈腳本不適用於本語言包，已移除。本 repo 直接保存可下載的包並提供 `pokeldn-source.json`，不需要沿用原本的 Publishing a version 流程。

The original fork's signing fingerprint and publishing script do not apply and have been removed. This repository stores downloadable packages directly and provides `pokeldn-source.json`; the former Publishing a version workflow is not required.
