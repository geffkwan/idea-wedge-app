# Vouch Ledger — interactive prototype

A single-file, high-fidelity prototype of the Vouch Ledger concept with the
paid-testing revenue model layered on top of the original verified-ledger idea.

Open `index.html` directly in a browser. No build step, no dependencies beyond
Google Fonts (falls back to system fonts offline). State lives in memory with
optional `localStorage` persistence; use **Reset demo** in the top bar to start over.

## What it covers

| Perspective | Screens |
| --- | --- |
| **Overview** | Landing page with the three audiences and a live ledger ticker |
| **Candidate** | Home, paid-test marketplace, active task workflow with escrow + on-chain minting moment, portable ledger, resume stamping, tracked apply links, earnings wallet |
| **Company** | Growth overview, campaign list + results (funnel, quotes, cost per customer), 3-step campaign builder, ranked tester pool, plans and billing |
| **Verify** | Public candidate page a hiring manager sees (no account), per-entry chain verification, stamped-resume checker |
| **Model** | Flywheel diagram, revenue sliders (plans + 20% take on payouts), pricing page and per-task cost table |

The two sides share one state: launch a campaign as the company and it appears
in the candidate marketplace; complete a task as the candidate and the company's
campaign counter, the wallet, the ledger and the public profile all update.

## Model assumptions baked in

- Plans: Starter $99 / Growth $299 / Scale $899 per month, buying tester seats.
- Tester payouts are set by the company and passed through; Vouch keeps 20%.
- Hiring managers and candidates never pay.
- Attestations follow an EAS-style schema on Base so the ledger is portable.

All people, companies, hashes and numbers are fictional.
