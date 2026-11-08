# BioEdu Studio：生物資訊教學製作團隊

一個 Claude Code plugin，裡面有 **1 位製作總監（skill）＋ 9 位專職 agent**，可以把一個生資主題從立項一路做到推廣。產出包括教學影片、簡報、程式碼、實作、互動網站和推廣素材。

## 團隊組成

```
                       ┌──────────────────────┐
         你 ─────────▶ │ 製作總監 /bioedu-studio │  立項・派工・閘門・發布
                       └──────────┬───────────┘
   ┌───────────┬──────────┬───────┴──┬────────────┬─────────────┐
 設計          核心內容              衍生教材            發布推廣     把關
 curriculum-   code-engineer        lab-designer        outreach-   qa-reviewer
 architect     video-producer       web-tutorial-       manager     （每個閘門）
 domain-       slide-designer        builder
 scientist
```

| Agent | 負責 | 會用到你現有的 skill |
|---|---|---|
| `curriculum-architect` 課程架構師 | 學習目標、集數切分、outline.md | — |
| `domain-scientist` 內容專家／查核 | 科學正確性、DOI 查證、參考庫 | `deep-research` |
| `code-engineer` 程式工程師 | renv/conda 環境、示範資料、實際跑過的 R/Python | — |
| `lab-designer` 實作評量 | 練習版挖空、分層練習、雙語題庫、助教解答 | `interactive-tutorial-site`（題庫 schema） |
| `slide-designer` 簡報設計 | spec 產生 pptx、示意圖、轉 PDF 驗版面 | `bilingual-academic-deck`、Q/B/C 系列 skill |
| `video-producer` 影片編劇 | 逐頁講稿、分鏡、錄影清單、SRT、章節時間碼 | — |
| `web-tutorial-builder` 互動網站 | 拖滑桿看參數效果的靜態網站 | `interactive-tutorial-site` |
| `outreach-manager` 推廣經理 | README、YouTube 文案、社群貼文、工作坊公告、發布時程 | — |
| `qa-reviewer` 品質審查 | 9 大類檢查表，只出報告不改檔 | — |

所有 agent 都遵守 `skills/bioedu-studio/TEAM_CHARTER.md`，裡面已經寫進你既有的規矩：不覆蓋手改、先備份、版面問題不刪內容、敘述保守、產物不是原始碼、`github/` 是唯一的發布邊界，以及顏色不可以是唯一編碼。

## 工作流程與閘門

| 階段 | 誰 | 閘門 |
|---|---|---|
| 0 立項 | 總監問你需求，建立 `_課程簡報單.md` | — |
| 1 設計 | 架構師 → 內容專家審 | **G1：你確認 outline** |
| 2 核心內容 | 程式、講稿、簡報（平行） | — |
| 3 衍生教材 | 練習題庫、網站、簡報定稿 | **G2：QA 審查，🔴 退回修正（最多 2 輪）** |
| 4 發布推廣 | 整理 `github/` ＋推廣草稿 | **G3：任何對外動作都要你同意** |

## 安裝

**方法 A：當 plugin 安裝（推薦）**。把這個資料夾放進一個 GitHub repo，然後：
```
/plugin install bioedu-studio --marketplace <你的帳號>/<repo>
```
（repo 根目錄需要一份 `.claude-plugin/marketplace.json` 列出這個 plugin。要上 GitHub 的話，我可以幫你補上這份檔案。）
或者在本機直接載入測試：
```bash
claude --plugin-dir ./bioedu-studio
```

**方法 B：直接複製到個人設定（所有專案都能用）**
```bash
cp bioedu-studio/agents/*.md ~/.claude/agents/
```
```bash
cp -r bioedu-studio/skills/bioedu-studio ~/.claude/skills/
```

Windows 對應的路徑是 `C:\Users\<你>\.claude\agents\` 和 `...\.claude\skills\`。

## 使用範例

```
/bioedu-studio 幫我做一個空間轉錄體（Visium HD）入門系列，給研究生，3 集，R + Seurat
```
```
/bioedu-studio 幫 B 系列做推廣素材和 YouTube 文案（只派 outreach-manager）
```
```
請 qa-reviewer 審查 Q系列_快速上手篇 的 github/ 資料夾
```
