---
title: "Event Management Platform — Product Requirements (V1)"
status: draft
type: new-feature
market: Egypt / Arab training market
created: 2026-06-17
updated: 2026-06-17
source: brainstorming-session-2026-06-17-1150.md, brief-event-mangment-iti-session-kiro-2026-06-17
---

# Event Management Platform — Requirements (V1)

> **Scope note:** This document is requirements only. No code, no database schema, no architecture. V1 is intentionally small and practical.

---

## 1. Product Overview

The Event Management Platform is a focused **payment confirmation and attendee status system** for trainers and training centers in the Egypt/Arab market.

**Core wedge:** The product does **not** change how money moves. Attendees keep paying through manual wallets and transfers (Vodafone Cash, InstaPay, bank transfer, cash) exactly as they do today. What the product replaces is how payment gets **verified, tracked, and communicated**.

It collapses today's fragmented workflow — Google Forms for registration, WhatsApp for payment screenshots, and Excel for tracking — into one source of truth, with one simple flow:

> **Organizer creates event → Attendee registers → Attendee submits manual payment proof → Organizer reviews → Organizer approves or rejects → Attendee status updates → Event link unlocks only for confirmed or exempt attendees.**

---

## 2. Problem Statement

Trainers and small training centers manage registrations and payments manually across disconnected tools. Registration lives in Google Forms, payment proof arrives over WhatsApp/Messenger, and the verdict — *who is actually confirmed* — exists only in the organizer's head and a manually maintained Excel sheet.

The real pain is not registration. It is the gap **after** registration:

> "How can I know who registered, who paid, who is confirmed, and who should receive the event link — without manually checking WhatsApp, bank screenshots, and Excel?"

Past roughly 50 attendees this collapses: the organizer spends hours matching payment screenshots to registrations, payer names don't match registrant names, amounts are wrong, people register or pay twice, and a flood of "Am I confirmed?" messages arrives. The event link gets blasted to a WhatsApp group, so unpaid people get in for free while confirmed attendees lose it in the noise. There is no audit trail and no trustworthy view of confirmed revenue.

---

## 3. Target Users

- **Independent trainers** running courses, workshops, and webinars.
- **Small training centers** with one or a few staff managing events.
- **Attendees / participants** in the Egypt/Arab market, who pay via manual wallets/transfers and communicate primarily over WhatsApp.

Market characteristics that shape every requirement: **manual payment culture** (no default card gateway) and **WhatsApp-first communication**.

---

## 4. User Roles

| Role | Description | In V1? |
|---|---|---|
| **Organizer / Admin** | Creates and manages events, reviews payments, approves/rejects, manages attendee status. Single account is enough for MVP. | ✅ Yes |
| **Attendee / Participant** | Registers for an event, submits payment proof, tracks their own status, receives the event link when confirmed. | ✅ Yes |
| **Instructor / Speaker** | Delivers the event. No dedicated portal in V1. | ❌ Deferred |
| **Training-center staff (multi-user)** | Multiple staff sharing a dashboard with roles/permissions. | ❌ Deferred (V2+) |

---

## 5. In Scope for V1

1. **Event creation** — organizer creates an event (course, workshop, webinar, meetup, conference, training session) with title, description, date, time, capacity, price, and event link.
2. **Public registration form** — required fields name/phone/email, optional per-event fields, and payment-method selection.
3. **Manual payment proof submission** — method (Vodafone Cash, InstaPay, bank transfer, cash, or other manual); screenshot upload; required transaction reference; "payer name if different" field.
4. **Simple flat status model** — `PENDING`, `UNDER_REVIEW`, `CONFIRMED`, `REJECTED`, `WAITLISTED`, `EXEMPT`, `CANCELLED`.
5. **Organizer payment review dashboard** — see pending proofs; review attendee data, method, amount, reference, screenshot, payer name; approve / reject-with-reason / waitlist / mark exempt / cancel / reopen.
6. **Auto flags** — duplicate phone or email; duplicate transaction reference; amount mismatch; missing payment proof; missing transaction reference; capacity already full.
7. **Attendee status page** — unique link per attendee; shows current status; rejected attendees see the reason and can resubmit proof.
8. **Event link gating** — link visible only for `CONFIRMED` or `EXEMPT`; hidden for all other states.
9. **Communication** — auto email on important status changes; copyable WhatsApp template; "Open WhatsApp" button with pre-filled message. No WhatsApp Business API.
10. **Capacity and waitlist** — set capacity; full seats route new registrations to `WAITLISTED`; organizer can manually promote `WAITLISTED → CONFIRMED`.
11. **Audit log** — every status change recorded with who, when, old status, new status, and reason if available.
12. **Search, filter, export** — search by name/phone/email/reference; filter by status; export to Excel or CSV.
13. **Basic group registration** — one person paying for multiple attendees; one payment proof connected to multiple attendees.
14. **Undo / reopen** — reverse mistaken approvals or rejections.

