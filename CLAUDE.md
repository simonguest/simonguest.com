# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

Quarto is managed via a Python `uv` virtual environment.

```bash
# Preview the site locally with live reload
uv run quarto preview

# Build the site to _site/
uv run quarto render
```

## Architecture

This is a [Quarto](https://quarto.org) website (`_quarto.yml` sets `type: website`). All site configuration — navbar, theme, Open Graph, analytics — lives in `_quarto.yml`. The global HTML theme is `litera` with overrides in `styles.css`.

### Content structure

| Path | Purpose |
|------|---------|
| `index.qmd` | Home page; listing of all posts from `p/` |
| `presentations.qmd` | Listing of all presentations from `s/` |
| `p/<slug>/index.qmd` | Individual blog posts |
| `s/<slug>/slides.qmd` | Individual Reveal.js presentations (revealjs format) |
| `s/<slug>/index.qmd` | Listing entry for a presentation (metadata + `href: slides.html`) |
| `about/index.qmd` | About page |

Posts (`p/`) use the standard Quarto HTML format. Presentations (`s/`) use `format: revealjs`. The `s/<slug>/index.qmd` file is a thin metadata stub that points the listing at the rendered `slides.html` — it is not a standalone page.

The `p/` folder name exists for backwards compatibility with an older blog's URL scheme. New slugs should follow the same pattern for posts.

### Post front matter conventions

```yaml
title: "Post Title"
description: "One-sentence description."
date: "YYYY-MM-DD"
categories: ["Tag1", "Tag2"]
image: "./main.webp"
image-alt: "Alt text"
title-block-banner: "./banner.webp"
title-block-banner-color: "#fff"
```

### Presentation front matter conventions

`slides.qmd`:
```yaml
title: "Presentation Title"
author: "Simon Guest"
format:
  revealjs:
    slide-number: true
    incremental: true
    center-title-slide: true
    theme: [default, dark.scss]
bibliography: references.bib  # if citations used
```

`index.qmd` (listing stub):
```yaml
title: "Presentation Title"
description: "One-sentence description."
date: "YYYY-MM-DD"
categories: ["Tag1"]
image: "./images/cover.png"
href: slides.html
```

### Generating banner images from post images

```bash
ffmpeg -i main.webp -vf "eq=brightness=-0.2:contrast=0.9,boxblur=4:1" banner.webp
```

### Build outputs

- `_site/` — rendered site (deploy target)
- `_freeze/` — cached Quarto execution results
- `.quarto/` — Quarto internal cache
