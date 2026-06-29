# CLAUDE.md — RCCG The Shelter website

Project context for Claude Code. Read this before editing.

## What this is
A single-page marketing/landing site for **RCCG The Shelter**, Okota — the youth
expression of RCCG under Youth Province 2. Tagline: *"a place of refuge and strength."*
Audience: young people + visitors in Lagos. The page's job: make a first-time visitor
feel welcome and get them to **plan a visit** or **watch/listen live**.

Live at: `https://emmyxayo.github.io/rccgtheshelterhouse/`

## Stack & hard constraints (do not break these)
- **One file:** everything is in `index.html` (HTML + CSS + vanilla JS inline). No framework, no build step, no bundler.
- **Images stay separate** in `images/` — never base64-inline them into the HTML (GitHub Pages + file-size reasons). Reference with relative paths.
- **Deploys to GitHub Pages at repo root.** `index.html` must stay at root; keep paths relative.
- **No new heavy dependencies.** Allowed externals: Google Fonts, the YouTube `<iframe>` embed, the Google Maps embed. Otherwise vanilla JS only.
- Keep the page light and fast. Lazy-load below-the-fold images. No layout shift (CLS).
- **Accessibility & motion:** visible `:focus-visible` rings, keyboard-operable, semantic landmarks, and **fully respect `prefers-reduced-motion`** (animations collapse to instant). Mobile-clean down to 360px, no horizontal scroll.

## Brand tokens (already defined as CSS vars in `:root`)
- Indigo (anchor): `--indigo:#291670` · `--indigo-deep:#190A4A` · `--indigo-2:#3A2391`
- The five "shelter" colors: purple `#A9518B`, cyan `#01AFEE`, green `#A8CE45`, red `#EC3237`, yellow `#FFF112`
- Type: **Bricolage Grotesque** (display) · **Inter** (body/UI) · **Fraunces** italic (the tagline accent only)
- **Signature element:** the five-arch "shelter" motif — inline SVG `<symbol id="shelterMotif">`. Reused in hero + footer. This is the brand's memorable device; build animation around it, don't replace it.

## Conventions
- Drive all color from the CSS vars above; don't hardcode new hexes outside the palette.
- Sections use `.section-pad`, headings use `.head`, scroll-in uses `.reveal` (IntersectionObserver adds `.in`).
- Social icons are SVG `<symbol>`s (`#i-ig`, `#i-yt`, `#i-fb`, `#i-mx`, `#i-wa`).
- Keep the existing section order/ids: `#about #services #watch #sermons #events #gallery #quiz #give #visit`.

---

# BRIEF: make the landing (hero) exceptional

Spend the boldness in the hero; keep everything below it calm. Ship these, smallest-risk first. After each, verify the acceptance criteria before moving on.

### 1. Orchestrated hero entrance (load animation)
On first paint, run one ~1.2s sequence (not scattered effects):
- The connecting arch line **draws in** (animate `stroke-dashoffset`).
- The five arches **rise + fade** in a staggered sequence, left→right (~80ms apart).
- Headline reveals with a clip/mask wipe; tagline (`.tag`) fades up after; lead + CTAs follow.
- Reduced-motion: everything visible instantly, no transforms.

### 2. Ambient "refuge" atmosphere
The theme is shelter / rest / His presence — use light, gently.
- A soft godray / light-glow behind the arches (CSS gradients or a low-opacity SVG), very subtly drifting.
- Optional fine grain/noise overlay (CSS or tiny inline SVG) for depth — keep it whisper-quiet.
- Must not hurt text contrast or LCP. No heavy canvas loops.

### 3. Next-service countdown + live state  ⭐ (highest value)
Replace/augment the three static info chips with a live, useful widget:
- Service times: **Sundays 08:00** and **Wednesdays 18:30**, timezone **Africa/Lagos (WAT, UTC+1)** — compute correctly regardless of the visitor's own timezone.
- During a service window (start → +90 min): show **"● We're live now"** linking to Listen Live (Mixlr) / the `#watch` section.
- Otherwise: **"Next gathering: Sunday · in 2d 14h 22m"** with a ticking countdown.
- Pure JS, no libs. Update every second; clean up nicely.

### 4. Cursor-reactive arches
- On pointer move over the hero, the arches do a subtle parallax tilt / glow (a few px). Disable on touch + reduced-motion. Keyboard users unaffected.

### 5. Micro-polish
- `:focus-visible` rings on all interactive elements.
- Nav highlights the section currently in view (scroll-spy).
- A quiet scroll-cue chevron at the bottom of the hero.

## Acceptance criteria (check every item)
- [ ] Lighthouse: Performance ≥ 90, Accessibility ≥ 95 (mobile).
- [ ] No CLS; hero text is the LCP and paints fast (no blocking on the iframe).
- [ ] `prefers-reduced-motion: reduce` → no entrance/parallax/ambient motion.
- [ ] 360px wide: no horizontal scroll; countdown + arches legible.
- [ ] Countdown shows the correct next service from a few spoofed clocks (Sat night, Sun 08:15 = live, Wed 18:00, Thu).
- [ ] Still one file; `images/` untouched; deploys to Pages root unchanged.

## Out of scope (leave alone unless asked)
Below-the-hero sections, giving details (still placeholder — owner to provide Paystack + account), copy rewrites.

## Working style
Single-purpose commits, one enhancement at a time, show a diff/preview before moving on. Don't refactor working code that isn't part of the task.