---

## 6. Out of Scope for V1

1. Real payment gateway integration (Paymob, Fawry, Stripe, card payments, automatic gateway confirmation).
2. WhatsApp Business API automation (pre-filled messages and templates only).
3. Auto certificate generation (V2 / paid add-on).
4. QR check-in / attendance (candidate for V1.5).
5. Instructor / speaker portal.
6. Advanced analytics (revenue, no-show, conversion dashboards) — basic counts only.
7. Multi-staff roles and permissions.
8. Complex conference features (agenda builder, tracks, speaker/sponsor/exhibitor management).
9. Discount / scholarship rules engine (use `EXEMPT` manually instead).
10. Partial payments and installments.
11. Full CRM / long-term attendee profiles.
12. Native mobile app (responsive web only).
13. AI / OCR screenshot reading (manual but organized review).
14. Public marketplace / event discovery.
15. Subscription billing system (monetization validated manually first).

---

## 7. User Stories

### Organizer
- **US-O1** — As an organizer, I want to create an event with its details, capacity, price, and link, so I can open registration.
- **US-O2** — As an organizer, I want a public registration link to share, so attendees can sign up without me handling each one.
- **US-O3** — As an organizer, I want a single dashboard of pending payment proofs, so I stop searching WhatsApp, bank apps, and Excel.
- **US-O4** — As an organizer, I want each review card to show the registrant, payer name, amount, reference, and screenshot together, so I can decide in seconds.
- **US-O5** — As an organizer, I want the system to auto-flag duplicates, amount mismatches, and missing data, so I catch problems without manual checking.
- **US-O6** — As an organizer, I want to approve, reject-with-reason, waitlist, mark exempt, cancel, or reopen a registration, so I can handle every real situation.
- **US-O7** — As an organizer, I want status changes to automatically email the attendee and give me a pre-filled WhatsApp message, so I stop typing confirmations by hand.
- **US-O8** — As an organizer, I want capacity limits with automatic waitlisting, so I don't oversell seats.
- **US-O9** — As an organizer, I want an audit log of every status change, so I can resolve disputes and trust my confirmed-revenue number.
- **US-O10** — As an organizer, I want to search, filter, and export registrations, so I can replace my Excel sheet entirely.
- **US-O11** — As an organizer, I want to connect one payment proof to multiple attendees, so group/corporate registrations work.
- **US-O12** — As an organizer, I want to undo a mistaken approval or rejection, so human error is recoverable.

### Attendee
- **US-A1** — As an attendee, I want to register for an event with my basic details, so I can request a seat.
- **US-A2** — As an attendee, I want to choose my payment method and submit proof with a transaction reference, so the organizer can verify my payment.
- **US-A3** — As an attendee, I want to declare a different payer name when someone else pays for me, so my payment isn't flagged as a mismatch.
- **US-A4** — As an attendee, I want a personal status page, so I always know whether I'm pending, under review, confirmed, rejected, waitlisted, exempt, or cancelled — without messaging anyone.
- **US-A5** — As an attendee, I want to see the rejection reason and resubmit my proof, so I can fix a problem myself.
- **US-A6** — As a confirmed attendee, I want the event link to appear on my status page and arrive by email, so I can actually attend.

---

## 8. Functional Requirements

### FR-1 Event Management
- **FR-1.1** Organizer can create an event with: type (course/workshop/webinar/meetup/conference/training), title, description, date, time, capacity, price, event link.
- **FR-1.2** Each event has a unique public registration link.
- **FR-1.3** Organizer can edit and close/unpublish an event.

