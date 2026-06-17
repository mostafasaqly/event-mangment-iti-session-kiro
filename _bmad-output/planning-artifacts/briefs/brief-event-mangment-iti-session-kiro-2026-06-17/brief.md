---
title: "Product Brief: Event Management Platform (V1)"
status: final
created: 2026-06-17
updated: 2026-06-17
---

# Product Brief: Event Management Platform

## Executive Summary

Trainers and small training centers in Egypt and the wider Arab market run their events on a patchwork of Google Forms, WhatsApp, and Excel. Registration happens in one place, payment proof arrives in another, and the verdict — *who is actually confirmed* — lives only in the organizer's head. Past ~50 attendees this collapses into hours of manual screenshot-matching and a flood of "Am I confirmed?" messages.

This platform replaces that patchwork with **one source of truth** for registration and payment status. Crucially, it does **not** change how money moves — attendees keep paying by Vodafone Cash, InstaPay, bank transfer, or cash, exactly as they do today. What changes is how payment gets **verified, tracked, and communicated**: attendees submit a transaction reference and proof, organizers approve or reject from a single review queue, and every attendee gets a live status page that unlocks the event link the moment they are confirmed.

The wedge is deliberately narrow and shippable: manual payment collection + smart-assisted review + attendee status tracking. It meets the market where it is (manual wallets, WhatsApp-first communication) rather than forcing a payment gateway nobody is ready for, which is exactly why it can win where generic event tools have not.

## The Problem

The organizer's real pain is not registration — it is the gap *after* registration. The job-to-be-done is:

> "How can I know who registered, who paid, who is confirmed, and who should receive the event link — without manually checking WhatsApp, bank screenshots, and Excel?"

