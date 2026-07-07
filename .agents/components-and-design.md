# Components And Design

## Design Tokens

- Fonts:
  - Headings/handwritten: `Caveat` and `LXGW WenKai TC`.
  - Body: `LXGW WenKai TC`.
  - Code: `JetBrains Mono`.
- Colors:
  - `--primary`: `#49B6E5`
  - `--secondary`: `#263D5B`
  - `--text`: `#111827`
  - `--success`: `#16A34A`
  - `--warning`: `#D97706`
  - `--danger`: `#DC2626`
- Layout:
  - Base font size 18px, line-height 1.9.
  - Container max-width 900px, horizontal padding 32px.
  - Notebook-line background.
  - Responsive breakpoints around 640px and 768px.

## Reusable Components

- `.tool-card` - tool introduction with pros/cons.
- `.prompt-block` / `.prompt-content` - copyable prompts with `.copy-btn`.
- `.card` / `.card-grid` - information cards.
- `.analogy` - medical analogy callout.
- `.box-tip`, `.box-danger`, `.box-success` - callouts.
- `.site-header` - sticky header using the CSS checkbox menu.
- `.site-footer` - footer with IG, GitHub, and portfolio links.
- `.result-compare` - default image comparison/gallery format.

## Image Rules

- Store page images in `images/<page>/`.
- Use ASCII filenames and WebP for content images.
- Target long edge no more than 1200px and keep files reasonably small.
- Use `.result-compare` thumbnails plus the lightbox script for in-page images.
- Do not guess alt text from filenames; inspect the image and describe the actual content.
- For tool comparisons, use `.tool-chatgpt` and `.tool-gemini` labels in captions.

## Prompt Blocks

- Keep `copyPrompt()` defined in each page that has copy buttons. This duplication is intentional to avoid external JS dependencies.
- Copy button count should match expected prompt blocks.
- Do not extract shared JS unless the project direction changes.

## Print Attribution

Print output uses `style.css` `@media print` with footer/watermark attribution. If official attribution changes, update both:

- Every screen footer in page HTML.
- Print attribution in `style.css`.
