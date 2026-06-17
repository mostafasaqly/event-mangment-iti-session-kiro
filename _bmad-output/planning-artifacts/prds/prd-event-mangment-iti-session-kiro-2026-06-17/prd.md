---
title: Event Management Platform
status: final
created: 2026-06-17
updated: 2026-06-17
---

# PRD: Event Management Platform
*Working title — confirm.*

## 0. Document Purpose

This PRD is for the product owner (Saqly) and the downstream UX, architecture, and epics/stories workflows. It defines **capabilities, not implementation** — no schema, tech stack, or screen mockups. It builds on three existing artifacts and does not duplicate them: the finalized product brief (`_bmad-output/planning-artifacts/briefs/brief-event-mangment-iti-session-kiro-2026-06-17/brief.md`), the requirements spec (`_bmad-output/planning-artifacts/requirements.md`), and the brainstorming session (`_bmad-output/brainstorming/brainstorming-session-2026-06-17-1150.md`). Vocabulary is anchored in the Glossary (§3); features are grouped with FRs nested and globally numbered (FR-1…FR-N) for stable downstream references; assumptions are tagged inline and indexed in §9.

## 1. Vision

Trainers and small training centers in the Egypt/Arab market run events on a patchwork of Google Forms, WhatsApp, and Excel. Registration lives in one place, payment proof arrives in another, and the verdict — *who is actually confirmed* — exists only in the organizer's head. Past ~50 attendees this collapses into hours of manual screenshot-matching and a flood of "Am I confirmed?" messages.

The Event Management Platform replaces that patchwork with **one source of truth** for registration and payment status. Its defining constraint: it does **not** change how money moves. Attendees keep paying by Vodafone Cash, InstaPay, bank transfer, or cash, exactly as they do today. What changes is how payment gets **verified, tracked, and communicated** — attendees submit a transaction reference and proof, organizers approve or reject from one review queue, and each attendee gets a live status page that unlocks the event link the moment they are confirmed.

V1 is deliberately narrow: a focused **payment-confirmation and attendee-status system**, not a full event-management suite. It wins by being precisely right for one underserved market — manual-payment, WhatsApp-first — where generic global tools assume card payment and fail.

## 2. Target User

### 2.1 Jobs To Be Done

- **Functional (organizer):** Know at a glance who registered, who paid, who is confirmed, and who should receive the event link — without checking WhatsApp, bank screenshots, and Excel.
- **Functional (organizer):** Review and verify dozens of manual payments quickly, with confidence the confirmed-revenue number is real.
- **Emotional (organizer):** Stop dreading the post-registration chaos; trust the system instead of one's own memory and a fragile spreadsheet.
- **Functional (attendee):** Register and pay through familiar manual methods and know — without asking anyone — whether they're in.
- **Social (attendee):** Avoid the awkward repeated "Am I confirmed?" messages and get the event link the moment they're approved.

### 2.2 Non-Users (v1)

- **Instructors / speakers** — no dedicated portal in v1.
- **Training-center staff teams** — no multi-user roles/permissions in v1; a single organizer account operates the event.
- **Large-conference organizers** — agenda/tracks/sponsor/exhibitor needs are out of scope.

### 2.3 Key User Journeys

- **UJ-1. Mariam confirms 80 payments in one sitting instead of all evening.**
  - **Persona + context:** Mariam runs a small training academy; she's launching a 3-day workshop and has 80 registrations to reconcile against wallet/bank transfers.
  - **Entry state:** Authenticated as organizer, on the review dashboard, filtered to the review queue.
  - **Path:** She opens the queue → each card shows registrant, payer name (if different), expected vs. declared amount, transaction reference, and screenshot thumbnail, with auto-flags surfaced → she approves clean ones, rejects an unclear one with a reason, and waitlists one who paid after seats filled.
  - **Climax:** The queue empties; every confirmed attendee was auto-emailed and the link unlocked — she never opened WhatsApp or Excel.
  - **Resolution:** She trusts the confirmed count as real revenue; an audit log backs every decision. *Realizes FR-7, FR-8, FR-9, FR-11, FR-12.*
  - **Edge case:** A transfer arrives from a different name; because the attendee declared the payer name, the card shows both and isn't flagged as fraud — she approves in seconds.

