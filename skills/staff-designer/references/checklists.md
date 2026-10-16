# Interface Checklists

Consolidated quality checks. Apply them to the artifact, platform and task. Aesthetic patterns are prompts to inspect the product's intent and user impact, rather than universal requirements. Concrete correctness and applicable accessibility failures still need findings.

Severity: 🔴 Blocker | 🟡 Warning | 🟢 Suggestion

---

## Visual Coherence

The interface as a composition, not a collection of items.

### Color

- 🟡 **Intentional color palette** — Not random hex values; colors belong to a family
- 🟡 **Color reinforces hierarchy** — Check whether action, status and decoration have clear roles and appropriate visual weight
- 🟢 **Color meanings are legible** — Flag ambiguous meanings that mislead, rather than any reuse of a hue

### Depth

- 🟡 **Intentional depth** — Borders, shadows and surface tints communicate coherent grouping and layering
- 🟡 **Elevation communicates hierarchy** — Modal > card > base surface
- 🟢 **Intentional and consistent border radius** — border radius scale used across the interface

### Type

- 🟡 **Type scale with clear levels** — Each size visibly distinct from neighbors
- 🟡 **One hero size** — Single largest size establishes importance
- 🟡 **Sizes don't compete** — No two sizes so close they're indistinguishable
- 🟢 **Weight matches importance** — Boldest text is most important content

### Weight Distribution

- 🟡 **Visual weight matches semantic importance** — Heaviest elements are the most important
- 🟡 **Decoration doesn't compete with action** — Primary CTA is visually dominant
- 🟢 **Clear focal point** — One obvious entry point, not everything competing

---

## States

If it fetches data or takes action, it needs states.

### Data States

- 🔴 **Loading state exists** — Structural skeletons, not spinners in empty space
- 🔴 **Empty state exists** — Not blank; one clear action to fix it
- 🔴 **Error state exists** — Displayed adjacent to triggering action, not just console
- 🟡 **Success feedback** — User knows the action worked

### Interaction States

- 🔴 **All five states defined** — default, hover, active, focus, disabled
- 🟡 **Hover doesn't shift layout** — No size/position changes on hover
- 🟡 **Disabled has explanation** — Why can't I click this?
- 🟢 **Focus visible without mouse** — Tab through the UI, focus always apparent

---

## Accessibility

### Critical

- 🔴 **Accessible names** — All controls labeled; icon buttons have `aria-label`
- 🔴 **Keyboard accessible** — Every interactive element reachable via Tab
- 🔴 **No div/span buttons** — Use `<button>` or accessible primitives
- 🔴 **Focus trapped in modals** — Can't Tab outside open dialogs
- 🔴 **Escape closes dialogs** — Standard expectation
- 🔴 **Focus restored on close** — Returns to trigger element

### High Priority

- 🟡 **Semantic HTML** — Proper heading levels, lists, landmarks
- 🟡 **Form errors linked** — `aria-describedby` connects error to input
- 🟡 **Required fields announced** — Screen readers know what's required
- 🟡 **Color contrast 4.5:1** — Normal text minimum; 3:1 for large text

### Medium Priority

- 🟡 **Live regions for errors** — `aria-live` for critical errors
- 🟡 **Loading announced** — `aria-busy` on loading containers
- 🟢 **Alt text accurate** — Describes content, not "image of..."
- 🟢 **Decorative images hidden** — `aria-hidden` or empty alt

---

## Hierarchy & Typography

### Typography

- 🟡 **Intentional type scale used** — primary, secondary, tertiary, muted
- 🟡 **Headings use `text-balance`** — Prevents orphans
- 🟡 **Body uses `text-pretty`** — Better line breaks
- 🟡 **Data uses `tabular-nums`** — Numbers align in columns
- 🟢 **Line length 65-75 chars** — Optimal readability
- 🟢 **Line height 1.5-1.75** — Body text breathes

### Text Hierarchy

Use the hierarchy levels the content needs. These are possible roles, not a mandatory count:

| Level     | Role                 | Example Use                |
| --------- | -------------------- | -------------------------- |
| Primary   | Default text         | Body copy, main content    |
| Secondary | Supporting text      | Descriptions, help text    |
| Tertiary  | Metadata             | Timestamps, counts, labels |
| Muted     | Disabled/placeholder | Inactive states, hints     |

- 🟡 **Useful text hierarchy** — Important content and supporting detail are distinguishable; the number of levels fits the task
- 🟡 **Levels used consistently** — Same level = same meaning throughout
- 🟡 **Hierarchy visible without color** — Weight and size create hierarchy, not just color

### Visual Hierarchy

- 🟡 **Clear color priorities** — Multiple accents can work when their roles and relative emphasis are clear
- 🟡 **Surfaces support meaning** — Structural and expressive colors support the intended hierarchy
- 🟡 **Squint test passes** — Blur vision; hierarchy still perceivable
- 🟢 **Headlines have presence** — Weight + tight tracking

### Layering & Depth

**Choose treatments that explain the hierarchy. These approaches may be combined for distinct roles:**

| Strategy             | Feel                 | When to Use                        |
| -------------------- | -------------------- | ---------------------------------- |
| Borders-only         | Clean, technical     | Dense tools, data-heavy interfaces |
| Subtle shadows       | Soft lift            | Approachable products              |
| Layered shadows      | Premium, dimensional | Cards that need presence           |
| Surface color shifts | Background tints     | Hierarchy without shadows          |

- 🟡 **Coherent depth strategy** — Different treatments preserve consistent grouping and layer relationships
- 🟡 **Subtle elevation shifts** — Lightness changes of a few percentage points, not dramatic jumps
- 🟡 **Sidebar relationship is clear** — Shared or distinct surfaces reflect its role relative to the canvas
- 🟡 **Inputs are identifiable** — Styling and labels make editable controls clear in the actual theme
- 🟢 **Dropdowns above parent surface** — One level up in elevation

