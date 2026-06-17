# Google Stitch Prompts — Event Management Platform

> **How to use:** Each screen below is a **complete, self-contained prompt**. Copy the entire fenced block for ONE screen and paste it into Google Stitch to generate that page. The brand spec is repeated inside every block, so you never assemble anything — one block = one page.
>
> Source design: [DESIGN.md](./DESIGN.md) · [EXPERIENCE.md](./EXPERIENCE.md). Built on Angular Material (MD3). Bilingual EN/AR, full RTL.
>
> **Suggested order:** start with **O5 Review Queue** and **A3 Status Page** — they carry the product.

---

## O1 — Organizer Login

```
Design a Material Design 3 web screen for "Event Management Platform" — a clean, trustworthy
payment-confirmation app for trainers in the Egypt/Arab market.

BRAND: calm, finance-grade, like a clean bank statement. Generous whitespace, no gradients.
Primary/brand color (action only, never status): Trust Blue #1F6FEB on #FFFFFF.
Surfaces: background #F7F8FA, surface #FFFFFF, on-surface #1A2330, muted text #5B6675, outline #C4C9D2.
Type: Inter (Latin) + IBM Plex Sans Arabic. Display 28/700, headline 20/600, body 15/400, label 13/500.
Shape: inputs 6px, buttons 10px, cards 14px. Cards at 1dp elevation.

SCREEN: Organizer Login (responsive web, centered, no nav).
A single centered Material card (14px corners, 1dp) on #F7F8FA, app name/logo above it,
EN/ع language toggle in the top corner.
Card contents: title "Sign in" (headline); Email field (Material outline); Password field
(outline, show/hide toggle); full-width filled primary "Sign in" button (Trust Blue);
small "Forgot password?" text link in primary color.

Generate these variants:
1. Default empty.
2. Error: calm inline message under the fields — "Email or password is incorrect." (no hint which);
   keep the entered email.
3. Loading: button shows a spinner, fields disabled.
Also produce the Arabic RTL mirrored version.
```

---

## O2 — Events List

```
Design a Material Design 3 web screen for "Event Management Platform" — a clean, trustworthy
payment-confirmation app for trainers in the Egypt/Arab market.

BRAND: calm, finance-grade, like a clean bank statement. Generous whitespace, no gradients.
Primary/brand color (action only, never status): Trust Blue #1F6FEB on #FFFFFF.
Surfaces: background #F7F8FA, surface #FFFFFF, surface-container #EEF1F5, on-surface #1A2330,
muted text #5B6675, outline #C4C9D2.
Type: Inter + IBM Plex Sans Arabic. Display 28/700, headline 20/600, title 16/600, label 13/500.
Shape: cards 14px, status chips full pill. Cards at 1dp.
STATUS CHIP COLORS (chip = container bg + colored text, always with a label):
Confirmed green (#1E8E5A on #E4F4EC), Pending gray-blue (#5B6675 on #EEF1F5),
Waitlisted neutral (#5B6675 on #EEF1F5).

SCREEN: Organizer Events List (desktop-first web).
Shell: left Material sidenav (Events active) + top toolbar (app name, EN/ع toggle, avatar menu).
Page title "Your events" + a filled primary "+ New Event" button top-right.
Main area: a responsive grid of event cards (Material cards, 14px, 1dp). Each card:
event title (title style); event type as a small chip (e.g. "Workshop"); date + time (muted label);
a row of status count chips — Confirmed (green), Pending (gray-blue), Waitlisted (neutral),
each a small chip with a number; a subtle "View" affordance.

Generate these variants:
1. Populated: 4-6 event cards in the grid.
2. EMPTY: centered block "No events yet. Create your first event to start taking registrations."
   + a filled primary "+ New Event" button.
3. Loading: skeleton cards.
Also produce the Arabic RTL mirrored version.
```

---

## O3 — Create / Edit Event

