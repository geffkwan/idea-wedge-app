# Vouch Ledger — design system notes

Shared by the marketing site (`../index.html`) and the product (`../app/index.html`).
Tokens and components live in `tokens.css`. This file is the "why" and the rules.

## Voice

We sound **defiant, energetic, inspirational, empowering, wise, confident**.
We act **innovative, expressive, responsive, visionary, adventurous, authentic**.

- Short declaratives. Second person. No hedging, no "we believe".
- Terminal vocabulary where it is honest: `verified`, `signed`, `issued`, `anchored`,
  `[01]`, `>`, `//`. Never fake CLI output that implies a feature that does not exist.
- The chain is invisible on the reading side. "Verify" is a button, not a wallet.
- Marketing copy may be placeholder / lorem ipsum. The two messages that must land:
  - **Companies:** distribution into high-value, high-signal users.
  - **Candidates:** build and bolster your resume, make applications credible, get
    access and exposure to cutting-edge technology and ideas.

## Look

**Neo-brutalist technical minimalism, infused with terminal/hacker aesthetics and
speculative retro-futurism.** Influence: TypeSafe AI.

Rules:

1. **Palette is closed.** Only the seven swatches plus white (`--paper`).
   - `#201A21` ink: nearly all text, every border, inverted sections.
   - `#E1B9ED` lilac and `#F0F2B3` butter: the main colors. Large fills, panels, highlights.
   - `#EE4239` signal: used *less*. High-impact sections, the one CTA that matters,
     error/alert, the index bracket color, cursor, prompt glyph.
   - `#ECEDE4` bone: the neutral ground. Use it to give the reader a break between
     colorful sections. It is the default page background.
   - `#32326C` navy and `#A15A71` plum: sparingly. Navy = info/links in prose. Plum =
     pending/warm secondary. Never as large fills on the site; small accents only.
2. **No border radius.** Ever. Square avatars, square chips, square modals.
3. **2px ink borders** on anything that is an object (a card in the pool, a plan, a
   button, a modal). Content that is merely *in view* gets reticle corners or a single
   rule, not a box, and sits directly on bone. Hard offset shadows (`4px 4px 0 ink`)
   on anything that is raised or interactive. Press-down physics on buttons (hover
   lifts, active drops).
4. **Type:** Archivo (variable; display at `font-stretch: 118%`, weight 900,
   uppercase, tight tracking) for headlines and big numbers. JetBrains Mono for
   labels, buttons, tags, data, code. Archivo normal width for body.
5. **Labels are terminal labels.** `[01] CANDIDATES`, `// WHY IT WORKS`, `> VERIFY`.
   Uppercase mono, 11–12px, letterspaced. The bracket index is signal red.
6. **Textures are derivatives of the name.** Working direction is "Seen", so every
   texture descends from sight: halftone that resolves into focus (`.tex-resolve`),
   aperture/iris rings (`.tex-aperture`), a scan raster (`.tex-raster`, `.tex-scan` on
   inverted sections), and viewfinder reticle marks (`.reticle`) in place of full
   frames. The grid is retired. Bone sections stay mostly flat so the reader gets a
   break. One texture per section, not three. If the name changes, re-derive.
7. **Rhythm on the site:** alternate loud and quiet. A lilac or butter section,
   then a bone section. Signal red at most once or twice per page as a full
   section. Inverted ink sections for "terminal" moments (live ledger, how
   verification works).
8. **Rhythm in the app:** bone ground, white boxes with ink borders, butter for
   "verified"/success, lilac for selection and primary-shadow, signal only for
   alerts and the single most important CTA on a screen. The app takes fewer
   risks than the site but must not read as stock shadcn: square everything,
   mono labels, hard shadows on primary actions, terminal-style status rows.
9. **Status colors:** verified = ink on butter (not green). Pending = plum.
   Info = navy. Alert = signal. There is no green and no blue anywhere.
10. **Motion:** fast and mechanical. 120ms transforms, step blinks, linear marquees.
    No easing curves that feel soft. Respect `prefers-reduced-motion`.

## Shared components (see tokens.css)

`.box` `.box.raised` `.box-head` `.btn` (`.primary` `.signal` `.lilac` `.butter`
`.ghost` `.flat` `.sm` `.lg`) `.tag` (`.ok` `.pending` `.info` `.alert`) `.chip`
`.lbl` (`.sq` `.gt` `.sl`) `.idx` `.stamp` `.term` `.term-bar` `.marquee` `.tbl`
`.field` `.bar` `.meter` `.avatar` (`.anon`) `.kpi` `.big` `.note` `.toast`
`.modal` and section tints `.inv` `.on-lilac` `.on-butter` `.on-signal` `.on-bone`.

## Linkage between site and app

- The site's **"Browse the pool"** section shows anonymized candidates (role,
  seniority, verified-skill tags, ledger strength, vouch count, last active). No
  names, no photos, no employers. The same anonymized card is what a company sees
  in the app's tester pool before an engagement exists.
- Site → app: "Sign in" and every CTA deep-link to `app/index.html` with a role
  hash (`#candidate`, `#company`, `#voucher`).
- App → site: the public profile (`vouch.id/m/handle`) is rendered in the site's
  chrome because hiring managers arrive from outside, with no account.
