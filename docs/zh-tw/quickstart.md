# 快速開始

## 適合誰

這頁給第一次使用 Codex PPT 的人看。你只需要準備一份文章、報告、大綱、論文或課程筆記，然後讓 agent 使用 `codex-ppt` skill 產生 PPT。

## 最短使用方式

先安裝 skill，參見[安裝與設定](installation.md)。然後，在 Codex 裡直接使用這個 skill 進行 PPT 製作。

```text
請使用 codex-ppt skill，把 /path/to/article.md 做成 10 頁左右的中文 PPT。
```

如果你已經知道風格和用途，可以寫得更具體：

```text
請使用 codex-ppt skill，把這篇技術文章做成 12 頁中文分享 PPT。風格偏清爽專業，適合內部技術分享；第 5 頁必須使用我提供的架構圖，第 8 頁必須保留實驗結果圖。
```

## 第一次使用建議

- 先讓 agent 產生 `outline.md`，確認頁數、標題和每頁要點。
- 不要跳過範例投影片確認。先看一頁效果，再批次產生整套 PPT。
- 如果某一頁不滿意，優先只改那一頁，不要整套重做。
- 如果有參考 PPT、截圖或 PDF，先讓 agent 分析風格，再產生新 PPT。

## 產生結果

最終通常會得到：

- `outline.md`：PPT 大綱
- `origin_image/slide_XX.png`：每頁正式圖片
- `speech.md`：每頁演講備註
- `{PPT名稱}.pptx`：最終 PowerPoint 檔案
