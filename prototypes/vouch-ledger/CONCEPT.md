# Vouch Ledger — concept and strategy notes

Companion to the interactive prototype in this folder (`index.html`). This document
explains where the idea came from, what changed between the first concept and this
version, who the actors are, how money moves, why the trust layer is built the way it
is, and which product decisions in the prototype exist for a strategic reason rather
than a cosmetic one. It ends with a pass through the Idea Wedge Playbook's five gates.

Everything in the prototype (people, companies, figures, chain data) is fictional.

---

## 1. The idea in one paragraph

Vouch Ledger is a portable career record where each resume claim is confirmed by
identity-verified people who were actually there, anchored on a public chain so the
record belongs to the candidate and not to us. The record is funded by a second
business: startups pay a flat monthly plan to put their product in front of these
vetted candidates as paid testers, interviewees, beta users and expert labelers. The
candidate earns money while job hunting, every completed task adds a company-signed
attestation to the record, and the growing record makes the next match better.
Hiring managers read the record for free through a single link.

## 2. Where it started, and what was wrong with it

The original Vouch Ledger concept was a verification product:

- Candidates build a profile, ask former managers and peers to vouch for specific
  claims, and get attestations written to a chain.
- Candidates put a link to that profile in cover letters and application fields.
- Hiring managers review the profile and see which claims are backed.
- Resume stamping (a sealed, hash-anchored PDF) as an add-on.

The trust mechanics were sound. The revenue model was not. Every plausible payer had a
problem:

| Candidate payer | Job seekers are cash-constrained and price-sensitive. Charging them caps the supply side at the worst moment. |
| --- | --- |
| **Employer payer** | Asks HR and hiring managers to adopt a new habit and a new vendor before there is any candidate density. Long sales cycles, procurement, and a "why not just call the reference" objection. |
| **Voucher payer** | Nobody pays to do someone else a favour. |

That left the product with strong trust mechanics and no first dollar. The question
that produced this version was: what do we already have that someone with budget
wants right now?

## 3. The reframe: distribution is the product, verification is the exhaust

The biggest problem early-stage software companies face is distribution. Getting
real, relevant people to sign up, try a workflow, sit for an interview, or label data
is expensive and slow. Existing options are paid ads (untargeted, low intent),
research panels (expensive, generic participants), and founder hustle (does not
scale). Founders already spend on this, and they would spend $50 to $500+ a month
without a committee meeting if the people on the other end were real and relevant.

Vouch Ledger has exactly those people: professionals, currently between jobs or open
to moves, with a verified record of what they can do. So:

- Companies pay us to reach them.
- We broker the task, hold the payout in escrow, and take a fee.
- Candidates get paid to wait, and every task they finish becomes a signed
  attestation on the record they were building anyway.
- The stronger the record, the better we match, the more companies get, the more
  they pay, the more candidates earn.

Verification stops being the thing we sell and becomes the thing the marketplace
produces as a side effect. That is the flywheel in the Model tab of the prototype.

## 4. The actors and what each one gets

**Candidate (Alex Rivera in the prototype).** Earns money during a search that
would otherwise be unpaid dead time. Leaves every task with a third-party-confirmed
entry. Owns a portable record they can point to from any application. Pays nothing.

**Voucher (Maya Thompson).** A neutral outsider, not us and not the hiring company:
a former manager, peer, client or report. Verifies their identity, confirms one
specific claim they directly observed, and signs it. In return each vouch is an entry
on their own record, and their "standing" as a voucher rises when their vouches hold
up. Pays nothing. This actor is the source of most of the record's credibility, which
is why the second iteration of the prototype gave them a full persona rather than a
form field.

**Company (Relay Analytics).** Buys distribution it can budget for: a monthly plan
with tester seats, plus payouts it sets itself. Gets sign-ups, usability sessions,
interviews, beta usage, discovery calls or expert-labeled data from people selected
by verified skills. Many testers convert to customers. Issues attestations in its
own name, which puts its brand on candidates' public records.

**Hiring manager.** Opens a link, sees who vouched for what and the chain record
behind it, checks a stamped resume in one paste. No account, no fee. Removing the
employer as a payer removes the adoption barrier that killed the original model.

## 5. How the money moves

| Flow | Amount |
| --- | --- |
| Company → Vouch Ledger | Plan fee, monthly. Starter $99 (10 seats), Growth $299 (40 seats), Scale $899 (150 seats). |
| Company → Vouch Ledger → Tester | Payout set by the company. 80% passes through to the tester, 20% stays with us. |
| Voucher | $0. Earns standing and record entries. |
| Hiring manager | $0. |
| Candidate | $0. Earns. |