```
Design a Material Design 3 web screen for "Event Management Platform" — a clean, trustworthy
payment-confirmation app for trainers in the Egypt/Arab market.

BRAND: calm, finance-grade. Generous whitespace, no gradients.
Primary/brand color (action only): Trust Blue #1F6FEB on #FFFFFF.
Surfaces: background #F7F8FA, surface #FFFFFF, on-surface #1A2330, muted #5B6675, outline #C4C9D2.
Type: Inter + IBM Plex Sans Arabic. Headline 20/600, title 16/600, body 15/400, label 13/500.
Shape: inputs 6px, buttons 10px, cards 14px.
PAYMENT-METHOD DOTS (small ~8px dot beside the method name, never tint the row):
Vodafone Cash #E60000, InstaPay #5C2D91, bank #2B5797, cash #1E8E5A, other #5B6675.

SCREEN: Create / Edit Event (desktop-first web form).
Shell: left sidenav + top toolbar. Page title "Create event" (or "Edit event"). Form on
Material cards, comfortable spacing.
Fields (Material outline): event TYPE select (Course/Workshop/Webinar/Meetup/Conference/Training);
Title; Description (multiline); Date + Time pickers; Capacity (number); Price + currency (EGP);
Event link (URL) with note "shown only to confirmed attendees".
PAYMENT METHODS SECTION (key): heading "Payment methods" + a repeatable list of method rows.
Each row: method select (each option shows its colored dot), an "instructions" text field, and a
"destination" field (number/handle/account), with a small remove (x). An "+ Add payment method"
text button below. Footer: filled primary "Save event" + stroked "Cancel".

Generate these variants:
1. Create (empty form, one blank payment-method row).
2. Edit (pre-filled, two payment-method rows: Vodafone Cash + InstaPay).
3. Validation error: required fields (title, capacity) show inline Material errors.
Also produce the Arabic RTL mirrored version.
```

---

## O4 — Event Dashboard

```
Design a Material Design 3 web screen for "Event Management Platform" — a clean, trustworthy
payment-confirmation app for trainers in the Egypt/Arab market.

BRAND: calm, finance-grade. Generous whitespace, no gradients.
Primary/brand color (action only): Trust Blue #1F6FEB on #FFFFFF.
Surfaces: background #F7F8FA, surface #FFFFFF, on-surface #1A2330, muted #5B6675, outline #C4C9D2.
Type: Inter + IBM Plex Sans Arabic. Display 28/700, headline 20/600, title 16/600, label 13/500.
Shape: cards 14px, chips full pill. Cards at 1dp.
STATUS COLORS (stat card tint + label): Confirmed green (#1E8E5A/#E4F4EC),
Under review amber (#B7791F/#FCF3E3), Pending gray-blue (#5B6675/#EEF1F5),
Waitlisted neutral (#5B6675/#EEF1F5).

SCREEN: Organizer Event Dashboard (desktop-first web) — one event's home.
Shell: left sidenav (this event's sub-nav: Dashboard active, Review Queue, Registrations, Settings)
+ top toolbar. Header: event title + type chip + date.
Top: a row of summary stat cards (Material cards, 14px), each a big number + label, tinted with the
matching status color: Confirmed (green), Under review (amber), Pending (gray-blue),
Waitlisted (neutral); plus a "Capacity" card "62 / 80 seats" with a thin progress bar.
Below: two prominent quick-link panels — "Review payments" (shows count waiting, e.g. "12 waiting")
and "All registrations". Optional small "Share registration link" block with a copy button.

Generate these variants:
1. Active event, healthy numbers, 12 payments waiting.
2. Early state: mostly zeros, "Share your registration link to get started."
Also produce the Arabic RTL mirrored version.
```

---

## O5 — Review Queue ★ (hero)

