# Jing Chu Yuan Project Handoff

Last updated: 2026-06-01 20:36 CST

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
- [ ] Replace placeholder LINE and Instagram links.
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

- `a942336 Initialize Astro project`
- `fe26cd6 Build initial website draft`
- `1be68e1 Initial commit`

## Current Git State

As of 2026-06-01 20:36 CST, current branch state:

- Local branch: `main`
- Remote branches:
  - `origin/main`
  - `origin/cloudflare/workers-autoconfig`
- `main` has local commit `cf573f9 Add project handoff workflow` and is ahead of `origin/main` by 1 commit.
- `origin/cloudflare/workers-autoconfig` has commit `d4be162 Add Cloudflare Workers configuration`, diverging from `fe26cd6 Build initial website draft`.

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

1. Commit current documentation/skill updates if desired.
2. Push `main` if the handoff commit should be available on GitHub.
3. Do not use or merge `origin/cloudflare/workers-autoconfig`.
4. Add the prepared images to `public/images/...` using the exact filenames in `IMAGE_PLAN.md`.
5. Run `npm run build`.
6. Commit image/content changes.
7. Push to GitHub.
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
