# Jing Chu Yuan Project Handoff

Last updated: 2026-06-01 21:08 CST

## Project Overview

Repo: `/Users/admin/Desktop/程式/jingchuyuan`  
Remote: `https://github.com/ivy081499/jingchuyuan.git`  
Stack: Astro static website  
Target deployment: Cloudflare Pages

This website is for "靜初苑". It is intended to be the first public contact point for a service provider. The first release is an information-focused website with clear service explanation and contact channels. Later versions may add contact form submission, LINE Official Account notifications, data storage, and online booking.

## Business Logic

Primary visitor path:

1. Visitor lands on the home page.
2. Visitor understands what service is provided and whether it fits them.
3. Visitor checks service details, FAQ, and provider background.
4. Visitor contacts through LINE/IG or, in a later phase, submits a form.
5. Service provider manually confirms time and details.

Current product stance:

- Keep first version lightweight.
- Prefer LINE Official Account as the main contact path.
- Use form UI as a placeholder until backend behavior is confirmed.
- Use manual booking first; add automated booking only after client confirms process.

## Current Site Structure

- `/` Home: hero, service summary, suitable audience, booking flow, feedback.
- `/service/`: service details, price and booking explanation.
- `/about/`: provider intro and profile image slot.
- `/faq/`: common questions.
- `/contact/`: LINE/IG contact and placeholder form.

## Design Direction

Reference direction provided by user:

- White background.
- Thin gold typography.
- Centered brand area.
- Simple horizontal navigation.
- Calm, elegant, spacious layout.
- Watercolor/natural/plant image mood.

Current implementation follows that direction through `src/layouts/BaseLayout.astro` and page-level styles.

## Implemented

- Astro project initialized.
- Node 22 installed locally under user home for this project.
- Multi-page static site created.
- Shared layout created: `src/layouts/BaseLayout.astro`.
- Reusable image slot component created: `src/components/PictureSlot.astro`.
- Image slots are wired to fixed paths.
- Content request checklist created: `CONTENT_CHECKLIST.md`.
- Image plan created: `IMAGE_PLAN.md`.
- Cloudflare Pages deployment note created: `CLOUDFLARE_DEPLOY.md`.
- Project-local handoff skill created: `.codex/skills/jingchuyuan-handoff/SKILL.md`.
- Build verified with `npm run build`.

## Image Slots

Expected image files:

- `public/images/home/hero.webp`
- `public/images/home/service-intro.webp`
- `public/images/home/feedback.webp`
- `public/images/service/service-scene.webp`
- `public/images/about/profile.webp`
- `public/images/contact/contact.webp`

If files are missing, `PictureSlot.astro` displays a placeholder with the expected path.

## Not Implemented Yet

- [ ] Replace draft copy with client-provided official copy.
- [ ] Add final images.
- [ ] Replace placeholder LINE link with real LINE Official Account URL once provided.
- [ ] Make contact form submit data.
- [ ] Store submitted form data.
- [ ] Send form notification to LINE Official Account.
- [ ] Add spam protection such as Cloudflare Turnstile.
- [ ] Add online booking, if client confirms need.
- [ ] Deploy to Cloudflare Pages successfully.
- [ ] Configure custom domain, if client buys one.
- [ ] Commit current handoff/deployment documentation files.

## Deployment Notes

Recommended deployment:

1. Commit latest content/images.
2. Push to GitHub.
3. Connect repo to Cloudflare Pages.

Cloudflare Pages settings:

```text
Framework preset: Astro
Build command: npm run build
Build output directory: dist
Node version: 22
```

If Cloudflare asks for environment variables:

```text
NODE_VERSION=22
```

Important: this project is currently a static Astro site. Do not deploy it with `npx wrangler versions upload` or `npx wrangler deploy`. If Cloudflare logs mention `@astrojs/cloudflare`, `SESSION`, or KV provisioning, the Cloudflare project was likely created as a Worker-style deployment instead of a simple Pages static deployment. See `CLOUDFLARE_DEPLOY.md`.

Latest Cloudflare deployment troubleshooting:

- User first created a Worker-style project. Cloudflare required `Deploy command`, ran `npx wrangler versions upload`, and failed while provisioning `SESSION` KV with `a namespace with this account ID and title already exists [code: 10014]`.
- Root cause: wrong Cloudflare flow. The repo itself has no `@astrojs/cloudflare`, no `wrangler.jsonc`, and local `astro build` outputs static files to `dist/`.
- User later showed the correct Pages Build settings screen. Correct values:
  - `Framework preset`: `None` or `Astro`
  - `Build command`: `npm run build`
  - `Build output directory`: `dist`
  - `NODE_VERSION`: `22`
- If the screen says `Create a Worker` or asks for mandatory `Deploy command`, it is the wrong flow. Back out and choose Pages / static site / import Git repository.
- Cloudflare free `*.pages.dev` URL is fine for previews. For formal production, recommend buying a custom domain. Estimated yearly domain cost discussed: `.com` around NT$350-600/year, `.tw` around NT$800-1,200/year.

## Useful Commands

