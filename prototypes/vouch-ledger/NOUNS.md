# Vouch Ledger — the nouns

A vocabulary extraction for data modeling. This is the set of things the product
talks about, pulled from the prototype (`index.html`) and the strategy notes
(`CONCEPT.md`). It describes what each thing is, what it is not, the states it moves
through, and how it relates to its neighbours. It deliberately stops short of fields,
keys, tables or a diagram. Those are yours.

Nouns are grouped by area. Within each area they are roughly in order of importance.
Words in **bold** are the nouns. Words in *italics* are candidate names for the same
thing that the prototype uses interchangeably; pick one.

---

## 1. People and identity

**Person.** A human being. One person can play several roles at once: a candidate
with a ledger, a voucher for someone else, a member of a company's team, a hiring
manager reading a profile. The roles are hats, not separate people. The prototype
shows Alex as a candidate and as a row in a company's tester pool; Maya as a voucher
with her own ledger. Everything that signs anything is ultimately a person or a
company.

**Candidate** (*member*, *tester*). A person who has a ledger and uses it. "Candidate"
is the job-search framing, "tester" is the marketplace framing, "member" is the
neutral term the public URL uses (`vouch.id/m/handle`). They are the same role seen
from three sides. Not every person is a candidate: a voucher may never build a ledger
of their own beyond the vouches they give.

**Voucher.** A person who confirms a specific claim about someone else. Always
external to Vouch Ledger and to the hiring company. Has an identity tier and a
standing. A voucher is not an endorser in the LinkedIn sense: they never vouch for a
person in general, only for one claim at a time.

**Hiring manager** (*reader*). Someone who opens a public profile or checks a stamp.
Usually anonymous. Pays nothing, has no account in the base product. Exists in the
model mainly as the origin of view events on apply links and stamp checks.

**Company** (*organization*, *verified org*). The paying customer on the marketplace
side. Has a plan, team members, campaigns, a billing relationship, and a verified
status that lets it issue attestations in its own name. A company is an issuer of
attestations but never a voucher.

**Team member.** A person acting on behalf of a company: creates campaigns, invites
testers, confirms completions, pays invoices. The prototype shows a single implicit
member; a real company will have several with different permissions.

**Identity verification.** A check a person has passed that proves something about
who they are. The prototype has three kinds: LinkedIn sign-in (the profile exists
and how old it is), work email at a named employer (they were there), and government
ID (they are one person). Each is an event with a date and an outcome, not a boolean
on the person, because they can expire, be re-run, or be revoked. Work-email
verification is tied to a specific employer, which matters for relationship
weighting.

**Identity tier.** The level a person has reached as a result of their
verifications: Tier 1 (profile only), Tier 2 (profile plus work email at the
employer named), Tier 3 (plus government ID), or unverified. Derived from
verifications, not stored as truth. It multiplies the weight of every vouch the
person gives.

**Handle.** The public, human-readable name in a profile URL (`alex-rivera`).
Unique, chosen, changeable with care.

**DID** (*decentralized identifier*). The stable, machine-readable identity that
attestations are issued to and signed by. Never changes. The thing a chain record
points at when it says "recipient" or "attester".

**Employment** (*tenure*). A period during which a person worked at a company, with
a role. Comes from LinkedIn import or work-email verification. Used to establish
overlap between two people, which is what lets a relationship be verified rather
than asserted.

**Relationship.** How two people were connected at a time and place: manager, peer,
cross-functional lead, skip-level, report, client. Asserted by the requester,
confirmed by the voucher, ideally corroborated by employment overlap. Carries a
weight multiplier. A relationship is between two people at a specific employer and
period, not a permanent fact about the pair.

## 2. The ledger and trust

**Ledger** (*record*, *profile*). The complete set of entries about one person.
Portable: exportable as JSON-LD, readable on-chain without Vouch Ledger. One per
person. The public profile is a rendering of the ledger, not a separate thing.
Vouchers' ledgers and candidates' ledgers are the same kind of thing; they just tend
to contain different kinds of entries.

