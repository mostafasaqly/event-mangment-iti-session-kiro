---
name: Event Management Platform
status: final
description: Clean, trustworthy payment-confirmation and attendee-status system for trainers in the Egypt/Arab market. Angular + Angular Material (Material Design 3); brand-layer delta on top of MD3. Bilingual AR/EN, full RTL. Includes a per-screen Screen Catalog ready to drive Google Stitch generation for every page.
sources:
  - "{planning_artifacts}/prds/prd-event-mangment-iti-session-kiro-2026-06-17/prd.md"
  - "{output_folder}/brainstorming/brainstorming-session-2026-06-17-1150.md"
ui_system: "Angular Material — Material Design 3 (m3). Tokens below map to MD3 system tokens; everything unlisted inherits MD3 defaults."
updated: 2026-06-17
colors:
  # Brand-layer overrides on MD3 COLOR ROLES. Generated from a trust-blue source color via
  # Material Theme Builder; only the roles we deliberately set are listed. All other MD3 roles
  # (surface-variant, outline, inverse-*, scrim, surface-container-* tiers) inherit MD3 defaults.
  # --- MD3 brand seed ---
  source-seed: '#1F6FEB'                  # trust-blue seed for the MD3 tonal palette
  # --- Primary role (action & identity) ---
  primary: '#1F6FEB'                      # md.sys.color.primary
  on-primary: '#FFFFFF'                   # md.sys.color.on-primary
  primary-container: '#D7E3FF'            # md.sys.color.primary-container
  on-primary-container: '#001B3E'         # md.sys.color.on-primary-container
  # --- Secondary / tertiary kept quiet (finance-grade restraint) ---
  secondary: '#565F71'                    # md.sys.color.secondary — muted slate
  tertiary: '#6B46C1'                     # md.sys.color.tertiary — reserved (aligns w/ exempt purple)
  # --- Surfaces & neutrals ---
  background: '#F7F8FA'                    # md.sys.color.background
  surface: '#FFFFFF'                       # md.sys.color.surface
  surface-container: '#EEF1F5'             # md.sys.color.surface-container — cards/queue rows
  on-surface: '#1A2330'                    # md.sys.color.on-surface
  on-surface-variant: '#5B6675'            # md.sys.color.on-surface-variant — secondary text
  outline: '#C4C9D2'                       # md.sys.color.outline — borders/dividers
  outline-variant: '#E2E6EC'               # md.sys.color.outline-variant — subtle dividers
  # --- Error role (MD3) reused for destructive + rejected ---
  error: '#C0392B'                         # md.sys.color.error
  on-error: '#FFFFFF'                      # md.sys.color.on-error
  error-container: '#FBE9E7'               # md.sys.color.error-container
  on-error-container: '#410E0B'            # md.sys.color.on-error-container
  # --- CUSTOM MD3 COLOR GROUPS (Theme Builder "custom colors") — the 7-status system. ---
  # Each is a custom color group with color/on-color/container/on-container, used as a
  # status badge (container + on-container) everywhere a Status appears. Status colors are
  # SEMANTIC and never reused for chrome or action.
  status-pending: '#5B6675'                # gray-blue — awaiting attendee
  status-pending-container: '#EEF1F5'
  status-review: '#B7791F'                 # amber — awaiting organizer
  status-review-container: '#FCF3E3'
  status-confirmed: '#1E8E5A'              # green — paid & in
  status-confirmed-container: '#E4F4EC'
  status-rejected: '#C0392B'               # red — action needed (shares MD3 error)
  status-rejected-container: '#FBE9E7'
  status-waitlisted: '#5B6675'             # neutral — seats full
  status-waitlisted-container: '#EEF1F5'
  status-exempt: '#6B46C1'                 # purple — VIP/free (aligns w/ MD3 tertiary)
  status-exempt-container: '#EEE7FB'
  status-cancelled: '#9AA3B2'              # faded gray — terminal
  status-cancelled-container: '#F1F3F6'
  # --- Money emphasis (custom) — amount the organizer verifies against proof ---
  amount-match: '#1E8E5A'
  amount-mismatch: '#B7791F'
  # --- Payment-method identity accents (FR-1b) — dot-scale only, never surface/status ---
  method-vodafone: '#E60000'               # Vodafone Cash red
  method-instapay: '#5C2D91'               # InstaPay purple
  method-bank: '#2B5797'                   # bank transfer blue-gray
  method-cash: '#1E8E5A'                   # cash green
  method-other: '#5B6675'                  # other manual — neutral
