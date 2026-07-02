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
├── index.html          # 首頁（課程卡片牆）
├── ai-fundamentals.html # Part 1 — AI 基礎觀念
├── ai-image.html       # Part 2 — AI 圖像生成
├── ai-video.html       # Part 3 — AI 影片製作
├── google-flow.html    # Part 4 — Google Flow 實戰
├── 404.html            # GitHub Pages 404（連結用 /ai-workshop/ 絕對路徑）
└── og-image.png        # OG 分享圖（doodle 插畫 1024x1024，與 website Insights 卡片同一張）
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
- `.site-header` — sticky header + 純 CSS 漢堡選單（checkbox hack）
- `.site-footer` — footer 含 IG/GitHub SVG icon

## 導航結構

所有頁面共用 header/footer：
- Header：✏️ AI Workshop logo → 首頁 / AI 基礎 / AI 圖像 / AI 影片 / Google Flow / 作品集 ↗
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
- [ ] CapCut 教學頁面
- [ ] Canva 教學頁面
- [ ] AI Agent 教學頁面（index.html 已有 coming-soon 卡片）
- [ ] GitHub Pages 建站教學頁面（index.html 已有 coming-soon 卡片）
- [ ] 醫學筆記/衛教圖專區（待規劃）

### 技術
- [x] OG 圖片（og-image.png，doodle 插畫，與 website repo `public/images/insights/ai-workshop.png` 是同一張圖，換圖時要兩邊同步）
- [ ] favicon
- [ ] Google Analytics（可選）
- [ ] sitemap.xml

## 注意事項

- 不要用 Delius Swash Caps 字型（大寫 I 看起來像 J，對 AI 主題致命）
- Prompt 區塊的 `copyPrompt()` 函式在每個頁面的 `<script>` 中重複定義（刻意，避免外部 JS 依賴）
- Google Flow 的免費額度是每日 50 credits，付費方案是每月額度
- 影片模型：Gemini Omni（最新旗艦）和 Veo 3.1 並存
