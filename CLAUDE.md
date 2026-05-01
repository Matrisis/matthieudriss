# CLAUDE.md

Project-specific instructions for Claude Code.

These rules bias toward correctness, maintainability, and safety over speed.
For trivial tasks, use judgment and avoid unnecessary ceremony.

---

## Project Context

Landing page for Audit Claude Code & Agentic Dev service. French B2B lead generation site. Single-page static site, no build step.

Stack: HTML, CSS, vanilla JS

Important directories: `/` — root contains index.html, styles.css, DESIGN.md, CLAUDE.md

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

Use the strongest applicable verification method:
- Unit tests
- Integration tests
- Type checks
- Linting
- Build checks
- Manual runtime checks
- UI verification when relevant

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
- Dropping databases
- Running destructive migrations
- Overwriting environment files
- Merging branches
- Rebasing shared branches
- Force installing or removing dependencies

If unsure whether a command is destructive, ask first.

---

# Low-Priority References

## Scoped Rule Files

Load these rules when working in the relevant area:

- API work: `docs/ai-rules/api.md`
- Frontend/UI work: `docs/ai-rules/frontend.md`
- Database work: `docs/ai-rules/database.md`
- Testing work: `docs/ai-rules/testing.md`

Do not load unrelated scoped rules unless the task touches that area.

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
