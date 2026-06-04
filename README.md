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
python3 -m http.server 8085
```

Then open `http://localhost:8085`.
