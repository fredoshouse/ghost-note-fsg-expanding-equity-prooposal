# Ghost Note × FSG — Expanding Equity

Proposal site for the Welcome Back & Welcome campaign. Built on the Beaverton
proposal template — CSS, JS, nav, gate, section toggles, phase accordions, bio
modal, gantt, and footer carried over unchanged. Only content and a small set of
additive classes differ.

**Access code:** `fsg2026`

## Deploy

    npx vercel --prod

Or drag this folder into the Vercel dashboard. Static, no build step, no framework.

## Files

| File | What it is |
|---|---|
| `index.html` | The entire proposal. Single file. |
| `vercel.json` | Noindex headers, clean URLs, no-referrer. |
| `robots.txt` | Belt and braces on indexing. |
| `README.md` | This. |

## Structure

Twelve sections, all collapsed by default so the page reads as a scannable
outline until she opens what she wants.

1. **Who We Are** — agency framing, capability lists
2. **Point of View** — the ghost note idea, the resonance argument
3. **The Opportunity** — the 3,300-dot member field, three tensions, what the project must do
4. **What This Work Is** — lifecycle education, the five stages
5. **One Risk** — deliverability, image-backed dark section
6. **Our Approach** — the four Ghost Note values applied to this brief
7. **Scope & Phases** — three phase accordions
8. **Core Team** — two groups, bio modals
9. **Project Management** — cadence and touchpoints
10. **Timeline** — gantt across Aug–Jan
11. **Investment** — live toggle, phase pricing, minimum-viable vs elevated reasoning
12. **Assumptions** / **Contact**

## Pricing

Phase totals only. No per-component dollar figures.

- Phase 01 Campaign Design — $65,000 – $85,000
- Phase 02 Lifecycle, CRM Architecture & Deployment — $30,000 – $50,000
- Scope B, both phases — $95,000 – $135,000
- Sustained partnership — $8,000 – $12,000 / month

The central argument: at $95,000 the low end of Scope B fits inside the $100,000
FSG already has, so both phases are reachable without reopening the budget. The
"Where The Money Goes" block carries the minimum-viable vs elevated reasoning
qualitatively, without attaching numbers to components.

The toggle in the Investment section switches Phase 02 on and off and updates the
headline range and the note beneath it.

## Images

No standalone image sections. Photography is layered into section headers via
`.hd-media`, which sits in the blank space to the right of the headline on
desktop (≥1081px) and stacks full-width beneath the intro copy on mobile. Because
it lives in the header rather than the collapsible body, it's visible while
scrolling without expanding anything.

- Hero background — `expandingequity.com/.../expanding-equity.jpg`
- The Opportunity header — `wkkf.org/.../signature-efforts-expanding-equity.jpg`
- Risk section background — same WKKF image, scrimmed
- Scope & Phases header — `expandingequity.com/.../Potential-4th-image-EE-1500x843.jpg`
- Team headshots — `ghostnoteagency.com` uploads

All hot-linked with `onerror` fallbacks that remove the container, so a blocked
hot-link degrades cleanly rather than leaving a dead frame. To self-host, save the
files here and switch to relative paths.

## Motion

The page was reading as a wall of text, so there's a light reveal system:

- `.rv` / `.rv.in` — scroll-triggered fade-up on headlines, media, tension blocks,
  pillars, opp rows, team cards, gantt rows, option cards, and table rows, with a
  70ms stagger between siblings
- Hero content animates up on unlock; the hero image settles from a 1.07 scale
- Gantt bars and budget bars wipe in from the left when their row reveals
- Cards lift on hover, the section toggle rotates 90°
- `__rvRescan()` fires when a section expands so newly revealed content animates
  rather than appearing pre-shown
- Everything is disabled under `prefers-reduced-motion`

## Mobile

Audited at 360, 390, 430, and 768px. Zero horizontal overflow, no console errors,
no tap target under 36px at any width.

- The 3,300-dot member field drops to 3px dots below 640px, taking it from ~780px
  tall to ~330px so it reads as one striking block rather than a scroll marathon
- The gantt and the team card rows scroll horizontally, so both carry an animated
  "swipe" hint — without it there was no affordance telling anyone to try
- Section expand buttons invert to a solid fill and grow to 40px
- The pricing switch grows to 66×38, the menu button to 40px min-height, the modal
  close to 44×44, and nav links get 11px of vertical padding
- Layered section images stack full-width beneath the intro copy with the expand
  button pinned top-right

## Hero buttons

- **See the Options** — jumps to Investment
- **Read Proposal** — jumps to Point of View
- **Case Studies** — opens the Pitch capabilities deck in a new tab

## Team

Bios live in the `bios` object near the bottom of `index.html`.

**Delivery Leadership:** Aminata Sow (Strategy Lead), Natalia Arias (Design Lead),
Adam Akisanya (Sr. Program Management Lead), Lifecycle & CRM Architect.

**Leadership:** Alfred Adarkwah (Account Lead), Reggie Snowden (Executive Lead),
Sarah Duarte (Strategy Director), Amiri Rose (Creative Direction).

The Lifecycle & CRM Architect is deliberately an open seat — its bio explains why
rather than using a placeholder name.

Headshots are pulled from ghostnoteagency.com/about. Amiri Rose isn't on the team
page yet, so his uses the supplied benmoon portrait.

Avatars render as an `<img>` layered over the initials rather than a CSS
background. If a URL 404s the image removes itself and the initials show through,
so a bad link can never produce a blank coloured circle. That was the earlier bug:
Aminata's URL was the 800x800 variant, which the site doesn't serve, and Adam had
no photo at all — both produced empty dots because `font-size:0` was hiding the
initials underneath.

## Two fixes applied to the template

Worth patching upstream in the Beaverton master:

1. `.tcard-title` was set to a dark grey on a black card, making every team
   member's title invisible. Overridden here to a light value.
2. `.opp-hl` / `.opp-num` / `.opp-body` are coloured for dark sections only, so
   they render white-on-white in `.sl`, `.sl2`, and `.sw` sections. Scoped
   overrides added.

On mobile (≤960px) the section expand buttons are inverted to a solid fill —
lime on dark sections, near-black on light ones — because the template's default
hairline outline is easy to miss on a phone. Phase accordion arrows get the same
treatment.

Note also that `.sw` is the template's section-white class. Any new component
class must avoid that name — an earlier build collided with it and flattened both
white sections to 28px.
