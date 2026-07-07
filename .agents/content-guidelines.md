# Content Guidelines

## Audience And Tone

- Write for medical staff who are smart but may be new to AI.
- Prefer plain Traditional Chinese with concrete examples.
- Use medical analogies only when they make the concept easier, not as decoration.
- Make the takeaway actionable: what to try, what to avoid, and how to verify.
- Keep tool recommendations task-based: "use this for long documents", "use this for image drafts", etc.

## Medical Safety

- Treat safety and privacy as core curriculum, not a footnote.
- Never use real names, chart numbers, birthdays, exact dates, addresses, face photos, rare combinations, or other identifiable patient data in examples.
- Say explicitly that AI output is draft/support material and must be reviewed by qualified staff before patient-facing, academic, or clinical use.
- For clinical or policy claims, prefer conservative wording and point learners back to source verification.
- If content touches recording, transcription, or ambient scribe workflows, mention consent and institutional policy.

## Tool And Pricing Claims

- For plans, quotas, model names, availability, and prices, verify current official or primary sources first.
- Put a visible update note above tables or recommendation blocks, e.g. `資訊更新於 YYYY 年 M 月，以官方公告為準`.
- If an exact number cannot be verified, write "額度有限", "依方案而定", or similar conservative wording.
- Do not invent future product names, quota numbers, or release dates.

## Page Content Pattern

Course pages should generally include:

- Hero badge and clear `h1`.
- Short intro explaining why the topic matters to medical staff.
- Table of contents.
- Concept explanation.
- Practical examples or workflow.
- Safety/limitations section.
- Prompt examples when useful.
- A 5-15 minute "現在就做" task before bottom navigation.

## Pre-Course Review Checklist

Fast-changing tool info lives in these sections. Before each workshop session, re-verify against official sources and bump the `資訊更新於` date if anything changed:

- `google-flow.html` — 免費額度與方案 table (daily 50 credits, paid tiers), 影片生成 section (Gemini Omni / Veo 3.1 model names)
- `ai-image.html` — 進階之路 section (GPT Image 2, paid/open-source tools table)
- `ai-video.html` — 免費影片工具 and 付費高品質工具 tables (two update notes)
- `ai-agent.html` — 三大工具介紹 plans table
- `ai-writing.html` — 三大對話工具 free-tier notes
- `ai-fundamentals.html` — 主流工具比較 table
- `ai-safety.html` — 各家資料政策 table
- `notebooklm.html` / `canva.html` / `capcut.html` / `ai-transcribe.html` — 免費額度與方案 sections
- `course-prep.html` — account signup steps and free-tier claims

Search anchor: `grep -n "資訊更新於" *.html` lists every block that carries volatile claims.

## Suggested Improvements Backlog

- [x] Add a one-page "課前準備 / 帳號與工具清單" for learners. (course-prep.html, 2026-07)
- Add downloadable checklist or print-friendly handout for privacy review.
- Add learner gallery only after real examples are available.
- Keep patient education handouts in a separate site because the target audience is the public, not medical staff.