A concrete scenario: Mariam runs a 3-day workshop. She has 80 form responses, an Excel sheet she copy-pastes into by hand, and a WhatsApp inbox full of payment screenshots. The transfer for "Ahmed Hassan" arrives from "Mohamed Ahmed" (his brother's wallet). Someone paid the wrong amount. Two people registered twice out of anxiety. A dozen keep asking whether they are confirmed. The Zoom link gets blasted to a WhatsApp group, so unpaid people get in free and paid people lose it in 200 messages.

The cost of the status quo: hours of manual reconciliation per event, payment disputes with no audit trail, revenue the organizer can never fully trust, and a registration process that simply breaks at scale.

## The Solution

A web platform where the organizer creates an event, shares one registration link, and works a single dashboard:

- **Attendees** register, choose a payment method, pay manually, then submit a **transaction reference** (required) and optional screenshot. They get a personal **status page** that shows exactly where they stand.
- **Organizers** review pending payments in a purpose-built **triage queue** — each card shows the registrant, the declared payer name (if different), expected vs. declared amount, the reference, and a screenshot thumbnail, with auto-flags for mismatches and duplicates. One click approves, rejects (with a reason), waitlists, or marks exempt.
- **The system** flips status automatically, emails the attendee, and — because WhatsApp is the real channel here — gives the organizer a **pre-filled "Send WhatsApp" button**. The event link is revealed on the status page **only** when the attendee is Confirmed or Exempt.

The experience for the organizer is "work a queue, not play detective." The experience for the attendee is "I always know where I stand, and I stop having to ask."

## What Makes This Different

- **Meets the market's actual payment behavior.** It embraces manual wallets/transfers instead of requiring a gateway. Generic global tools (Eventbrite, etc.) assume card payment and fail here; this is built for Vodafone Cash / InstaPay reality.
- **Payment *verification* is the product, not an afterthought.** The review queue, transaction-reference uniqueness check, and status-gated event link are the core — not a bolt-on.
- **WhatsApp-respecting without WhatsApp-dependent.** V1 uses email + pre-filled WhatsApp links (near-zero infra), honoring how people actually communicate without taking on Business API complexity.
- **Honest moat:** this is **execution and market-fit**, not defensible technology. The advantage is being precisely right for one underserved market and shipping a focused wedge faster than generic tools can localize.

## Who This Serves

**Primary — Organizer / Admin (e.g., Mariam, runs a small training academy).** Needs to know at a glance who is registered, paid, confirmed, or waitlisted, and to stop reconciling screenshots by hand. Success = an event run end-to-end without touching Excel or chasing payments in WhatsApp.

**Primary — Attendee / Participant.** Needs certainty: *am I in?* Success = registering, paying, and knowing their confirmed status (and getting the event link) without ever messaging the organizer.

**Secondary — Instructor / Speaker.** A role in the long-term vision, but **not** a focus of V1 — no dedicated portal in the first version.

**Secondary — Training center staff (multi-user).** Shared dashboards with an audit trail matter for centers, but full multi-staff roles and permissions are deferred beyond V1.

## Success Criteria

Directional targets to confirm with real numbers once a pilot organizer is using the product:

- **Reconciliation time:** organizer spends < 15 minutes reviewing payments for an 80-person event (vs. hours today).
- **Self-service:** the "Am I confirmed?" message volume drops to near zero because the status page answers it.
- **Trust:** every confirmation is backed by a verified reference + audit-logged approval; the organizer trusts the confirmed-revenue number.
- **Adoption signal:** an organizer runs a *second* event on the platform without being asked (proof the wedge replaced the Forms+WhatsApp+Excel workflow).

## Scope

**V1 stays small, practical, and focused on the core wedge:** manual payment collection + payment proof review + attendee status tracking + event link gating. The flow is everything: *Register → submit payment proof → organizer reviews → status updates → event link unlocks for confirmed attendees only.*

### In Scope for V1

1. **Event creation** — organizer creates an event (course, workshop, webinar, meetup, conference, or training session) with title, description, date, time, capacity, price, and event link.
2. **Public registration form** — attendee registers; required fields name/phone/email, optional fields per event, and payment-method selection.
3. **Manual payment proof submission** — method (Vodafone Cash, InstaPay, bank transfer, cash, or other manual); screenshot upload; required transaction reference; "payer name if different" field.
4. **Simple flat status model** — `PENDING`, `UNDER_REVIEW`, `CONFIRMED`, `REJECTED`, `WAITLISTED`, `EXEMPT`, `CANCELLED`.
5. **Organizer payment review dashboard** — see pending proofs; review attendee data, method, amount, reference, screenshot, payer name; approve / reject-with-reason / waitlist / mark exempt / cancel / reopen.
6. **Auto flags** — duplicate phone or email; duplicate transaction reference; amount mismatch; missing payment proof; missing transaction reference; capacity already full.
7. **Attendee status page** — unique link per attendee showing their status; rejected attendees see the reason and can resubmit proof.
8. **Event link gating** — link appears only for `CONFIRMED` or `EXEMPT`; hidden for pending, rejected, waitlisted, or cancelled.
9. **Communication** — auto email on important status changes; copyable WhatsApp template; "Open WhatsApp" button with pre-filled message. No WhatsApp Business API.
10. **Capacity and waitlist** — set capacity; full seats route new registrations to `WAITLISTED`; organizer can manually promote `WAITLISTED → CONFIRMED` when a seat opens.
11. **Audit log** — every status change recorded with who, when, old status, new status, and reason if available.
12. **Search, filter, and export** — search by name/phone/email/reference; filter by status; export to Excel or CSV.
13. **Basic group registration** — one person paying for multiple attendees; connect one payment proof to multiple attendees.
14. **Undo / reopen** — reverse mistaken approvals or rejections.

### Out of Scope for V1

1. **Real payment gateway integration** — no Paymob, Fawry, Stripe, online card payments, or automatic gateway confirmation.
2. **WhatsApp Business API** — pre-filled messages and copyable templates only.
3. **Auto certificates** — deferred to V2 / paid add-on.
4. **QR check-in** — no QR attendance/check-in (candidate for V1.5).
5. **Instructor / speaker portal** — V1 serves organizer and attendee only.
6. **Advanced analytics** — no revenue, no-show, or conversion dashboards; basic counts only.
7. **Multi-staff permissions** — single organizer/admin account is enough for MVP.
8. **Complex conference features** — no agenda builder, tracks, speaker, sponsor, or exhibitor management.
9. **Discount / scholarship rules engine** — no coupon system; use `EXEMPT` manually for free/VIP/scholarship attendees.
10. **Partial payments and installments** — V1 supports paid / pending / rejected / confirmed only (candidate for V1.5/V2).
11. **Full CRM** — no long-term attendee profiles beyond event registration.
12. **Mobile app** — responsive web app only, no native app.
13. **AI / OCR screenshot reading** — review is manual but organized.
14. **Marketplace / public event discovery** — each organizer has their own registration page; no public marketplace.
15. **Subscription billing system** — no complex SaaS billing; monetization validated manually first.

### Scope Statement

**V1 is not a full event management platform.** It is a focused **payment confirmation and attendee status system** for trainers and training centers who currently rely on Google Forms, WhatsApp screenshots, and Excel. It replaces that messy workflow with one simple flow: *Register → submit payment proof → organizer reviews → status updates → event link unlocks for confirmed attendees only.*

**Architecture:** deliberately deferred to a later session — no schema or tech-stack decisions in this brief.

## Vision

V1 is the wedge: be the tool a single trainer trusts to run one event end-to-end. From there:

- **V1.5:** event setup wizard with type presets, one-tap check-in (QR/search), partial-payment handling, auto-nudges for unpaid registrations.
- **V2:** **auto-generated certificates** (a strong monetizable add-on that replaces manual Canva work), real WhatsApp Business API, two-axis status with installments, an instructor portal.
- **V3:** payment gateways, analytics, a rules engine for discounts/scholarships, and full multi-staff accounts for training centers.

**Monetization direction** (unvalidated — to test, not yet committed): per-confirmed-attendee fee; subscription tiers for trainers and centers (free under N attendees); certificates as a paid add-on; WhatsApp automation and payment-gateway margin as premium tiers later. If it succeeds, it becomes the default operating system for independent trainers and small training centers across the Arab market.
