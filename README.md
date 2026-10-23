# pokeldn 繁體中文（台灣）語言包
# pokeldn Traditional Chinese (Taiwan) Language Pack

為 [pokeldn](https://github.com/Decryptu/pokeldn) 提供符合台灣用語與寶可夢中文社群習慣的繁體中文介面。本 repo 專門維護語言包、翻譯來源及更新參照。

A community Traditional Chinese (Taiwan) language pack for [pokeldn](https://github.com/Decryptu/pokeldn), using Taiwanese terminology and familiar Pokémon terms. This repository maintains the package, editable translations, and reference files for future updates.

**版本 / Version:** `1.0.1` · **語系 / Locale:** `zh-TW` · **外掛 ID / Plugin ID:** `community-zh-tw`

以 pokeldn **0.35.0 / Plugin API 1.9** 為製作及檢查基準。這是社群翻譯，非 pokeldn 或寶可夢官方發布。

Prepared and checked against pokeldn **0.35.0 / Plugin API 1.9**. This is a community translation, not an official pokeldn or Pokémon release.

## 下載與安裝 / Download and installation

**[下載 / Download pokeldn-zh-TW-1.0.1.pokeplugin](https://raw.githubusercontent.com/jimmyorz/pokeldn-decrypt-plugins-zhTW/main/packages/pokeldn-zh-TW-1.0.1.pokeplugin)**

1. 開啟 **Plugins → Add a plugin**，選擇下載的 `.pokeplugin`，依畫面提示完成安裝。
   Open **Plugins → Add a plugin**, select the downloaded `.pokeplugin`, and complete the installation prompts.
2. 前往 **Settings → App language**，選擇 **繁體中文（台灣）語言包**。
   Go to **Settings → App language** and select **繁體中文（台灣）語言包**.
3. **完整退出 pokeldn，再重新開啟。**
   **Quit pokeldn completely, then launch it again.**

> **安裝或啟用外掛不會自動切換語言。** 如果介面仍是英文，請確認已完成第 2、3 步。「App language」控制介面語言，與訓練家／寶可夢的語言設定不同。
>
> **Installing or enabling the plugin does not automatically change the app language.** If the interface remains in English, check steps 2 and 3. “App language” controls the interface and is separate from the trainer/Pokémon language setting.

也可在 **Plugins → Sources** 加入 `jimmyorz/pokeldn-decrypt-plugins-zhTW`，再到 **Browse** 安裝本語言包，之後同樣需要選取介面語言並重新啟動。本包未簽章，並非原 fork 作者簽署的外掛。

Alternatively, add `jimmyorz/pokeldn-decrypt-plugins-zhTW` under **Plugins → Sources**, then install the language pack from **Browse**. You must still select the app language and restart. This package is unsigned; it is not signed by the author of the original fork source.

## 翻譯範圍 / Translation coverage

| 資源 / Resource | 範圍 / Coverage |
| --- | --- |
| 主介面 / Main interface | 1,688 個字串，與基準英文表的鍵值完全對應 / 1,688 strings matching every key in the baseline English table |
| 原文對照 / Literal messages | 1,641 筆，部分與主介面重疊 / 1,641 entries, partly overlapping with interface strings |
| 進階選項說明 / Tool help | 533 個常用說明 / 533 commonly used help entries |
| 遊戲與社群術語 / Game and community terms | 109 筆 / 109 entries |
| 動態訊息 / Dynamic message templates | 31 筆 / 31 entries |

採用「異色、個體值、努力值、特性、招式、配信、太晶團體戰、集友圈」等用語，相關欄位保留 IV、EV、PID 等縮寫。完整用語表與限制見 [語言包說明](language-pack/README.md)。

Terminology includes 異色 (Shiny), 個體值 (IVs), 努力值 (EVs), 特性 (Abilities), 招式 (Moves), 配信 (event distribution), 太晶團體戰 (Tera Raid Battles), and 集友圈 (Union Circle). Familiar abbreviations such as IV, EV, and PID are retained where useful. The [package notes](language-pack/README.md) contain the detailed Chinese glossary and limitations.

寶可夢種類、招式、特性等名稱在程式支援的位置使用 PKHeX 的繁體中文資料；本包未另行收錄完整的 PKHeX 名稱資料。

Pokémon species, moves, abilities, and related names use PKHeX's Traditional Chinese data where supported by the app. This package does not redistribute the complete PKHeX name tables.

### 尚未翻譯的範圍 / Remaining English content

- 基準版本的 2,167 個工具說明中，仍有 1,634 個主要涉及底層通訊與診斷的說明未翻譯。
  Of 2,167 tool-help entries in the baseline, 1,634 remain in English, mainly low-level communication and diagnostics.
- 使用文件、原始通訊紀錄、檔名、設定儲存值、尚未收錄的模組訊息及第三方外掛文字，仍可能保留英文。
  Documentation, raw communication logs, filenames, stored settings, uncovered module messages, and third-party plugins may remain in English.
- 33 個主介面值刻意保留原文，包括縮寫、指令、純變數排列及可匯入的 Showdown 範例。
  33 interface values intentionally remain unchanged, including abbreviations, commands, placeholder-only strings, and importable Showdown examples.
- 兩個原始訊息會由程式直接傳入英文複數字尾 `s`，純資料語言包無法移除；詳見語言包說明。
  Two upstream messages pass an English plural suffix `s` as a value; a data-only language pack cannot remove it. See the package notes.

## 檔案配置 / Repository layout

| 路徑 / Path | 用途 / Purpose |
| --- | --- |
| [`packages/`](packages/) | 可安裝的原始 `.pokeplugin` 檔 / Original installable package |
| [`language-pack/`](language-pack/) | 與 1.0.1 包內一致的可編輯來源，含主字串及所有補充 TOML / Editable sources matching the 1.0.1 archive, including all supplementary TOML resources |
| [`reference/strings.en.toml`](reference/strings.en.toml) | 製作時的上游英文基準 / Upstream English baseline |
| [`reference/strings.zh-TW.toml`](reference/strings.zh-TW.toml) | 同一基準的完整中文對照，內容與 `language-pack/strings.toml` 相同 / Complete Chinese counterpart, identical to `language-pack/strings.toml` |
| [`reference/upstream.json`](reference/upstream.json) | 上游 commit、檔案雜湊與比對結果 / Upstream commit, file hashes, and comparison results |
| [`docs/maintenance.md`](docs/maintenance.md) | 後續更新與檢查方式 / Updating and validation notes |

`language-pack/messages.toml`、`help.toml`、`terms.toml`、`templates.toml` 即為額外補充翻譯，均以可編輯文字保存。對照檔中的中文檔名為 `strings.zh-TW.toml`；安裝包使用 `strings.toml`，由 `plugin.toml` 指定，兩者內容相同。

The supplementary translations are stored as editable `messages.toml`, `help.toml`, `terms.toml`, and `templates.toml` in `language-pack/`. The Chinese reference file is named `strings.zh-TW.toml`; the package uses `strings.toml`, as declared in `plugin.toml`. Their contents are identical.

## 驗證與來源 / Validation and sources

上游基準為 [`Decryptu/pokeldn@7d1258a`](https://github.com/Decryptu/pokeldn/tree/7d1258a04c4f777bb446ae2cc47ddfdf45a99dd5)。2026-10-23 再次確認上游 `main` 仍為同一 commit，英文檔案 Git blob SHA 亦相符。主字串缺漏、多餘鍵值與格式變數差異均為 0；另通過封裝、安裝及重新啟動程序的語言載入檢查。完整圖形介面與所有遊戲功能未經全面測試。

The baseline is [`Decryptu/pokeldn@7d1258a`](https://github.com/Decryptu/pokeldn/tree/7d1258a04c4f777bb446ae2cc47ddfdf45a99dd5). On 2026-10-23, upstream `main` still pointed to that commit, and the English file's Git blob SHA matched. There are zero missing keys, extra keys, or format-field differences in the main string table. Package validation, installation, and language loading in a fresh process passed. The complete GUI and all game features have not been exhaustively tested.

- [上游英文範本 / Upstream English template](https://github.com/Decryptu/pokeldn/blob/main/pokeldn/app/data/strings.en.toml)
- [語言包格式 / Language-pack documentation](https://github.com/Decryptu/pokeldn/blob/main/docs/plugins.md)
- [原始檢查紀錄 / Original validation record](language-pack/validation.json)

## 版本紀錄 / Changelog

- **1.0.1**：外掛名稱改為「繁體中文（台灣）語言包」，翻譯內容不變。
  Renamed the plugin to “繁體中文（台灣）語言包”; translations are unchanged.
- **1.0.0**：初版。 / Initial version.

## 授權 / License

翻譯內容衍生自 pokeldn，依 **AGPL-3.0-or-later** 提供，完整條款見 [LICENSE](LICENSE)。寶可夢及相關名稱屬各權利人所有。

The translations are derived from pokeldn and provided under **AGPL-3.0-or-later**; see [LICENSE](LICENSE). Pokémon and related names belong to their respective rights holders.
