# Site configuration for halloween.onthecompound.org

Hugo site for the Halloween on the Compound light show, using the
[Ananke](https://github.com/gohugo-ananke/ananke) theme.

## Requirements

- [Hugo](https://gohugo.io/installation/) extended, matching the version pinned in
  `.github/workflows/docker.yml` (currently `0.164.0`)

## Local development

```sh
hugo server -D
```

This serves the site at `http://localhost:1313/` with drafts included and live reload
on file changes.

To produce a production build (output goes to `public/`):

```sh
hugo
```

## Structure

- `content/en/` — pages and posts (Markdown). Posts live under `content/en/post/`;
  give a post its own directory with an `index.md` (a "page bundle") when it has a
  co-located image, so the theme can resize it as a page resource.
- `layouts/` — local overrides of theme templates. Only files that need to differ
  from the theme belong here; everything else is inherited from Ananke.
- `static/` — files copied to the site root as-is (e.g. `static/images/`).
- `config.yml` — site config, including theme params under `params.ananke`
  (social links, list thumbnails, etc.) and pagination settings.

## Theme

The theme is pulled in as a Hugo module (see `go.mod`/`go.sum`), not vendored, so
upgrading it is a matter of bumping the version there. After changing `go.mod`, run:

```sh
hugo mod tidy
```

Ananke's own docs and available `params.ananke.*` options are documented in the
[theme's README](https://github.com/gohugo-ananke/ananke).

## Deployment

Pushes to `master` build the site with Hugo and publish a Docker image via
`.github/workflows/docker.yml`, then trigger a Watchtower webhook to redeploy.