### FR-2 Registration
- **FR-2.1** Attendee can register via the public form with required fields: name, phone, email.
- **FR-2.2** Form supports optional, per-event fields.
- **FR-2.3** Attendee selects a payment method during/after registration.
- **FR-2.4** On registration the attendee receives a unique **status page link** (by email).

### FR-3 Payment Proof Submission
- **FR-3.1** Attendee selects payment method: Vodafone Cash, InstaPay, bank transfer, cash, or other manual.
- **FR-3.2** Attendee can upload a payment screenshot.
- **FR-3.3** Attendee must enter a **transaction reference** (required for non-cash methods).
- **FR-3.4** Attendee can enter a **payer name** if different from their own.
- **FR-3.5** On submission the registration moves to `UNDER_REVIEW`.

### FR-4 Status Model
- **FR-4.1** Each registration has exactly one status from: `PENDING`, `UNDER_REVIEW`, `CONFIRMED`, `REJECTED`, `WAITLISTED`, `EXEMPT`, `CANCELLED`.
- **FR-4.2** Allowed transitions:
  - `PENDING → UNDER_REVIEW` (proof submitted)
  - `PENDING → WAITLISTED` (capacity full at registration)
  - `PENDING → EXEMPT` / `CANCELLED` (organizer)
  - `UNDER_REVIEW → CONFIRMED | REJECTED | WAITLISTED | EXEMPT | CANCELLED` (organizer)
  - `REJECTED → UNDER_REVIEW` (attendee resubmits)
  - `WAITLISTED → CONFIRMED | CANCELLED` (organizer)
  - `CONFIRMED → CANCELLED` (organizer) and reopen back to prior state (undo)

### FR-5 Organizer Review Dashboard
- **FR-5.1** Dashboard lists registrations, filterable by status, with the review queue (`UNDER_REVIEW`) prioritized.
- **FR-5.2** Each review item shows: registrant name + contact, method, expected vs. declared amount, transaction reference, payer name, screenshot thumbnail, and any auto-flags.
- **FR-5.3** Organizer actions per item: **Approve**, **Reject (with reason)**, **Waitlist**, **Mark Exempt**, **Cancel**, **Reopen**.

### FR-6 Auto Flags
- **FR-6.1** System flags: duplicate phone or email; duplicate transaction reference; amount mismatch (declared ≠ expected); missing payment proof; missing transaction reference; capacity already full.
- **FR-6.2** Flags are advisory — they warn the organizer but do not block manual action.

### FR-7 Attendee Status Page
- **FR-7.1** Each attendee has a unique, link-accessible status page (no login required for V1).
- **FR-7.2** Page shows the current status and the appropriate message/actions per state (see §11).
- **FR-7.3** `REJECTED` attendees see the rejection reason and can resubmit proof.

### FR-8 Event Link Gating
- **FR-8.1** The event link is rendered **only** for `CONFIRMED` and `EXEMPT` statuses.
- **FR-8.2** `PENDING`, `UNDER_REVIEW`, `REJECTED`, `WAITLISTED`, and `CANCELLED` never expose the link.

### FR-9 Communication
- **FR-9.1** System auto-sends an email on important status changes (registered, confirmed, rejected, waitlisted, exempt).
- **FR-9.2** Organizer can copy a WhatsApp message template per attendee.
- **FR-9.3** "Open WhatsApp" button opens a pre-filled message to the attendee's number.
- **FR-9.4** No WhatsApp Business API in V1.

### FR-10 Capacity & Waitlist
- **FR-10.1** Organizer sets a capacity per event.
- **FR-10.2** When capacity is reached, new registrations become `WAITLISTED`.
- **FR-10.3** Organizer can manually promote a `WAITLISTED` attendee to `CONFIRMED` when a seat opens.

### FR-11 Audit Log
- **FR-11.1** Every status change records: actor (who), timestamp (when), old status, new status, reason (if any).
- **FR-11.2** Audit history is viewable per registration.

### FR-12 Search / Filter / Export
- **FR-12.1** Organizer can search by name, phone, email, or transaction reference.
- **FR-12.2** Organizer can filter by status.
- **FR-12.3** Organizer can export registrations to Excel or CSV.

### FR-13 Group Registration
- **FR-13.1** One person can register/pay for multiple attendees.
- **FR-13.2** One payment proof can be linked to multiple attendee registrations.

