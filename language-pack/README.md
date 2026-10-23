# pokeldn 繁體中文（台灣）語言包

版本：1.0.2 · 語系：`zh-TW` · 外掛 ID：`community-zh-tw`

此語言包採用台灣繁體中文軟體用語、寶可夢官方譯名與台灣玩家熟悉的術語。這是社群翻譯，非 pokeldn 或寶可夢官方發布。

本版為本地測試版：左側選單的「寶可夢銀行」縮短為「銀行」，頁面標題維持原文。

## 安裝

1. 開啟 pokeldn，前往側邊選單底部的 **Plugins**，按 **Add a plugin**，選擇 `pokeldn-zh-TW-1.0.2.pokeplugin`。也可將檔案拖入 **Installed** 分頁。
2. 完成 App 原有的安裝提示。
3. 前往 **Settings → App language**，選擇 **繁體中文（台灣）語言包**。
4. 重新啟動 pokeldn。

本包使用外掛 API **1.9** 的語言資源。請使用支援 API 1.9 的版本；本包依 pokeldn **0.35.0** 的原始碼製作與檢查。

App 語言與寶可夢本身的語言不同。若要讓建立的寶可夢使用繁體中文，仍需在訓練家設定中選擇對應語言。

## 涵蓋範圍

| 資源 | 數量與用途 |
| --- | --- |
| `strings.toml` | 1,688 個介面鍵值，涵蓋英文範本的所有鍵；無缺漏或多餘鍵值 |
| `messages.toml` | 1,641 筆原文對照，包含介面原文、神秘禮物預設內容、遊戲強化說明與常見錯誤；部分與主字串表重疊 |
| `help.toml` | 533 個工具與選項的說明，涵蓋常用交換、配信、團體戰、集友圈與連線設定 |
| `terms.toml` | 109 個遊戲名稱、地區及社群術語 |
| `templates.toml` | 31 個動態訊息範本，用於禮物效果、欄位錯誤與檔案操作訊息 |

英文範本中的 33 個介面鍵值刻意原樣保留，包括遊戲縮寫、HP、BP、GTS、GitHub、Discord、純變數排列、指令與可匯入的 Showdown 配置範例。這些並非漏譯。

寶可夢種類、招式、特性、精靈球名稱與合法性報告，會在程式支援的顯示位置使用 PKHeX 的繁體中文資料；本包以 `zh-TW` 觸發程式既有的 `zh-Hant` 對應。未自行複製整套 PKHeX 名稱資料。

## 用語原則

| 英文 | 本包用語 |
| --- | --- |
| Pokémon | 寶可夢 |
| Shiny | 異色；社群也常稱「色違」 |
| IV / EV / AV | 個體值／努力值／覺醒值，相關欄位保留縮寫 |
| Ability / Hidden Ability | 特性／隱藏特性 |
| Move / Nature | 招式／性格 |
| OT / TID / SID | 初訓家／訓練家 ID／裏 ID |
| Trade / Trade evolution | 交換／通訊進化 |
| Max Raid / Tera Raid | 極巨團體戰／太晶團體戰 |
| Dynamax Adventure | 極巨大冒險 |
| Union Circle / Blueberry Quests | 集友圈／藍樂活任務 |
| Mystery Gift / Event Pokémon | 神秘禮物／配信寶可夢 |
| Save / Import / Export | 存檔／匯入／匯出 |
| Plugin / Board / Firmware | 外掛／開發板／韌體 |

`Legal` 與 `Illegal` 譯為「合法／不合法」，指 PKHeX 資料合法性分析的結果，並不表示能藉此驗證寶可夢取得來源。

## 目前仍會出現英文的範圍

- 專案共列出 2,167 個工具選項說明。本包翻譯其中 533 個；其餘 1,634 個主要是底層通訊、逆向分析與硬體診斷選項，仍使用英文原文。
- 沒有附上整套使用文件與指南的譯本，相關頁面會使用原始英文文件。
- 檔名、原始銀行與佇列摘要、GTS 資料、設定儲存值、連線紀錄、無線通訊輸出及 `[done]` 訊息，依程式設計保留其原始資料；本包只翻譯程式開放的顯示位置。
- 尚未列入對照表的模組訊息及第三方外掛文字，會按程式規則使用英文或只替換已知術語。
- 上游的 `bank.file_unreadable_0fd8f4` 與 `gts.asks_for_open_until_offer_answered_7137e1` 會直接把英文複數字尾 `s` 傳入格式變數。本包完整保留變數及其格式，因此這兩處在複數情況下仍可能多顯示一個 `s`；純資料語言包無法移除此由程式直接傳入的字尾。

## 來源與檢查

- 原始碼基準：[`Decryptu/pokeldn`，commit `7d1258a04c4f777bb446ae2cc47ddfdf45a99dd5`](https://github.com/Decryptu/pokeldn/tree/7d1258a04c4f777bb446ae2cc47ddfdf45a99dd5)。
- 格式依據：[Language packs](https://github.com/Decryptu/pokeldn/blob/7d1258a04c4f777bb446ae2cc47ddfdf45a99dd5/docs/plugins.md#language-packs-15)。
- 英文範本：`pokeldn/app/data/strings.en.toml`。
- 「藍樂活」「點心大叔」等專有名詞參照[寶可夢官方繁體中文頁面](https://www.pokemon.co.jp/ex/sv_dlc/tc/features/231207_01/)。
- 通過專案的語言包載入器、`scripts/check_language_pack.py` 及 `scripts/pack_plugin.py` 檢查。
- 主字串缺漏 0、多餘鍵值 0、格式變數差異 0；另比對所有變數的格式規格與轉換方式。
- 已檢查所有主字串的執行期格式化，並抽查動態訊息與術語替換。
- 未在真實 Switch 或完整圖形介面中實測。

`.pokeplugin` 本身是 ZIP 格式，內含可編輯的 TOML 原始檔與此說明。若要自行調整，可將副本改為 `.zip` 後解壓縮，修改文字，再使用專案的 `scripts/pack_plugin.py` 重新打包。請保留鍵值、變數名稱與格式規格。

本包僅包含文字資料與授權文件，不包含 Python 程式碼。衍生翻譯內容依 AGPL-3.0-or-later 授權提供；完整授權見 `LICENSE`。
