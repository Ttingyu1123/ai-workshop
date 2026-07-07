# Site Structure

## Files

- `index.html` - home page with section card walls: `#core`, `#create`, `#advanced`, `#extras`.
- `ai-fundamentals.html` - Part 1, AI fundamentals.
- `ai-writing.html` - Part 2, AI writing.
- `ai-safety.html` - Part 3, AI safety and privacy.
- `ai-image.html` - Part 4, AI image generation.
- `ai-video.html` - Part 5, AI video production.
- `google-flow.html` - Part 6, Google Flow.
- `ai-agent.html` - Part 7, AI Agent.
- `notebooklm.html`, `ai-transcribe.html`, `capcut.html`, `canva.html`, `github-pages.html`, `prompt-builder.html` - extra tools.
- `style.css` - shared doodle design system and print styles.
- `images/<page>/` - page-specific images. Use ASCII slugs.
- `sitemap.xml`, `robots.txt`, `404.html`, `qr-site.png`, `og-image.png`, favicons - deployment/support assets.

## Navigation

All pages share the same header/footer pattern.

- Header links are section anchors only: home, `#core`, `#create`, `#advanced`, `#extras`.
- Do not list every page in the header.
- Active section mapping:
  - Part 1-3: `index.html#core`
  - Part 4-6: `index.html#create`
  - Part 7: `index.html#advanced`
  - Extra pages: `index.html#extras`
- Portfolio link stays in footer only: `https://tingyudeco.com`.

## Reading Chain

Bottom `nav-links` order:

`Part 1 -> Part 2 -> Part 3 -> Part 4 -> Part 5 -> Part 6 -> Part 7 -> NotebookLM -> AI Transcribe -> CapCut -> Canva -> GitHub Pages`

When inserting a new page, update the previous page's next link, the new page's previous/next links, `index.html`, and `sitemap.xml`.

## New Page SOP

1. Copy `google-flow.html` as the template.
2. Update title, meta description, Open Graph fields, `og:url`, hero badge, and `h1`.
3. Keep header link list unchanged; only set the correct `.active` class.
4. Update the TOC and bottom `nav-links`.
5. Add a `.box-success` "現在就做" task before `nav-links`.
6. Ensure the GA4 snippet `G-L05KFZJS9L` is present before `</head>`.
7. Add the card to the correct `index.html` section and add the URL to `sitemap.xml`.
8. If the page has prompts, include the local `copyPrompt()` script.
