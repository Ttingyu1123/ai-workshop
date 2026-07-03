# AI Workshop — 醫療人員 AI 創作工作坊

靜態 HTML 教學網站，部署在 GitHub Pages。面向不熟悉 AI 的醫療人員，教 AI 圖像/影片/語音合成。

## 技術架構

- **純靜態站**：HTML + CSS + vanilla JS，零依賴、零 build
- **部署**：GitHub Pages（`main` branch → `https://ttingyu1123.github.io/ai-workshop/`）
- **設計系統**：Doodle 手繪風（基於 typeui.sh/design-skills/doodle）

## 檔案結構

```
ai-workshop/
├── CLAUDE.md           # 本檔
├── style.css           # 全站共用樣式（Doodle 設計系統）
├── index.html          # 首頁（分區卡片牆：#core / #create / #advanced / #extras）
├── ai-fundamentals.html # Part 1 — AI 基礎觀念
├── ai-writing.html     # Part 2 — AI 文字應用
├── ai-safety.html      # Part 3 — AI 安全與隱私（必修）
├── ai-image.html       # Part 4 — AI 圖像生成
├── ai-video.html       # Part 5 — AI 影片製作
├── google-flow.html    # Part 6 — Google Flow 實戰
├── ai-agent.html       # Part 7 — AI Agent 實作
├── notebooklm.html     # 番外 — NotebookLM 文獻工具
├── ai-transcribe.html  # 番外 — 語音轉文字
├── capcut.html         # 番外 — CapCut 剪輯
├── canva.html          # 番外 — Canva 設計
├── github-pages.html   # 番外 — GitHub Pages 建站
├── prompt-builder.html # 番外 — Prompt 產生器（純前端字串組裝，零 API；表單樣式在頁內 <style>）
├── sitemap.xml         # 新增頁面時記得加一條
├── robots.txt
├── qr-site.png         # 首頁 QR code（實體課投影片用）
├── 404.html            # GitHub Pages 404（連結用 /ai-workshop/ 絕對路徑）
├── og-image.png        # OG 分享圖（doodle 插畫 1024x1024，與 website Insights 卡片同一張）
├── favicon-32.png      # favicon（從 og-image 聽診器笑臉裁出）
├── favicon.png         # favicon 64x64
└── apple-touch-icon.png # iOS 書籤圖示 180x180
```

## 設計規範

### 字型
- **標題/手寫**：`Caveat`（Latin）+ `LXGW WenKai TC`（中文）
- **內文**：`LXGW WenKai TC`（中文主體）+ `Caveat`（Latin fallback）
- **程式碼**：`JetBrains Mono`
- 全部從 Google Fonts 載入

### 色彩 Token
| Token | Hex | 用途 |
|-------|-----|------|
| `--primary` | `#49B6E5` | 主色、連結、標籤 |
| `--secondary` | `#263D5B` | 深色文字、header |
| `--text` | `#111827` | 內文 |
| `--success` | `#16A34A` | 優點標記 |
| `--warning` | `#D97706` | 注意事項 |
| `--danger` | `#DC2626` | 禁止/缺點 |

### 排版
- Base font-size: 18px，line-height: 1.9
- Container: max-width 900px，padding 0 32px
- 背景：筆記本橫線（background-size 36px）
- 響應式斷點：640px、768px（header）

### 元件
- `.tool-card` — 工具介紹卡（含 pros-cons）
- `.prompt-block` — 可複製的 Prompt 區塊（含 `copyPrompt()` JS）
- `.card` / `.card-grid` — 資訊卡片
- `.analogy` — 醫學類比框
- `.box-tip` / `.box-danger` / `.box-success` — 提示框
- `.box-success` 小任務框 — 每個課程頁底部 nav-links 前有一個「🎯 現在就做」5-15 分鐘實作任務（新頁面必加）
- `.site-header` — sticky header + 純 CSS 漢堡選單（checkbox hack）
- `.site-footer` — footer 含 IG/GitHub SVG icon