- **UJ-2. Ahmed registers, pays by InstaPay, and knows he's in — without messaging anyone.**
  - **Persona + context:** Ahmed, a working professional, signs up for Mariam's workshop from his phone.
  - **Entry state:** Unauthenticated, arriving from a registration link Mariam shared on WhatsApp.
  - **Path:** He fills name/phone/email → selects InstaPay → submits → gets his personal status-page link by email → pays via his banking app → returns to the status page, uploads the screenshot, and enters the transaction reference.
  - **Climax:** His status flips to *Under review*, then later to *Confirmed*; the event link appears on his status page and arrives by email.
  - **Resolution:** He adds it to his calendar and never has to ask "Am I confirmed?" *Realizes FR-2, FR-3, FR-6, FR-8.*
  - **Edge case:** His screenshot is rejected as unclear; the status page shows the reason and re-opens the upload, so he resubmits without contacting Mariam.

- **UJ-3. Sara registers her whole team on one payment.**
  - Sara, an L&D coordinator, registers four colleagues and pays once; she links the single payment proof to all four registrations, which Mariam reviews together. *Realizes FR-13.*

## 3. Glossary

- **Event** — A scheduled offering created by an Organizer (course, workshop, webinar, meetup, conference, or training session) with a capacity, price, and event link. Has many Registrations.
- **Organizer** — The user who creates and manages Events and reviews payments. One Organizer account per Event in v1.
- **Attendee** — A person who submits a Registration to an Event. May differ from the Payer.
- **Registration** — One Attendee's request to attend one Event. Holds exactly one Status. Belongs to one Event.
- **Payment Method** — A manual way to pay configured by the Organizer per Event (Vodafone Cash, InstaPay, bank transfer, cash, or other), with display instructions and a destination (number/handle/account) where applicable. An Event has one or more.
- **Payment Proof** — Evidence of a manual payment: a Transaction Reference (required for non-cash, optional for cash) plus an optional screenshot, with an optional declared Payer name.
- **Internal Note** — A free-text note the Organizer attaches to a Registration (e.g., on cash confirmation); visible to the Organizer only, never on the Status Page.
- **Transaction Reference** — The Attendee-supplied identifier of a manual payment; the primary verifiable token. Expected unique per Event.
- **Payer** — The person whose wallet/account sent the money; may differ from the Attendee (declared via Payer name).
- **Status** — The single state of a Registration: `PENDING`, `UNDER_REVIEW`, `CONFIRMED`, `REJECTED`, `WAITLISTED`, `EXEMPT`, or `CANCELLED`.
- **Status Page** — A unique, link-accessible (no-login in v1) page showing one Attendee their current Status and state-appropriate actions.
- **Event Link** — The URL/details of attending (e.g., a Zoom link). Visible only for `CONFIRMED` and `EXEMPT` Registrations.
- **Review Queue** — The Organizer's list of Registrations in `UNDER_REVIEW`, awaiting an approve/reject decision.
- **Auto Flag** — An advisory, non-blocking warning the system raises on a Registration (e.g., duplicate reference, amount mismatch).
- **Audit Log** — The attributable, timestamped record of every Status change on a Registration.
- **Capacity** — The maximum number of `CONFIRMED` Attendees an Event allows; reaching it routes new Registrations to `WAITLISTED`.

## 4. Features

### 4.1 Event Management

**Description:** The Organizer creates and manages Events. Each Event carries the details attendees and the system need (type, schedule, capacity, price, Event Link) and exposes one public registration link. Realizes UJ-1. Uses Glossary terms exactly.

**Functional Requirements:**

#### FR-1: Create and manage an Event
The Organizer can create an Event with type (course/workshop/webinar/meetup/conference/training), title, description, date, time, Capacity, price, and Event Link; and can edit or unpublish it.

**Consequences (testable):**
- An Event can be created with all listed fields; type is one of the six allowed values.
- Each Event has exactly one unique public registration link.
- Unpublishing an Event stops new Registrations without deleting existing ones.

#### FR-1b: Configure manual Payment Methods per Event
For each Event, the Organizer can add one or more manual Payment Methods, each with its own instructions: Vodafone Cash number, InstaPay handle/phone, bank account details, cash payment instructions, or other manual method.

**Consequences (testable):**
- An Event can have one or more Payment Methods, each storing a method type plus display instructions and (where applicable) the destination number/handle/account.
- The configured instructions for the Attendee's selected method are what appear on the Status Page during payment (FR-7).
- Payment-method destination details are shown only to Attendees who are registering or completing payment — never publicly listed elsewhere.