typography:
  # MD3 TYPE SCALE roles. Brand sets the two type families; sizes follow the MD3 scale
  # (with minor brand tightening on display). Bilingual: Latin + Arabic faces.
  brand-font: "'Inter', 'IBM Plex Sans Arabic', system-ui, sans-serif"   # md.sys.typescale plain/brand
  arabic-font: "'IBM Plex Sans Arabic', 'Cairo', sans-serif"
  display-small:                          # md.sys.typescale.display-small
    fontSize: '28px'
    fontWeight: '700'
    lineHeight: '1.2'
  headline-small:                         # md.sys.typescale.headline-small
    fontSize: '20px'
    fontWeight: '600'
    lineHeight: '1.3'
  title-medium:                           # md.sys.typescale.title-medium
    fontSize: '16px'
    fontWeight: '600'
    lineHeight: '1.4'
  body-medium:                            # md.sys.typescale.body-medium — default body
    fontSize: '15px'
    fontWeight: '400'
    lineHeight: '1.55'
  label-medium:                           # md.sys.typescale.label-medium — form labels / table headers
    fontSize: '13px'
    fontWeight: '500'
    lineHeight: '1.4'
  label-small:                            # md.sys.typescale.label-small — timestamps / helper
    fontSize: '12px'
    fontWeight: '400'
    lineHeight: '1.4'
  mono:                                    # custom role — Transaction Reference & amounts
    fontFamily: "'Roboto Mono', ui-monospace, monospace"
    fontSize: '14px'
shape:
  # MD3 SHAPE SCALE (corner radius). Brand sits slightly tighter than MD3 defaults for a
  # crisper, finance-grade read; status badges use the MD3 "full" token.
  corner-extra-small: '6px'               # md.sys.shape.corner.extra-small — inputs/chips
  corner-small: '8px'                     # md.sys.shape.corner.small
  corner-medium: '10px'                   # md.sys.shape.corner.medium — buttons
  corner-large: '14px'                    # md.sys.shape.corner.large — cards / review cards
  corner-full: '999px'                    # md.sys.shape.corner.full — status badge / chip pills
spacing:
  # MD3 spacing aligns to a 4dp grid; tokens named for our use.
  xs: '4px'
  sm: '8px'
  md: '16px'
  lg: '24px'
  xl: '32px'
  2xl: '48px'
elevation:
  # MD3 ELEVATION LEVELS (dp → tonal+shadow). We use a restrained subset.
  level0: '0dp'                           # background, flat fields
  level1: '1dp'                           # cards, review-queue items (resting)
  level2: '3dp'                           # raised buttons / hovered card
  level3: '6dp'                           # menus, FAB
  level4: '8dp'                           # navigation drawer
  level5: '24dp'                          # dialogs / bottom sheets
