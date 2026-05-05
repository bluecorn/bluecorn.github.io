# Template options for the bluecorn.github.io Jaspr site

> Research notes from session ending 2026-05-05. Goal: pick a one-page,
> Creative-Commons-licensed developer-website template, then hand-convert
> it to Jaspr as a learning exercise.

## Headline finding

**There is no "awesome-jaspr" list yet.** Searches across GitHub topics and the
broader web don't surface a community-curated index. The closest references
that already live in this repo:

- `upstream/jaspr/apps/website/` — the source of [docs.jaspr.site](https://docs.jaspr.site)
  itself; production-grade reference, but complex.
- `upstream/jaspr/examples/` — small focused examples (Flutter embedding,
  Riverpod, Shelf backend, etc.). Mostly demonstrate non-static features; not
  a fit for a one-page landing.

So the candidate templates below are sourced from the broader CC / MIT
template ecosystem, with the conversion to Jaspr to happen by hand.

---

## Tier 1 — Plain HTML/CSS/JS (easiest to port)

These minimise the layers between source and rendered output, so each `<section>`
maps cleanly to a Jaspr `StatelessComponent` and each CSS rule to an `@css` block.

| Template | Demo | License | Tech | Why short-list |
|---|---|---|---|---|
| **Identity** (HTML5UP) | https://html5up.net/identity | CC BY 3.0 | HTML + CSS + Skel/Sass + a few JS lines | Tiny — single profile/card. Best "hello world" conversion. |
| **Highlights** (HTML5UP) | https://html5up.net/highlights | CC BY 3.0 | HTML + CSS + jQuery scroll plugin | True single-pager with 4–5 sections. Realistic dev landing. |
| **Hyperspace** (HTML5UP) | https://html5up.net/hyperspace | CC BY 3.0 | HTML + CSS + jQuery | Hero-style intro + sections. Modern aesthetic. |
| **Read Only** (HTML5UP) | https://html5up.net/read-only | CC BY 3.0 | HTML + CSS + minimal JS | Sidebar + scroll content. Good for text-heavy CV-like layout. |
| **nisarhassan12/portfolio-template** | https://github.com/nisarhassan12/portfolio-template ([demo](https://nisar.dev)) | MIT | **Pure** HTML + CSS + vanilla JS, zero frameworks | The cleanest source code of all of these. |

## Tier 2 — Still portable, more visual weight

| Template | Demo | License | Notes |
|---|---|---|---|
| **Massively** (HTML5UP) | https://html5up.net/massively | CC BY 3.0 | Article/blog parallax. More CSS to translate, but still single-page. |
| **Solid State** (HTML5UP) | https://html5up.net/solid-state | CC BY 3.0 | Sidebar nav + section columns. |
| **Paradigm Shift** (HTML5UP) | https://html5up.net/paradigm-shift | CC BY 3.0 | More modern, more visual chrome. |

## Tier 3 — Skip for a learning project

| Template | Why skip |
|---|---|
| **RyanFitzgerald/devportfolio** | MIT, but Astro + Tailwind v4 + TypeScript — conceptually distant from Jaspr's component model and CSS-in-Dart; you'd unlearn Astro idioms during the port. |
| **website-templates/portfolio_one-page-template** | MIT, but requires Pug + Sass + Gulp build before producing HTML. Extra step with no learning benefit; you'd port the dist output, not the source. |

---

## How to choose

Two questions:

1. **How much content do you actually have?**
   - Just "name, blurb, a few links" → **Identity**
   - 3–5 distinct sections (about / projects / skills / contact) → **Highlights** or **nisarhassan12/portfolio-template**
   - CV-style long-scroll → **Read Only** or **Massively**

2. **How much JS interactivity do you want from the start?**
   - HTML5UP templates lean on jQuery for scroll effects + mobile menus — those parts will be the most interesting to redo as `@client`-annotated Jaspr `StatefulComponent`s.
   - **nisarhassan12** uses tiny vanilla JS, so JS conversion is more direct.
   - For *learning Jaspr's hydration model*, having some JS to port is a feature, not a bug.

### Top pick for first conversion

**HTML5UP "Highlights"** or **nisarhassan12/portfolio-template** — both exercise:
- Multi-section layout → multiple Jaspr components
- Real CSS rules → `@css static List<StyleRule> get styles =>` blocks
- A small amount of JS interactivity → `@client` boundary practice

**Identity** is the better "warm-up" if you'd rather start with the absolute minimum.

---

## What the conversion will involve (preview)

When we resume:

1. **Download the chosen template** somewhere outside the build (likely `notes/` or a temp dir, gitignored).
2. **Read the original `index.html`** end to end — identify each top-level `<section>` and its purpose.
3. **Map sections → Jaspr components**:
   - Each `<section>` becomes a Dart class extending `StatelessComponent` in `lib/components/` or `lib/sections/`.
   - The page assembly lives in `lib/app.dart` (replacing the current `Home + About` placeholders).
4. **Translate CSS → `@css` blocks**:
   - Global rules go into `lib/constants/theme.dart` (we already have a theme file).
   - Component-scoped rules become `static List<StyleRule> get styles` on the relevant component.
   - Use the `jaspr-styling` skill we just installed for the canonical patterns.
5. **Re-implement JS interactivity**:
   - Smooth scroll, mobile menu toggle, scroll-spy → `StatefulComponent`s with `@client`.
   - The `jaspr-pre-rendering-and-hydration` skill explains the boundary.
6. **Replace placeholders**:
   - Swap the brick's `web/favicon.ico` and `web/images/logo.svg` with the template's assets.
   - Update `lib/main.server.dart` `Document(title: …)` to your real site title.
7. **Build + verify**:
   - `fvm dart run jaspr_cli:jaspr serve` for live dev
   - `fvm dart run jaspr_cli:jaspr build` for production
8. **Attribution**:
   - HTML5UP CC BY 3.0 → keep the credit footer (or buy a no-attribution license if preferred). Their templates already include it.
   - MIT GitHub templates → typically just keep the LICENSE file in `LICENSES/` or a `THIRD_PARTY_NOTICES.md`.

## Sources (for traceability)

- HTML5 UP index: https://html5up.net
- GitHub topic: https://github.com/topics/developer-portfolio-template
- GitHub topic: https://github.com/topics/portfolio-template
- nisarhassan12/portfolio-template: https://github.com/nisarhassan12/portfolio-template
- RyanFitzgerald/devportfolio (skip-listed): https://github.com/RyanFitzgerald/devportfolio
- Local Jaspr reference site: `upstream/jaspr/apps/website/`
