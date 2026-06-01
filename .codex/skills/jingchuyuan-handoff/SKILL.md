---
name: jingchuyuan-handoff
description: Use only for the /Users/admin/Desktop/程式/jingchuyuan Astro website project when the user asks to hand off, update handoff notes, summarize current Jing Chu Yuan/靜初苑 website work, or prepare the next AI/session. Do not use for other projects. Trigger only if the current repo is jingchuyuan or the user explicitly mentions jingchuyuan, 靜初苑, this website project, or /Users/admin/Desktop/程式/jingchuyuan together with phrases such as "交接", "交接工作", "更新交接", "寫交接", "handoff", or "handover".
---

# Jing Chu Yuan Handoff

## Project

- Repo path: `/Users/admin/Desktop/程式/jingchuyuan`
- GitHub remote: `https://github.com/ivy081499/jingchuyuan.git`
- Stack: Astro static site, deployed target is Cloudflare Pages.
- Node for local commands: `/Users/admin/.local/node-versions/node-v22.16.0-darwin-arm64/bin`

## When Triggered

Use this skill only if one of these is true:

- Current working directory is `/Users/admin/Desktop/程式/jingchuyuan` or inside it.
- The user explicitly mentions `jingchuyuan`, `靜初苑`, `這個網站專案`, or `/Users/admin/Desktop/程式/jingchuyuan`.

Do not use this skill for generic handoff requests in other repositories. Other projects may have their own handoff skills.

When the user asks for this project handoff:

1. Work in the repo root.
2. Read `PROJECT_HANDOFF.md`, `git status --short --branch`, `git branch -a`, `git branch -vv`, recent commits, and any changed files relevant to current work.
3. Update `PROJECT_HANDOFF.md` with:
   - exact date/time if useful
   - what changed today
   - current implementation status
   - decisions made
   - unfinished work
   - next recommended steps
   - risks/blockers
   - local and remote branch state, especially extra deployment-created branches
   - file-level diff summary for any deployment-created branch, not just branch names
   - commands already verified
4. Preserve useful previous context; do not erase open tasks unless completed.
5. Decide whether a branch is needed:
   - For documentation-only handoff updates on a clean or already-active working branch, update and commit directly.
   - For risky code changes, unrelated dirty worktree changes, or experimental handoff-related fixes, create a descriptive branch before editing.
   - Do not create a new branch for handoff documentation unless there is a clear isolation reason.
   - Never overwrite unrelated user changes.
6. Commit handoff updates by default unless the user explicitly asks not to commit.
7. Report the commit hash and any remaining uncommitted files.

## Current Product Context

This is a client-facing website for "靜初苑". Its purpose is to be the first public contact point for a service provider.

Business goals:

- Present the service clearly.
- Help visitors decide whether the service fits them.
- Provide contact channels such as LINE Official Account and Instagram.
- Later support a contact form, automatic provider notification, and possibly online booking.

Current recommended product direction:

- Multi-page static website, not only one-page.
- Mobile-first design.
- Calm visual style: white background, gold thin typography, generous spacing, light elegant mood, watercolor/natural image direction.
- Keep first release lightweight: service information + contact links + form UI placeholder.

Pages:

- `/` Home: hero, service summary, suitable audience, booking flow, feedback.
- `/service/`: service details, price/booking explanation.
- `/about/`: provider intro, background, philosophy, profile image.
- `/faq/`: common questions.
- `/contact/`: LINE/IG contact and form UI placeholder.

Image plan:

- `public/images/home/hero.webp`
- `public/images/home/service-intro.webp`
- `public/images/home/feedback.webp`
- `public/images/service/service-scene.webp`
- `public/images/about/profile.webp`
- `public/images/contact/contact.webp`

Supporting docs:

- `CONTENT_CHECKLIST.md`: content request checklist for client.
- `IMAGE_PLAN.md`: exact image slots, filenames, and sizing guidance.
- `PROJECT_HANDOFF.md`: persistent handoff notes.

## Current Technical Context

Use these commands:

```bash
cd /Users/admin/Desktop/程式/jingchuyuan
PATH=/Users/admin/.local/node-versions/node-v22.16.0-darwin-arm64/bin:$PATH npm run dev -- --host 127.0.0.1
PATH=/Users/admin/.local/node-versions/node-v22.16.0-darwin-arm64/bin:$PATH npm run build
```

Deployment plan:

- Push to GitHub.
- Deploy through Cloudflare Pages.
- Build command: `npm run build`
- Output directory: `dist`
- Node version: `22` or env var `NODE_VERSION=22`

## Important Boundaries

- The current contact form is visual only. It does not submit data.
- LINE/IG links are placeholders until client provides URLs.
- Online booking is not implemented.
- LINE Official Account notification is not implemented.
- Do not claim the site is fully functional until form/backend links are wired.
- Do not overwrite user-provided images or content without checking current git status first.

## Handoff Writing Style

Keep `PROJECT_HANDOFF.md` concise but specific. Prefer current facts and next actions over narrative. Use checkboxes for pending items. Include file paths when relevant.
