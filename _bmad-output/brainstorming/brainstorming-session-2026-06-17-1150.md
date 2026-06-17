---
stepsCompleted: [1, 2, 3, 4]
inputDocuments: []
session_topic: 'Event Management Platform — practical system for organizers to create, manage, and track multi-type events (courses, workshops, webinars, conferences, meetups, training)'
session_goals: 'Generate feature ideas, define MVP scope, confirm user roles, sketch user flows, suggest monetization, sequence build order, prioritize via MoSCoW, propose a practical roadmap (architecture deferred). No coding, no DB tables yet.'
selected_approach: 'progressive-flow'
techniques_used: ['Role Playing', 'What If Scenarios', 'Mind Mapping', 'Five Whys', 'Resource Constraints', 'SCAMPER', 'Decision Tree Mapping', 'Morphological Analysis']
ideas_generated: []
context_file: ''
---

# Brainstorming Session Results

**Facilitator:** Saqly
**Date:** 2026-06-17

## Session Overview

**Topic:** Event Management Platform — a practical system that helps organizers create, manage, and track different types of events (courses, workshops, webinars, conferences, meetups, training sessions).

**Goals:** Generate strong feature ideas, define MVP scope, identify the best user roles, suggest user flows, suggest monetization ideas, decide what to build first, prioritize features (Must/Should/Nice to Have), and propose a practical roadmap. Architecture to be designed later. No coding or DB schema yet.

### Session Setup

**Core problem:** Organizers manage registrations manually using Google Forms, WhatsApp, Excel, and manual confirmation messages — fragmented, error-prone, and unscalable.

**Primary users:**
1. Admin / Organizer
2. Instructor / Speaker
3. Attendee / Participant

**Supported event types:** Courses, Workshops, Webinars, Conferences, Meetups, Training sessions.

**Target market:** Egypt and Arab markets — trainers, training centers, and small organizers. Payment culture is manual wallets/transfers (Vodafone Cash, InstaPay, bank transfer, cash), and communication culture is WhatsApp-first.

---

## The Core Insight (the wedge)

> **The product is NOT about how money moves — wallets and transfers stay exactly as they are.**
> **The product is about how payment gets *verified, tracked, and communicated.***

The real pain isn't registration — it's the gap **after** registration:

> *"How can I know who registered, who paid, who is confirmed, and who should receive the event link — without manually checking WhatsApp, bank screenshots, and Excel?"*

Today this lives across three disconnected places: registration in Google Forms, payment proof in WhatsApp/Messenger, and the verdict in the organizer's head. The platform collapses those three into **one source of truth**.

---

## Phase 1 — Expansive Exploration (Ideas Generated)

### Problems & Pains (the "why")

