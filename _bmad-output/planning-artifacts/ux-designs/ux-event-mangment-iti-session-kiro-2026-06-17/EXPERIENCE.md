---
name: Event Management Platform
status: final
sources:
  - "{planning_artifacts}/prds/prd-event-mangment-iti-session-kiro-2026-06-17/prd.md"
updated: 2026-06-17
---

# Event Management Platform — Experience Spine

> Pairs with `DESIGN.md`. Owns *how it works*: information architecture, behavior, states, flows. Visual tokens referenced by name as `{path.to.token}`. Both spines win on conflict with any mock or import.

## Foundation

**Two responsive web surfaces, one app.** Built in **Angular with Angular Material (Material Design 3)** — components inherit MD3 anatomy, ripple/state-layer interactions, and accessibility defaults; `DESIGN.md` specifies only the brand-layer delta (color roles, type families, shape scale, the seven-status custom color groups, and a few custom tokens). This spine specifies the behavioral delta on top of Material — only where the product needs more than MD3 gives by default. There is no native mobile app.

- **Organizer surface** — desktop-first, authenticated (email + password, FR-15). Dense, scannable, keyboard-friendly; the Review Queue is the center of gravity. Degrades gracefully to mobile (a trainer checking payments on a phone).
- **Attendee surface** — mobile-first, **no login**. Reached only via two unguessable token links: the public registration link (per Event) and the personal Status Page link (per Registration, FR-7). Calm, single-column, reassuring.

