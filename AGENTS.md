# AI Workshop Agent Guide

Static HTML teaching site for medical staff learning practical AI creation: writing, safety, image, video, Google Flow, agents, and extra tools. The site is deployed from `main` to GitHub Pages at `https://ttingyu1123.github.io/ai-workshop/`.

## Project Basics

- Stack: plain HTML, CSS, and vanilla JS. No dependencies, no build step.
- Shared stylesheet: `style.css`.
- Design language: doodle / hand-drawn teaching material style.
- Audience: medical professionals who are new to AI. Keep copy concrete, low-jargon, and safety-aware.
- Official attribution: `衛生福利部台中醫院 感染科 曾婷玉醫師`.

## Detailed Instructions

- [Site Structure](.agents/site-structure.md)
- [Content Guidelines](.agents/content-guidelines.md)
- [Components And Design](.agents/components-and-design.md)
- [Verification Checklist](.agents/verification.md)

## Critical Rules

- Do not add build tooling or external JS dependencies.
- Do not change the shared header link list when adding pages; only update the active section class.
- Pages with pricing, quotas, tool availability, model names, or plans must be checked against current official or primary sources. If not verifiable, use conservative wording and avoid exact numbers.
- Never put identifiable patient data in prompts or examples. Use synthetic, de-identified cases only.
- If a page has `.prompt-block` / `.prompt-content` copy buttons, keep a page-local `copyPrompt()` script.
- New lesson pages need a `.box-success` "現在就做" task before `nav-links`.
- When changing attribution, update both screen footers in HTML and print attribution in `style.css`.

## Current Content Status

- Core lessons: Part 1 AI fundamentals, Part 2 writing, Part 3 safety.
- Creation lessons: Part 4 image, Part 5 video, Part 6 Google Flow.
- Advanced lesson: Part 7 AI Agent.
- Extras: NotebookLM, transcription, CapCut, Canva, GitHub Pages, Prompt Builder.
- Planned later: learner gallery / examples page. Patient education handouts should become a separate site, not this repo.
