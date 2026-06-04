# WiCS Website

Static website for Women in Computer Science at ASU. The site is intentionally simple: plain HTML files with page-local CSS and JavaScript, plus organized image assets. There is no build step, framework, package install, or backend required to preview the current version.

## Project Map

```text
.
|-- index.html
|-- events.html
|-- team.html
|-- sponsors.html
|-- images/
|   |-- branding/
|   |-- events/
|   |-- home-page-images/
|   |   `-- hero-photos/
|   |-- sponsors/
|   `-- team/
`-- README.md
```

## Pages

- `index.html`: landing page, moth hero, community photo mosaic, feature pillars, and scrolling sponsor band.
- `events.html`: monthly event calendar, event detail panel, recurring event cards, and past-event references.
- `team.html`: faculty advisors, honorary faculty supporters, and officer board cards.
- `sponsors.html`: sponsor logo page with tiers and involved partners.

## Shared Patterns

- Each page is standalone and includes its own `<style>` block. When changing a shared pattern like nav, mobile menu, colors, or footer, update each page that uses that pattern.
- Core visual tokens live near the top of each page in `:root`: `--bg`, `--ink`, `--purple`, `--purple-2`, `--purple-3`, `--mono`, `--serif`, and `--sans`.
- The navigation is repeated across all pages. Keep active links page-specific by applying `class="active"` only to the current page's nav link.
- Mobile support is CSS-only. The hamburger menu uses a hidden checkbox plus labels, so it works without JavaScript.
- The site uses external Google Fonts: `DM Serif Display`, `Instrument Sans`, and `Geist Mono`.

## Local Preview

Run a simple static server from the project root:

```bash
python3 -m http.server 8080
```

Then open `http://localhost:8080`.

If that port is busy, choose another one:

```bash
python3 -m http.server 8090
```

Then open the matching localhost URL, such as `http://localhost:8090`.

Opening an HTML file directly with `file://` can work for quick checks, but a local server is preferred because it matches deployment behavior more closely.

## Development Flow

1. Pull the latest `main`.
2. Start a local preview server.
3. Make the smallest focused change possible.
4. Check the changed page in desktop and mobile widths.
5. Check related pages when editing shared pieces such as nav, footer, colors, sponsor styling, or mobile drawer behavior.
6. Commit related changes together with a clear message.
7. Deploy only after the local version is reviewed and ready.

## Deployment

The current site is static and can be deployed directly through Vercel. There is no build command.

Preview deploy:

```bash
npx vercel deploy . -y
```

Production deploy, only when the team is ready:

```bash
npx vercel deploy . --prod -y
```

`.vercel/` is intentionally ignored so local Vercel project metadata and deployment settings do not get committed.

## Pre-Push Checklist

- Confirm changed pages load locally.
- Check mobile navigation on pages touched by nav or layout edits.
- Make sure new image paths are relative and case-correct.
- Do not commit `.DS_Store`, `.vercel/`, raw unused logo files, or private environment files.
- Keep secrets, tokens, calendar credentials, and API keys out of the repo.
