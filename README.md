# VNTGE CULTURE — Brand Identity + Website Build

![Brand](https://img.shields.io/badge/brand%20identity-A6FF4D?style=flat-square)
![Web](https://img.shields.io/badge/web%20build-single--file%20HTML%2BCSS-39F5B4?style=flat-square)
![Responsive](https://img.shields.io/badge/responsive-1440%20%2F%20390-43E6D0?style=flat-square)
![A11y](https://img.shields.io/badge/axe-0%20violations-43E6D0?style=flat-square)
![Fonts](https://img.shields.io/badge/fonts-self--hosted-43E6D0?style=flat-square)
![Requests](https://img.shields.io/badge/third--party%20requests-0-A6FF4D?style=flat-square)
![Status](https://img.shields.io/badge/status-concept%20%2F%20pre--launch-A6FF4D?style=flat-square)
![MIT](https://img.shields.io/badge/license-MIT-8a9a9a?style=flat-square)

> **Concept project — read the status before the screenshots.**
> VNTGE CULTURE is a **brand and website build**: identity, design system, static site and the
> document tooling behind it. The venture is **pre-launch**. Nothing in the site claims a
> result it hasn't earned: the hero figures are the build's own numbers (7 tokens, 2
> typefaces, 0 raster images), and the stockist strip is explicitly labelled
> **"illustrative marks — no affiliation"**. There are no invented sales figures and no real
> retailer names anywhere in the markup.

---

## Portfolio showcase

**Desktop — first fold**

![VNTGE CULTURE desktop preview](docs/preview-desktop.png)

**Full page**

![VNTGE CULTURE full page](docs/preview-full.png)

**Mobile — 390 px**

![VNTGE CULTURE mobile preview](docs/preview-mobile.png)

Real captures of the served site at 1440×900 and 390×844 — zero console errors, zero axe
violations, no horizontal scroll (measured, see [Verification](#verification)).

---

## The design system

Everything in the site comes from **seven tokens and two typefaces** — no framework, no build
step, no utility soup. The whole brand can be re-skinned from the `:root` block.

| Token | Value | Role |
|---|---|---|
| `--black` | `#1A1A1A` | Page ground — warm black, not pure `#000` |
| `--dark` | `#2D2D2D` | Panel / card elevation |
| `--gold` | `#C8A97E` | Primary accent — logo, CTAs, rules |
| `--gold-light` | `#E8D5B7` | Accent tint — stat labels, nav wordmark |
| `--cream` | `#F5F0E8` | Warm neutral for display and body copy |
| `--white` | `#FFFFFF` | Headings on dark |
| `--gray` | `#8E8A84` | Secondary copy, footer meta — tuned to clear 4.5:1 |

**Typography** — two families, split by job, **self-hosted** as variable woff2 (latin subset,
59 KB total, SIL OFL 1.1):

- **Montserrat** (300–900) for the brand voice: wordmark, display headlines, section titles.
  Heavy weights carry the vintage-archive feel; the tight letter-spacing on the wordmark
  (`VNTGE CULTURE`) is the identity's signature.
- **Space Grotesk** (400–700) for reading: body copy, navigation, labels. Its squarish
  terminals echo industrial clothing tags without fighting Montserrat for attention.

Self-hosting was the point, not a detail: the page makes **zero third-party requests**, so it
renders identically offline and leaks nothing to a font CDN.

**Structure** — `hero → marquee → collections → about → stockists → social → newsletter →
footer`, with a fixed translucent nav that picks up a hairline gold border.

**Signature moments**

1. The gold **hairline kicker** (`VINTAGE STREETWEAR — SS26 CONCEPT`) that frames the hero —
   it sets the archival tone before a word is read, and states the project's status.
2. The **marquee strip** between hero and collections (`AUTHENTIC VINTAGE · CURATED
   STREETWEAR · WORLDWIDE SHIPPING · WHOLESALE AVAILABLE`) — the wholesale promise stated
   as a rhythm, not a paragraph.
3. **Ten hand-drawn inline SVG garment glyphs** (tee, denim jacket, sneaker, cap, jeans,
   tote) — no raster image anywhere, so the art stays sharp at any density and the page
   weighs nothing. The sneaker carries a heel collar, laces and a toe cap; the cap carries
   panel seams and a peak — drawn, not emoji.
4. The **archive specimen card** in the About section: a typographic plate (`ARCHIVE 001`,
   the wordmark, a gold rule, `SS26 — PRE-LAUNCH`) doing the job a lookbook photo would do,
   in a build that ships no photography.

---

## Repository layout

```text
brand/
  logo.svg                 wordmark + mark (scalable, single file)
website/
  index.html               the full site — markup, design system, behaviour
  fonts/
    fonts.css              @font-face declarations
    montserrat-latin-var.woff2
    space-grotesk-latin-var.woff2
docs/
  preview-desktop.png      real capture, 1440×900
  preview-full.png         real capture, full page
  preview-mobile.png       real capture, 390×844
```

**Kept local on purpose** (excluded via `.gitignore`, never pushed): the company profile PDF,
the analytics dashboard XLSX, the pitch deck PPTX, email templates, and the launch plan —
built by `documents/build_streetwear.py` (`openpyxl` + `python-pptx` + `reportlab`).
Business material does not belong in a public repository; the tooling does.

---

## Verification

Measured on the served build, not asserted:

| Check | Result |
|---|---|
| axe-core — WCAG 2.1 A/AA, 1440×900 | **0 violations** |
| axe-core — WCAG 2.1 A/AA, 390×844 | **0 violations** |
| Console / page errors | **0** at both viewports |
| Horizontal scroll | **none** — `window.scrollTo(9999, y)` moves 0 px at both widths |
| Mobile navigation | disclosure button, `aria-expanded` toggles, `Escape` closes and returns focus |
| Third-party requests | **0** — fonts are local |
| Raster images | **0** |

Two defects were found by this pass and fixed rather than shipped: the `--gray` token
(`#6B6B6B`) failed contrast at 3.26:1 on the page ground — it is now `#8E8A84`; and the
`@VNTGECULTURE` heading could not wrap at 390 px, forcing a 23 px sideways scroll — section
headings are now fluid (`clamp(24px, 7vw, 36px)`).

---

## The build pipeline behind the brand

The brand is one half of a reusable pattern I use for venture builds:

| Stage | Output | Tooling |
|---|---|---|
| Identity | Logo, palette, type, voice | SVG + token block |
| Website | Responsive static site | Single-file HTML/CSS/JS |
| Office material | Company profile, dashboard, deck | `build_streetwear.py` (openpyxl / python-pptx / reportlab) |
| Templates | Email signatures, outreach | Local HTML templates |

The same pipeline produced the Quality House agricultural-export package — the point of the
pattern is that a venture's brand, site and collateral stay consistent because they are
generated from one token set, not re-typed per artefact.

---

## Status — honest labels

**Concept / pre-launch.** The brand system and site build are complete, responsive and
accessible. The venture behind it has not launched: the stockist marks are placeholders and
must be replaced with real partners before any commercial use, and the newsletter form is a
visual mockup with no backend.

## Licence

MIT for this repository's code and design — see [`LICENSE`](LICENSE).
Montserrat and Space Grotesk are licensed under the SIL Open Font License 1.1.