**Entry.** One item on a ledger. Every entry has a kind, an issuer, a subject, a
date, a status, a weight, and a chain anchor. The prototype shows six kinds:
*claim*, *skill attestation*, *endorsement*, *paid task*, *credential*, and *vouch
given*. Whether "entry" is one noun with a kind, or six nouns sharing a shape, is a
modeling choice. The prototype treats it as one noun and the UI switches on kind.

**Claim** (*resume claim*, *resume line*). A statement the candidate makes about
their own past ("Led the checkout redesign that lifted activation 18%"). Self-authored,
so it starts with no weight. Gains weight through vouches. Needs two independent
vouches to reach full weight. A claim is the thing a vouch attaches to, and the thing
a resume line maps to during stamping. The wording of a claim can be edited by a
voucher as part of confirming it, so the text has a history.

**Vouch.** A signed confirmation, by a voucher, of one specific claim. Carries the
voucher's decision (confirmed, confirmed with edits, secondhand), an optional note,
the relationship asserted, and the voucher's tier and standing at the moment of
signing. A vouch appears on two ledgers: as support for the claim on the candidate's,
and as a "vouch given" entry on the voucher's. It is revocable, and a revocation is
itself public. A decline is not a vouch; see below.

**Vouch request.** The ask that precedes a vouch. From a candidate, to a specific
person, about a specific claim, with asserted relationship and optional context.
States: pending, confirmed, declined, expired. A declined request is private to the
requester and never appears on either ledger. A request can be nudged. The person it
goes to may not yet be a verified voucher; verification happens on their way to
signing.

**Attestation.** The general term for a signed statement, by an issuer, about a
subject, following a schema, anchored on-chain. Vouches are attestations issued by
people. Paid-task and skill attestations are issued by companies. Credentials are
self-issued with a document hash. In the prototype every entry is backed by an
attestation. If you keep "entry" as the ledger-facing noun, "attestation" is the
chain-facing one; they may be the same row or two linked rows.

**Issuer** (*attester*). Whoever signed an attestation: a person (as voucher), a
company, or the subject themselves (self-attested credential). Identified by DID.

**Subject** (*recipient*). The person an attestation is about.

**Schema.** The named shape of an attestation (`vouch.task.v2`, `vouch.claim.v2`).
Versioned. Lets third-party tools read the chain record without us.

**Anchor** (*transaction*, *block*). The chain reference for an attestation:
transaction hash, block number, chain name. Immutable once written. The off-chain
copy is what the app reads; the anchor is what a sceptic verifies against.

**Revocation.** An issuer withdrawing an attestation. Public, dated, and leaves the
original in place with a revoked status rather than deleting it.

**Dispute** (*contest*). A challenge to a claim or vouch, with a review and an
outcome. If a vouched claim fails review, the voucher's standing falls. The prototype
shows the count on a voucher's profile but not the workflow.

**Standing.** A voucher's reputation as a voucher: a score that rises with vouches
that hold up and falls with disputes. Derived, recomputable, but also captured on
each vouch at signing time so a vouch's weight does not change retroactively when
the voucher's standing moves later. Do not confuse with ledger strength.

**Ledger strength.** A candidate's score, derived from the weights of their entries.
Shown with a breakdown by source: external vouches, company attestations, paid
tasks, credentials and stamp. Purely derived; never stored as truth. Used for
matching and ranking in the tester pool.

**Weight.** The contribution of one entry to ledger strength. Derived from the entry
kind, the issuer's tier and standing, the relationship multiplier, and whether the
entry is pending (half weight) or verified. Worth capturing at the moment it was
computed so history is explainable.

**Credential.** A self-attested entry backed by a document hash (a certification
PDF). Low weight. The hash is anchored; the document itself is not stored on-chain.

## 3. The marketplace

**Campaign.** What a company creates to get testers: a task type, a title and
description, a payout per tester, a number of seats, tester requirements, and the
attestation it will issue on completion. States: draft, live, paused, completed.
Owns its engagements and its results. The prototype keeps a company-side "campaign"
and a candidate-side "opportunity" as two records linked by an id; they are one
noun. The candidate sees a *listing* of the campaign.

