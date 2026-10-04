# Vouch Ledger — prototypes

Two surfaces, one design system, no build step. Open either HTML file directly in a
browser (Google Fonts load from the network; everything else is local).

| Path | What it is |
| --- | --- |
| `index.html` | **Marketing site.** Bold, neo-brutalist front door. Includes the anonymized "browse the pool" section so companies can look before they buy. Every CTA deep-links into the app. |
| `app/index.html` | **Product prototype.** Sign-in, then the candidate, voucher and company workspaces, plus the public profile a hiring manager sees. Shared in-memory state across all personas, persisted to `localStorage`. |
| `design/tokens.css` | **Shared design system.** Palette, type, borders, shadows, and the component classes both surfaces use. |
| `design/DESIGN.md` | Voice and look rules, palette usage, status colors, and how the site and app link together. |
| `CONCEPT.md` | Where the idea came from, the actors, how money moves, the trust architecture, and the Idea Wedge gates. |
| `NOUNS.md` | Domain vocabulary for data modeling. |

## Palette

| Swatch | Role |
| --- | --- |
| `#201A21` ink | Text, borders, inverted sections |
| `#E1B9ED` lilac, `#F0F2B3` butter | Main colors |
| `#EE4239` signal | Used less: impact sections, the one CTA that matters, alerts |
| `#ECEDE4` bone | Neutral ground to give the reader a break |
| `#32326C` navy, `#A15A71` plum | Sparing accents (info, pending) |

## Model assumptions baked in

- Plans: Starter $99 / Growth $299 / Scale $899 per month, buying tester seats.
- Tester payouts are set by the company and passed through; Vouch keeps 20%.
- Vouches come from identity-verified outsiders (LinkedIn, work email, optional
  government ID), tied to one specific claim, signed onto both records.
- Hiring managers, candidates and vouchers never pay. Vouchers earn standing.
- Phase one is centralized: records are signed and sealed in our store and can be
  mirrored to a public chain later. The UI no longer talks about blocks or hashes.

All people, companies and numbers are fictional.
