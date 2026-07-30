# Codex PPT Skill 說明文件

Codex PPT 是一個面向 Codex 的 PPT 產生 skill，也可在 Claude Code、OpenClaw、Hermes Agent 等支援 `SKILL.md` 的 agent 中使用。它把文章、報告、論文、課程筆記或粗略想法轉換成圖片式簡報：先規劃大綱和視覺風格，再逐頁產生完整投影片圖片，最後組裝成 `.pptx` 檔案。

## 這套文件怎麼讀

如果你只是想快速上手，先看[快速開始](quickstart.md)。

如果你要安裝、設定模型或接入不同 agent，再看[安裝與設定](installation.md)。

如果你想理解完整產生過程、確認點和品質控制，再看[標準工作流](workflow.md)。

如果你已經在使用，並且遇到了問題，請查閱[常見問題](faq.md)。

## 子頁面

- [快速開始](quickstart.md)：第一次使用時的最短路徑、範例命令和產物說明。
- [設計理念](design.md)：為什麼採用圖片式 PPT、階段確認和雙 skill 分工的設計。
- [安裝與設定](installation.md)：Codex、OpenClaw、Claude Code、Hermes Agent 的安裝與更新方式，以及 API/CLI fallback 設定。
- [標準工作流](workflow.md)：從大綱確認、風格確認、後端確認、範例投影片確認到整套產生和組裝的完整流程。
- [風格與個人風格庫](styles.md)：12 種內建風格預覽、仿照參考材料重現風格，以及把滿意的風格儲存到個人風格庫長期重複使用。
- [常見問題](faq.md)：可編輯性、API key、範例投影片、素材插入、單頁修改等常見問題。
- [範例提示詞](prompts.md)：文章轉 PPT、論文口試、管理層報告、指定風格、修改單頁等可直接重複使用的提示詞。

## 特色功能

- 圖片式 PPT 產生：每一頁都是完整 16:9 投影片圖片，適合追求強視覺表達和統一風格的場景。
- 分階段確認流程：先確認大綱、視覺風格、圖片產生方式和範例投影片，再產生整套 PPT，減少返工。
- 內建 12 種風格：包括手繪技術解說風、學術口試風、清爽專業風、麥肯錫風格、政務紅風格、教學教材風等方向，參見[風格與個人風格庫](styles.md)。
- 支援參考材料仿風格：可以閱讀使用者提供的 PPT、PDF 或截圖，理解每頁圖片風格後再仿照產生。
- 可沉澱個人風格庫：滿意的風格可以儲存到 `~/.codex-ppt-skill/references/`，存放在 skill 安裝目錄之外，更新 skill 不丟失，後續製作直接按名字重複使用。
- 支援指定素材入頁：可以把論文原圖、實驗結果圖、架構圖或截圖指定到具體頁面中使用。
- 支援多 agent 環境：除 Codex 外，也可在 Claude Code、OpenClaw、Hermes Agent 等支援 `SKILL.md` 的 agent 中使用。
- 自動組裝 PowerPoint：產生 `outline.md`、每頁圖片、`speech.md`，並最終組裝為 `.pptx` 檔案。
- 支援透過第三方 API 使用文字模型和 `gpt-image-2` 圖片生成模型。
- 支援配套產生 PPT 演講稿，預設會自動插入 PPT 備註頁。
- 支援產生後針對特定不滿意的頁面做定向修改，參見[常見問題](faq.md)。

## 適用場景

- 技術文章轉分享 PPT
- 論文、研究報告或調研材料轉演示稿
- 課程筆記轉教材
- 產品介紹、商業報告、專案總結
- 科研口試、專案申報、中期檢查、結題驗收
- 需要統一視覺語言的圖片式簡報

## 關鍵提醒

Codex PPT 產生的是圖片式 PPT：視覺一致性強，但頁面裡的文字、圖表和形狀不能像傳統 PPT 那樣逐項編輯。

如果你需要進一步轉換成可編輯 PPT，可以在產生後再使用 [image-to-editable-ppt-skill](https://github.com/ningzimu/image-to-editable-ppt-skill)。

如果你沒有 `gpt-image-2` 圖片生成模型的使用權限，則無法使用該 skill，參見[安裝與設定](installation.md)。

## 相關連結

- GitHub 儲存庫：https://github.com/ningzimu/codex-ppt-skill
- ClawHub 頁面：https://clawhub.ai/ningzimu/codex-ppt
- 使用案例展示區：https://github.com/ningzimu/codex-ppt-skill/issues/34
- 可編輯 PPT 轉換 skill：https://github.com/ningzimu/image-to-editable-ppt-skill