```
Design a Material Design 3 web screen for "Event Management Platform" — a clean, trustworthy
payment-confirmation app for trainers in the Egypt/Arab market.

BRAND: calm, finance-grade, like a clean bank statement. Generous whitespace, no gradients.
Primary/brand color (action only, never status): Trust Blue #1F6FEB on #FFFFFF.
Surfaces: background #F7F8FA, surface #FFFFFF, surface-container #EEF1F5, on-surface #1A2330,
muted #5B6675, outline #C4C9D2.
Type: Inter + IBM Plex Sans Arabic. Headline 20/600, title 16/600, body 15/400, label 13/500.
MONO font (Roboto Mono) ONLY for transaction references and money amounts.
Shape: cards 14px, chips full pill. Cards at 1dp.
STATUS CHIP COLORS (chip = container bg + colored text + label): Confirmed green, Under review amber,
Rejected red (#C0392B/#FBE9E7), Waitlisted neutral, Exempt purple (#6B46C1/#EEE7FB).
PAYMENT-METHOD DOTS (~8px beside the method name): Vodafone Cash #E60000, InstaPay #5C2D91,
bank #2B5797, cash #1E8E5A.

SCREEN: Organizer Review Queue (desktop-first web) — the hero screen.
Shell: left Material sidenav (Events; current-event sub-nav: Dashboard, Review Queue [badge],
Registrations, Settings) + top toolbar (app name, EN/ع toggle, avatar). Content on #F7F8FA.
Main area: a stack of "review cards" (Material cards, 14px, 1dp), one payment per card. Each card:
- Registrant name + phone/email.
- Payer name shown beside it when different ("Payer: Mohamed (declared)").
- Payment method with its colored dot.
- Amount pair in MONO: "Expected 1500 / Declared 1500 EGP" (green when equal, amber when not).
- Transaction reference in MONO.
- Payment screenshot thumbnail.
- Auto-flag chips when relevant (amber "amount mismatch", red "duplicate reference").
- Action row: Approve (filled primary), Reject, Waitlist, Mark Exempt, Cancel.

Generate these variants:
1. Queue with several clean cards.
2. A card with an amber AMOUNT-MISMATCH flag (Expected 1500 / Declared 1000, amount amber).
3. A card with a red DUPLICATE-REFERENCE flag.
4. A GROUP card labeled "3 attendees on one payment" with one Approve action.
5. EMPTY STATE = a green success moment: big check + "All caught up. No payments waiting."
Also produce the Arabic RTL mirrored version.
```

---

## O6 — Reject / Cancel Dialog

```
Design a Material Design 3 web screen for "Event Management Platform" — a clean, trustworthy
payment-confirmation app for trainers in the Egypt/Arab market.

BRAND: calm, finance-grade. No gradients.
Primary/brand color: Trust Blue #1F6FEB. Error/destructive: #C0392B on #FFFFFF.
Surfaces: surface #FFFFFF, on-surface #1A2330, muted #5B6675, outline #C4C9D2, dimmed scrim behind.
Type: Inter + IBM Plex Sans Arabic. Title 16/600, body 15/400, label 13/500.
Shape: dialog 14px corners, buttons 10px.

SCREEN: Reject / Cancel Reason Dialog (Material dialog overlay, dimmed scrim).
A centered Material dialog (higher elevation). Contents:
- Title "Reject this payment?" (or "Cancel registration?").
- A line naming the attendee + payment: "Ahmed Hassan · InstaPay · 1500 EGP".
- Reason select (Material) with: "Wrong amount", "Unclear screenshot", "No payment found",
  "Duplicate", "Other".
- An optional note field (multiline) shown when needed (e.g. "Other").
- Helper line: "The attendee will be notified with this reason and can resend their proof."
- Footer: error-toned filled "Reject" button + stroked "Keep".

Generate these variants:
1. Default (a reason picked from the list).
2. "Other" selected with the note field filled in.
Also produce the Arabic RTL mirrored version.
```

---

## O7 — Registrations Table