### FR-14 Undo / Reopen
- **FR-14.1** Organizer can reopen/undo a mistaken approval or rejection, returning the registration to its prior state.
- **FR-14.2** Undo/reopen actions are themselves recorded in the audit log.

---

## 9. Non-Functional Requirements

- **NFR-1 Platform:** Responsive web application (desktop + mobile browser). No native app.
- **NFR-2 Usability:** Reviewing one payment should take seconds; an organizer should review ~80 payments in well under 15 minutes.
- **NFR-3 Localization:** Designed for the Egypt/Arab market; support Arabic-friendly content and right-to-left readiness. (Full i18n depth TBD.)
- **NFR-4 Security & privacy:** Attendee status-page links must be unguessable (random tokens). Personal data (phone, email, screenshots) handled per basic privacy expectations.
- **NFR-5 Reliability:** Status changes and audit-log writes must be durable and consistent — no lost or duplicated status updates.
- **NFR-6 Performance:** Dashboard and review queue remain responsive for events up to several hundred attendees.
- **NFR-7 Communication delivery:** Email sends are reliable; WhatsApp is assisted (pre-filled), not API-guaranteed.
- **NFR-8 Auditability:** Every state change is attributable and timestamped.
- **NFR-9 Data export:** Export must be self-serve and produce a clean Excel/CSV the organizer can use independently.

---

## 10. Acceptance Criteria

- **AC-1 (Event link gating):** Given an attendee whose status is not `CONFIRMED` or `EXEMPT`, when they open their status page, then the event link is **not** visible anywhere.
- **AC-2 (Confirmation unlock):** Given an attendee in `UNDER_REVIEW`, when the organizer approves them, then their status becomes `CONFIRMED`, the event link appears on their status page, and a confirmation email is sent.
- **AC-3 (Reject with reason):** Given an attendee in `UNDER_REVIEW`, when the organizer rejects with a reason, then status becomes `REJECTED`, the reason is shown on the status page, the attendee is notified, and they can resubmit proof (→ `UNDER_REVIEW`).
- **AC-4 (Auto flags):** Given a submitted proof with a transaction reference already used by another registration, when it enters the review queue, then it is flagged as a duplicate reference, but the organizer can still act manually.
- **AC-5 (Payer name mismatch handled):** Given an attendee who declared a different payer name, when the organizer reviews, then the card shows both registrant and payer names and is **not** auto-rejected.
- **AC-6 (Capacity / waitlist):** Given an event at full capacity, when a new attendee registers, then their status is `WAITLISTED`; when the organizer promotes them, then status becomes `CONFIRMED` and the link unlocks.
- **AC-7 (Exempt):** Given a VIP/free/scholarship attendee, when the organizer marks them `EXEMPT`, then they are treated as confirmed (link unlocked) with no payment required.
- **AC-8 (Audit log):** Given any status change, when it occurs, then an audit entry records actor, timestamp, old status, new status, and reason if present.
- **AC-9 (Undo):** Given a mistakenly approved/rejected registration, when the organizer reopens it, then it returns to the prior state and the reversal is logged.
- **AC-10 (Group registration):** Given one payer registering N attendees, when one proof is submitted, then it can be linked to all N registrations and reviewed together.
- **AC-11 (Export):** Given a set of registrations, when the organizer exports, then a valid Excel/CSV is produced containing the registrations and their statuses.
- **AC-12 (Status-page security):** Given a status-page link, when guessed or altered, then it does not grant access to another attendee's record.

---

## 11. Main User Flows

### Flow A — Organizer creates an event
1. Organizer logs in → creates event → fills type, title, description, date/time, capacity, price, event link.
2. System generates a public registration link.
3. Organizer shares the link (WhatsApp, social, etc.).

### Flow B — Attendee registers and pays
1. Attendee opens the registration link → fills name/phone/email (+ optional fields).
2. Attendee selects a payment method → sees the organizer's payment details.
3. Registration is created as `PENDING`; attendee receives a status-page link by email.
4. Attendee pays manually through their wallet/bank.
5. Attendee returns to the status page → uploads screenshot + enters transaction reference (+ payer name if different).
6. Status → `UNDER_REVIEW`.

