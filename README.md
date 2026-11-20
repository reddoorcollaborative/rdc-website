# Red Door Collaborative - website

Staging rebuild of reddoorcollaborative.com, built with [Astro](https://astro.build) and deployed to GitHub Pages. Production stays on Squarespace for now. The RDC design system (the org default design system in Claude) governs colors, type, logo, and components.

- Preview: https://reddoorcollaborative.github.io/rdc-website/
- This repo and the published site are both public.

## Rules

- Commit only media already published on the live site. Never commit unreleased client work, drafts, or QA versions.
- Never commit font files. Licensed Suisse fonts live in the private repo `reddoorcollaborative/rdc-brand-fonts` and are copied into `src/fonts/` at build time.
- Never hardcode an internal link. Build it from `import.meta.env.BASE_URL` with a trailing slash, for example `` href={`${BASE}about/`} ``.
- Every push to `main` deploys. Use a branch and pull request for unapproved changes.

## Local development

```bash
npm install
npm run dev       # http://localhost:4321
npm run build     # outputs ./dist
npm run preview
```

A local build needs the font files in `src/fonts/`.

## Structure

- `src/layouts/Layout.astro`: shared head, nav, footer
- `src/components/`: Nav, Footer, CTASection
- `src/pages/`: index, about, services, work, careers, contact, contact-success, and the case studies (Azure Essentials, VSS Benefits, Procraft)
- `src/media/`: images processed by Astro
- `public/`: files served as-is (favicon, logo SVGs, video, CNAME)
- `src/styles/global.css`: design system tokens and shared classes

## Deploying

`.github/workflows/deploy.yml` builds and deploys on every push to `main`. It needs the `FONTS_REPO_TOKEN` Actions secret: a fine-grained token with read-only Contents access to `rdc-brand-fonts`.

## Contact form

`src/pages/contact.astro` posts to Web3Forms. The access key is still a placeholder.

## Custom domain

Out of scope until the owner decides to move production off Squarespace. When that happens, set the custom domain in Settings, then Pages, point DNS at GitHub Pages, and change `base` in `astro.config.mjs` to `'/'`.