```
Design a Material Design 3 web screen for "Event Management Platform" — a clean, trustworthy
payment-confirmation app for trainers in the Egypt/Arab market.

BRAND: calm, finance-grade. Generous whitespace, no gradients.
Primary/brand color (action only): Trust Blue #1F6FEB on #FFFFFF.
Surfaces: background #F7F8FA, surface #FFFFFF, on-surface #1A2330, muted #5B6675, outline #C4C9D2.
Type: Inter + IBM Plex Sans Arabic. Headline 20/600, body 15/400, label 13/500.
MONO font (Roboto Mono) ONLY for transaction references and amounts.
Shape: chips full pill. STATUS CHIP COLORS (chip = container + colored text + label):
Pending gray-blue, Under review amber, Confirmed green, Rejected red, Waitlisted neutral,
Exempt purple, Cancelled faded gray (#9AA3B2/#F1F3F6).
PAYMENT-METHOD DOTS beside the method: Vodafone Cash #E60000, InstaPay #5C2D91, bank #2B5797,
cash #1E8E5A, other #5B6675.

SCREEN: Organizer Registrations Table (desktop-first web) — the "Excel killer".
Shell: left sidenav (Registrations active) + top toolbar. Page title "Registrations".
Toolbar row above the table: a search field ("Search name, phone, email, or reference");
a row of status filter chips (All, Pending, Under review, Confirmed, Rejected, Waitlisted,
Exempt, Cancelled) in the status colors; an "Export" button (stroked, download icon) on the right.
Material table columns: Name | Contact | Method (with colored dot) | Status (status chip) |
Amount (mono) | Reference (mono) | Date. The status chip is the visual anchor of each row.
Clicking a row opens detail.

Generate these variants:
1. Populated table with a mix of statuses (so all chip colors appear).
2. FILTERED TO ZERO: "No registrations match these filters." + clear-filters action.
3. SEARCH NO MATCH: "Nothing matches 'ahmed'. Try a name, phone, email, or reference."
4. EMPTY (none yet): "No one's registered yet. Share your event link." + copy-link button.
5. Loading: skeleton rows.
Also produce the Arabic RTL mirrored version.
```

---

## O8 — Registration Detail

```
Design a Material Design 3 web screen for "Event Management Platform" — a clean, trustworthy
payment-confirmation app for trainers in the Egypt/Arab market.

BRAND: calm, finance-grade. Generous whitespace, no gradients.
Primary/brand color (action only): Trust Blue #1F6FEB on #FFFFFF.
Surfaces: background #F7F8FA, surface #FFFFFF, surface-container #EEF1F5 (muted note block),
on-surface #1A2330, muted #5B6675, outline #C4C9D2.
Type: Inter + IBM Plex Sans Arabic. Headline 20/600, title 16/600, body 15/400, label 13/500.
MONO font ONLY for reference + amounts. Shape: cards 14px, chips full pill.
STATUS CHIP COLORS as defined (Confirmed green, Rejected red, Waitlisted neutral, Exempt purple,
Pending gray-blue, Cancelled faded gray). Method dot beside the method name.

SCREEN: Organizer Registration Detail (desktop-first web).
Shell: left sidenav + top toolbar. Header: attendee name + a large status chip.
TWO-PANE layout:
LEFT (record + actions): attendee block (name, phone, email, registration date); payment-proof block
(method with dot, amount pair in mono — Expected vs Declared, amber if mismatched, transaction
reference in mono, viewable screenshot); action row (Approve / Reject / Waitlist / Mark Exempt /
Cancel / Reopen — show only actions valid for the current status).
RIGHT (history + notes): audit log — reverse-chronological list, each entry "actor · timestamp ·
old → new status · reason"; internal-note block (organizer-only, muted gray, e.g. "Cash received at
center"), clearly marked internal, never shown to the attendee.

Generate these variants:
1. CONFIRMED registration (action row offers Cancel / Reopen; audit log shows the approval).
2. REJECTED registration (rejection reason visible; audit log shows it).
3. CASH registration in PENDING: a "Mark confirmed" / "Mark exempt" action + an "Add internal note"
   field (e.g. "Cash received at center"); no screenshot/reference required.
Also produce the Arabic RTL mirrored version.
```

---

## O9 — Settings

