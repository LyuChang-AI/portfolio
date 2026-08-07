# Lyu Chang — Academic Portfolio

Single-page academic portfolio for Lyu Chang, PhD researcher at Universitat de
Barcelona (Programa de Doctorat en Física), researching large language model
auditing for digital gender-based violence.

Live at: https://lyuchang-ai.github.io/portfolio/

## Tech stack

Plain HTML with inline CSS. No JavaScript, no framework, no CMS, no build
step — the whole site is one `index.html` file.

## Local preview

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000 in a browser.

## Structure

- `index.html` — the entire site (single page): identity, contact links,
  research summary, education, supervisors, recent academic activity
- `assets/img/avatar.jpg` — profile photo
- `404.html` — GitHub Pages error page

## Updating content

Everything (bio, links, education, activity list) lives directly as plain
HTML in `index.html` — edit it and push, no data files or templating.

## Deploy

Pushing to `main` publishes automatically — GitHub Pages, "Deploy from a
branch": branch `main`, folder `/ (root)`. No CI pipeline.
