# 驗證紀錄與來源

## 翻譯基準

- 上游專案：[`Decryptu/pokeldn`](https://github.com/Decryptu/pokeldn)。
- 基準版本：pokeldn **0.35.0**／外掛 API **1.9**。
- 基準 commit：[`7d1258a04c4f777bb446ae2cc47ddfdf45a99dd5`](https://github.com/Decryptu/pokeldn/tree/7d1258a04c4f777bb446ae2cc47ddfdf45a99dd5)。
- [該版本的英文範本](https://github.com/Decryptu/pokeldn/blob/7d1258a04c4f777bb446ae2cc47ddfdf45a99dd5/pokeldn/app/data/strings.en.toml)。
- [該版本的語言包格式說明](https://github.com/Decryptu/pokeldn/blob/7d1258a04c4f777bb446ae2cc47ddfdf45a99dd5/docs/plugins.md)。

2026-10-23 檢查時，上游 `main` 仍為上述 commit，英文檔案的 Git blob SHA 與保存的基準相符。詳細來源與雜湊見 [`reference/upstream.json`](../reference/upstream.json)。

## 檢查結果

- 主字串缺漏、多餘鍵值與格式變數差異均為 0。
- 通過專案的語言包格式與封裝檢查。
- 已驗證安裝流程，以及選取語言後在新程序中載入中文。
- 1.0.1 已通過安裝、中文載入及外掛來源清單檢查；包內僅外掛資訊與說明文件有變更，翻譯內容與 1.0.0 相同。
- 1.0.2 通過封裝與字串載入檢查，並由使用者確認左側選單顯示正常。發布檔案與測試時提供的檔案完全相同；包內「本地測試版」說明保留為該檔案的製作紀錄。
- 完整圖形介面與所有遊戲功能未經全面測試。

原始檢查紀錄見 [`language-pack/validation.json`](../language-pack/validation.json)，後續更新方式見 [maintenance.md](maintenance.md)。