**Bilingual Arabic + English, full RTL.** A language toggle is always reachable; the entire layout mirrors in Arabic using logical properties. Numbers, currency (EGP), and dates follow locale. The Transaction Reference is always LTR even in RTL context (it's a code).

`DESIGN.md` is the visual identity reference. This spine specifies behavior and copy intent only.

## Information Architecture

### Organizer surface (authenticated, desktop-first)

| Surface | Reached from | Purpose |
|---|---|---|
| Login | App open (unauthenticated) | Email + password sign-in |
| Events list | Login / left nav "Events" | All the organizer's Events with at-a-glance counts (confirmed / pending / waitlisted) |
| Create / Edit Event | Events list "+ New Event" / event row | Event details + Capacity + price + Event Link + Payment Methods config (FR-1, FR-1b) |
| Event dashboard | Events list row | One Event's home: summary counts, quick links to the queue and registrations |
| **Review Queue** | Event dashboard / nav badge | The hero surface — `UNDER_REVIEW` registrations awaiting a decision (FR-5) |
| Registrations table | Event dashboard | All registrations, searchable/filterable/exportable (FR-12); the Excel-killer |
| Registration detail | Queue card / table row | Full record: status, payment proof, payer, amount, reference, audit log, internal notes, actions |
| Settings | Avatar menu | Account, language, WhatsApp/email template defaults |

Left nav (desktop) collapses to a top bar + drawer below `md`. A persistent badge on **Review Queue** shows the count awaiting review.

### Attendee surface (token links, mobile-first, no login)

| Surface | Reached from | Purpose |
|---|---|---|
| Registration form | Public Event link | Register: name/phone/email + optional fields + payment-method selection (FR-2) |
| Registration confirmation | After submit | "You're registered — check your email for your status link" + immediate link to the Status Page |
| **Status Page** | Personal token link (email) | The attendee's home — current Status + state-appropriate content (FR-7); the "Am I confirmed?" killer |
| Payment submission | Status Page (PENDING, non-cash) | Method instructions + reference + proof upload + payer-name (FR-3) |

→ Composition references rendered at Finalize live in `mockups/` (Review Queue, Status Page states). Spine wins on conflict.

**Surface closure:** every PRD capability lands on a surface, and every surface is reached by a flow below. Closed.

## Voice and Tone

Microcopy is **plain, reassuring, and honest** — never hype, never blame. The attendee is often anxious about money; the organizer is busy. Speak to both like a competent, calm colleague. Arabic copy is written natively (not translated literally) and carries the same calm tone.

| Do | Don't |
|---|---|
| "Payment received — we're reviewing it." | "Thanks!! Your payment is being processed 🎉" |
| "You're in. Here's your event link." | "Congratulations, registration successful!" |
| "We couldn't match this payment. Here's why: {reason}. You can resend your proof below." | "Payment rejected." |
| "Seats are full right now. You're #4 on the waitlist." | "Registration failed — event is full." |
| "Enter the transaction reference from your transfer." | "Reference number (required field)" |
| Organizer: "12 payments waiting." | "You have 12 items pending your review." |

Status names shown to attendees are humanized ("Under review," "You're in," "Action needed"); the system status codes (`UNDER_REVIEW`, etc.) are organizer/internal vocabulary.

## Component Patterns

Behavioral rules; visual specs live in `DESIGN.md.Components`.

| Component | Use | Behavioral rules |
|---|---|---|
| **Status badge** ({components.status-badge}) | Everywhere a Status appears | Color is bound to the Status and never varies by surface. Read-only; it reflects state, never sets it. |
| **Review card** ({components.review-card}) | Review Queue | Shows registrant + contact, payer name (if declared, both shown), expected vs. declared amount, Transaction Reference (mono), screenshot thumbnail (tap to zoom), auto-flag chips, and the action row. One card = one decision. Keyboard: `A` approve, `R` reject, `W` waitlist, `E` exempt. |
| **Auto-flag chip** | Review card | Advisory only (FR-6). Warning tone (amber) for amount mismatch / capacity full; error tone (red) for duplicate reference / duplicate phone-email / missing reference. Never blocks an action. A declared payer-name mismatch is **not** flagged. |
| **Action row** | Review card, Registration detail | Approve (primary), Reject (needs reason), Waitlist, Mark Exempt, Cancel, Reopen — only the actions legal for the current Status are shown (per FR-4 transitions). Reject and Cancel open a confirm step capturing a reason. |
| **Payment-method card** | Attendee payment submission | Shows the selected method's instructions + destination (number/handle/account) with a **copy** button; amount to pay prominent. |
| **Reference input** | Payment submission | Monospace, with helper "from your transfer receipt." Required for non-cash, optional/hidden for cash. |
| **Screenshot uploader** | Payment submission | Single image, shows thumbnail preview + replace. Optional even for non-cash (reference is the primary token). |
| **Empty / error / success block** | All surfaces | One display line + one body line + ≤1 action. Consistent everywhere. |
| **Audit log list** | Registration detail | Reverse-chronological: actor · timestamp · old→new Status · reason/note. Read-only (FR-11). |

## State Patterns

### Attendee Status Page — one screen, seven states (FR-7, FR-8)

The Status Page *is* the product for the attendee. It renders exactly one state:

| Status | Headline (display) | Body / actions | Event Link? |
|---|---|---|---|
| **PENDING** (non-cash) | "Complete your payment" | Payment-method card (instructions + destination + copy), amount, Transaction Reference field, screenshot upload, payer-name-if-different, **Submit proof** button | No |
| **PENDING** (cash) | "Pay at the venue" | Cash instructions; "Your spot is held — you'll be confirmed once payment is received in person." No reference/upload fields | No |
| **UNDER_REVIEW** | "Payment received — we're reviewing it" | "Usually within {review-window}. We'll email you." No action needed | No |
| **CONFIRMED** | "🎉 You're in!" ({color.status-confirmed}) | **Event Link** (prominent) + add-to-calendar + event details + resend-link | **Yes** |
| **EXEMPT** | "You're confirmed as our guest" | Event Link + details | **Yes** |
| **REJECTED** | "Action needed" ({color.status-rejected}) | Rejection **reason** shown; proof form **re-opened** to resubmit (→ UNDER_REVIEW) | No |
| **WAITLISTED** | "Seats are full" | "You're #{n} on the waitlist. We'll notify you if a spot opens." | No |
| **CANCELLED** | "This registration was cancelled" | Calm, terminal; contact-organizer hint | No |

The Event Link is rendered **only** for CONFIRMED and EXEMPT — enforced at render, not just hidden via CSS.

### Organizer dashboard states

| State | Surface | Treatment |
|---|---|---|
| **Empty — no events** | Events list | "No events yet. Create your first event to start taking registrations." + primary **New Event**. |
| **Empty — queue clear** | Review Queue | "All caught up. No payments waiting." (success-toned, green check). The good empty state. |
| **Empty — no registrations** | Registrations table | "No one's registered yet. Share your event link." + copy-link button. |
| **Loading** | Any list/queue | Skeleton rows matching layout; resolve on data. |
| **Filtered to zero** | Registrations table | "No registrations match these filters." + clear-filters action. |
| **Search no match** | Registrations table | "Nothing matches '{query}'. Try a name, phone, email, or reference." |

### Error states

| Error | Where | Treatment |
|---|---|---|
| Required field missing | Registration form / payment | Inline under the field, calm: "Enter your phone number." Submit stays disabled until resolved. |
| Reference missing (non-cash) | Payment submission | Inline: "Enter the transaction reference from your transfer." |
| Upload failed | Payment submission | "Couldn't upload that image. Try again." Keeps entered reference. |
| Duplicate reference (attendee) | Payment submission | **Not** blocked — submission proceeds; the duplicate becomes an organizer-side auto-flag (trust-but-verify). |
| Capacity full at registration | Registration form | Not an error — attendee is accepted as WAITLISTED with a clear message. |
| Save/action failed | Organizer action | Toast (destructive): "Couldn't save that. Trying again." Action state retained; retry. |
| Expired/invalid token link | Status Page | "This link isn't valid. Check your email for the latest one, or contact the organizer." Never leaks another record. |
| Login failed | Login | "Email or password is incorrect." No which-one disclosure. |

### Success states

| Success | Treatment |
|---|---|
| Registration submitted | Confirmation screen + "check your email for your status link" + direct link. |
| Proof submitted | Status Page flips to UNDER_REVIEW with "Payment received — we're reviewing it." |
| Organizer approves | Row leaves the queue; toast "Confirmed — attendee notified." Event Link now live on their Status Page + email sent. |
| Reject with reason | Toast "Marked rejected — attendee notified with your reason." |
| Waitlist / Exempt / Cancel | Toast naming the new state + "attendee notified." |
| Reopen | Toast "Reopened — back to {prior status}." Audit entry written. |
| Export | Toast "Exported {n} registrations." File downloads. |

## Interaction Primitives

**Organizer (desktop, throughput-oriented):**
- Review Queue card actions have keyboard shortcuts: `A` approve, `R` reject, `W` waitlist, `E` exempt, `C` cancel; `J`/`K` move between cards; `Enter` opens detail.
- Reject and Cancel always require a reason (typed or picked from common reasons: "wrong amount," "unclear screenshot," "no payment found," "duplicate").
- Group registrations: approving a linked group proof confirms all N in one action (FR-13); the queue shows "{n} attendees on one payment."
- "Send WhatsApp" opens a pre-filled message in a new tab (`wa.me` deep link, FR-9); "Copy template" copies to clipboard. No WhatsApp API.

**Attendee (mobile, low-anxiety):**
- One primary action per screen. Copy buttons on every payment destination (number/handle/account).
- The Status Page auto-reflects the latest status on load (no manual refresh expectation); a "Refresh" affordance exists for the impatient.

**Banned everywhere:** auto-confirming a payment without an organizer decision (every CONFIRMED traces to a human, per PRD counter-metric SM-C2); blocking an attendee on an advisory flag; exposing the Event Link in any non-CONFIRMED/EXEMPT state; hover-only actions on touch.

## Accessibility Floor

Behavioral; visual contrast lives in `DESIGN.md` (status pairs verified for AA).

- **WCAG 2.2 AA** across both surfaces.
- **Status is never color-alone** — every status badge pairs its color with a text label (and optional icon/dot), so color-blind users and screen readers get the state. Critical given seven statuses.
- Full **keyboard operability** on the organizer surface; visible focus rings ({colors.ring}).
- **Screen reader** announces Status Page state on load ("Status: confirmed. Your event link is available.") and announces queue actions ("Confirmed. 11 payments remaining.") via `aria-live`.
- **RTL**: tab/reading order follows visual order in both directions; logical properties throughout.
- Form errors associated with inputs (`aria-describedby`); the Transaction Reference field announces its format hint.
- Touch targets ≥ 44px on the attendee surface.

## Responsive & Platform

| Surface | ≥ lg (desktop) | md (tablet) | < md (phone) |
|---|---|---|---|
| Organizer dashboard | Left nav + wide tables; Review Queue as multi-column card grid | Nav collapses to icons; queue single column | Top bar + drawer; queue is a vertical card stack; tables become stacked rows |
| Attendee surface | Centered single column (~520px), lots of margin | Same column, more margin | Full-width single column — the design target |

Organizer dashboard is desktop-first but must be *usable* on a phone (a trainer reviewing payments on the go). Attendee surface is phone-first and merely centers on larger screens.

## Key Flows

### Flow 1 — Mariam clears the review queue (organizer, desktop, evening before the workshop)

1. Mariam logs in (email + password) and opens the **Review Queue** for "Intro to Data Analysis" — the nav badge reads **18**.
2. The first review card shows Ahmed: InstaPay, expected 1500 / declared 1500 EGP, a monospace reference, a screenshot thumbnail, and a green-free card (no flags). She presses `A`.
3. Next card carries an amber **amount-mismatch** flag (declared 1000). She taps the screenshot to zoom, decides it's a partial she won't accept, presses `R`, and picks "wrong amount" as the reason.
4. A card shows **"3 attendees on one payment"** (Sara's team). She approves once; all three confirm together.
5. A late registrant is auto-**WAITLISTED** because confirmed seats hit Capacity; she leaves them.
6. **Climax:** The queue badge ticks down to **0** and the surface shows the green "All caught up. No payments waiting." Every approved attendee was emailed and their Event Link unlocked — Mariam never opened WhatsApp or Excel. She trusts the confirmed count as real revenue, and every decision sits in the audit log.

Failure: she approves the wrong person by reflex → opens their detail, hits **Reopen**, status returns to UNDER_REVIEW, link removed, reversal logged.

### Flow 2 — Ahmed registers, pays, and knows he's in (attendee, phone)

1. Ahmed taps Mariam's registration link from WhatsApp. The form (mobile, single column) asks name/phone/email and a payment method; he picks **InstaPay** and submits.
2. Confirmation: "You're registered — check your email for your status link." He opens the email and lands on his **Status Page**, now **PENDING**: an InstaPay payment-method card with the destination handle and a **copy** button, the amount, a reference field, and an upload box.
3. He pays in his banking app, copies the transaction reference, returns, pastes it (monospace), uploads the screenshot, and taps **Submit proof**.
4. The page flips to **UNDER_REVIEW**: "Payment received — we're reviewing it. Usually within a few hours."
5. **Climax:** Later, Mariam approves him. His Status Page (and a confirmation email) now reads **"🎉 You're in!"** in green with the **event link** front and center and an add-to-calendar button. He never sent a single "Am I confirmed?" message.

Failure: his screenshot was unclear → page shows **REJECTED / "Action needed"** with the reason and a re-opened upload form; he resubmits without contacting anyone (→ UNDER_REVIEW).

### Flow 3 — Cash at the center (organizer + walk-in attendee)

1. A walk-in registers on a tablet at the center and selects **Cash**; their registration sits **PENDING** with "Pay at the venue — your spot is held."
2. They hand cash to the front desk. Mariam opens their registration detail and chooses **Mark Confirmed**, adding the internal note "Cash received at center."
3. **Climax:** Status flips to **CONFIRMED**, the event link appears on the attendee's status page, a confirmation email goes out, and the audit log records the cash confirmation with Mariam's note — money that never touched a screenshot is now tracked exactly like every other payment.