### 4.2 Registration

**Description:** An Attendee registers through the Event's public link with basic details and a chosen payment method, and immediately receives their personal Status Page link. Realizes UJ-2.

**Functional Requirements:**

#### FR-2: Register for an Event
An Attendee can submit a Registration via the public form with required fields (name, phone, email), optional per-Event fields, and a selected payment method. Realizes UJ-2.

**Consequences (testable):**
- A Registration cannot be submitted without name, phone, and email.
- On submission, the Registration is created with Status `PENDING` (or `WAITLISTED` if Capacity is full — see FR-10).
- The Attendee receives a unique Status Page link by email.

### 4.3 Manual Payment Proof

**Description:** After paying through their own wallet/bank, the Attendee submits Payment Proof — a required Transaction Reference, an optional screenshot, and an optional declared Payer name when someone else paid. This moves the Registration into the Review Queue. The product does not move money; it captures verifiable evidence of money already moved. Realizes UJ-2.

**Functional Requirements:**

#### FR-3: Submit Payment Proof
An Attendee can select a payment method (Vodafone Cash, InstaPay, bank transfer, cash, or other manual), upload a screenshot, enter a Transaction Reference, and enter a Payer name if different from their own.

**Consequences (testable):**
- Transaction Reference is required for non-cash methods and **optional for the `cash` method**.
- Submitting Payment Proof transitions the Registration from `PENDING` (or `REJECTED`) to `UNDER_REVIEW`.
- A declared Payer name is stored and shown to the Organizer at review.

**Out of Scope:**
- Automatic verification of the payment with any bank/wallet (no gateway, no OCR).

#### FR-3b: Cash-payment flow
When the Attendee selects `cash`, the Registration stays `PENDING` (no proof step) until the Organizer confirms cash was received in person; the Organizer can then mark it `CONFIRMED` or `EXEMPT` from the dashboard and attach an internal note.

**Consequences (testable):**
- A `cash` Registration is not required to submit a Transaction Reference or screenshot and does not auto-enter `UNDER_REVIEW`.
- From the dashboard the Organizer can move a `cash` Registration directly `PENDING → CONFIRMED` (or `EXEMPT`) and record an internal note (e.g., "Cash received at center," "Cash received by trainer," "Paid on-site").
- The cash confirmation writes an Audit Log entry (FR-11), including the internal note when present.
- Internal notes are visible to the Organizer only — never on the Attendee Status Page.

### 4.4 Status Model

**Description:** Every Registration holds exactly one Status from a single flat list. Transitions are constrained but the Organizer retains manual control. This is the spine the whole product turns on.

**Functional Requirements:**

#### FR-4: Single flat Status with constrained transitions
A Registration has exactly one Status: `PENDING`, `UNDER_REVIEW`, `CONFIRMED`, `REJECTED`, `WAITLISTED`, `EXEMPT`, `CANCELLED`.

**Consequences (testable):**
- Allowed transitions:
  - `PENDING → UNDER_REVIEW` (proof submitted), `PENDING → WAITLISTED` (capacity full), `PENDING → EXEMPT | CANCELLED` (Organizer)
  - `UNDER_REVIEW → CONFIRMED | REJECTED | WAITLISTED | EXEMPT | CANCELLED` (Organizer)
  - `REJECTED → UNDER_REVIEW` (Attendee resubmits)
  - `WAITLISTED → CONFIRMED | CANCELLED` (Organizer)
  - `CONFIRMED → CANCELLED` (Organizer), and reopen to a prior Status (FR-14)
- No Status transition outside this set is permitted.

### 4.5 Payment Review

**Description:** The Organizer works a single Review Queue. Each item presents everything needed to decide in seconds — registrant, Payer, expected vs. declared amount, Transaction Reference, screenshot, and Auto Flags — and offers one-tap actions. Realizes UJ-1.

**Functional Requirements:**

#### FR-5: Review a Registration and act
From the Review Queue, the Organizer can view a Registration's full detail (registrant + contact, method, expected vs. declared amount, Transaction Reference, Payer name, screenshot, Auto Flags) and take exactly one action: **Approve**, **Reject (with reason)**, **Waitlist**, **Mark Exempt**, **Cancel**, or **Reopen**. Realizes UJ-1.