```
Design a Material Design 3 web screen for "Event Management Platform" — a clean, trustworthy
payment-confirmation app for trainers in the Egypt/Arab market.

BRAND: calm, finance-grade. Generous whitespace, no gradients.
Primary/brand color (action only): Trust Blue #1F6FEB on #FFFFFF.
Surfaces: background #F7F8FA, surface #FFFFFF, on-surface #1A2330, muted #5B6675, outline #C4C9D2.
Type: Inter + IBM Plex Sans Arabic. Headline 20/600, title 16/600, body 15/400, label 13/500.
Shape: cards 14px, inputs 6px, buttons 10px.

SCREEN: Organizer Settings (desktop-first web).
Shell: left sidenav (Settings active) + top toolbar. Page title "Settings". Content in Material cards:
1. ACCOUNT: name, email (read-only), a "Change password" action.
2. LANGUAGE: a segmented control for default interface language (English / العربية).
3. MESSAGE TEMPLATES: two editable multiline fields with variable chips ({name}, {event},
   {status}, {link}):
   - "Email template" — auto-email body sent on status changes.
   - "WhatsApp template" — the pre-filled WhatsApp message the organizer copies/sends.
   Each with a small live preview and a "Reset to default" link.
A "Save changes" filled primary button.

Generate the default state, and also produce the Arabic RTL mirrored version.
```

---

## A1 — Attendee Registration Form

```
Design a Material Design 3 web screen for "Event Management Platform" — a clean, trustworthy
payment-confirmation app for trainers in the Egypt/Arab market.

BRAND: calm, reassuring, low-anxiety, finance-grade. No gradients.
Primary/brand color: Trust Blue #1F6FEB on #FFFFFF.
Surfaces: background #F7F8FA, surface #FFFFFF, on-surface #1A2330, muted #5B6675, outline #C4C9D2.
Type: Inter + IBM Plex Sans Arabic. Display 28/700, body 15/400, label 13/500.
Shape: inputs 6px, buttons 10px, cards 14px.
PAYMENT-METHOD DOTS (small dot beside each option): Vodafone Cash #E60000, InstaPay #5C2D91,
bank #2B5797, cash #1E8E5A, other #5B6675.

SCREEN: Attendee Registration Form (mobile-first web, single centered ~520px column, NO nav).
Slim header: event name + EN/ع toggle.
Top: a small event summary card (title, type chip, date/time, price in EGP, capacity note).
Form (Material outline fields, generous spacing): Full name (required); Phone (required);
Email (required); one example optional per-event field; Payment method select (each option shows its
colored dot); a full-width filled primary "Register" button; helper line "You'll get a personal
status link by email to complete payment."

Generate these variants:
1. Default empty form.
2. Validation error: required fields show calm inline errors ("Enter your phone number").
3. Capacity-full notice: an inline banner "Seats are full — you'll be added to the waitlist."
   above the Register button.
Also produce the Arabic RTL mirrored version.
```

---

## A2 — Registration Confirmation

```
Design a Material Design 3 web screen for "Event Management Platform" — a clean, trustworthy
payment-confirmation app for trainers in the Egypt/Arab market.

BRAND: calm, reassuring, finance-grade — no loud confetti. No gradients.
Primary/brand color: Trust Blue #1F6FEB on #FFFFFF.
Surfaces: background #F7F8FA, surface #FFFFFF, on-surface #1A2330, muted #5B6675.
Type: Inter + IBM Plex Sans Arabic. Display 28/700, body 15/400. Shape: buttons 10px.

SCREEN: Attendee Registration Confirmation (mobile-first web, single centered ~520px column, NO nav).
Slim header: event name + EN/ع toggle.
Centered success block: a calm success icon/illustration; headline (display) "You're registered.";
body "Check your email for your personal status link to complete your payment."; a prominent filled
primary button "Open my status page"; a small muted line "Didn't get the email? Check spam, or
contact the organizer."

Generate the default state, and also produce the Arabic RTL mirrored version.
```

---

## A3 — Attendee Status Page ★ (hero, 7 states)

