# AI Workshop — 醫療人員 AI 創作工作坊

靜態 HTML 教學網站，部署在 GitHub Pages。面向不熟悉 AI 的醫療人員，教 AI 圖像/影片/語音合成。

## 技術架構

- **純靜態站**：HTML + CSS + vanilla JS，零依賴、零 build
- **部署**：GitHub Pages（`main` branch → 自訂網域 `https://workshop.tingyudeco.com/`；舊網址 301 轉址；DNS 在 Cloudflare CNAME `workshop`）
- **設計系統**：Doodle 手繪風（基於 typeui.sh/design-skills/doodle）

## 檔案結構

頁面平鋪於根目錄，無 build，僅 `images/` 子目錄。核心課程頁 7 個（ai-fundamentals~ai-agent.html，Part 1-7）；番外工具頁約 16 個（notebooklm/capcut/canva/comfyui/kling 等教學頁 + qr-maker/watermark 等零依賴小工具）。

**踩坑**（改對應頁面前必看）：
- **404.html**：連結用根目錄絕對路徑，勿加 `/ai-workshop/` 前綴
- **qr-maker.html**：勿用 qrcodejs（中文 UTF-8 overflow），改用 qrcode-generator（cdnjs）
- **watermark.html**：canvas 用 LXGW 字型前須 `await document.fonts`
- **voice-notes.html**：限 Chrome/Edge、辨識走雲端非離線，頁內已標示勿口述病人資料
- **handout-20260723.html**：**學員限定隱藏頁**，不進 index/sitemap/header、head 有 noindex，靠課堂 QR code 進入——審計勿當 orphan page「補登」。Prompt 正本在 Obsidian `03_Projects/AI-Workshop/第一堂課 課堂講義.md`，改講義先改正本
- **about.html**：僅 footer 連入
- **index.html**：`.workshop-grid` 兩欄排列，header 錨點不含 `#tools`（小工具累積到 4-5 個再考慮升格）

## 設計規範

### 字型
標題/手寫 `Caveat`+`LXGW WenKai TC`；內文 `LXGW WenKai TC` 主體+`Caveat` fallback；程式碼 `JetBrains Mono`（皆 Google Fonts）。

### 文案語體（全站一致，新頁面與改稿一律遵守）
- **專業但親切**：受眾是不熟 AI 的醫療人員，要好懂；但這是**課堂教學素材**，語體須正式，**避免網路口語與俚俗填充詞**。
- **禁用口語詞 →改法**：很能打→表現出色｜手癢加字→自行加入文字｜踩雷→誤觸風險｜追新→採用最新｜塞爆→佔滿｜八成是→多半是｜跑跑看→實際測試｜別被…嚇到→無需理會｜玩玩看→了解運作｜整包送你→一併提供｜說了算→由…決定｜給不了→無法提供｜上雲端→改用雲端｜類 stock→圖庫素材｜想抽幾張就抽幾張→可不限次數生成。同 register 的其他口語一併比照。
- **保留（不算口語）**：醫學／生活類比（`.analogy` 框）、`🎯 現在就做` 語氣、emoji、第二人稱「你」。交給 subagent 寫／改頁面時把本節一併貼進 prompt。

### 色彩 Token
`--primary #49B6E5` 主色/連結/標籤｜`--secondary #263D5B` 深色文字/header｜`--text #111827` 內文｜`--success #16A34A` 優點｜`--warning #D97706` 注意｜`--danger #DC2626` 禁止/缺點

### 排版
Base 18px / line-height 1.9；container max-width 900px；背景筆記本橫線；斷點 640px/768px（header）。

### 元件
`.tool-card`／`.prompt-block`+`copyPrompt()`／`.card`,`.card-grid`／`.analogy`／`.box-tip`,`.box-danger`,`.box-success`／`.result-compare`（見下方）／`.site-header`,`.site-footer`（sticky header+CSS 漢堡選單；footer 無 GitHub icon，作者有未完成專案）。`.box-success`／`.box-tip.page-summary` 用法見 SOP 步驟 5。

### 圖片擺放規範（預設格式）
內文圖一律用 `.result-compare` 縮圖 + lightbox，不要放大圖撐版面。Markup／lightbox IIFE 從 `ai-image.html` 頁尾複製（同 `copyPrompt()` 慣例，每頁 `<script>` 重複定義不抽外部 JS）。

- **檔案**：存 `images/<頁名>/`，ASCII slug 檔名（CJK 檔名 URL 會亂編碼）；WebP 長邊 ≤1200px（Pillow `quality=Q, method=6`）。一般照片/截圖 quality 82；**滿版小字海報用 74**（省重量、字仍清晰）。單檔目標 ~150-195KB
- **批次流程**：來源 `Downloads\教學素材` → md5sum 查重複 → 逐張 Read 寫 alt → Pillow 轉檔 → 插入章節 → Playwright 全頁捲動驗證（lazy load 要捲到才載入，直接查 `naturalWidth` 會誤判 BROKEN）→ commit+push
- **縮圖**：CSS 固定高度裁切頂部（桌面 180px/手機 130px），直式海報用裁切不用等比縮小
- **圖說**：工具對比用 `.tool-chatgpt`（綠）/`.tool-gemini`（藍）著色；alt 須先看過圖片內容再寫，不從檔名猜