**Consequences (testable):**
- Approve sets `CONFIRMED`; Reject requires a reason and sets `REJECTED`; Waitlist sets `WAITLISTED`; Mark Exempt sets `EXEMPT`; Cancel sets `CANCELLED`.
- Every action writes an Audit Log entry (FR-11) and triggers communication (FR-9).

#### FR-6: Advisory Auto Flags
The system raises non-blocking Auto Flags on a Registration: duplicate phone or email, duplicate Transaction Reference, amount mismatch (declared ≠ expected), missing Payment Proof, missing Transaction Reference, Capacity already full. Realizes UJ-1, UJ-2.

**Consequences (testable):**
- A Transaction Reference already used on the same Event raises a duplicate-reference flag.
- Flags warn the Organizer but never block a manual action and never auto-change Status.
- A declared-Payer-name mismatch does **not** raise a flag and is never auto-rejected.

### 4.6 Attendee Status Page

**Description:** Each Attendee has a unique, link-accessible page that always answers "where do I stand?" — eliminating the repeated "Am I confirmed?" question. Rejected attendees see the reason and can fix it themselves. Realizes UJ-2.

**Functional Requirements:**

#### FR-7: View status and self-serve
An Attendee can open their unique Status Page (no login in v1) to see their current Status and the appropriate message/actions; a `REJECTED` Attendee sees the rejection reason and can resubmit Payment Proof. Realizes UJ-2.

**Consequences (testable):**
- The page reflects the current Status for each of the seven states.
- For a `PENDING` (non-cash) Registration, the page shows: the selected payment method, its configured payment instructions (FR-1b), the amount to pay, the Transaction Reference field (if required for the method), the Payment Proof upload field, and the "Payer name if different" field.
- For a `PENDING` `cash` Registration, the page shows the cash payment instructions and that confirmation happens in person (no proof/reference fields required).
- A `REJECTED` Registration shows the reason and re-opens the proof form (→ `UNDER_REVIEW` on resubmit).
- Status Page links are unguessable (random tokens) and never expose another Attendee's Registration.

### 4.7 Event Link Gating

**Description:** The Event Link is a reward for being confirmed, not a broadcast. One hard rule prevents the single biggest leak in the current workflow.

**Functional Requirements:**

#### FR-8: Gate the Event Link by Status
The Event Link is rendered **only** for `CONFIRMED` and `EXEMPT` Registrations, on the Status Page and in communications. Realizes UJ-1, UJ-2.

**Consequences (testable):**
- For `PENDING`, `UNDER_REVIEW`, `REJECTED`, `WAITLISTED`, `CANCELLED`, the Event Link appears nowhere.
- Transitioning into `CONFIRMED`/`EXEMPT` reveals the link; transitioning out (e.g., Cancel) removes it.

### 4.8 Communication

**Description:** Email is the automatic channel; WhatsApp is honored as the market's real channel through assisted, pre-filled messages — without taking on Business API complexity in v1.

**Functional Requirements:**

#### FR-9: Status-change communication
On important Status changes the system auto-sends an email; for any Attendee the Organizer can copy a WhatsApp message template or open a pre-filled WhatsApp message to the Attendee's number.

**Consequences (testable):**
- Confirmation, rejection, waitlist, and exempt transitions each send an email.
- A confirmation email includes the Event Link; a rejection email includes the reason.
- The "Open WhatsApp" action opens a pre-filled message; no WhatsApp Business API is used.

### 4.9 Capacity & Waitlist

**Description:** Capacity prevents overselling; the waitlist absorbs latecomers and lets the Organizer fill freed seats deliberately.

**Functional Requirements:**

#### FR-10: Capacity limit and waitlist
The Organizer sets a Capacity; when reached, new Registrations become `WAITLISTED`; the Organizer can manually promote a `WAITLISTED` Attendee to `CONFIRMED`.

**Consequences (testable):**
- Once `CONFIRMED` count reaches Capacity, new Registrations are created `WAITLISTED`.
- Promotion sets `CONFIRMED` and unlocks the Event Link (FR-8).
- Capacity counts only `CONFIRMED` and `EXEMPT` Registrations toward the limit; `PENDING`/`UNDER_REVIEW` do not hold a seat. New Registrations become `WAITLISTED` only once `CONFIRMED + EXEMPT` reaches Capacity.

### 4.10 Audit Log

**Description:** Every Status change is attributable and timestamped — the basis for resolving disputes and trusting confirmed revenue, and a quiet selling point for centers.