Two revenue lines with different shapes. Plan fees are predictable and cover the
matching engine and pool curation. The take on payouts scales with usage and is where
upside lives. The Revenue tab in the prototype lets you drag customer counts and task
volume to see the mix; at a modest 32 paying companies doing 14 tasks a month at an
$80 average payout, plan revenue and fee revenue are roughly the same size.

Pricing anchors: Starter is priced to beat a single paid-social experiment. Scale is
priced against a UX research vendor retainer. Payouts are always shown to both sides
with the fee visible, because opacity here would poison the tester side.

## 6. Trust architecture (why the ledger can be believed)

The marketplace only works if a company can trust the record, and the record only
works if a hiring manager can. Everything below is in the prototype's Voucher and
Vouches views.

1. **Identity before signature.** A voucher proves who they are before anything they
   say counts. LinkedIn sign-in proves the profile exists and how old it is. A work
   email at the employer named in the claim proves they were there. An optional
   government ID check proves they are one person. These form tiers (Tier 1 to 3)
   that multiply the weight of a vouch. Unverified people cannot vouch at all.

2. **One claim, not a person.** A vouch attaches to a single resume line
   ("Shipped the mobile app 0→1"), never to a person in general ("great to work
   with"). Vouchers can edit the wording, mark it secondhand at reduced weight, or
   decline privately. Two independent vouches take a claim to full weight.

3. **Relationship weighting.** Managers and clients weigh most, then peers and
   cross-functional leads, then reports. The voucher confirms the relationship too.

4. **Skin in the game.** Every vouch is public on both ledgers. If a signed claim is
   later contested and fails review, the voucher's standing drops and all their
   vouches weigh less. Careful vouchers gain standing and become the people others
   want a vouch from. This is what makes vouching self-policing instead of a
   LinkedIn-endorsement popularity contest.

5. **Company attestations are secondary by design.** A company that paid a tester
   has an interest in saying nice things. So a paid-task attestation confirms only
   that the task happened, was paid, and which specific skill was observed. It never
   vouches for a resume claim. On the sample ledger, external vouches are the largest
   share of strength and that ratio is a stated design goal.

6. **Portable and open.** Attestations follow an EAS-style schema on a public chain
   (Base in the prototype), so any wallet or explorer can read them without us.
   Candidates can export JSON-LD and host it anywhere. This is a promise to the
   candidate that we cannot hold their record hostage, and it is the reason the link
   in a cover letter is credible even to someone who has never heard of us.

7. **Resume stamping.** A sealed PDF with a check code and QR, hash-anchored on a
   date. Proves the document an employer holds is byte-identical to what was stamped
   and which lines were verified at that time. Free, because it is a distribution
   mechanism for the public profile, not a product.

## 7. Product decisions in the prototype and the reason behind each

| Decision | Why |
| --- | --- |
| Candidate never sees a fee; both sides see the 80/20 split on every line | Trust on the supply side is the scarce asset. Hidden fees would be the fastest way to lose it. |
| Payout held in escrow, released on company confirmation or automatically after 72 hours | Testers need certainty they will be paid; companies need a window to confirm. Auto-release removes the "company ghosts the tester" failure. |
| Companies see verified attestations, never contact details, until a tester accepts | Prevents the pool from being scraped as a sourcing list, which would turn the product into a recruiter tool and drive candidates out. |
| Company sets the payout; we show the median for the task type | Higher payouts attract stronger ledgers faster. Letting the market set the price keeps us out of the pricing fight. |
| Attestation issued in the company's name on completion | Puts the startup's brand on candidates' public records. That is free distribution and a reason to keep issuing tasks. |
| "Can't confirm" is private and never penalises the requester | Otherwise candidates only ask people who are sure to say yes, and the record stops meaning anything. |
| Vouches are revocable, and the revocation is public | Records must survive people changing their minds without letting them silently rewrite history. |
| Hiring managers get everything for free, with no account | Every barrier on the reading side reduces the value of the link the candidate is putting in applications. |
| Tracked apply links per application | Gives candidates a reason to actually use the link, and gives us a read on which employers open records (a future data product). |
| Ledger "strength" shown with a breakdown by source | Makes the weighting legible and shows the candidate the next best action (get a second vouch, stamp the resume). |
| One shared state across all four personas | Demonstrates the flywheel physically: a campaign launched by the company appears in the candidate marketplace; a vouch signed by Maya flips Alex's claim and updates the public page. |

## 8. Wedge and smallest sellable version

**The wedge in one sentence.** We win by being the only distribution channel where
the people on the other end are identity-verified professionals with a checkable
track record, and where paying for their time also builds a public asset for them.

**Smallest sellable version.** One task type (onboarding walkthrough + 20-minute
interview), one plan tier, manual matching by us, Stripe escrow, LinkedIn-based
identity for vouchers, a public profile page, and attestations written to a testnet
or even a signed append-only log with chain anchoring added later. The prototype
deliberately shows more than this so the whole model is visible, but the first
build should be a fraction of it.

**Explicitly out of scope for v1.** Training-data campaigns, government ID
verification, revenue slider, resume stamping, API export, tester leagues, and every
item in the "kitchen sink offshoots" list.

## 9. Distribution path for Vouch Ledger itself

- **First buyer:** seed-stage B2B SaaS founders who are already paying for user
  research panels or ads and are unhappy with participant quality.
- **First channel:** founder communities and accelerator cohorts, where "we'll get
  you 20 verified operators using your product this week for $299" is a message
  that travels by word of mouth.
- **First supply:** design and product professionals in active job searches,
  reached through the same communities and layoff lists. Their incentive is
  immediate (money this week), which is easier to sell than the deferred benefit
  of a verified record.
- **First proof point:** a campaign result page like the one in the prototype:
  20 seats, 14 completions, 3 converted customers, cost per customer well under the
  founder's paid-social CAC.

## 10. Structural risks and what the design does about them

| Risk | Mitigation in the model |
| --- | --- |
| Two-sided cold start | Start supply-side with money, not with the promise of a record. Paid tasks are a reason to show up today. Companies can be sold one at a time by hand. |
| Professional testers gaming the pool | Matching favours ledger strength built from external vouches, which professional testers cannot manufacture. Completion rate and company confirmations are visible. |
| Collusion rings in vouching | Identity tiers, relationship verification against employment overlap, public signatures on both ledgers, and standing that falls on contested claims. Rings are expensive and leave evidence. |
| LinkedIn dependence for identity | LinkedIn is one tier input, not the only one. Work email and government ID stand on their own. Employment overlap can also come from payroll or HRIS integrations later. |
| Blockchain skepticism from hiring managers | The chain is invisible in the reading experience. The public page reads like a profile; "Verify" is a button, not a wallet. Anchoring exists for portability and tamper evidence, not as a pitch. |
| Payout compliance (1099s, KYC, payment rails) | Use an existing payouts provider from day one. The prototype's wallet already assumes 1099 reporting. |
| Companies using the pool as a sourcing list | No contact details until acceptance; tasks are scoped; recruiter use is a separate, later product with candidate consent. |
| Competitors | Research panels (UserTesting, User Interviews, Respondent, Prolific) have participants but no verified record and no job-search framing. Credential and endorsement products (LinkedIn, Credly) have no external verification of claims and no distribution business. Background-check vendors verify employment dates, not work. Nobody combines paid distribution with a voucher-built record. |

## 11. Hypotheses to test first

1. Founders will pay $99 to $299 a month for verified testers before the pool is
   large. Test with hand-matched campaigns for five companies.
2. Job seekers will complete tasks for $40 to $150 and then ask for vouches. Track
   task completion rate and the share of testers who send at least one vouch request
   within 30 days.
3. Vouchers will verify identity and sign for a specific claim when asked by
   someone they worked with. Track request-to-signature rate and time to sign.
4. A share of testers convert to paying customers of the companies they test for.
   Track conversion per campaign; the prototype's sample assumes roughly one in eight.
5. Hiring managers open the link. Track apply-link opens per application.

If 1 and 2 hold and 3 does not, the business is a research panel with a nicer
pool. If 3 holds and 1 does not, it is the original verification product again with
no payer. All three need to hold for the flywheel to exist.

## 12. Kitchen-sink offshoots (later, not now)

Referral bounties for bringing in verified vouchers; cohort betas for pre-launch
startups; skill screens sold as paid tests (a language screen, a SQL screen) that
also produce attestations; recruiter search over ledgers with candidate consent; an
attestation API for ATS vendors; tester leagues and reputation tiers; founder office
hours as a paid task type.

## 13. Idea Wedge Playbook gates

| Gate | Read | Notes |
| --- | --- | --- |
| Market exists | Strong | Founders already buy user research, beta users and ads. Job seekers already do gig work. Both are existing spend categories. |
| Clear wedge | Strong | Verified professionals as a distribution channel, with the buyer's spend also building a public asset for the participant. No existing panel offers this. |
| Small MVP scope | Medium | The full model is wide (four personas). The sellable v1 is narrow (one task type, one plan, manual matching), but discipline is needed to keep it there. |
| Distribution path | Medium | Founder communities and accelerators are reachable and word-of-mouth friendly. The supply side has an immediate incentive. Neither is proven yet. |
| Structural risk | Medium | Identity and payout compliance are handled by existing providers. The real risks are cold start and vouch quality, both of which the design addresses but which only usage can confirm. |

Provisional decision: approve for a hand-run pilot of five companies and fifty
candidates, with the three hypotheses in section 11 as the pass/fail criteria.