**Listing** (*opportunity*, *paid test*). The candidate-facing face of a live
campaign: what it pays, how long it takes, how many seats are left, what it issues,
and how well it matches. Not a separate thing to store; a projection of a campaign
plus a match score for the viewer.

**Task type.** The category of work a campaign asks for: UX walkthrough and
interview, beta usage with check-ins, moderated usability session, unmoderated
reaction test, customer discovery call, expert data labeling. Determines default
steps, typical duration, and median payout. A small, slowly changing reference set.

**Requirement** (*criteria*, *needs*). What a tester must have on their ledger to be
matched: specific skills, claims, or employment facts. Matched against verified
entries, never against self-description.

**Seat.** One unit of a company's plan capacity: the right to engage one tester in
one campaign within a billing cycle. Seats are consumed when a campaign goes live
(reserved) and returned if unused, depending on policy. The prototype decrements
seats at launch.

**Engagement** (*participation*, *assignment*). One candidate in one campaign. The
central marketplace noun. Created when a candidate accepts a listing or a company's
invitation. States: invited, accepted, started, completed, confirmed, auto-released,
expired, withdrawn. Owns the step progress, the escrowed payout, the company's
confirmation, the feedback the tester gave, and the attestation issued at the end.

**Step.** One item in an engagement's checklist ("Connect the sample data source").
Comes from the campaign's template, instanced per engagement with a done state.
Ordered.

**Invitation.** A company asking a specific tester from the pool to join a campaign.
Precedes an engagement; may be declined or ignored. Distinct from a vouch request
even though both are "asks".

**Match.** A score between a candidate and a campaign, derived from requirement
overlap and ledger strength. Computed, not stored as truth, though caching it is
reasonable.

**Tester pool.** The set of candidates a company can see for a campaign, ranked by
match and strength, with contact details withheld until an engagement exists. A
view, not a thing.

**Completion confirmation.** The company's act of confirming an engagement was
completed. Releases escrow and triggers the attestation. If absent after 72 hours,
the system auto-releases. The confirmation has an actor, a time, and a method
(manual or automatic).

**Feedback.** What a tester gives back inside an engagement: daily check-ins,
ratings, interview transcripts, labeled items. Shape varies by task type. The
company's campaign results are built from it.

**Quote.** A short excerpt of feedback, attributed to a tester by first name and
role, surfaced on campaign results. A projection of feedback, not a separate store.

**Conversion.** The fact that a tester later became a paying customer of the
company. Reported by the company or detected through an integration. Attached to
an engagement. Drives the "cost per customer" number.