**Functional Requirements:**

#### FR-11: Record every Status change
The system records, per Status change: actor (who), timestamp (when), old Status, new Status, and reason (if any); the history is viewable per Registration. Realizes UJ-1.

**Consequences (testable):**
- Every transition — including Reopen/Undo (FR-14) — produces one Audit Log entry.
- Each entry carries actor, timestamp, old→new Status, and reason when present.

### 4.11 Search, Filter & Export

**Description:** The Excel-killer. The Organizer can find any Registration and pull the whole list out as a clean file.

**Functional Requirements:**

#### FR-12: Search, filter, export
The Organizer can search by name, phone, email, or Transaction Reference; filter by Status; and export Registrations to Excel or CSV. Realizes UJ-1.

**Consequences (testable):**
- Search returns matches across name/phone/email/Transaction Reference.
- Export produces a valid Excel/CSV containing Registrations and their Statuses.

### 4.12 Group Registration

**Description:** One Payer can register several Attendees and attach a single Payment Proof to all of them, so corporate/team sign-ups don't break the model. Realizes UJ-3.

**Functional Requirements:**

#### FR-13: One payment for multiple Attendees
One person can register multiple Attendees, and one Payment Proof can be linked to multiple Registrations reviewed together. Realizes UJ-3.

**Consequences (testable):**
- A single Payment Proof can be associated with N Registrations.
- Approving a linked group Payment Proof confirms all associated Registrations in one action; the audit log records the confirmation for each.

### 4.13 Undo / Reopen

**Description:** Human error is recoverable. The Organizer can reverse a mistaken decision and the reversal is itself recorded.

**Functional Requirements:**

#### FR-14: Reopen a decided Registration
The Organizer can reopen/undo a mistaken Approve or Reject, returning the Registration to its prior Status; the action is logged.

**Consequences (testable):**
- Reopening a `CONFIRMED`/`REJECTED` Registration returns it to its prior Status and (for un-confirm) removes the Event Link.
- The reversal writes an Audit Log entry (FR-11).

### 4.14 Access & Accounts

**Description:** The Organizer has an authenticated account; Attendees never log in — their Status Page is reached by an unguessable token link. This keeps the attendee path frictionless while protecting the Organizer's dashboard.

**Functional Requirements:**

#### FR-15: Organizer authentication
The Organizer signs in with an email-and-password account to access event creation and the Review Queue/dashboard. Attendee Status Pages remain no-login, token-secured (FR-7).

**Consequences (testable):**
- Event management and the Review Queue are accessible only to an authenticated Organizer.
- Attendees access only their own Status Page via token; no account is created for Attendees.

## 5. Non-Goals (Explicit)

- **Not** a payment processor — money never moves through the system; no gateway, no card payments, no automatic gateway confirmation (Paymob/Fawry/Stripe deferred).
- **Not** a WhatsApp automation tool in v1 — pre-filled/copyable messages only; no Business API.
- **Not** a certificate generator in v1 — deferred to v2 / paid add-on.
- **Not** an instructor/speaker platform — no instructor portal.
- **Not** a multi-staff admin system — no roles/permissions; single Organizer account.
- **Not** a full conference suite — no agenda builder, tracks, speaker/sponsor/exhibitor management.
- **Not** a CRM — no long-term attendee profiles beyond Event Registration.
- **Not** a marketplace — each Organizer has their own registration page; no public event discovery.
- **Not** an analytics product in v1 — basic counts only; no revenue/no-show/conversion dashboards.
- **Not** a native mobile app — responsive web only.

## 6. MVP Scope

### 6.1 In Scope

- Event creation with type, schedule, Capacity, price, Event Link, and a public registration link (FR-1).
- Per-Event configuration of one or more manual Payment Methods with instructions (FR-1b).
- Public registration with required name/phone/email + per-Event optional fields + payment-method selection (FR-2).
- Manual Payment Proof: method, screenshot, Transaction Reference (optional for cash), declared Payer name (FR-3); in-person cash confirmation with Internal Note (FR-3b).
- Single flat Status model with constrained transitions (FR-4).
- Organizer Review Queue with full detail + Approve/Reject-with-reason/Waitlist/Mark Exempt/Cancel/Reopen (FR-5).
- Advisory Auto Flags (FR-6).
- Attendee Status Page with self-serve resubmission (FR-7).
- Event Link gating to `CONFIRMED`/`EXEMPT` (FR-8).
- Email on Status change + pre-filled/copyable WhatsApp message (FR-9).
- Capacity + manual waitlist promotion (FR-10).
- Audit Log of every Status change (FR-11).
- Search / filter / export to Excel/CSV (FR-12).
- Basic group registration: one proof → many Registrations (FR-13).
- Undo / reopen mistaken decisions (FR-14).
- Organizer email-and-password authentication; token-secured no-login Attendee Status Pages (FR-15).
- **Bilingual (Arabic + English) interface**, with attendee-facing content RTL-ready.