components:
  # Each maps to an Angular Material component; we set only the brand delta.
  m-button-filled:                        # <button mat-flat-button color="primary">
    role: '{colors.primary}'
    on: '{colors.on-primary}'
    shape: '{shape.corner-medium}'
  m-button-outlined:                      # <button mat-stroked-button>
    outline: '{colors.outline}'
    on: '{colors.on-surface}'
    shape: '{shape.corner-medium}'
  m-button-error:                         # destructive (Reject/Cancel confirm)
    role: '{colors.error}'
    on: '{colors.on-error}'
    shape: '{shape.corner-medium}'
  m-chip-status:                          # <mat-chip> as status badge — pill, per-status group
    shape: '{shape.corner-full}'
    # container + on-container bound per status from status-*-container / status-* tokens
  m-chip-flag:                            # <mat-chip> auto-flag — amber (warning) / error (red)
    shape: '{shape.corner-full}'
  m-card-review:                          # <mat-card> — the organizer hero component
    surface: '{colors.surface}'
    outline: '{colors.outline-variant}'
    shape: '{shape.corner-large}'
    elevation: '{elevation.level1}'
  m-card:                                 # <mat-card> generic
    surface: '{colors.surface}'
    shape: '{shape.corner-large}'
    elevation: '{elevation.level1}'
  m-form-field:                           # <mat-form-field appearance="outline">
    outline: '{colors.outline}'
    shape: '{shape.corner-extra-small}'
    focus: '{colors.primary}'
  amount-pair:                            # custom — expected vs. declared
    font: '{typography.mono}'
    match: '{colors.amount-match}'
    mismatch: '{colors.amount-mismatch}'
  method-dot:                             # custom — ~8px tinted pill beside method label
    shape: '{shape.corner-full}'
  event-link-reward:                      # custom — gated link as MD3 tonal "success" surface
    surface: '{colors.status-confirmed-container}'
    on: '{colors.status-confirmed}'
    shape: '{shape.corner-large}'
    elevation: '{elevation.level1}'
  internal-note:                          # custom — organizer-only muted block (FR-3b)
    surface: '{colors.surface-container}'
    on: '{colors.on-surface-variant}'
    shape: '{shape.corner-small}'
---

## Brand & Style

The Event Management Platform is a **trust instrument**: it tells a trainer who has paid and tells an attendee whether they're in. The brand expression is *calm, legible, and finance-grade* — the visual equivalent of a clean bank statement. Confidence comes from clarity, not decoration: one trust-blue brand color, a disciplined status palette that reads at a glance, generous whitespace, and zero ornamental flourish. When money is involved, restraint signals competence.

**Built on Angular Material (Material Design 3).** This DESIGN.md specifies only the **brand-layer delta** on top of MD3 — a trust-blue seed color run through the MD3 tonal system, the seven-status custom color groups, a couple of custom roles (mono, money, method dots), and slightly tighter corners. Everything else inherits MD3: the elevation system, ripple/state-layer interactions, the component anatomy of `mat-card`, `mat-chip`, `mat-form-field`, `mat-table`, `mat-button`, and the accessibility defaults. Customizing MD3's interaction patterns, touch targets, or component internals is **against** the brand discipline — MD3's defaults are the contract; we change color, type family, shape scale, and a small set of semantic custom tokens, nothing more.

Two audiences, one MD3 theme. The **organizer dashboard** is dense, scannable, desktop-first — built to work a review queue fast. The **attendee surface** is calm, mobile-first, reassuring — built for one person who just wants to know "am I in?" Same tokens, different density. **Bilingual Arabic + English with full RTL** via Angular's built-in `dir="rtl"` and CDK BidiModule; every layout mirrors.

## Colors

Generated from the trust-blue seed (`#1F6FEB`) using **Material Theme Builder**, then narrowed to the roles we deliberately set.

