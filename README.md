# WiCS Website

Static website for Women in Computer Science at ASU. The site is intentionally simple: plain HTML files with page-local CSS and JavaScript, plus organized image assets. There is no build step, framework, package install, or backend required to preview the current version.

## Live Site

- Firebase Hosting: `https://wics-asu.web.app`
- Production source branch: `main`
- Primary deployment config: `firebase.json`

This repository currently serves as the deployment-ready source for the redesigned WiCS website. Keep the public site, GitHub source, and Firebase project aligned when making production changes.

## Project Map

```text
.
|-- index.html
|-- events.html
|-- team.html
|-- sponsors.html
|-- firebase.json
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

## Tech Stack

- HTML, CSS, and vanilla JavaScript
- Firebase Hosting for deployment
- Google Fonts for typography
- Static image assets organized by page or content type

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

### Recommended Local Check

Before sharing or deploying a change, open the affected page through localhost and check:

- Desktop width around `1440px`.
- Tablet/mobile width around `390px` to `430px`.
- Navigation links and mobile drawer behavior.
- Image paths, especially new team, event, and sponsor assets.
- Hover states for sponsor logos and buttons.

## Development Flow

1. Pull the latest `main`.
2. Start a local preview server.
3. Make the smallest focused change possible.
4. Check the changed page in desktop and mobile widths.
5. Check related pages when editing shared pieces such as nav, footer, colors, sponsor styling, or mobile drawer behavior.
6. Commit related changes together with a clear message.
7. Deploy only after the local version is reviewed and ready.

Suggested commit style:

- Keep content updates, asset updates, and deployment config changes separate when possible.
- Use short messages that describe the outcome, for example `Update sponsor logo treatment`.
- Confirm `git status --short` is clean after committing and deploying.

## Deployment

The current site is static and can be deployed on the Firebase Hosting free tier. There is no build command.

Install Firebase CLI once:

```bash
npm install -g firebase-tools
```

Log in:

```bash
firebase login
```

Connect this local folder to the team's Firebase project:

```bash
firebase use --add
```

Deploy when the local version is reviewed and ready:

```bash
firebase deploy --only hosting
```

`firebase.json` is committed because it describes how Firebase Hosting should serve the static site. `.firebase/` is intentionally ignored because it contains local deployment cache files. Do not commit Firebase service account files, tokens, private keys, or environment files.

### Firebase Notes

- The committed `.firebaserc` points to the Firebase project alias used for this site.
- `firebase.json` deploys from the project root because the site has no build output folder.
- The ignore list in `firebase.json` intentionally excludes `.git/`, `.firebase/`, `.vercel/`, logs, and private env files. Do not remove those exclusions.
- If deploy output says Firebase found hundreds of files, stop and inspect `firebase.json`; it may be trying to upload repo internals.
- A healthy deploy should upload only the changed site files and then print the Hosting URL.

## Pre-Push Checklist

- Confirm changed pages load locally.
- Check mobile navigation on pages touched by nav or layout edits.
- Make sure new image paths are relative and case-correct.
- Do not commit `.DS_Store`, `.firebase/`, raw unused logo files, or private environment files.
- Keep secrets, tokens, calendar credentials, and API keys out of the repo.

## Editing Content

### Landing Page

Edit `index.html`.

- Hero copy, stats, feature pillars, and sponsor band markup live in the HTML body.
- The community mosaic uses images from `images/home-page-images/hero-photos/`.
- The sponsor band appears near the bottom of the page and is duplicated once for continuous scrolling. If you add, remove, or reorder sponsors, update both sponsor sets so the loop stays seamless.

### Events Page

Edit `events.html`.

- Calendar/event data is stored in page JavaScript near the bottom of the file.
- Event detail cards include title, date, description, image, registration link, and add-to-calendar behavior.
- Recurring event cards use images from `images/events/`.
- Completed events should not keep active registration or add-to-calendar actions.
- If the calendar later connects to Google Calendar, keep public event display separate from any private credentials or API keys.

### Team Page

Edit `team.html`.

- Faculty advisor and supporter cards are written directly in the HTML.
- Officer cards are generated from the `TEAM_MEMBERS` array near the bottom of the file.
- Team photos live in `images/team/`.
- Use `images/team/blank-profile-circle.png` for missing photos.
- Officer links should use full `https://` URLs when possible so they work consistently after deployment.

### Sponsors Page

Edit `sponsors.html`.

- Sponsor cards are grouped by tier in the order shown on the page.
- Use labels like `Silver`, `Bronze`, `Tech Talk`, or `Involved`.
- Sponsor logos live in `images/sponsors/`.
- Prefer transparent PNG or SVG logos. If a logo has a white or checkerboard background baked in, create/use a cleaned transparent version and reference that from the page.

## Asset Guidelines

- Use lowercase, hyphenated filenames when adding new assets, for example `poojitha-nuthalapati.jpeg`.
- Keep images in the folder that matches their purpose:
  - `images/branding/` for WiCS logo and moth artwork.
  - `images/home-page-images/hero-photos/` for homepage mosaic photos.
  - `images/events/` for recurring event and past-event images.
  - `images/team/` for advisor, supporter, and officer photos.
  - `images/sponsors/` for company logos.
- Compress large photos before committing when possible.
- Do not commit duplicate raw files when only the cleaned/display-ready version is used.

## Maintainer Handoff Notes

- Keep officer names, roles, emails, LinkedIn links, and photos updated in `team.html`.
- Keep sponsor tiers and sponsor logo files updated together in `sponsors.html` and the homepage sponsor band.
- Keep event descriptions short and evergreen unless a date-specific event is intentionally being promoted.
- When a new webmaster takes over, walk them through local preview, Git commits, Firebase login, and one test deploy before handing off fully.
- Store private planning docs, Drive links, credentials, and internal notes outside this public repo.

## Common Tasks

Add an officer:

1. Add the officer image to `images/team/`.
2. Add or update the member object in `TEAM_MEMBERS` inside `team.html`.
3. Include `name`, `role`, `image`, `email`, and `linkedin` when available.

Add a recurring event card:

1. Add the image to `images/events/`.
2. Update the recurring event card data or markup in `events.html`.
3. Keep the description short and specific.

Add a sponsor:

1. Add the logo to `images/sponsors/`.
2. Add the sponsor to `sponsors.html` under the correct tier.
3. Add it to both sponsor-band sets in `index.html`.
4. Confirm it is visible on dark backgrounds and does not show a boxed background.

## Known Follow-Ups

- The calendar currently uses page-defined event data. If the team wants live calendar syncing, connect it to the public WiCS calendar feed without committing private credentials.
- Shared CSS is duplicated across pages. If the site grows, consider moving common styles into a shared stylesheet.
- Raw sponsor logo files with backgrounds may exist locally during cleanup; only display-ready assets should be committed.
- If the team later reconnects `asuwics.org`, confirm the custom domain inside Firebase Hosting before changing DNS or deployment settings.