```
Design a Material Design 3 web screen for "Event Management Platform" — a clean, trustworthy
payment-confirmation app for trainers in the Egypt/Arab market.

BRAND: calm, reassuring, finance-grade. Generous whitespace, no gradients.
Primary/brand color (action only, never status): Trust Blue #1F6FEB on #FFFFFF.
Surfaces: background #F7F8FA, surface #FFFFFF, on-surface #1A2330, muted #5B6675, outline #C4C9D2.
Type: Inter + IBM Plex Sans Arabic. Display 28/700 (the verdict headline), body 15/400, label 13/500.
MONO font (Roboto Mono) ONLY for the transaction reference and amount.
Shape: cards 14px, chips full pill.
STATUS CHIP COLORS (chip = container bg + colored text + label): Pending gray-blue (#5B6675/#EEF1F5),
Under review amber (#B7791F/#FCF3E3), Confirmed green (#1E8E5A/#E4F4EC), Rejected red (#C0392B/#FBE9E7),
Waitlisted neutral (#5B6675/#EEF1F5), Exempt purple (#6B46C1/#EEE7FB), Cancelled faded gray.
EVENT-LINK RULE: the event link appears ONLY in Confirmed and Exempt, styled as a soft-green
"reward" block (#1E8E5A text on #E4F4EC) — never a plain link, never in any other state.
PAYMENT-METHOD DOT beside the method name: InstaPay #5C2D91, etc.

SCREEN: Attendee Status Page (mobile-first web, single centered ~520px column, NO nav).
Slim header: event name + EN/ع toggle. One big status verdict per state.
This single screen has SEVEN states — generate each as its own frame:
1. PENDING (non-cash): headline "Complete your payment". Payment-method card (InstaPay handle/number
   + COPY button + instructions), amount to pay, a MONO transaction-reference input, a screenshot
   upload box, a "payer name if different" field, and a filled "Submit proof" button.
2. PENDING (cash): headline "Pay at the venue" + cash instructions + "Your spot is held — you'll be
   confirmed once payment is received in person." No reference/upload fields.
3. UNDER REVIEW: amber chip, headline "Payment received — we're reviewing it", subtext "Usually
   within a few hours. We'll email you."
4. CONFIRMED: green chip, headline "🎉 You're in!", a soft-green EVENT-LINK REWARD block with the
   event link prominent + add-to-calendar + event details.
5. EXEMPT: "You're confirmed as our guest" + the green event-link reward block.
6. REJECTED: red chip, headline "Action needed", the rejection reason shown, and a re-opened upload
   form to resubmit proof.
7. WAITLISTED: neutral chip, "Seats are full — you're #4 on the waitlist."
(Optional 8th: CANCELLED — a calm terminal message.)
Also produce the Arabic RTL mirrored version.
```

---

## A4 — Attendee Payment Submission

```
Design a Material Design 3 web screen for "Event Management Platform" — a clean, trustworthy
payment-confirmation app for trainers in the Egypt/Arab market.

BRAND: calm, reassuring, finance-grade. No gradients.
Primary/brand color: Trust Blue #1F6FEB on #FFFFFF.
Surfaces: background #F7F8FA, surface #FFFFFF, on-surface #1A2330, muted #5B6675, outline #C4C9D2.
Type: Inter + IBM Plex Sans Arabic. Headline 20/600, body 15/400, label 13/500.
MONO font (Roboto Mono) ONLY for the transaction reference and amount.
Shape: inputs 6px, buttons 10px, cards 14px.
PAYMENT-METHOD DOT beside the method name: InstaPay #5C2D91, etc.

SCREEN: Attendee Payment Submission (mobile-first web, single centered ~520px column, NO nav).
Reached from the PENDING status page. Slim header: event name + EN/ع toggle.
Contents: headline "Complete your payment" + the amount to pay, prominent (mono); a PAYMENT-METHOD
CARD for the chosen method (e.g. InstaPay) showing the destination handle/number with a COPY button +
the payment instructions + the method's colored dot; a transaction-reference input (Material outline,
MONO) with helper "from your transfer receipt"; a screenshot uploader (tap/drop area → thumbnail
preview + "Replace"); a "payer name if different" field (optional) with helper "if someone else paid
for you"; a full-width filled primary "Submit proof" button.

Generate these variants:
1. Empty (nothing entered).
2. Filled (reference entered, screenshot thumbnail showing).
3. Upload error: "Couldn't upload that image. Try again." (reference kept).
4. Submitting: button shows a spinner.
Also produce the Arabic RTL mirrored version.
```