- **Primary role (`#1F6FEB`)** — the single brand color, on MD3's `primary` / `primary-container`. Filled buttons, active nav, links, selected states, focus. Action and identity only — never a status.
- **Secondary / tertiary** — kept quiet. `secondary` is a muted slate; `tertiary` reserves the exempt purple. We do not introduce extra accent hues in chrome.
- **Surfaces & neutrals** — MD3 surface tiers on a near-white `#F7F8FA` background; `surface-container` carries cards and queue rows. The dashboard lives in neutrals so status color carries all the signal.
- **Error role** — MD3 `error` does double duty for destructive actions and the Rejected status.
- **Seven status custom color groups** — each status is an MD3 *custom color* (color + container + on-container), rendered as a `mat-chip` status badge **identically everywhere** a Status appears (badge, status page, queue row, audit log) so a color always means one thing: Pending gray-blue, Under-review amber, Confirmed green, Rejected red, Waitlisted neutral, Exempt purple, Cancelled faded gray.
- **Payment-method accents** — each manual method (FR-1b) has a recognizable brand tint (Vodafone Cash red, InstaPay purple, bank blue-gray, cash green, other neutral). Used **only** as an ~8px method dot beside the label so an organizer recognizes the rail at a glance — never surface, status, or chrome color.
- **Amount emphasis** — expected-vs-declared reads in mono, neutral when equal, amber when mismatched (FR-6). The one number checked against the screenshot.

Avoid: using the primary for any status; adding accent hues to chrome; gradients; tinting surfaces with method colors. Status color is semantic and sacred. Dark theme is deferred to v2 (MD3 generates it from the same seed when we turn it on).

## Typography

MD3 **type scale**, brand sets the families. Latin in **Inter**, Arabic in **IBM Plex Sans Arabic** (Cairo fallback), both on the MD3 plain/brand font roles so a single label can mix scripts. The **Transaction Reference** and **amounts** render in **Roboto Mono** (a custom role) — digits and letters unambiguous to read and compare against a bank statement; this is the one place mono is mandatory.

Roles used: `display-small` (28/700) page titles and the attendee verdict ("You're in!"); `headline-small` (20/600) section titles; `title-medium` (16/600) card titles; `body-medium` (15/400) default; `label-medium` (13/500) form labels and table headers; `label-small` (12/400) timestamps and helper text. Other MD3 type roles inherit defaults.

## Layout & Spacing

MD3 4dp spacing grid (`xs 4 → 2xl 48`). The dashboard uses a persistent `mat-sidenav` (desktop) collapsing to a top `mat-toolbar` + drawer on mobile, on MD3's Compact/Medium/Expanded breakpoints. Dashboard tables (`mat-table`) max-width ~1200px; the attendee surface is a single centered column, max-width ~520px. **RTL** via `dir="rtl"` + CDK `BidiModule`; use logical properties (`margin-inline-start`) and let Material's RTL-aware components mirror.

## Elevation & Depth

MD3 **elevation levels**, used sparingly. `level1` (1dp) for resting cards and review-queue items; `level2` on hover/raised buttons; `level3` menus/FAB; `level4` the nav drawer; `level5` (24dp) dialogs and bottom sheets. Let MD3's tonal-elevation + shadow do the work; no custom heavy shadows, no neumorphism. Depth means "interactive surface," nothing more.

## Shapes

MD3 **shape scale**, tightened one notch for a crisper read: `extra-small 6` inputs/chips, `small 8`, `medium 10` buttons, `large 14` cards and review cards, `full` for status/flag chips. Status badges are always `corner-full` pills so they're instantly recognizable as status, distinct from buttons.

## Components

Each maps to an Angular Material component; we set only the brand delta. Behavioral specs live in `EXPERIENCE.md`.

