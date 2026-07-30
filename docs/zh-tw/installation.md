# 安裝與設定

## 一句話安裝

推薦直接把下面這句話發給 Codex，讓它幫你安裝：

```text
請幫我安裝這個 codex-ppt skill，連結是：https://github.com/ningzimu/codex-ppt-skill
```

## Codex 手動安裝

在命令列中執行以下命令，將 `codex-ppt` skill 安裝到 Codex 全域性 skills 目錄：

```bash
npx -y skills@latest add ningzimu/codex-ppt-skill \
  --skill codex-ppt \
  --agent codex \
  --global
```

安裝後重啟 Codex，讓新 skill 生效。

也可以從 [GitHub Releases](https://github.com/ningzimu/codex-ppt-skill/releases) 下載 `codex-ppt-skill-v*.zip`，解壓後把其中的 `codex-ppt` 資料夾放到 `~/.codex/skills/codex-ppt`，然後重啟 Codex。

如果你在本地開發這個儲存庫，可以把 skill 目錄符號連結到 Codex skills 目錄，方便即時除錯修改：

```bash
mkdir -p ~/.codex/skills
ln -s /path/to/codex-ppt-skill/skills/codex-ppt ~/.codex/skills/codex-ppt
```

## OpenClaw 安裝

```bash
openclaw skills install codex-ppt
```

如果使用 OpenClaw 的 skill allowlist，需要把 `codex-ppt` 加入允許列表。

## Claude Code / Hermes Agent

Claude Code：

```bash
npx -y skills@latest add ningzimu/codex-ppt-skill \
  --skill codex-ppt \
  --agent claude-code \
  --global
```

Hermes Agent：

```bash
npx -y skills@latest add ningzimu/codex-ppt-skill \
  --skill codex-ppt \
  --agent hermes-agent \
  --global
```

常見目標目錄：Claude Code 使用 `~/.claude/skills/codex-ppt`，Hermes Agent 使用 `~/.hermes/skills/codex-ppt`。本地開發時同樣可以用符號連結替代複製。

## 更新 skill

推薦直接把下面這句話發給你的 agent，讓它幫你更新：

```text
請幫我更新 codex-ppt skill 到最新版本，儲存庫是：https://github.com/ningzimu/codex-ppt-skill
```

手動更新時，重新執行上面對應 agent 的安裝命令即可，會用最新版本覆蓋已安裝的 skill；也可以從 [GitHub Releases](https://github.com/ningzimu/codex-ppt-skill/releases) 下載最新的 `codex-ppt-skill-v*.zip`，解壓後替換原來的 `codex-ppt` 目錄。更新完成後重啟 agent 生效。

更新是安全的：API key 等執行時設定儲存在 `~/.codex-ppt-skill/.env`，個人風格庫儲存在 `~/.codex-ppt-skill/references/`，都在 skill 安裝目錄之外，更新或重灌不會丟失。每個版本的變更內容可以檢視 [Releases 頁面](https://github.com/ningzimu/codex-ppt-skill/releases)或儲存庫的 `CHANGELOG.md`。

## 圖片生成模型設定

如果你沒有 `gpt-image-2` 模型的使用權限，就無法使用該 skill。該 skill 強依賴 `gpt-image-2` 圖片生成模型。

## 如何判斷是否具備 `gpt-image-2` 使用權限？

- 如果你購買了 ChatGPT Plus、Pro 會員，預設就可以使用 `gpt-image-2` 模型；Codex 有一個內建工具用於圖片生成。
- 如果你使用第三方中轉 API 接入 Codex，可以讓它產生一張包含複雜中文文字的圖片，例如要求用行楷寫一首詩。觀察是否能正常圖片生成，以及產生的圖裡是否有中文字型錯誤。如果一切正常，也無需設定。
- 如果上面兩個都不行，就需要自行購買具備 `gpt-image-2` 模型使用權限的中轉 API。

通常不需要手動設定圖片生成模型。你在使用 Codex PPT 的過程中，AI 會自動檢測圖片生成後端；如果不可用，會提示你設定圖片生成後端 API，並引導你完成設定。

## 第三方 API 注意事項

本 skill 內建了一個適配 OpenAI 官方圖片生成方式的指令碼。如果你用的是第三方 `gpt-image-2` 中轉 API，可以嘗試提供：

- 轉接服務的 base URL
  - 轉接服務範例如果是 `https://xxx/v1/images/generations`，base URL 填 `https://xxx/v1`。
  - 如果轉接服務已經給的是 `https://xxx/v1`，不要再加一層，避免 `.../v1/v1`。
  - 如果是官方 OpenAI，`OPENAI_BASE_URL` 可以不填，預設就是官方 `https://api.openai.com/v1`。
- 轉接服務的 API key
- 轉接服務的 `gpt-image-2` 具體模型名

將上述資訊提供給 AI 之後，嘗試讓其圖片生成。如果跑不通，則可能你使用的轉接服務有自訂的圖片生成使用方案，不完全相容 OpenAI 圖片生成介面。請將轉接服務官方的圖片生成使用文件發給 AI，讓它學習並適配圖片生成指令碼。
