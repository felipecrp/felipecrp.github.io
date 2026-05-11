# felipecrp.github.io

Personal site and blog of Felipe Curty, built with [Hugo](https://gohugo.io/) and the [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme. Deployed to GitHub Pages from `main` via the workflow in [.github/](.github/).

Live: https://felipecrp.github.io

## Requirements

- Hugo **extended**, v0.160.1 or newer
- Git (with submodule support)

On Arch / WSL:

```sh
sudo pacman -S hugo
```

## Setup

The PaperMod theme is a git submodule and must be initialized after cloning:

```sh
git clone https://github.com/felipecrp/felipecrp.github.io.git
cd felipecrp.github.io
git submodule update --init --recursive
```

If Hugo complains about missing partials (e.g. `partials/templates/_funcs/get-page-images not found`), the pinned PaperMod commit predates your Hugo version. Update the theme:

```sh
cd themes/PaperMod
git checkout master
git pull origin master
cd ../..
git add themes/PaperMod
git commit -m "Update PaperMod theme"
```

## Local preview

Run the dev server with drafts visible:

```sh
hugo server -D
```

Site will be served at http://localhost:1313/.

## Authoring

### Create a new post

```sh
hugo new content posts/YYYY-MM-DD-slug.md
```

Posts live in [content/posts/](content/posts/). Filename convention: `YYYY-MM-DD-slug.md`.

### Front matter

Existing posts use YAML front matter:

```yaml
---
title: Post Title
description: One-line summary shown on listings and social cards.
date: YYYY-MM-DD
author: 'Felipe Curty'
tags:
  - tag1
  - tag2
---
```

Set `draft: true` to keep a post out of production builds; remove or set `false` when ready to publish.

### Drafts

The [_drafts/](_drafts/) folder is a holdover from the prior Jekyll setup and is **not** rendered by Hugo. To resume one, move the file into `content/posts/`, rename it to the `YYYY-MM-DD-slug.md` convention, and add proper front matter.

## Structure

```
content/
  posts/           Blog posts
  projects.md      /projects page
  publications.md  /publications page
  search.md        /search page
  assets/          Images and other assets referenced by posts
archetypes/        Templates used by `hugo new`
layouts/           Local overrides on top of PaperMod
themes/PaperMod/   Theme (git submodule)
hugo.yml           Site config (menu, social icons, Disqus, GA)
```

## Deployment

Pushing to `main` triggers the GitHub Actions workflow in [.github/](.github/), which builds the site and publishes to GitHub Pages. No manual build step required.