## 導航結構

所有頁面共用 header/footer：
- Header 是**分區錨點導航**（不列單頁，永不爆版）：首頁 / 基礎必修(#core) / 創作應用(#create) / 進階實戰(#advanced) / 番外工具(#extras) — 錨點指向 index.html 的四個 section。作品集連結只在 footer，不放 header
- 每頁把自己所屬分區的連結標 `.active`：Part 1-3 → #core、Part 4-6 → #create、Part 7 → #advanced、番外頁 → #extras
- 閱讀鏈（底部 nav-links）：Part 1→2→3→4→5→6→7 → 番外 notebooklm → ai-transcribe → capcut → canva → github-pages
- 課程分區：基礎必修（基礎/文字/安全）、創作應用（圖像/影片/Flow）、進階實戰（Agent）、番外工具（5 頁）
- **新增課程不要動 header** — 只加 index 卡片和串閱讀鏈
- Footer：© TingYu's Deco — AI Workshop + IG + GitHub + 作品集
- 當前頁 nav link 加 `.active` class
- 作品集連結：https://tingyudeco.com（外部連結）

## 新增頁面 SOP

1. 複製任一現有頁面作模板
2. 更新 `<title>` / `<meta description>` / hero badge / h1
3. 更新 header nav 的 `.active` class
4. 更新 TOC 和底部 nav-links
5. 在 index.html 加對應的課程卡片
6. 確認 footer 連結正確

## 待做項目

### 內容
- [ ] 加入用戶生成的圖片範例（ai-image.html 的 `<!-- TODO -->` 標記處）
- [ ] 範例牆／學員作品頁（靜態 gallery + Google 表單收件，等有作品再做）
- [x] AI 文字應用（ai-writing.html，Part 2）
- [x] AI 安全與隱私（ai-safety.html，Part 3）
- [x] NotebookLM 文獻工具（notebooklm.html，番外）
- [x] 語音轉文字（ai-transcribe.html，番外）
- [x] CapCut 教學頁面（capcut.html）
- [x] Canva 教學頁面（canva.html）
- [x] AI Agent 教學頁面（ai-agent.html，Part 5）
- [x] GitHub Pages 建站教學頁面（github-pages.html）
- [ ] 衛教單專區 → **獨立成站**（預計 >20 張，受眾是民眾非醫療人員，另開 repo，不放本站）

### 技術
- [x] OG 圖片（og-image.png，doodle 插畫，與 website repo `public/images/insights/ai-workshop.png` 是同一張圖，換圖時要兩邊同步）
- [x] favicon（聽診器笑臉，從 og-image.png 裁出三種尺寸）
- [ ] Google Analytics — 等用戶提供 GA4 measurement ID（G-XXXX）後在各頁 head 加 gtag snippet
- [x] sitemap.xml + robots.txt（新增頁面時 sitemap 要補一條）
- [x] Prompt 產生器（prompt-builder.html）
- [x] 每課「現在就做」小任務框
- [x] 首頁 QR code（qr-site.png）

## 注意事項

- **官方署名**：衛生福利部台中醫院 感染科 曾婷玉醫師（螢幕 footer 與列印版權行都用這個，不放 IG/GitHub/個人網站）。列印（Ctrl+P）時每頁自動帶版權 footer 與淡浮水印（style.css `@media print` 的 `body::before/::after`），螢幕上不顯示；改署名時螢幕 footer（各頁 HTML）和 print（style.css）兩處都要改

- 不要用 Delius Swash Caps 字型（大寫 I 看起來像 J，對 AI 主題致命）
- Prompt 區塊的 `copyPrompt()` 函式在每個頁面的 `<script>` 中重複定義（刻意，避免外部 JS 依賴）
- Google Flow 的免費額度是每日 50 credits，付費方案是每月額度
- 影片模型：Gemini Omni（最新旗艦）和 Veo 3.1 並存
