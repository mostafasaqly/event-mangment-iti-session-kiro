---
name: Event Management Platform
status: final
description: Clean, trustworthy payment-confirmation and attendee-status system for trainers in the Egypt/Arab market. Angular + SCSS, custom token system (no component library). Bilingual AR/EN, full RTL.
sources:
  - "{planning_artifacts}/prds/prd-event-mangment-iti-session-kiro-2026-06-17/prd.md"
  - "{output_folder}/brainstorming/brainstorming-session-2026-06-17-1150.md"
updated: 2026-06-17
colors:
  # Full token set — Angular + SCSS, no library inheritance. Light theme primary; dark deferred to v2.
  background: '#F7F8FA'
  surface: '#FFFFFF'
  foreground: '#1A2330'
  muted: '#EEF1F5'
  muted-foreground: '#5B6675'
  border: '#E2E6EC'
  input: '#FFFFFF'
  ring: '#1F6FEB'
  primary: '#1F6FEB'            # confident trust-blue — primary actions, active nav, links
  primary-foreground: '#FFFFFF'
  primary-hover: '#1A5FCC'
  # Status palette — each status reads instantly and is reused everywhere a Status appears.
  status-pending: '#8A94A6'        # gray-blue — awaiting attendee action
  status-pending-bg: '#EEF1F5'
  status-review: '#B7791F'         # amber — awaiting organizer
  status-review-bg: '#FCF3E3'
  status-confirmed: '#1E8E5A'      # green — paid & in
  status-confirmed-bg: '#E4F4EC'
  status-rejected: '#C0392B'       # red — action needed
  status-rejected-bg: '#FBE9E7'
  status-waitlisted: '#5B6675'     # neutral — seats full
  status-waitlisted-bg: '#EEF1F5'
  status-exempt: '#6B46C1'         # purple — VIP/free, confirmed without payment
  status-exempt-bg: '#EEE7FB'
  status-cancelled: '#9AA3B2'      # faded gray — terminal
  status-cancelled-bg: '#F1F3F6'
  destructive: '#C0392B'
  destructive-foreground: '#FFFFFF'
  success: '#1E8E5A'
  warning: '#B7791F'
  # Money emphasis — the amount the organizer verifies against proof. Match = neutral; mismatch = warning.
  amount-foreground: '#1A2330'
  amount-match: '#1E8E5A'
  amount-mismatch: '#B7791F'
  # Payment-method identity accents (FR-1b). Used ONLY as a small method dot/icon tint so the
  # organizer recognizes the rail at a glance in the queue — never as surface or status color.
  method-vodafone: '#E60000'      # Vodafone Cash red
  method-instapay: '#5C2D91'      # InstaPay purple
  method-bank: '#2B5797'          # bank transfer blue-gray
  method-cash: '#1E8E5A'          # cash green
  method-other: '#5B6675'         # other manual — neutral
typography:
  # Bilingual ramp: Latin + Arabic faces. Body face must carry Arabic glyphs cleanly.
  font-family-base: "'Inter', 'IBM Plex Sans Arabic', system-ui, sans-serif"
  font-family-arabic: "'IBM Plex Sans Arabic', 'Cairo', sans-serif"
  display:
    fontSize: '28px'
    fontWeight: '700'
    lineHeight: '1.2'
  heading:
    fontSize: '20px'
    fontWeight: '600'
    lineHeight: '1.3'
  subheading:
    fontSize: '16px'
    fontWeight: '600'
    lineHeight: '1.4'
  body:
    fontSize: '15px'
    fontWeight: '400'
    lineHeight: '1.55'
  label:
    fontSize: '13px'
    fontWeight: '500'
    lineHeight: '1.4'
  caption:
    fontSize: '12px'
    fontWeight: '400'
    lineHeight: '1.4'
  mono:
    fontFamily: "'JetBrains Mono', ui-monospace, monospace"
    fontSize: '13px'
    # Used for Transaction Reference — must be unambiguous to read/compare.
rounded:
  sm: '6px'
  md: '10px'
  lg: '14px'
  pill: '999px'
spacing:
  # 4px base scale.
  xs: '4px'
  sm: '8px'
  md: '16px'
  lg: '24px'
  xl: '32px'
  2xl: '48px'