## 導航結構

- Header 是**分區錨點導航**：首頁 / 基礎必修(#core) / 創作應用(#create) / 進階實戰(#advanced) / 番外工具(#extras)，指向 index.html 四個 section；作品集連結只在 footer
- 每頁標自己所屬分區 `.active`：Part 1-3→#core、Part 4-6→#create、Part 7→#advanced、番外頁→#extras
- 閱讀鏈：Part 1→2→3→4→5→6→7→notebooklm→ai-transcribe→capcut→canva→github-pages→chrome-skills→comfyui→kling
- **新增課程不要動 header** — 只加 index 卡片和串閱讀鏈；Footer 含署名/授權句/IG/作品集，不放 GitHub

## 新增頁面 SOP

1. 複製 google-flow.html 作模板（骨架最標準）
2. 更新 title/meta description/og 四項/hero badge/h1；同步 `rel="canonical"`（同 og:url）與 JSON-LD name/description/url（`@type`：教學頁 `LearningResource`、工具頁 `WebApplication`；author/license 照抄不動）
3. header nav **不要動連結清單**，只標自己分區 `.active`
4. 更新 TOC；nav-links 串進閱讀鏈（同時改前一頁「下一課」連結）
5. nav-links 前加 `.box-success`「🎯 現在就做」任務框（5-15 分鐘）；教學頁另在 `<main>` 開頭加 `.box-tip.page-summary`「📌 本頁重點」（教什麼/適合誰/注意；工具頁不放）
6. 確認 `</head>` 前有 GA4 snippet（G-L05KFZJS9L）
7. index.html 對應分區加課程卡片；sitemap.xml 補一條
8. 方案/價格/額度內容加「📅 資訊更新於 YYYY 年 M 月」；查不到就寫保守描述，不編數字
9. 有 `.prompt-block` 帶頁尾 `copyPrompt()` script（每頁重複定義不抽外部 JS）
10. 有圖照「圖片擺放規範」：`.result-compare` + lightbox IIFE
11. 驗收：連結都指向存在檔案、hero badge 與分區 active 一致、img src 都有實體檔案

### 交給 subagent 寫頁面時
- Prompt 直接貼「完整 header nav 標記」與「底部 nav-links 標記」，不要讓 agent 自己推導
- 要求先 WebSearch 查證工具現況，查不到就寫保守版，嚴禁編造額度/價格數字
- 明確劃界：只寫這一個新檔案，不碰導航、不 commit
- 完成後必驗：檔案存在、結尾是 `</html>`、`copyPrompt` 與 copy-btn 數量相符——agent 可能撞額度死掉，回報可能只是 rate-limit 錯誤

## 待做項目

- [ ] 範例牆／學員作品頁（靜態 gallery + Google 表單收件，等有作品再做）
- [ ] 衛教單專區 → **獨立成站**（受眾是民眾非醫療人員，另開 repo，不放本站）
- [ ] 番外 — 得獎作品復盤：Midjourney × Kling 工作流，一頁講完不拆頁；寫完回頭在 ai-video.html Kling 卡、ai-image.html Midjourney 卡加導流
- [ ] chrome-skills.html 補圖

過程紀錄不留本檔——查 git log 或 Obsidian `03_Projects/AI-Workshop/`。

## 工具實測事實（改頁前引用，勿憑印象改數字；完整數據見 Obsidian）

- **Google Flow**：免費層每日 50 credits 不累計；Veo Lite 10 credits **不是 0**；影片固定 8 秒、下載僅 270p GIF/720p；口白引號會同義改寫，需逐字校對
- **Kling**：每日贈靈感值約 66 點（政策常變，頁內標「以 App 顯示為準」）；免費層限 2.6，3.0 需 Pro
- **ComfyUI**：Comfy Cloud 免費層已收；RunningHub 每日贈 100 credits 為入口
- **NotebookLM**：表格輸出露 `<br><br>`，提問加「儲存格不要用 HTML 標記」可解

## 注意事項

- **署名**：衛生福利部台中醫院 感染科 曾婷玉醫師（不放 IG/GitHub/個人網站）。改署名時螢幕 footer 與列印版權行（style.css `@media print`）兩處同步
- **授權條款**：全站教材採 **CC BY-NC-SA 4.0**（正本 about.html）。改授權須同步四處：(1) 各頁 head `rel="license"` + JSON-LD `license` (2) footer `.footer-license` (3) style.css `body::after` (4) about.html 條款內文
- 不要用 Delius Swash Caps（大寫 I 像 J，對 AI 主題致命）
- **GA4**：獨立 property `544090519`（`G-L05KFZJS9L`），與 website（532664866）分開，`.env` 的 `GA4_PROPERTY_ID_WORKSHOP` 指向本站
- og-image.png 與 website repo `public/images/insights/ai-workshop.png` 同一張圖，換圖兩邊同步