- **Status badge** — `mat-chip` bound to a status custom-color group (container + on-container). The most repeated component; identical everywhere a Status shows. Color is always paired with a text label (never color-alone).
- **Review card** — `mat-card` at `level1`, `corner-large` — the organizer hero. Holds registrant + payer + amount-pair + reference (mono) + screenshot thumbnail + flag chips + action row. Dense but breathable.
- **Buttons** — MD3 variants: `mat-flat-button color="primary"` (filled, primary action), `mat-stroked-button` (secondary), error-toned filled for destructive Reject/Cancel confirmation. Action verbs only.
- **Auto-flag chip** — `mat-chip` in warning (amber) or error (red) tone on the review card; advisory, never blocks (FR-6).
- **Payment-method card** — attendee-facing `mat-card`; method instructions + destination (number/handle/account) with a copy button; carries the method dot.
- **Amount pair** — custom; expected vs. declared in mono, aligned decimals, neutral on match / amber on mismatch.
- **Method dot** — ~8px `corner-full` pill tinted per rail, beside the method label; brand recognition at a glance, never beyond dot-scale.
- **Event-link reward** — the gated Event Link (FR-8), shown only on CONFIRMED/EXEMPT, styled as an MD3 tonal success surface (`status-confirmed-container`) — the visual payoff of being "in," not a plain link.
- **Internal note** — organizer-only muted block (FR-3b), e.g. "Cash received at center"; `surface-container`, quiet, never on the attendee surface.
- **Empty / error / success blocks** — centered, one display line + one body line + ≤1 action. The cleared review queue is a green success moment, not a sad empty state — for the organizer, an empty queue is the win.

## Do's and Don'ts

| Do | Don't |
|---|---|
| Inherit MD3 component anatomy, ripple, and a11y defaults | Re-skin `mat-*` internals or replace MD3 interaction patterns |
| Set brand only via color roles, type family, shape, custom tokens | Hand-build components MD3 already provides |
| Render each status as a `mat-chip` from its custom color group | Invent a new color for a status in one view |
| Render Transaction Reference and amounts in mono | Render them in body font (mismatches hide) |
| Use the primary role only for action/identity | Use primary for a status or decoration |
| Use `dir="rtl"` + CDK Bidi + logical properties | Hardcode left/right margins |
| Keep method accents at dot-scale next to the label | Tint a whole row/card with a method's brand color |
| Treat the Event Link as an earned green reward | Show a plain link, or reveal it in any non-confirmed state |
| Make the cleared review queue a green success moment | Show a sad/empty placeholder when the queue is done |
| Pair every status color with a text label | Rely on status color alone |

## Screen Catalog (for Google Stitch generation)

Every page to generate, with its purpose, MD3 layout, key components, and the states to produce. Apply the brand spec above to all of them: trust-blue `primary`, the seven-status `mat-chip` system, mono for references/amounts, MD3 elevation, tightened shape scale, and **bilingual AR/EN with full RTL** (generate an Arabic RTL variant of each screen, or note RTL mirroring). Two surfaces: **Organizer** (desktop-first, `mat-sidenav` shell) and **Attendee** (mobile-first, single ~520px column, no nav chrome).

### Global shells
- **Organizer shell** — `mat-toolbar` top bar (app name, language toggle EN/ع, organizer avatar menu) + persistent left `mat-sidenav` (Events, current-event sub-nav: Dashboard · Review Queue [badge count] · Registrations · Settings). Collapses to a drawer below the Medium breakpoint. Content area on `background`.
- **Attendee shell** — no nav. Centered column on `background`, a slim header (event name + language toggle), generous vertical rhythm. Phone-first.

### Organizer screens (desktop-first)