components:
  button-primary:
    background: '{colors.primary}'
    foreground: '{colors.primary-foreground}'
    radius: '{rounded.md}'
    hover: '{colors.primary-hover}'
  button-secondary:
    background: '{colors.surface}'
    foreground: '{colors.foreground}'
    border: '{colors.border}'
    radius: '{rounded.md}'
  button-destructive:
    background: '{colors.destructive}'
    foreground: '{colors.destructive-foreground}'
    radius: '{rounded.md}'
  status-badge:
    radius: '{rounded.pill}'
    # background/foreground bound per status from the status-* tokens above.
  review-card:
    background: '{colors.surface}'
    border: '{colors.border}'
    radius: '{rounded.lg}'
    shadow: '0 1px 2px rgba(26,35,48,0.06)'
  card:
    background: '{colors.surface}'
    border: '{colors.border}'
    radius: '{rounded.lg}'
  input:
    background: '{colors.input}'
    border: '{colors.border}'
    radius: '{rounded.md}'
    focusRing: '{colors.ring}'
  amount-pair:
    # "expected vs. declared" — the money the organizer checks against the screenshot.
    foreground: '{colors.amount-foreground}'
    match: '{colors.amount-match}'
    mismatch: '{colors.amount-mismatch}'
    font: '{typography.mono}'      # amounts in mono too — align decimals, compare fast
  method-dot:
    radius: '{rounded.pill}'
    # tint bound per method from method-* tokens; size ~8px, paired with the method label
  event-link-reward:
    # The gated Event Link, revealed only on CONFIRMED/EXEMPT (FR-8). Visually a "reward."
    background: '{colors.status-confirmed-bg}'
    foreground: '{colors.status-confirmed}'
    border: '{colors.status-confirmed}'
    radius: '{rounded.lg}'
  internal-note:
    # Organizer-only note (FR-3b), e.g. "Cash received at center". Never shown to attendee.
    background: '{colors.muted}'
    foreground: '{colors.muted-foreground}'
    radius: '{rounded.sm}'
---

## Brand & Style

The Event Management Platform is a **trust instrument**: it tells a trainer who has paid and tells an attendee whether they're in. The brand expression is therefore *calm, legible, and finance-grade* — the visual equivalent of a clean bank statement, not a marketing site. Confidence comes from clarity, not decoration: one trust-blue brand color, a disciplined status palette that reads at a glance, generous whitespace, and zero ornamental flourish. When money is involved, restraint signals competence.

Two audiences, one identity. The **organizer dashboard** is dense, scannable, desktop-first — built for working a review queue fast. The **attendee surface** is calm, mobile-first, reassuring — built for one person who just wants to know "am I in?" Same tokens, different density. The product is **bilingual Arabic + English with full RTL**; every layout, icon direction, and alignment must mirror correctly.

## Colors

- **Trust Blue (`#1F6FEB`)** — the single brand color. Primary buttons, active nav, links, focus rings, the "selected" state. Used for action and identity, never for status.
- **Status palette** — seven statuses, each with a foreground + soft background pair, reused *everywhere* a Status appears (badge, status page, queue row, audit log) so a color always means the same thing:
  - **Pending** gray-blue — awaiting the attendee.
  - **Under review** amber — awaiting the organizer.
  - **Confirmed** green — paid and in.
  - **Rejected** red — action needed.
  - **Waitlisted** neutral gray — seats full.
  - **Exempt** purple — VIP/free, confirmed without payment.
  - **Cancelled** faded gray — terminal, de-emphasized.
- **Neutrals** — cool grays on a near-white `#F7F8FA` background with white surfaces. The dashboard lives in neutrals so the status colors carry all the signal.
- **Payment-method accents** — each manual method (FR-1b) has a recognizable brand tint (Vodafone Cash red, InstaPay purple, bank blue-gray, cash green, other neutral). These appear **only** as a small method dot/icon beside the method label, so an organizer scanning the queue recognizes the rail instantly. They are never surface, status, or chrome colors — they live at dot-scale only.
- **Amount emphasis** — the verified money (expected vs. declared) reads in mono and turns neutral when amounts match, warning-amber when they don't (FR-6 amount-mismatch flag). This is the one number the organizer checks against the screenshot, so it earns its own treatment.

Avoid: using the brand blue for any status; multiple accent colors in chrome; gradients; colored surfaces. Status color is sacred — never reuse a status hue for a non-status purpose. Method accents never leave dot-scale. Dark theme is deferred to v2.

