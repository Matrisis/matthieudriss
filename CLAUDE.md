# CLAUDE.md

Project-specific instructions for Claude Code.

These rules bias toward correctness, maintainability, and safety over speed.
For trivial tasks, use judgment and avoid unnecessary ceremony.

---

## Project Context

French B2B lead generation landing page for "Audit IA & Agentic Dev" consulting service.
Service: "Diagnostic IA" (500€ HT). Funnel: free discovery call → Diagnostic IA → MVP Build.

Stack: HTML, CSS, vanilla JS — no build step, no framework, no package manager.

Deployed on Vercel. Push to `main` triggers automatic redeploy — no manual step needed.

Important files:
- `index.html` — single-page site; all content lives here
- `styles.css` — all styles; design system defined here
- `DESIGN.md` — design decisions and color reference
- `og-image.png` — social preview card; must be regenerated manually when service name or pricing changes in HTML
- `.vercelignore` — blocks sensitive files (CLAUDE.md, DESIGN.md, etc.) from Vercel production
- `sitemap.xml` — SEO sitemap

Architecture notes:
- Teal accent: `oklch(48% 0.09 195)` = `#006d6d`. Use when generating images or matching design.
- `og-image.png` generated with Python/Pillow using SF Mono (IBM Plex Mono as target font).
- PageSpeed Insights public API has rate limits — avoid repeated calls in automation.

---

# Hard Rules

These rules are non-negotiable.

## 1. Think Before Coding

Do not assume. Do not hide confusion. Surface tradeoffs.

Before implementing:
- State assumptions explicitly.
- If multiple interpretations exist, present them instead of silently choosing.
- If a simpler approach exists, mention it.
- Push back when the requested approach seems overcomplicated or risky.
- If something is unclear and materially affects the implementation, ask before coding.

For trivial tasks, proceed without unnecessary back-and-forth.

## 2. Simplicity First

Use the minimum code required to solve the problem correctly.

Do not add:
- Features beyond what was asked.
- Abstractions for single-use code.
- Speculative flexibility or configurability.
- New dependencies unless clearly justified.
- Error handling for impossible scenarios.
- New infrastructure unless required.

If you write 200 lines and it could be 50 without losing correctness, rewrite it.

Ask: "Would a senior engineer consider this overcomplicated?"
If yes, simplify.

## 3. Surgical Changes

Touch only what is necessary for the requested task.

Every changed line must trace directly back to the user's request.

Do not:
- Refactor unrelated code.
- Reformat unrelated files.
- Rename unrelated variables, functions, or files.
- Upgrade dependencies unless required.
- Fix unrelated bugs without permission.
- Delete pre-existing dead code unless asked.

Match the existing code style, even if you would personally write it differently.

If you notice unrelated issues, mention them separately instead of fixing them.

When your own changes create unused imports, variables, functions, files, or comments, clean them up.
Do not clean up pre-existing dead code unless explicitly asked.

## 4. Goal-Driven Execution

Before implementation, define success criteria.

For each task, identify:
- Expected behavior.
- Files or areas likely to change.
- Verification steps.
- Tests or checks that should pass.

For multi-step tasks, use this format:

1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]

## 5. Verify Before Reporting Completion

Do not report a task as complete until the implementation has been verified.

Use the strongest applicable method for this project:
- Visual browser check for UI changes.
- grep/inspect HTML source for content changes.
- Visual check of og-image.png after regeneration.

When reporting completion, include:
- What changed.
- How it was verified.
- Any checks that could not be run.
- Any remaining risks or follow-up work.

Code existing is not the same as the feature working.

## 6. Destructive Commands Require Permission

Do not run irreversible or destructive commands without explicit user confirmation.

This includes, but is not limited to:
- `git push --force`
- `git reset --hard`
- `git clean -fd`
- `rm -rf`
- Deleting branches
- Overwriting environment files
- Merging or rebasing shared branches
- Force installing or removing dependencies

If unsure whether a command is destructive, ask first.

---

# Medium-Priority Rules

## UI Verification

Browser verification is the primary quality check — this project has no tests or build step.

For UI changes:
- Verify the page renders without errors in a browser.
- Check the affected section visually.
- Use Playwright or Claude Chrome extension when configured.
- Do not rely only on reading HTML/CSS for visual changes.

If browser verification is unavailable, state that clearly and provide manual steps.

## Coupled Changes

Some changes require paired updates — missing one half is a bug:
- **Service name or pricing in `index.html`** → also regenerate `og-image.png`.
- **New sensitive file added to repo** → also add it to `.vercelignore`.

## Content: Do Not Revert

- Service name: "Diagnostic IA" (was "Consultation personnalisée" — do not revert)
- Price: 500€ HT (was 300€ — do not revert)
- H1 must contain "Diagnostic IA" keyword for SEO.

---

# Low-Priority References

## Learning From Corrections

If the user corrects Claude's implementation or says the approach was wrong:

1. Apply the correction first.
2. Identify the underlying reusable lesson.
3. Add the lesson to `docs/AI_LEARNINGS.md` if it is likely to matter again.
4. Keep the note short and actionable.

Do not add one-off task details to the learning file.

## File Size Rule

Keep this file short.

- Ideal: under 200 lines.
- Maximum: under 300 lines.

Move detailed or area-specific instructions into scoped rule files instead of expanding this file.