**[Problem #1]: "Did I Even Get In?" — the Confirmation Black Hole**
_Concept:_ Attendees register then hear nothing — they don't know if they're confirmed, waitlisted, or lost in a spreadsheet. The organizer spends hours manually replying "yes, you're confirmed."
_Solution direction:_ A live, per-attendee registration **status page** with real-time confirmed/pending/rejected state.

**[Problem #2]: The Screenshot Reconciliation Nightmare** ⭐ (the #1 pain)
_Concept:_ Names on the form don't match payer names on transfers; proof arrives via WhatsApp/Messenger; the organizer plays detective matching screenshots to registrations across 3+ apps. Breaks badly past ~50 attendees.
_Solution direction:_ A **payment status pipeline** where each registrant has a clear state and the proof is **attached to their record**, not buried in a chat. Review becomes "work a queue," not "play detective."

**[Problem #3]: The Confirmation Gate = The Event Link**
_Concept:_ The Zoom/event link is blasted to a WhatsApp group, so unpaid people get in free and paid people lose it in 200 messages.
_Solution direction:_ Make the event link **invisible until Confirmed**, auto-delivered the moment payment is approved. The status page is the single door.

### Payment-Review Workflow Ideas (smart-assisted + trust-but-verify)

**[Feature #4]: The Review Queue as a Swipe Deck**
_Concept:_ One screen, one card per pending payment — name, method, expected amount, **typed transaction reference**, screenshot thumbnail, Approve/Reject buttons + keyboard shortcuts. 80 payments reviewed in minutes.
_Novelty:_ Purpose-built triage UI instead of a generic table; the reference field next to the screenshot means the image rarely needs opening.

**[Feature #5]: Reject-With-a-Reason (auto-message)**
_Concept:_ Rejection picks a reason (wrong amount / unclear screenshot / no payment found / duplicate) → attendee instantly notified + status page flips to "Action needed: re-upload" with the specific reason.
_Novelty:_ Turns rejection into a one-click, self-service fix — attendee resolves it without the organizer typing.

**[Feature #6]: Self-Declared Transaction Reference = Fast Lane**
_Concept:_ For InstaPay/Vodafone Cash, the **reference** is the real proof. Attendee types it (required), screenshot optional. Organizer cross-checks a batch against the bank/wallet statement.
_Novelty:_ Shifts the verifiable token onto the attendee; review becomes "does this ref look valid?" not "decode this blurry image."

### Edge Cases Mined (the stuff that breaks spreadsheets)

- **#10 Name mismatch** — payer ≠ registrant (family wallet). → add **"Payer name if different"** field.
- **#11 Wrong / partial amount** — under-pay, typo, "pay rest later." → **Paid vs Expected** on every card; **Partial** state + balance due.
- **#12 Duplicate registration / duplicate payment** — anxiety-driven double actions. → **dedupe on phone/email**; flag repeated reference.
- **#13 "Paid but never submitted proof" ghost** → **auto-nudge** if registered with no proof after X hours.
- **#14 Recycled / fake screenshot** → **transaction-reference uniqueness check** (same ref twice = auto-flag). No OCR/AI needed for V1.
- **#15 Audit trail** — shared staff dashboards, disputes. → every status change **timestamped + attributed** (who/when/old→new/reason).

**Full edge-case inventory (organizer-validated):** different payer name; wrong amount; late payment after full; unclear screenshot; old screenshot from a previous event; missing reference; same proof used twice; one person paying for many; multi-registration with different numbers; wrong phone/email; paid-but-no-proof; proof-but-money-not-arrived; approve-by-mistake; reject-by-mistake; payment-fee amount differences; refund after confirmation; seat transfer to another person; paid-after-full; early-bird vs normal price mismatch; discount/scholarship rules; free/VIP guests confirmed without payment; corporate/group one-payer-many; repeated "Am I confirmed?"; link must not reach pending/rejected; audit log need; revenue-accuracy trust.

**Top-priority edge cases for V1:** (1) payer-name mismatch, (2) wrong amount, (3) duplicate registration, (4) one payment for multiple attendees, (5) unclear/missing proof, (6) paid after seats full, (7) manual approval mistake, (8) repeated confirmation requests.

### Communication Channel Decision (market-fit)

WhatsApp is the real channel in this market, **but V1 must not depend on the WhatsApp API.** Agreed V1 approach:
- **Email** = default automatic channel (confirmations, status updates, event link)
- **Status page link** per attendee
- **Copyable WhatsApp template** + **"Open WhatsApp" button** that opens a *pre-filled* message to the attendee
- **V2:** real WhatsApp Business API integration

### Timeline Features Surfaced (parked for later phases)

- **[#7 Before] Event Setup Wizard with type presets** — webinar vs workshop vs conference pre-configures the right fields. (Should-have)
- **[#8 During] One-Tap Check-In** — confirmed list + QR/search, live show-up count. (Should-have / V1.5)
- **[#9 After] Auto Certificates** — personalized PDF certificates for attendees who showed. **Strong V2 + monetizable.** Replaces manual Canva/PowerPoint work; answers "when's my certificate? / fix my name? / resend it?"

---

## Phase 2–3 — Converged Structures (the MVP definition)

> **Design decision (Saqly):** Keep V1 a **simple app**. Use **one flat status list**, not a two-axis model. The two-axis (Registration × Payment) model is captured as a **V2 refinement**.

### 1. Simple Status Model (V1 — one flat list)

```
PENDING        → registered, hasn't paid / no proof yet
UNDER_REVIEW   → proof submitted, waiting for organizer
CONFIRMED      → approved & paid → event link unlocked
REJECTED       → issue with payment → action needed (can re-submit → back to UNDER_REVIEW)
WAITLISTED     → seats full
EXEMPT         → VIP / free guest / scholarship → confirmed without payment
CANCELLED      → refund / seat transfer / dropped
```

_(V2 idea: split into two axes — Registration status × Payment status — to cleanly handle Partial payments and installments.)_

### 2. Payment Review Workflow

1. Attendee submits proof → registration enters **UNDER_REVIEW** queue.
2. Review card (pre-filled): registrant name + contact · **payer name if different** · method · **expected vs declared amount** · **transaction reference (uniqueness-checked)** · screenshot thumbnail · ⚠️ auto-flags (amount mismatch / duplicate ref / seats full / duplicate phone).
3. Organizer acts: ✅ **Approve** → CONFIRMED · ❌ **Reject (+reason)** → action-needed · ⏸️ **Waitlist** · 🎁 **Mark Exempt**.
4. Action writes to **audit log** (who / when / old→new / reason).
5. Status change auto-fires: **email + status-page update**, plus a **"Send WhatsApp" pre-filled button**.

### 3. Required Dashboard Actions (V1)

Review queue (filterable triage deck) · Approve / Reject-with-reason / Waitlist / **Mark Exempt** · auto-flag panel · **seat counter + capacity lock → auto-waitlist** · **undo / re-open** a confirmed or rejected record · **per-person audit log** · **group registration** (one payment → N attendees) · **search by name/phone/reference** · **filter + export** (the Excel-killer) · **Send WhatsApp / Resend email** per attendee.

### 4. Attendee Status Page States

| State | Page shows |
|---|---|
| Pending payment | "Complete your payment" + method details + upload proof + reference field |
| Under review | "✅ Proof received — reviewing (usually within X hrs)" |
| Confirmed | "🎉 You're in!" + **event link unlocked** + add-to-calendar + resend |
| Rejected / action needed | "⚠️ Issue: [reason]. Please re-upload" + form re-opened |
| Waitlisted | "Seats full — you're #N on the waitlist" |
| Exempt (VIP/free) | "🎉 Confirmed as our guest" + event link |

**Hard rule:** the **event link renders ONLY in Confirmed / Exempt** states — never pending, rejected, or waitlisted.

---

## MVP Scope (V1 — Must Have)

1. Multi-type event creation + **capacity / seat limit**
2. Public **registration form** per event
3. **Payment method selection** + **proof upload** + **transaction reference (required)**
4. **"Payer name if different"** field
5. **Simple status model** (one flat list)
6. Organizer **review queue** with auto-flags
7. **Approve / Reject-with-reason / Waitlist / Mark Exempt**
8. **Capacity lock → auto-waitlist**
9. **Audit log** per registration
10. **Group / one-payment-for-many** registration
11. **Live attendee status page** (link-gated by status)
12. **Auto email** on every status change
13. **"Send WhatsApp" pre-filled button** + copyable template
14. **Search / filter / export** (Excel-killer)
15. **Undo / re-open** mistaken approvals

## Prioritization (MoSCoW)

**Must Have (V1):** items 1–15 above — the register → pay → review → confirm → status-page → link loop.

**Should Have (V1.5):** event setup wizard with type presets · one-tap check-in (QR/search) · partial-payment / balance-due handling · auto-nudge for unpaid registrations · bulk approve.

**Nice to Have (V2+):** auto certificates (monetizable) · real WhatsApp Business API · payment gateway integration (Paymob / Fawry / Stripe) · two-axis status model + installments · instructor/speaker portal · analytics (no-shows, revenue) · discount/early-bird/scholarship rules engine · multi-staff roles & permissions for training centers.

## Suggested Build Order (what to build first)

1. **Event + registration form** (the entry point)
2. **Status model + attendee status page** (the source of truth + kills "Am I confirmed?")
3. **Payment proof submission** (method + reference + screenshot)
4. **Organizer review queue + approve/reject** (the core wedge)
5. **Auto email on status change + link-gating**
6. **"Send WhatsApp" pre-filled button**
7. **Capacity / waitlist + audit log + export**

## Roadmap (high level)

- **V1 (MVP):** manual payment collection + smart-assisted review + attendee status tracking (Must-Have list).
- **V1.5:** setup wizard, check-in, partial payments, auto-nudges.
- **V2:** certificates (monetizable), WhatsApp Business API, two-axis status, instructor portal.
- **V3:** payment gateways, analytics, rules engine, multi-staff training-center accounts.

## Monetization Ideas (early)

- **Per-event / per-attendee fee** (small fee per confirmed registration).
- **Subscription tiers** for trainers / training centers (free up to N attendees, paid beyond).
- **Certificates as a paid add-on** (high willingness to pay — replaces Canva labor).
- **WhatsApp automation** as a premium tier (V2).
- **Payment gateway** with a small transaction margin (V3).

## Architecture

_Deferred by request — to be designed in a later session._

---

## Session Wrap-Up

**Status:** ✅ Complete.

### What we accomplished

| Goal | Outcome |
|---|---|
| Generate strong feature ideas | 15+ features + 6+ edge-case-driven mechanisms mined |
| Define MVP scope | 15-item Must-Have list locked |
| Identify user roles | Organizer + Attendee (V1 primary); Instructor + multi-staff (deferred) |
| Suggest user flows | Register → pay → review → confirm → status-page → link loop defined |
| Suggest monetization | 5 directions (per-attendee fee, tiers, paid certificates, WhatsApp, gateway margin) |
| Decide what to build first | 7-step build order sequenced |
| Prioritize (MoSCoW) | Must / Should / Nice-to-Have split complete |
| Practical roadmap | V1 → V1.5 → V2 → V3 outlined |
| Architecture | Deliberately deferred |

### Key decisions made
- **The wedge:** verify/track/communicate payment — don't change how money moves.
- **Simple V1:** one flat status model (not two-axis), manual payment only.
- **WhatsApp:** pre-filled link/template in V1; Business API in V2.
- **Certificates:** parked as V2 monetizable add-on, kept out of V1.

### Most valuable breakthroughs
1. The event link gated to Confirmed/Exempt status — one rule that solves the "link reaches unpaid people" problem.
2. The review queue as a purpose-built triage deck (transaction reference next to screenshot).
3. Reframing "one payment for many" and "corporate" as a registration-*unit* concept, not an edge case.

### Facilitation notes
Strong, market-grounded session. User repeatedly pulled the focus back to real Egyptian/Arab market behavior (manual wallets, WhatsApp-first) and made disciplined scope calls (parking certificates, choosing the simple flat status model). Highest energy was on payment-review edge cases — correctly identified as the core wedge.

### Next steps
- ✅ **Product Brief** drafted from this session → `_bmad-output/planning-artifacts/briefs/brief-event-mangment-iti-session-kiro-2026-06-17/brief.md`
- ▶️ Recommended follow-ons: finalize the brief → PRD → UX flows → architecture (later).