---

## Layout & Spacing

### Spacing

- 🟡 **Consistent base unit** — 4px or 8px scale throughout
- 🟡 **Spacing test passes** — Inconsistent spacing = no system
- 🟡 **Symmetrical padding default** — Asymmetry only when content requires
- 🟢 **Use `size-*` for squares** — Not `w-*` + `h-*`

### Structure

- 🔴 **`h-dvh` not `h-screen`** — Accounts for mobile browser chrome
- 🔴 **`safe-area-inset` on fixed elements** — Respects notches/home indicators
- 🟡 **Fixed z-index scale** — Documented layers, not arbitrary numbers
- 🟡 **No layout shift on load** — Content stable as assets load
- 🟢 **Sidebar separation is purposeful** — Borders or surface changes explain its relationship to the content

---

## Motion & Animation

### Constraints

- 🔴 **`prefers-reduced-motion` respected** — Check and disable/reduce
- 🔴 **Compositor props only** — `transform`, `opacity`; never animate layout
- 🟡 **Max 200ms for feedback** — Interaction responses feel instant
- 🟡 **150-300ms for transitions** — UI state changes
- 🟡 **Looping animations pause off-screen** — Performance + respect

### Anti-patterns

- 🔴 **No animated layout props** — `width`, `height`, `top`, `left`, margins
- 🟡 **No animation unless requested** — Don't add decoration
- 🟢 **Large surfaces don't animate** — Full-screen, large images excluded

---

## Mobile

Touch targets and mobile-specific patterns. Applies when viewport < 768px or touch device.

- 🔴 **44x44px minimum touch targets** — Buttons, links, interactive elements
- 🔴 **Thumb zone awareness** — Primary actions reachable one-handed
- 🟡 **No hover-only interactions** — Everything works on tap
- 🟡 **Inputs don't zoom on focus** — Font size ≥ 16px
- 🟢 **Bottom sheet over modal on mobile** — Easier to reach/dismiss

---

## Red Flags

Use these as inspection prompts. For visual and craft choices, explain the observed failure of hierarchy, usability, or fit with the approved brief before assigning severity. A style choice alone is not a warning. Keep structural and accessibility defects actionable, with severity based on their impact.

### Visual

- 🟡 Harsh borders demanding attention
- 🟡 Dramatic surface lightness jumps
- 🟡 White cards on colored backgrounds obscure grouping or create distracting contrast
- 🟡 Decorative gradients (unless intentional brand)
- 🟡 Surface colors with unclear roles or competing emphasis
- 🟡 Large radius on small elements
- 🟡 Glow effects as primary affordances
- 🟡 Sidebar treatment obscures grouping or competes with the main task
- 🟢 Emoji instead of consistent icon set

### Structural

- 🔴 Missing interaction states
- 🔴 Missing data states (loading/empty/error)
- 🟡 Depth treatments contradict grouping or layer order
- 🟡 Dramatic drop shadows
- 🟡 Inconsistent spacing
- 🟡 Multiple accent colors competing
- 🟡 Text hierarchy fails to distinguish the roles the content needs

### Craft

- 🟡 Hardcoded hex colors instead of tokens
- 🟡 Font choice impairs legibility, hierarchy, or fit with the approved brief
- 🟡 Arbitrary spacing values with no scale
- 🟡 Missing polish — no hover, focus, or transition states
- 🟢 Token meanings are unclear to the people maintaining the product

---

## AI Anti-Patterns

Common UX issues in AI-generated interfaces.

### The Core Problem

AI generates interfaces that work in the happy path demo. It doesn't design for:

- What happens when things go wrong
- What happens when users make mistakes
- What happens when the network fails
- What happens when users leave and come back

### Detection Checklist

| Anti-Pattern                         | What Users Experience                       | Principle Violated |
| ------------------------------------ | ------------------------------------------- | ------------------ |
| State doesn't survive refresh        | "I refreshed and everything is gone"        | Persistence        |
| Silent failures                      | "I clicked submit and nothing happened"     | Transparency       |
| Buttons that do nothing              | "This button looks active but doesn't work" | Transparency       |
| Double-action risk                   | "I got charged twice"                       | Forgiveness        |
| Permanent actions without safeguards | "I accidentally removed everything"         | Reversibility      |
| Fake success                         | "It said it saved but my changes are gone"  | Transparency       |
| Missing UI states                    | Crash on first load, blank on empty         | Forgiveness        |
| Trapped states                       | "I can't close this popup"                  | Escape             |

Quick checks:

- [ ] State lost on page refresh
- [ ] No feedback when actions fail
- [ ] Buttons that appear active but do nothing
- [ ] No loading or processing indicators
- [ ] Delete actions without confirmation or undo
- [ ] Success shown before server confirmation
- [ ] No empty state when lists have no items
- [ ] No error state when data fails to load
- [ ] Modals with no way to close them

---

## Quality Tests

Manual tests for craft. Run these during review.

### Swap Test

> Would the design feel different if you replaced the typeface or layout with standard alternatives?

If no → you defaulted. 🟡

### Squint Test

> Blur your vision. Is hierarchy still perceivable without harsh jumps?

If no → hierarchy relies on color alone. 🟡

### Signature Test

> Do the choices fit this product's purpose, content and visual language?

Assess observable fit. There is no required number of unique visual elements.

### Spacing Test

> Is spacing consistent throughout? Same gaps for same relationships?

Check whether the different gaps serve different relationships before treating them as inconsistency.

### Token Test

> Do CSS variable names reflect this product's world or generic templates?

Generic names alone do not establish an unexamined design. Inspect their roles and actual use.
