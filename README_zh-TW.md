# Codex PPT Skill

[简体中文](README.md) · **繁體中文（台灣）** · [English](README_en.md) · [한국어](README_ko.md)

[![文件](https://img.shields.io/badge/%E6%96%87%E6%A1%A3-%E4%BD%BF%E7%94%A8%E6%8C%87%E5%8D%97-111827)](https://ningzimu.github.io/codex-ppt-skill/#/) [![支援](https://img.shields.io/badge/%E6%94%AF%E6%8C%81-%E8%8E%B7%E5%8F%96%E5%B8%AE%E5%8A%A9-2CA5E0)](https://t.me/CodexPPT) [![ClawHub](https://img.shields.io/badge/ClawHub-codex--ppt-cd3b35)](https://clawhub.ai/ningzimu/codex-ppt) [![ClawMama](https://img.shields.io/badge/ClawMama-codex--ppt-2CA5E0)](https://app.clawmama.run/skills/5lak48/hermes?utm_source=github&utm_medium=issue&utm_campaign=skill_outreach_ningzimu_codex_ppt_skill) [![GitHub stars](https://img.shields.io/github/stars/ningzimu/codex-ppt-skill?style=flat&logo=github&label=stars)](https://github.com/ningzimu/codex-ppt-skill/stargazers) [![GitHub forks](https://img.shields.io/github/forks/ningzimu/codex-ppt-skill?style=flat&logo=github&label=forks)](https://github.com/ningzimu/codex-ppt-skill/forks)

一個面向 Codex 的 PPT 產生 skill，也可在 Claude Code、OpenClaw、Hermes Agent 等支援 `SKILL.md` 的 agent 中使用；在這些非 Codex 環境中通常需要設定 `gpt-image-2`、第三方圖片生成 API 或 OpenAI 相容格式的圖片生成介面。它把文章、報告、論文、課程筆記等內容轉換成“整頁圖片式”的簡報：先規劃大綱和視覺風格，再產生每頁投影片圖片，最後用本地指令碼組裝為 `.pptx`。

## 贊助

<table>
<tr>
<td width="180"><img src="assets/atlas-cloud-logo.png" alt="Atlas Cloud" width="160"></td>
<td>感謝 <a href="https://www.atlascloud.ai/?utm_source=github&utm_medium=link&utm_campaign=codex-ppt-skill">Atlas Cloud</a> 贊助本專案。AtlasCloud 是多模態 AI 推理平臺，提供統一 API 接入圖片產生、影片產生和大語言模型等能力；本 skill 已支援透過現有 API key、base URL 和模型名設定接入 AtlasCloud 的 GPT Image 2 圖片生成和編輯圖介面，按量計費，開箱即用。完整模型列表可檢視 <a href="https://www.atlascloud.ai/zh/models">Atlas Cloud 模型頁</a>。</td>
</tr>
</table>

## 溫馨提示

> [!TIP]
> 本 skill 負責從文章、報告、大綱或想法產圖片生成片式 PPT，適合強視覺表達，但頁面元素本身不可直接編輯。如果你需要進一步轉換成可編輯 PPT，可以在產生完成後嘗試使用 [image-to-editable-ppt-skill](https://github.com/ningzimu/image-to-editable-ppt-skill) 進行轉換。
>
> 關於 `codex-ppt` 和 `image-to-editable-ppt` 這兩個技能的詳細介紹，參見 [skill_duo_intro.pdf](assets/skill_duo_intro.pdf)。該 PPT 由 `codex-ppt` skill 產生，提示詞為：“請分別閱讀 Codex PPT和 Image to Editable PPT 這兩個技能的內容，然後用 Codex PPT 幫我做一個PPT吧，20頁，每個技能的介紹10頁。”
>
> 另外，關於這個 PPT Skill 設計和調優的實踐經驗，可以看這篇文章：[2000 個 GitHub Star 換來的經驗：好的 AI Skill 是調出來的，不是寫出來的](https://mp.weixin.qq.com/s/LaxWBX-nogHPpSxlk-Vs8Q)。

> [!NOTE]
> 想檢視更多使用者用這個 skill 做出的 PPT 效果，可以前往置頂 Issue 的案例展示區：[歡迎分享 codex-ppt 使用案例和 PPT 效果](https://github.com/ningzimu/codex-ppt-skill/issues/34)。

這個 skill 主要給大家提供一個還不錯的 PPT 產生流程。為了儘量通用，它的流程設計會稍微複雜一些；複雜也會帶來不穩定性或者冗餘性。比如它同時相容 Codex 內建圖片生成和 API/CLI fallback 圖片生成，也會相容有無子 agent 可用這兩種情況，但大部分人日常使用時其實只會固定走其中一條路線。

建議大家在走通自己常用的路線之後，讓 AI 幫你改一下這個 skill，把你的偏好固定下來，省得每次都重新選擇。比如固定使用內建圖片生成或固定使用某個 API，固定是否使用子 agent，固定常用輸出目錄、風格、頁數節奏等。

另外，如果你在做 PPT 的過程中遇到了自己喜歡的版式或排版，無論是這個 skill 做出來的，還是從別的地方找到的 PPT 風格圖片，都可以讓 AI 儲存到你的個人風格庫（`~/.codex-ppt-skill/references/`）裡，逐步沉澱自己的風格。個人風格庫存放在 skill 安裝目錄之外，更新或重灌 skill 都不會丟失。Skills 本質上是非常個性化的流程，鼓勵大家在使用這個 skill 的基礎上，按自己的偏好持續調優，讓它更適配自己的工作流。

關於 skills 如何設計和使用，可以參考 [good-skill-design.pptx](assets/good-skill-design.pptx)。這個 PPT 也是用本 skill 做的，採用的是手繪技術解說風；內容基於 Claude 在設計 skills 方面的最佳實踐文章 [The Complete Guide to Building Skills for Claude](https://resources.anthropic.com/hubfs/The-Complete-Guide-to-Building-Skill-for-Claude.pdf)。祝大家玩得愉快！

## 特點

- 多 agent 可用：支援 Codex、Claude Code、OpenClaw、Hermes Agent 等支援 `SKILL.md` 的環境；最推薦在 Codex 中使用，優先走內建圖片生成和編輯圖能力。
- 第三方圖片生成供應商接入：支援 OpenAI 相容介面、AtlasCloud、`base URL` 和自訂模型名設定，方便透過 API/CLI fallback 使用 `gpt-image-2` 或相容模型。
- 穩定的階段化流程：先確認大綱、頁數、視覺風格、圖片生成後端和範例投影片，再進入整套產生，降低一次產生完整 PPT 時的返工和偏航。
- 不是無腦產生：會先引導你確認 `outline.md`、每頁要點、風格方向和範例投影片效果，再按確認後的方案繼續。
- 低門檻輸入：文章、報告、論文、課程筆記、Markdown、大綱、PDF、Word 等材料都可以作為起點。
- 內建 12 種 PPT 風格參考：包括清爽專業、科研口試、黨政紅、教學教材、電子墨水雜誌、手繪技術解釋、儀表盤、麥肯錫等；不會寫提示詞也可以先從內建風格開始，尤其推薦手繪技術解說風。
- 支援自訂風格重現：可以上傳喜歡的圖片、PDF 或 PPT/PPTX，讓 agent 先分析配色、版式、字型和視覺元素，再按該風格產生新 PPT。
- 可沉澱個人風格庫：產生滿意後，可以把當前風格儲存到個人風格庫（`~/.codex-ppt-skill/references/`），下次直接重複使用；風格庫存放在 skill 安裝目錄之外，更新 skill 不會丟失，同名時個人風格優先於內建風格。
- 多 agent 併發產生：範例投影片確認後，支援一個子 agent 負責一頁，並對文字清晰度、風格一致性和內容完整性做自檢，發現問題及時返修。
- 支援指定圖片插入：可以要求某一頁必須放入論文原圖、實驗結果圖、截圖、架構圖等素材，並讓頁面圍繞這些圖片適配主題和版式。
- 自動產生演講稿：會產生 `speech.md`，並在組裝 PPTX 時寫入每頁備註，方便直接演示或二次修改。

## 產生效果

下面是一套技術分享 PPT 的產生效果範例。每頁都是由 `gpt-image-2` 產生的完整 16:9 投影片圖片，再由本地指令碼組裝為 PPTX。

![產生 PPT 效果範例](assets/slides_example.png)

下面是一套論文口試風案例，來源於論文 [Attention Is All You Need](https://arxiv.org/abs/1706.03762)。它展示瞭如何在指定頁中插入論文原始圖片作為輸入素材，例如模型架構圖、attention 模組圖和 attention 視覺化圖，並圍繞這些圖片產生統一風格的 PPT（見 Issue #14）。

![論文原圖插入案例](assets/paper-figures-example.png)

## 風格範例

以下是已產生預覽圖的風格，範例圖均由 `gpt-image-2` 產生，用於幫助使用者在開始製作前選擇視覺方向。

| 清爽專業風 | 創意雜誌風 |
| --- | --- |
| ![清爽專業風](assets/style-previews/clean-professional.png) | ![創意雜誌風](assets/style-previews/creative-magazine.png) |
| 電子墨水雜誌風 | 資料儀表板風 |
| ![電子墨水雜誌風](assets/style-previews/e-ink-magazine.png) | ![資料儀表板風](assets/style-previews/data-dashboard.png) |
| 復古扁平插畫風 | 手繪技術解說風 |
| ![復古扁平插畫風](assets/style-previews/retro-flat-illustration.png) | ![手繪技術解說風](assets/style-previews/handdrawn-technical.png) |
| 手繪白板風 | 溫暖手作風 |
| ![手繪白板風](assets/style-previews/handdrawn-whiteboard.png) | ![溫暖手作風](assets/style-previews/warm-handmade.png) |
| 學術口試風 | 麥肯錫風格 |
| ![學術口試風](assets/style-previews/scientific-defense.png) | ![麥肯錫風格](assets/style-previews/mckinsey-style.png) |
| 政務紅風格 | 教學教材風 |
| ![政務紅風格](assets/style-previews/party-government-red.png) | ![教學教材風](assets/style-previews/teaching-courseware.png) |

## 輸出結構

每個 PPT 會產生一個獨立專案目錄：

```text
{基礎目錄}/{PPT名稱}/        # 當前 PPT 的獨立專案目錄
├── origin_image/           # 正式投影片圖片目錄，只放最終採用的頁面
│   ├── slide_01.png        # 第 1 頁投影片圖片
│   ├── slide_02.png        # 第 2 頁投影片圖片
│   └── ...                 # 後續頁面圖片，按頁碼順序命名
├── outline.md              # 經確認的 PPT 大綱、頁數、每頁標題和要點
├── speech.md               # 演講稿，會寫入 PPT 每頁備註
└── {PPT名稱}.pptx          # 最終組裝產生的 PowerPoint 檔案
```

你可以在 `origin_image/` 裡檢視每一頁最終採用的投影片圖片，檔案會按 `slide_01.png`、`slide_02.png` 這樣的順序排列。想預覽整套 PPT 的視覺效果，或只挑某一頁繼續修改時，直接看這裡最方便。

`speech.md` 是配套演講稿。產生 `.pptx` 時，這些內容會自動寫入每頁 PPT 的備註區，你可以在 PowerPoint 裡直接檢視、修改，或演示時作為講稿使用。

## 適用場景

- 技術文章轉分享 PPT
- 論文或報告轉演示稿
- 課程筆記轉教材
- 科研專案申報、中期檢查、結題驗收和論文口試
- 商業報告、產品介紹、調研總結
- 需要強視覺統一性的圖片式簡報

## 安裝

### 一句話安裝

【推薦】可以直接把下面這句話發給你的 Agent，讓它幫你安裝：

```text
請幫我安裝這個 codex-ppt skill，連結是：https://github.com/ningzimu/codex-ppt-skill
```

### 手動安裝到 Codex

如需手動安裝到 Codex，可以使用 `skills` CLI 安裝到 Codex 的全域性 skills 目錄：

```bash
npx -y skills@latest add ningzimu/codex-ppt-skill \
  --skill codex-ppt \
  --agent codex \
  --global
```

安裝完成後，重啟 Codex 讓新 skill 生效。

也可以從 GitHub Releases 下載 `codex-ppt-skill-v*.zip`，解壓後把其中的 `codex-ppt` 資料夾放到 `~/.codex/skills/codex-ppt`，然後重啟 Codex。

如果你是在本地開發這個儲存庫，也可以把 skill 目錄連結到 Codex skills 目錄，方便即時除錯修改：

```bash
mkdir -p ~/.codex/skills
ln -s /path/to/codex-ppt-skill/skills/codex-ppt ~/.codex/skills/codex-ppt
```

### OpenClaw

可以透過 ClawHub 安裝：

```bash
openclaw skills install codex-ppt
```

ClawHub 頁面：[clawhub.ai/ningzimu/codex-ppt](https://clawhub.ai/ningzimu/codex-ppt)

如果使用 OpenClaw 的 skill allowlist，需要把 `codex-ppt` 加入允許列表。

### Claude Code、Hermes Agent

這些 agent 都可以讀取 `SKILL.md` 形式的 skill。也可以使用 `skills` CLI 安裝：

```bash
# Claude Code
npx -y skills@latest add ningzimu/codex-ppt-skill \
  --skill codex-ppt \
  --agent claude-code \
  --global

# Hermes Agent
npx -y skills@latest add ningzimu/codex-ppt-skill \
  --skill codex-ppt \
  --agent hermes-agent \
  --global
```

常見目標目錄是：Claude Code 使用 `~/.claude/skills/codex-ppt`，Hermes Agent 使用 `~/.hermes/skills/codex-ppt`。

如果你是在本地開發這個儲存庫，也可以用符號連結替代複製，方便即時除錯修改。

### 更新

重新執行一遍上面對應的安裝命令即可覆蓋為最新版本，也可以直接讓 agent 幫你更新：

```text
請幫我更新 codex-ppt skill 到最新版本，儲存庫是：https://github.com/ningzimu/codex-ppt-skill
```

更新後重啟 agent 生效。API key 設定（`~/.codex-ppt-skill/.env`）和個人風格庫（`~/.codex-ppt-skill/references/`）都在 skill 安裝目錄之外，更新或重灌不會丟失。

## 圖片生成模型設定

> [!TIP]
> 你可以先正常使用 Codex PPT 開始製作 PPT。一般不需要自己手動設定圖片生成模型；當流程走到“選擇圖片生成後端”時，AI 會根據當前環境判斷是否需要設定，並在需要時引導你提供相關資訊。
>
> - 如果你使用的是 Codex 內建圖片產生能力，通常不需要額外設定 API key。
> - 如果你確定要使用第三方供應商或 OpenAI 相容轉接服務，請讓 AI 先閱讀 [圖片生成模型設定指南](skills/codex-ppt/docs/image-model-configuration.md)，再設定 API key、base URL 和模型名。

指定圖片解析度、提高品質或要求修改某一頁，本身不會觸發第三方 API 設定。如果你是透過 GPT 會員訂閱使用 Codex，並且 Codex 內建圖片產生工具可用，通常可以繼續使用內建圖片生成能力，不需要準備 API key。

## 使用方式

在 Codex、Claude Code、OpenClaw 或 Hermes Agent 中明確指定使用 `codex-ppt` skill，例如：

```text
請使用 codex-ppt skill 把 /path/to/article.md 做成 10 頁左右的 PPT。
```

skill 會按以下流程執行：

1. 閱讀內容並規劃 PPT 大綱
2. 產生 `outline.md`，並請求你確認頁數、標題和每頁要點
3. 給出 2-3 個視覺風格選項，並推薦一個讓使用者確認
4. 在首次圖片生成前說明將使用的圖片生成方式，並請求你確認
5. 使用確認後的圖片產生後端產生 1 頁範例投影片，讓使用者確認風格、版式節奏和文字品質
6. 建立 PPT 專案目錄
7. 使用同一圖片產生後端逐頁產生全部投影片圖片
8. 檢查文字清晰度、風格一致性和內容完整性
9. 產生 `speech.md`
10. 使用 `assemble_ppt.py` 組裝 `.pptx`
11. 可選：如果產生的 PPT 風格你很喜歡，可以儲存到風格庫；如果使用的是內建風格，則無需重複儲存

## 使用技巧

- Codex 會員預設會優先使用內建圖片生成工具，其產生的圖片解析度比較低，且目前不能手動指定解析度。如果需要更高解析度的影像，需要改用 `gpt-image-2` API 的方式產生（即 API/CLI fallback，提供 API key、base URL 和模型名）。API/CLI fallback 場景下，指令碼預設解析度是 2K 16:9 橫屏；如果產生的投影片圖片仍然比較模糊，尤其是文字較多的頁面，可以讓 AI 改用 4K 解析度產生。
- 如果只是不滿意某一頁的內容、排版、配色或文字表達，可以直接讓當前 agent 針對這一頁做細緻修改，不需要整套 PPT 重新產生。

![單頁局部修改示意：開啟 PPT、點選標註，並框選需要修改的位置](assets/single-slide-revision-example.png)

- 你也可以提供喜歡的 PPT 風格參考，可以是一張截圖、多張截圖，或完整 PPT/PDF。建議先讓當前 agent 分析參考材料的配色、版式、字型和視覺元素，再按這個風格產生新 PPT。產生滿意後，也可以讓 agent 把這套風格儲存到個人風格庫（`~/.codex-ppt-skill/references/`）裡，方便以後重複使用，且不會因更新 skill 而丟失。
- 如果需要插入論文原圖、實驗結果圖、截圖或架構圖，可以在大綱中指定這些圖片對應的頁碼和用途。

## 我的其他專案

- [image-to-editable-ppt-skill](https://github.com/ningzimu/image-to-editable-ppt-skill)：把投影片截圖、PDF 頁面或圖片版 PPTX 重建為可編輯 PowerPoint，適合在 `codex-ppt` 產生整頁圖片後繼續做可編輯化。
- [codex-gpt-image](https://github.com/ningzimu/codex-gpt-image)：透過 Codex OAuth / 會員登入呼叫 `gpt-image-2` 的圖片生成 skill。
- [handdrawn-tech-illustrations](https://github.com/ningzimu/handdrawn-tech-illustrations)：面向中文技術內容的手繪配圖 skill，可以把技術文章、產品筆記、截圖、大綱或粗略想法產生正文配圖、概念解釋圖、微信公眾號封面和小紅書封面；風格強調親和、輕卡通、中文可讀和適中的資訊密度。
- [awesome-ai-ppt](https://github.com/ningzimu/awesome-ai-ppt)：精選的 AI PPT 相關開源專案，按 HTML-first、圖片產生式、PPTX-native、轉換與自動化基礎設施等工作流分類，關注能幫助 agent 或開發者建立、編輯、轉換、檢查 PPT 的 GitHub 儲存庫。
- [claude-code-lens](https://github.com/ningzimu/claude-code-lens)：Claude Code 本地觀測工具，用來檢視 API 流量、日誌、prompt 和工具呼叫，適合排查 agent 實際在做什麼。

## 支援

遇到問題？請檢視[使用文件](https://ningzimu.github.io/codex-ppt-skill/#/)，加入 [CodexPPT](https://t.me/CodexPPT)，或[提交 Issue](https://github.com/ningzimu/codex-ppt-skill/issues/new)。

## 許可證

MIT

## 致謝

感謝 [LinuxDO](https://linux.do) 社群的支援。
