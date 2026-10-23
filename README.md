# pokeldn 繁體中文（台灣）語言包

為 [pokeldn](https://github.com/Decryptu/pokeldn) 提供符合台灣用語與寶可夢中文社群習慣的繁體中文介面。本儲存庫專門維護語言包、翻譯來源及更新參照。

## 下載與安裝

**[下載最新 pokeldn-zh-TW-pokeplugin](https://raw.githubusercontent.com/jimmyorz/pokeldn-decrypt-plugins-zhTW/main/packages/pokeldn-zh-TW-1.0.3.pokeplugin)**

1. 開啟 **Plugins → Add a plugin**，選擇下載的 `.pokeplugin`，依畫面提示完成安裝。
2. 前往 **Settings → App language**，選擇 **繁體中文（台灣）**。
3. **完整退出 pokeldn，再重新開啟。**

> **安裝或啟用外掛不會自動切換語言。** 如果介面仍是英文，請確認已完成第 2、3 步。「App language」控制介面語言，與訓練家／寶可夢的語言設定不同。

也可在 **Plugins → Sources** 加入 [pokeldn-decrypt-plugins-zhTW](https://raw.githubusercontent.com/jimmyorz/pokeldn-decrypt-plugins-zhTW/refs/heads/main/pokeldn-source.json)，再到 **Browse** 安裝本語言包，之後同樣需要選取介面語言並重新啟動。本包未簽章。

可按下方程式碼區塊右上角的複製按鈕，複製來源網址：

```text
https://raw.githubusercontent.com/jimmyorz/pokeldn-decrypt-plugins-zhTW/refs/heads/main/pokeldn-source.json
```

## 版本資訊

| 項目 | 內容 |
| --- | --- |
| 目前翻譯對應版本 | pokeldn **0.35.0** |
| 更新日期 | **2026-10-23** |
| 語言包版本 | `1.0.3` |
| 外掛 API | `1.9` |
| 語系 | `zh-TW` |
| 外掛 ID | `community-zh-tw` |

此語言包以表列的 pokeldn 版本與外掛 API 為製作及檢查基準，屬於社群翻譯，非 pokeldn 或寶可夢官方發布。

## 檔案配置

| 路徑 | 用途 |
| --- | --- |
| [`packages/`](packages/) | 可安裝的 `.pokeplugin` 檔 |
| [`language-pack/`](language-pack/) | 主字串及所有補充翻譯的 TOML 原始檔 |
| [`language-pack/README.md`](language-pack/README.md) | 翻譯涵蓋範圍、用語原則與已知限制 |
| [`reference/strings.en.toml`](reference/strings.en.toml) | 製作時的上游英文基準 |
| [`reference/strings.zh-TW.toml`](reference/strings.zh-TW.toml) | 同一基準的完整中文對照，內容與 `language-pack/strings.toml` 相同 |
| [`reference/upstream.json`](reference/upstream.json) | 上游版本與檔案比對資料 |
| [`docs/maintenance.md`](docs/maintenance.md) | 後續更新與檢查方式 |
| [`docs/validation.md`](docs/validation.md) | 驗證紀錄與來源 |
| [`CHANGELOG.md`](CHANGELOG.md) | 版本更新紀錄 |

`language-pack/messages.toml`、`help.toml`、`terms.toml`、`templates.toml` 即為額外補充翻譯，均以可編輯文字保存。對照檔中的中文檔名為 `strings.zh-TW.toml`；安裝包使用 `strings.toml`，由 `plugin.toml` 指定，兩者內容相同。

## 授權 / License

翻譯內容衍生自 pokeldn，依 **AGPL-3.0-or-later** 提供，完整條款見 [LICENSE](LICENSE)。寶可夢及相關名稱屬各權利人所有。

The translations are derived from pokeldn and provided under **AGPL-3.0-or-later**; see [LICENSE](LICENSE). Pokémon and related names belong to their respective rights holders.