### Flow C — Organizer reviews payment
1. Organizer opens the review queue (`UNDER_REVIEW` items).
2. Reviews the card (registrant, payer, amount, reference, screenshot, auto-flags).
3. Chooses an action: **Approve** → `CONFIRMED`; **Reject (reason)** → `REJECTED`; **Waitlist** → `WAITLISTED`; **Mark Exempt** → `EXEMPT`; **Cancel** → `CANCELLED`.
4. System records the audit entry, updates status, sends email, and offers a pre-filled WhatsApp message.

### Flow D — Attendee gets confirmed
1. Status becomes `CONFIRMED` (or `EXEMPT`).
2. Status page now shows "You're in!" with the **event link** unlocked + add-to-calendar.
3. Confirmation email (with link) is sent; organizer optionally sends the pre-filled WhatsApp message.

### Flow E — Rejection and resubmission
1. Status becomes `REJECTED` with a reason.
2. Status page shows the reason and re-opens the proof form.
3. Attendee resubmits → status returns to `UNDER_REVIEW` → back to Flow C.

### Flow F — Waitlist promotion
1. Event is full → new registrants are `WAITLISTED`.
2. A confirmed seat frees up (cancellation).
3. Organizer promotes a waitlisted attendee → `CONFIRMED` → link unlocks (Flow D).

---

## 12. Edge Cases

| # | Edge case | Handling in V1 |
|---|---|---|
| 1 | Payer name differs from registrant name | "Payer name if different" field; card shows both; not auto-rejected |
| 2 | Wrong / partial amount paid | Amount-mismatch auto-flag; organizer decides (approve / reject-with-reason). True partials deferred |
| 3 | Duplicate registration (same person) | Duplicate phone/email auto-flag |
| 4 | One payment for multiple attendees | Group registration; one proof linked to N registrations |
| 5 | Unclear or missing screenshot | Reject-with-reason → resubmit; reference is the primary verifiable token |
| 6 | Missing transaction reference | Missing-reference auto-flag |
| 7 | Same proof / reference reused | Duplicate-reference auto-flag |
| 8 | Old screenshot from a previous event | Reference uniqueness + manual review |
| 9 | Paid but never submitted proof | Stays `PENDING`; organizer can see it (auto-nudge deferred to V1.5) |
| 10 | Proof submitted but money never arrived | Organizer rejects-with-reason after checking their statement |
| 11 | Approved/rejected by mistake | Undo / reopen (FR-14) |
| 12 | Payment-method fees cause small amount difference | Amount-mismatch flag is advisory; organizer can still approve |
| 13 | Refund / cancellation after confirmation | `CONFIRMED → CANCELLED` (refund handled outside the system) |
| 14 | Seat transfer to another person | Cancel original + register/confirm new attendee |
| 15 | Paid after seats full | `WAITLISTED`; organizer promotes if a seat opens |
| 16 | Free / VIP / scholarship attendees | `EXEMPT` (no payment required, link unlocked) |
| 17 | Corporate / group one-payer-many | Group registration (FR-13) |
| 18 | Repeated "Am I confirmed?" questions | Self-serve status page answers it |
| 19 | Link must not reach unpaid people | Event-link gating (FR-8) |
| 20 | Disputes over who approved/rejected | Audit log (FR-11) |
| 21 | Status-page link guessing | Unguessable random tokens (NFR-4) |

**Deferred edge cases (not V1):** partial payments/installments; early-bird vs. normal price rules; discount/coupon rules; OCR/AI screenshot verification; automated auto-nudge sequences.

---

## 13. Success Metrics

> Directional targets — to be confirmed with real numbers once a pilot organizer uses the product.

- **Reconciliation time:** organizer reviews payments for an ~80-person event in **< 15 minutes** (vs. hours today).
- **Self-service:** "Am I confirmed?" inbound messages drop to **near zero** because the status page answers it.
- **Confirmation accuracy / trust:** 100% of confirmations are backed by a transaction reference and an audit-logged approval; the organizer trusts the confirmed-revenue count.
- **Link-leak elimination:** **0** unpaid attendees receive the event link (gating enforced).
- **Workflow replacement:** organizer runs the event **end-to-end without Excel or WhatsApp screenshot-chasing**.
- **Adoption signal:** an organizer runs a **second event** on the platform without being prompted.

---

## Deferred to Later (not in this document)

- Architecture and tech-stack decisions.
- Database schema / data model.
- UX/UI design specifications and screen mockups.
- Implementation / code.