```bash
cd /Users/admin/Desktop/程式/jingchuyuan
PATH=/Users/admin/.local/node-versions/node-v22.16.0-darwin-arm64/bin:$PATH npm run dev -- --host 127.0.0.1
PATH=/Users/admin/.local/node-versions/node-v22.16.0-darwin-arm64/bin:$PATH npm run build
git status --short
```

## Recent Commits

- `1be68e1 Initial commit`
- `a942336 Initialize Astro project`
- `fe26cd6 Build initial website draft`
- `cf573f9 Add project handoff workflow`
- `9a4f85f Document Cloudflare branch state in handoff`
- `863f82c Document Worker autoconfig changes`
- `59c6653 Merge handoff branch workflow`
- `b2fd665 Merge no-push rule`

## Current Git State

As of 2026-06-01 21:08 CST, current branch state:

- Current branch: `chore/contact-alerts-and-workflow-rules`
- Local branch: `main` at `b2fd665`
- Remote branches:
  - `origin/main`
  - `origin/cloudflare/workers-autoconfig`
- `main` and `origin/main` both point at `b2fd665 Merge no-push rule`.
- `origin/cloudflare/workers-autoconfig` has commit `d4be162 Add Cloudflare Workers configuration`, diverging from `fe26cd6 Build initial website draft`.
- Current branch has uncommitted changes in:
  - `.codex/skills/jingchuyuan-handoff/SKILL.md`
  - `PROJECT_HANDOFF.md`
  - `src/pages/contact.astro`

Current uncommitted contact page changes:

- Instagram button now links to `https://www.instagram.com/jing_chu_yuan?utm_source=ig_web_button_share_sheet&igsh=ZDNlZDc0MzIxNw==`.
- "加入 LINE" is now a button that shows a simple `alert()` asking for LINE Official Account name, add-friend URL, LINE ID, or QR Code.
- Form button text changed from `送出表單預留` to `送出表單`.
- Form button now shows a simple `alert()` saying the form is not active yet and needs a notification target such as LINE, Email, or Google Sheet.
- Build verified after these changes with `npm run build`.

Important workflow correction:

- Normal development work should not be committed or merged unless the user explicitly asks.
- Handoff work may update and commit handoff files, but must not accidentally commit unrelated normal-development changes.
- Never run `git push`; user handles push manually.

Important: `origin/cloudflare/workers-autoconfig` was created by Cloudflare during the wrong Worker-style setup. Do not merge it into `main` for the current static Pages site. It likely contains Worker/Wrangler configuration that caused or relates to the failed deployment path.

Do not delete the remote branch without explicit user approval. Recommended handling is to ignore it for now and deploy from `main` using Cloudflare Pages static settings.

Inspected contents of `origin/cloudflare/workers-autoconfig`:

- `astro.config.mjs`: imports `@astrojs/cloudflare` and sets `adapter: cloudflare()`.
- `package.json`: adds `@astrojs/cloudflare`, `wrangler`, `deploy`, `generate-types`, `preview: npm run build && wrangler dev`, and a Vite override.
- `package-lock.json`: adds the large dependency tree for those packages.
- `wrangler.jsonc`: configures a Worker with `main: "@astrojs/cloudflare/entrypoints/server"` and assets binding.
- `public/.assetsignore`: ignores `_worker.js` and `_routes.json`.
- `tsconfig.json`: includes `worker-configuration.d.ts`.
- `.gitignore`: adds wrangler-related ignore entries.

Decision: none of these Worker/autoconfig changes should be brought into `main` for the current static Pages deployment. The only arguably harmless change is wrangler ignores in `.gitignore`, but it is unnecessary until a Worker backend is intentionally added. Keep `main` as a pure static Astro site.

## Next Recommended Steps

1. For normal development requests, start from `main`, create a descriptive branch, make edits, verify, then stop. Do not commit or merge unless the user explicitly asks.
2. For explicit handoff requests, update handoff files on a branch, commit, then merge back into `main`.
3. Do not push. The user handles all `git push` operations.
4. Do not use or merge `origin/cloudflare/workers-autoconfig`.
5. Add the prepared images to `public/images/...` using the exact filenames in `IMAGE_PLAN.md`.
6. Run `npm run build`.
7. Tell the user when `main` is ahead and let the user push to GitHub.
8. Deploy through Cloudflare Pages, not Workers.
9. After client review, update official copy and links.
10. Decide whether first release needs real form submission or only LINE/IG contact buttons.

## Handoff Skill

Project-local handoff skill is stored at:

```text
.codex/skills/jingchuyuan-handoff/SKILL.md
```

Only use this handoff file for the `jingchuyuan` / `靜初苑` website project. Other projects may have their own handoff skills and files.

When the user says "交接", "交接工作", "更新交接", "寫交接", or similar while working inside this repo or while explicitly referring to this project, update this file with the latest work state and unfinished tasks.

Branch workflow rule: normal development should be done on a branch created from `main`, but should not be committed or merged unless the user asks. Explicit handoff updates should be committed on a branch and merged back into `main` after verification. Cloudflare Pages production should use `main`.

Push rule: never run `git push` for this project unless the user gives a new explicit push instruction in the same turn. The user wants to handle pushing manually.