| # | Screen | Purpose | MD3 layout & key components | States to generate |
|---|---|---|---|---|
| O1 | **Login** | Email + password sign-in (FR-15) | Centered `mat-card`, two `mat-form-field` (outline), filled primary button, language toggle | default · error ("Email or password is incorrect") · loading |
| O2 | **Events list** | All the organizer's events with at-a-glance counts | `mat-toolbar` + grid/list of event `mat-card`s, each with title, type chip, date, and count chips (confirmed/pending/waitlisted), "+ New Event" FAB | populated · **empty** ("No events yet…" + primary) · loading skeleton |
| O3 | **Create / Edit Event** | Event details + capacity + price + Event Link + payment methods (FR-1, FR-1b) | Form on `mat-card`: type `mat-select`, title/description, date/time pickers, capacity, price, event-link field; **repeatable Payment-Method rows** (method `mat-select` + instructions + destination, each with its method dot) + "Add method" | create (empty) · edit (filled) · validation error |
| O4 | **Event dashboard** | One event's home: summary + entry points | Summary count cards (confirmed/pending/under-review/waitlisted as status-colored stat cards), quick-link buttons to Review Queue & Registrations | populated · early (mostly zeros) |
| O5 | **Review Queue** ★hero | Work `UNDER_REVIEW` payments fast (FR-5, FR-6) | Stack/grid of **review `mat-card`s**: registrant + contact, payer-name (both shown if different), **amount-pair** (expected vs declared, mono), **reference** (mono), screenshot thumbnail, **auto-flag chips** (amber/red), action row (Approve / Reject / Waitlist / Exempt / Cancel) | queue with items · card with amber **amount-mismatch** flag · card with red **duplicate-reference** flag · **group card** ("3 attendees on one payment") · **empty = green "All caught up"** success · loading skeleton |
| O6 | **Reject dialog** | Capture a reason on reject/cancel | MD3 `mat-dialog`: reason `mat-select` (wrong amount / unclear screenshot / no payment found / duplicate) + optional note, error-toned confirm button | default · custom-reason typed |
| O7 | **Registrations table** | The Excel-killer: search/filter/export (FR-12) | `mat-table` columns: name, contact, method (with dot), **status chip**, amount, reference (mono), date; search field, status `mat-chip` filter row, **Export** button | populated · **filtered-to-zero** · **search no-match** · **empty** ("No one's registered yet…" + copy-link) · loading |
| O8 | **Registration detail** | Full record + actions + history (FR-11) | Two-pane on desktop: left = attendee + payment proof (screenshot, amount-pair, reference) + action row; right = **audit-log list** (actor · time · old→new status · reason) + **internal-note** block (FR-3b) | confirmed · rejected (reason shown) · waitlisted · exempt · cancelled · **cash** (mark-confirmed + add internal note) |
| O9 | **Settings** | Account, language, message templates | `mat-card` sections: account, default language, editable **email & WhatsApp templates** | default |

### Attendee screens (mobile-first, no login)

| # | Screen | Purpose | MD3 layout & key components | States to generate |
|---|---|---|---|---|
| A1 | **Registration form** | Register for the event (FR-2) | Single column: event summary card, `mat-form-field`s (name/phone/email + optional), **payment-method `mat-select`** (each option with its method dot), filled primary "Register" | default · validation error · capacity-full notice (will be waitlisted) |
| A2 | **Registration confirmation** | "You're registered — check your email" | Centered success block + direct link to Status Page | default |
| A3 | **Status Page** ★hero | The "Am I confirmed?" killer — one screen, seven states (FR-7, FR-8) | Big `display-small` verdict headline + status chip; content swaps per state | **PENDING (non-cash):** payment-method card (instructions + destination + copy), amount, reference field (mono), screenshot upload, payer-name field, submit · **PENDING (cash):** cash instructions, "spot held" · **UNDER_REVIEW:** "Payment received — reviewing" · **CONFIRMED:** 🎉 + **event-link reward** (green) + add-to-calendar · **EXEMPT:** "confirmed as guest" + link · **REJECTED:** reason + re-opened upload · **WAITLISTED:** "#N on waitlist" · **CANCELLED:** terminal |
| A4 | **Payment submission** | Submit proof from PENDING (FR-3) | Payment-method card (with copy buttons), mono reference input + helper, screenshot uploader (thumbnail/replace), payer-name-if-different, submit | empty · filled · upload error · submitting |

### Cross-cutting states to render for every screen
Generate, where applicable: **empty**, **loading** (MD3 skeleton/progress), **error** (calm inline copy), **success** (toast/`mat-snack-bar` confirmation), and the **Arabic RTL** mirror. Status colors, mono treatment, and the gated event-link rule are invariant across all of them.
