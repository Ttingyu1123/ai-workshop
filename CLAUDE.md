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
├── images/<頁名>/       # 內文圖片，一頁一資料夾（規格見「圖片擺放規範」）；ai-image/ = Part 4 對比圖（來源 PNG 在 Downloads\教學素材）
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
- `.result-compare` — **本站圖片擺放的預設格式**（見下方「圖片擺放規範」）
- `.site-header` — sticky header + 純 CSS 漢堡選單（checkbox hack）
- `.site-footer` — footer 含 IG/GitHub SVG icon

### 圖片擺放規範（預設格式）

內文放圖一律用 `.result-compare` 縮圖 + lightbox 點擊放大，不要直接放大圖撐版面：

```html
<div class="result-compare">
  <figure>
    <img src="images/<頁名>/<slug>.webp" alt="<具體描述圖片內容>" loading="lazy">
    <figcaption><span class="tool-chatgpt">ChatGPT</span> 生成結果</figcaption>
  </figure>
  <figure>…</figure>
</div>
```

- **檔案**：存 `images/<頁名>/`，ASCII slug 檔名（CJK 檔名在 URL 會亂編碼）；WebP 長邊 ≤1200px（Pillow：`im.save(out, "WEBP", quality=Q, method=6)`）。quality 依內容：一般照片/截圖用 82；**滿版小字教學海報用 74**（82 會到 200-250KB，74 落在 150-195KB 且小字仍清晰 — Part 1 全 14 張的實測值，2026-07）。單檔目標 ~150-195KB
- **海報批次流程**（Part 1 已跑完一輪的 SOP）：來源在 `Downloads\教學素材`（編號＋中文檔名）→ 先 md5sum 查重複（曾有 04/08 同檔）→ 逐張 Read 看內容寫 alt → Pillow 轉檔 → 插入對應章節 → Playwright 全頁捲動驗證（lazy load 圖要捲到才載入，直接查 `naturalWidth` 會誤判 BROKEN）→ commit+push
- **縮圖**：CSS 固定高度裁切頂部（桌面 180px / 手機 130px，`object-fit: cover`），雙欄並排；點擊開 lightbox 看全圖。直式海報用裁切、不用等比縮小（縮成細長條反而看不清）
- **圖說**：工具對比用 `.tool-chatgpt`（綠）/ `.tool-gemini`（藍）著色；非對比情境 figcaption 寫圖片說明即可
- **lightbox JS**：跟 `copyPrompt()` 同慣例，每頁 `<script>` 重複定義、不抽外部 JS — 從 ai-image.html 頁尾複製那段 IIFE（建立 `.lightbox`、點擊/Esc 關閉、鎖背景捲動）
- **alt 文字**：必須先實際看過圖片內容再寫，不要從檔名猜

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

1. 複製 google-flow.html 作模板（骨架最標準）
2. 更新 `<title>` / `<meta description>` / og 四項（og:url 指向新頁）/ hero badge / h1
3. header nav **不要動連結清單**，只把自己所屬分區標 `.active`（分區歸屬見「導航結構」）
4. 更新 TOC；底部 nav-links 串進閱讀鏈（同時要改前一頁的「下一課」連結）
5. nav-links 前加一個 `.box-success`「🎯 現在就做」小任務框（5-15 分鐘可完成的實作）
6. 確認 `</head>` 前有 GA4 snippet（G-L05KFZJS9L，從模板複製就會帶到）
7. 在 index.html 對應分區加課程卡片；sitemap.xml 補一條
8. 含方案/價格/額度的內容：表格上方加「📅 資訊更新於 YYYY 年 M 月 — 以官方公告為準」；查證不到的數字寫保守描述，不編數字
9. 有 `.prompt-block` 就要帶頁尾 `copyPrompt()` script（刻意每頁重複定義，不抽外部 JS）
10. 有內文圖片就照「圖片擺放規範」：`.result-compare` 縮圖 + 頁尾 lightbox IIFE（從 ai-image.html 複製）
11. 驗收：`grep` 檢查頁內連結都指向存在的檔案、hero badge 與分區 active 一致；有圖的頁面確認每個 img src 都有對應實體檔案

### 交給 subagent 寫頁面時
- Prompt 裡直接貼「完整 header nav 標記」與「底部 nav-links 標記」，不要讓 agent 自己推導
- 要求先 WebSearch 查證工具現況（2-3 查詢），查不到就寫保守版，嚴禁編造額度/價格數字
- 明確劃界：只寫這一個新檔案，不碰導航、不 commit
- agent 回報完成後必驗：檔案存在、行數合理、結尾是 `</html>`、`copyPrompt` 與 copy-btn 數量相符 — agent 可能中途撞額度死掉，回報訊息可能只是 rate-limit 錯誤

## 待做項目

### 內容
- [x] 加入用戶生成的圖片範例（ai-image.html 全 9 個 prompt 附 ChatGPT vs Gemini 對比圖，`.result-compare` 元件在 style.css）
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
- [ ] 番外 — 本機／開源生圖入門（ComfyUI ＋ RunningHub 免顯卡線上跑）：定位是操作課不是節點工程 — 動機（本機生成＝資料不出機器，呼應 Part 3）→ 桌面版安裝 → 跑出第一張圖 → 沒顯卡走 RunningHub。寫完後把 ai-image.html `#advanced-tools` 的 ComfyUI／RunningHub 兩張卡加上導流連結（2026-07-07 決策）
- [ ] 番外 — 得獎作品復盤：Midjourney × Kling 工作流（用戶的得獎影片＝MJ 生圖 → Kling 圖生影片，兩工具是上下游、一頁講完不拆兩頁）：定位是案例復盤不是工具大全 — 從得獎作品倒推每個決策（MJ 段：風格 prompt、角色/風格一致性；Kling 段：圖生影片、首尾幀銜接、運鏡），學員不必跟做付費段，想動手的用 ChatGPT 免費生圖＋Kling 免費額度跟做圖生影片（接 Part 4→5 產線）。素材（得獎影片、MJ 原圖、prompt 紀錄）由用戶提供。若 MJ prompt 技巧內容爆量再拆獨立頁（2026-07-07 修正決策：原「MJ 不開頁」的前提「用戶不熟 MJ」錯誤 — 得獎作品即 MJ+Kling 製作）

### 技術
- [x] OG 圖片（og-image.png，doodle 插畫，與 website repo `public/images/insights/ai-workshop.png` 是同一張圖，換圖時要兩邊同步）
- [x] favicon（聽診器笑臉，從 og-image.png 裁出三種尺寸）
- [x] Google Analytics — GA4 已掛全站（Measurement ID `G-L05KFZJS9L`，snippet 在各頁 `</head>` 前；新頁面記得帶上）
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