**Perk.** A non-cash benefit a campaign offers in addition to payout ("3 months
free"). Optional.

## 4. Money

**Payout.** The amount a tester earns for an engagement. Set by the company per
campaign. Has a gross (what the company is billed) and a net (what the tester
keeps). One payout per engagement. States: pending (in escrow), paid, cancelled.

**Platform fee.** The difference between gross and net: 20% of gross in the
prototype. Shown on every line to both sides. A rate that may vary by plan later, so
capture the rate used, not just the amount.

**Escrow.** Funds held for a payout between acceptance and release. The payout's
pending state, plus the ledger of money movements behind it. Released on
confirmation or auto-release.

**Plan.** A company's subscription tier: Starter, Growth, Scale. Determines monthly
price, seat allowance, and feature access. A small reference set with a history of
changes per company.

**Subscription** (*billing cycle*). A company's current plan, its renewal date,
seats used this cycle, and payment method. The thing that renews.

**Invoice** (*charge*). What a company is billed for in a cycle: the plan fee, the
pass-through payouts, and the platform fee on those payouts. Line items reference
engagements.

**Withdrawal.** A tester moving available balance to their payout method. Batches
multiple payouts.

**Payout method.** Where a tester's money goes (bank account). Held by the payments
provider; we store a reference.

**Tax document.** Year-end reporting for testers (1099 in the US). Generated from
payouts. Mentioned in the prototype, not modeled.

## 5. Documents, links and the reading side

**Resume.** A document the candidate uploads. Has lines that are matched to claims.
Has a hash. A candidate may upload several versions.

**Resume line.** One statement in a resume. Mapped to a claim where one exists.
Carries a status at stamping time: verified, pending, unverified.

**Stamp.** The act and the record of sealing one resume version: the document hash,
the date, a check code, the status of each line at that moment, and a chain anchor.
Immutable. A new version of the resume gets a new stamp. The stamped PDF is an
output, not the record.

**Stamp check.** Someone entering a check code or dropping a PDF to verify a stamp.
An event with an outcome. Anonymous.

**Public profile.** The rendering of a ledger at `vouch.id/m/handle`. Not stored
separately. Reads the ledger, the vouchers' tiers and standings, the stamp, and the
strength breakdown.

**Apply link.** A tracked URL a candidate creates for one application
(`vouch.id/m/alex-rivera/lnr-7k2`). Has a label (company and role), an optional
note shown to the reader, and a count of opens. Many per candidate.

**Open** (*view event*). A recorded visit to an apply link or public profile. Time,
link, coarse source. The basis for "profile views" and "4 from employers".

**Export.** A candidate pulling their ledger as JSON-LD. An event, and a file. The
file's shape is governed by the schemas.

## 6. Same thing, different names

Collapse these before you start:

- *Candidate*, *member*, *tester* → one role.
- *Campaign*, *opportunity*, *paid test*, *listing* → one noun (campaign) plus a
  projection (listing).
- *Entry*, *attestation* → decide whether these are one thing or an app-facing and a
  chain-facing pair.
- *Issuer*, *attester*, *signer* → one noun.
- *Record*, *ledger*, *profile* → ledger is the data; profile is the public
  rendering.
- *Engagement*, *participation*, *assignment*, *active task* → one noun.

## 7. Things that look like nouns but are derived

Do not store these as truth. Compute them, and cache if you must, with a timestamp.

- Ledger strength and its breakdown
- Identity tier (from verifications)
- Standing (from vouches and disputes)
- Match score
- Entry weight (though capture the inputs at the time)
- Seats remaining
- Cost per completed task, cost per customer
- Profile views and link opens (aggregates of open events)

## 8. Invariants the product depends on

Not a schema, but things the model must make impossible or at least visible:

- A vouch always points at exactly one claim and one voucher, and the voucher is
  never the claim's subject.
- A vouch records the voucher's tier and standing at signing; later changes to the
  voucher do not retroactively change the vouch.
- A claim's status cannot reach "verified" with fewer than two independent vouches
  from different people.
- Company-issued attestations can confirm a task or an observed skill; they can
  never support a claim.
- A declined vouch request leaves no trace on any ledger.
- A revoked attestation stays on the ledger with its revocation; nothing is deleted.
- A payout exists only inside an engagement, and an engagement has at most one.
- Contact details of a candidate are not visible to a company until an engagement
  exists between them.
- A stamp is immutable; a changed resume is a new stamp.
- Every entry that counts toward strength has a chain anchor or is explicitly marked
  as pending one.

## 9. Decisions I am leaving to you

Open questions where the prototype took a shortcut and the real model should
choose:

1. Is a **claim** an entry on the ledger from the moment it is written, or does it
   become an entry only when the first vouch arrives? The prototype shows pending
   claims on the ledger at half weight.
2. Is **identity verification** history kept (each check, each outcome) or only the
   current tier? The weighting rules suggest history.
3. Where does the **off-chain copy** of an attestation live relative to the
   **entry**, and which one is the source of truth when they disagree?
4. Does an **engagement** own its **payout**, or does a payout reference an
   engagement? The invariants only require a one-to-one.
5. Are **campaign steps** a template copied into each engagement, or referenced with
   per-engagement progress kept separately?
6. How is a **relationship** verified: stored as its own fact between two people at
   an employer, or recomputed from employment overlap each time it is needed?
7. Is a **revocation** a status change on the attestation or a new attestation that
   references the old one? The chain side will likely force the second.
8. Multi-tenancy for **companies**: a team member can belong to more than one
   company. Decide early.
9. **Seats**: reserved at launch, consumed at engagement, or consumed at completion?
   The prototype reserves at launch, which is the simplest and the least fair.
10. Which **task types** need their own feedback shape, and whether that is a typed
    structure or a schemaless blob per type.
