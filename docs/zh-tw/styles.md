# 風格與個人風格庫

Codex PPT 的視覺風格來自兩個地方：隨 skill 釋出的**內建風格**，以及存放在你本機、更新 skill 也不會丟失的**個人風格庫**。

## 內建風格

skill 內建 12 種風格參考，不會寫提示詞也可以直接從這裡開始。製作 PPT 時直接說風格名即可，例如：

```text
請使用 codex-ppt skill，把這份材料做成 10 頁 PPT，使用內建的「手繪技術解說風」。
```

| 清爽專業風 | 創意雜誌風 |
| --- | --- |
| ![清爽專業風](https://raw.githubusercontent.com/ningzimu/codex-ppt-skill/main/assets/style-previews/clean-professional.png) | ![創意雜誌風](https://raw.githubusercontent.com/ningzimu/codex-ppt-skill/main/assets/style-previews/creative-magazine.png) |
| 電子墨水雜誌風 | 資料儀表板風 |
| ![電子墨水雜誌風](https://raw.githubusercontent.com/ningzimu/codex-ppt-skill/main/assets/style-previews/e-ink-magazine.png) | ![資料儀表板風](https://raw.githubusercontent.com/ningzimu/codex-ppt-skill/main/assets/style-previews/data-dashboard.png) |
| 復古扁平插畫風 | 手繪技術解說風 |
| ![復古扁平插畫風](https://raw.githubusercontent.com/ningzimu/codex-ppt-skill/main/assets/style-previews/retro-flat-illustration.png) | ![手繪技術解說風](https://raw.githubusercontent.com/ningzimu/codex-ppt-skill/main/assets/style-previews/handdrawn-technical.png) |
| 手繪白板風 | 溫暖手作風 |
| ![手繪白板風](https://raw.githubusercontent.com/ningzimu/codex-ppt-skill/main/assets/style-previews/handdrawn-whiteboard.png) | ![溫暖手作風](https://raw.githubusercontent.com/ningzimu/codex-ppt-skill/main/assets/style-previews/warm-handmade.png) |
| 學術口試風 | 麥肯錫風格 |
| ![學術口試風](https://raw.githubusercontent.com/ningzimu/codex-ppt-skill/main/assets/style-previews/scientific-defense.png) | ![麥肯錫風格](https://raw.githubusercontent.com/ningzimu/codex-ppt-skill/main/assets/style-previews/mckinsey-style.png) |
| 政務紅風格 | 教學教材風 |
| ![政務紅風格](https://raw.githubusercontent.com/ningzimu/codex-ppt-skill/main/assets/style-previews/party-government-red.png) | ![教學教材風](https://raw.githubusercontent.com/ningzimu/codex-ppt-skill/main/assets/style-previews/teaching-courseware.png) |

風格是一套視覺系統（配色、字型氣質、版式密度、插畫語言），不是固定模板；同一套風格下，每頁版式會根據內容角色變化，不會每頁長得一樣。

## 仿照參考材料的風格

如果內建風格不滿足需求，可以提供自己喜歡的風格參考：一張截圖、多張截圖，或完整 PPT/PDF。建議先讓 agent 分析參考材料的配色、版式、字型和視覺元素，再按這個風格產生新 PPT：

```text
請使用 codex-ppt skill 產生 PPT。視覺風格參考我上傳的這份 PDF。請詳細閱讀我提供材料中的每一頁圖片，確保瞭解其風格，然後仿照其風格進行產生。
```

注意：預設只仿風格、不復用內容。除非你明確要求，參考材料裡的文字和資料不會被搬進新 PPT。

## 個人風格庫

如果產生的 PPT 風格你很滿意，無論是調出來的自訂風格，還是從參考材料重現的風格，都可以讓 agent 儲存下來，以後直接重複使用：

```text
這套 PPT 的視覺風格我很喜歡，請儲存到個人風格庫。
```

儲存機制的幾個要點：

- **存放位置**：個人風格庫位於 `~/.codex-ppt-skill/references/`（可透過 `CODEX_PPT_HOME` 環境變數改變位置），在 skill 安裝目錄**之外**。更新或重新安裝 skill 時，個人風格不會被覆蓋或丟失。
- **自動發現**：儲存後無需任何登記。之後製作 PPT 選擇風格時，agent 會自動掃描個人風格庫，把你的風格和內建風格一起列出來。
- **同名優先**：如果個人風格和某個內建風格同名，以你的個人風格為準。你也可以利用這一點自訂內建風格：儲存一個同名的調整版即可覆蓋預設效果。
- **重複使用方式**：以後直接說風格名即可，例如「用『深色資料科技風』產生這份 PPT」。

產生完成後，如果這套 deck 用的是自訂或調整過的風格，agent 也會在最終報告裡主動提示你可以儲存。使用未修改的內建風格時無需重複儲存。

## 相關頁面

- [範例提示詞](prompts.md)：指定內建風格、仿照參考風格、儲存風格的完整提示詞。
- [常見問題](faq.md)：風格偏離、頁面不滿意時的處理方式。