### 6.2 Out of Scope for MVP

- Real payment gateway integration — deferred to v3; manual payment is the market reality. `[NOTE FOR PM]` revisit when card payment demand is proven.
- WhatsApp Business API — deferred to v2; pre-filled links cover v1 at near-zero infra cost.
- Auto certificates — deferred to v2 / paid add-on. `[NOTE FOR PM]` emotionally load-bearing and monetizable; revisit early in v2.
- QR check-in / attendance — deferred to v1.5.
- Partial payments / installments — deferred to v1.5/v2; v1 handles amount mismatch only via advisory flag + approve/reject.
- Instructor portal, multi-staff roles, conference suite, CRM, marketplace, analytics dashboards, native app — see §5.

## 7. Success Metrics

> Directional targets — confirm with real numbers once a pilot Organizer uses the product.

**Primary**
- **SM-1: Reconciliation time** — an Organizer reviews payments for an ~80-Attendee Event in **< 15 minutes** (vs. hours today). Validates FR-5, FR-6, FR-12.
- **SM-2: "Am I confirmed?" inbound** — repeated confirmation-status messages drop to **near zero**. Validates FR-7, FR-8, FR-9.
- **SM-3: Event-link leakage** — **0** non-`CONFIRMED`/`EXEMPT` Attendees receive the Event Link. Validates FR-8.

**Secondary**
- **SM-4: Workflow replacement** — Organizer runs an Event end-to-end **without Excel or WhatsApp screenshot-chasing**. Validates FR-5, FR-11, FR-12.
- **SM-5: Adoption signal** — an Organizer runs a **second Event** unprompted. Validates the product overall.

**Counter-metrics (do not optimize)**
- **SM-C1: Review speed vs. accuracy** — do not push reconciliation time down by encouraging blind bulk-approval; wrongful confirmations (later cancelled for non-payment) must stay low. Counterbalances SM-1.
- **SM-C2: Automation vs. trust** — do not auto-confirm to cut "Am I confirmed?" volume; every `CONFIRMED` must trace to an Organizer decision in the Audit Log. Counterbalances SM-2.

## 7a. Monetization (out of v1 build)

No billing system, payment-gateway billing, or automated plan management ships in v1 — monetization is validated **manually** and lives outside product implementation for now. Intended path, in order: (1) free pilot for the first few Organizers; (2) paid per-Event or per-confirmed-Attendee; (3) subscription tiers for trainers and training centers; (4) certificates as a paid add-on (v2); (5) WhatsApp automation as a premium feature (v2); (6) payment-gateway monetization (v3).

## 8. Open Questions

*All v1 open questions resolved.* Remaining items below are deferred-by-design (not gaps in v1):

1. **Monetization model** — validated **manually** in v1 (not built). Suggested future path: free pilot for the first few Organizers → paid per-Event or per-confirmed-Attendee → subscription tiers for trainers/centers; certificates as a paid add-on (v2); WhatsApp automation as premium (v2); payment-gateway monetization (v3). See §7a.

*Resolved this session:* capacity accounting → only `CONFIRMED`/`EXEMPT` hold seats (FR-10); group approval → confirm all N at once (FR-13); Organizer auth → email + password (FR-15); localization → bilingual AR/EN, RTL-ready (§6.1); cash payments → reference optional, in-person confirm with internal note (FR-3b); payment-details display → configured per Event, shown on `PENDING` Status Page (FR-1b, FR-7).

## 9. Assumptions Index

*Remaining inferred items, surfaced for explicit confirmation:*
- **§2 / scope** — A single Organizer account operates each Event in v1 (no multi-user); carried from the brief/requirements.
- **§4.6 / FR-7 / FR-15** — Attendee Status Pages require no login in v1, secured by unguessable tokens; the Organizer authenticates with email + password.