## Typography

Bilingual ramp. Latin text in **Inter**; Arabic in **IBM Plex Sans Arabic** (Cairo fallback) — both carried by the base family so a single label can mix scripts cleanly. The **Transaction Reference** renders in **JetBrains Mono** so digits and letters are unambiguous to read and compare against a bank statement — this is the one place monospace is mandatory.

Roles: `display` (28/700) for page titles and the attendee status verdict ("You're in!"); `heading` (20/600) section titles; `subheading` (16/600) card titles; `body` (15/400) default; `label` (13/500) form labels and table headers; `caption` (12/400) timestamps and helper text.

## Layout & Spacing

4px base scale (`xs 4 → 2xl 48`). The dashboard uses a persistent left nav (desktop) that collapses to a top bar + drawer on mobile. Content max-width ~1200px for dashboard tables; the attendee surface is a single centered column, max-width ~520px, comfortable on a phone. **RTL:** all horizontal spacing, nav position, and alignment mirror; use logical properties (`margin-inline-start`, not `margin-left`) throughout.

## Elevation & Depth

Mostly flat. One soft shadow (`0 1px 2px rgba(26,35,48,0.06)`) lifts cards and review-queue items off the background; a slightly stronger shadow for modals/drawers. No heavy drop shadows, no neumorphism. Depth communicates "this is an interactive surface," nothing more.

## Shapes

Rounded but not playful: `sm 6` inputs/badges-inline, `md 10` buttons/inputs, `lg 14` cards and review cards, `pill` for status badges. Status badges are always pills so they're instantly recognizable as status, distinct from buttons.

## Components

- **Status badge** — pill, status-color background + foreground pair, optional small dot. The single most repeated component; identical rendering everywhere a Status shows.
- **Review card** — the hero component (organizer). White `lg`-radius card, soft shadow, holds registrant + payer + amount + reference (mono) + screenshot thumbnail + flags + action row. Dense but breathable.
- **Buttons** — primary (blue), secondary (outline), destructive (red, for Cancel/Reject confirmation). Action verbs only.
- **Auto-flag chip** — small amber/red inline chip (warning vs. error tone) sitting on the review card; advisory, never blocks.
- **Payment-method card** — attendee-facing, shows the method's instructions + destination (number/handle/account) with a copy button. Carries the method's identity dot ({components.method-dot}).
- **Amount pair** ({components.amount-pair}) — "expected vs. declared," both in mono so decimals align; neutral when equal, amber when mismatched. The number the organizer verifies against the screenshot.
- **Method dot** ({components.method-dot}) — ~8px pill tinted per payment rail, paired with the method label in the queue and on the payment-method card. Brand recognition at a glance; never grows beyond dot-scale.
- **Event-link reward** ({components.event-link-reward}) — the gated Event Link, shown only on CONFIRMED/EXEMPT (FR-8). Styled as a soft-green reward block on the attendee Status Page and confirmation email — the visual payoff of being "in," distinct from a plain link.
- **Internal note** ({components.internal-note}) — organizer-only muted block (FR-3b), e.g. "Cash received at center." Visually quiet; clearly internal; never rendered on the attendee surface.
- **Empty / error / success blocks** — centered, one display line + one body line + at most one action. Consistent across surfaces. The "queue clear" empty state is success-toned (green check), not a sad empty state — for the organizer, an empty queue is the win.

## Do's and Don'ts

| Do | Don't |
|---|---|
| Reuse the exact status color everywhere a Status appears | Invent a new color for a status in one view |
| Render Transaction Reference in mono | Render reference in body font (hard to compare) |
| Use trust-blue only for action/identity | Use blue for a status or decoration |
| Mirror every layout for RTL with logical properties | Hardcode left/right margins |
| Keep the attendee surface calm and single-column | Port the dense dashboard layout to the attendee phone view |
| Let whitespace and status color carry the signal | Add gradients, ornament, or chrome color |
| Keep method accents at dot-scale next to the label | Tint a whole row/card with a method's brand color |
| Render expected & declared amounts in mono, aligned | Bury the amount in body text where mismatches hide |
| Treat the Event Link as a green "reward" only when earned | Show a plain link, or reveal it in any non-confirmed state |
| Make the cleared review queue a green success moment | Show the organizer a sad/empty placeholder when the queue is done |
