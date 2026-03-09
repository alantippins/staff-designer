---
name: interface-review
description: Quick UX check for PRs — catches interaction safety gaps before they ship.
---

# Interface Review

Terse PR comments. Actionable findings for code review, not teaching.

---

## When to Use

- Reviewing a PR
- CI/automated checks
- When brevity matters

---

## Interaction Principles (Quick Reference)

### Law of Reversibility
**Every action should be undoable or recoverable.**
- Delete has safeguard (confirmation, undo toast, or soft delete)
- Bulk actions protected
- State changes reversible

| Situation | Severity |
|-----------|----------|
| No safeguard at all | 🔴 Blocker |
| Confirmation dialog only (no undo) | 🟡 Warning |

### Law of Forgiveness
**Software should assume human error and prevent harm.**
- Submit disabled during async
- Destructive actions styled distinctly
- Forms preserve on error

### Law of Persistence
**User work should survive navigation, refresh, failure, and closing.**
- Long forms have draft state
- State survives refresh (not just React state)
- Failed submissions preserve input

### Law of Transparency
**System state should be visible and understandable at all times.**
- Actions confirm completion
- Errors explain what to do
- Pending states visible

### Law of Escape
**Users should always have a way out of any state.**
- Modals have escape routes (X, ESC, backdrop)
- Multi-step flows have back/cancel
- Browser back works

### Law of Consistency
**The same action should work the same way everywhere.**
- Platform conventions followed
- Same gesture = same result everywhere
- Consistent terminology

### Law of Craft
**The interface should show intentional design choices, not defaults.**
- Typography intentional
- Color coherent (tokens, not random hex)
- Spacing systematic
- ONE depth strategy (borders OR shadows, not both)

### Law of Recognition
**Show users what they need — don't make them remember.**
- Recent items visible
- Options discoverable
- Search over navigation for large sets

---

## Visual Principles (Quick Reference)

### States

**Data States:**

| Check | Severity |
|-------|----------|
| Loading state exists | 🔴 |
| Empty state exists | 🔴 |
| Error state exists | 🔴 |
| Success feedback | 🟡 |

**Interaction States:**

| Check | Severity |
|-------|----------|
| All five states defined (default, hover, active, focus, disabled) | 🔴 |
| Hover doesn't shift layout | 🟡 |
| Disabled has explanation | 🟡 |
| Focus visible without mouse | 🟢 |

### Accessibility

**Critical (🔴):**
- Accessible names (icon buttons have `aria-label`)
- Keyboard accessible (Tab reaches everything)
- No div/span buttons (use `<button>`)
- Focus trapped in modals
- Escape closes dialogs
- Focus restored on close

**High Priority (🟡):**
- Semantic HTML
- Form errors linked (`aria-describedby`)
- Color contrast 4.5:1
- Live regions for errors

### Typography

| Check | Severity |
|-------|----------|
| Four text levels max (primary, secondary, tertiary, muted) | 🟡 |
| Headings use `text-balance` | 🟡 |
| Body uses `text-pretty` | 🟡 |
| Data uses `tabular-nums` | 🟡 |
| Line length 65-75 chars | 🟢 |
| Line height 1.5-1.75 for body | 🟢 |
| Single accent color per view | 🟡 |

### Layout & Structure

| Check | Severity |
|-------|----------|
| `h-dvh` not `h-screen` | 🔴 |
| `safe-area-inset` on fixed elements | 🔴 |
| Consistent spacing (4px/8px scale) | 🟡 |
| No layout shift on load | 🟡 |

### Motion

| Check | Severity |
|-------|----------|
| `prefers-reduced-motion` respected | 🔴 |
| Compositor props only (`transform`, `opacity`) | 🔴 |
| Max 200ms for feedback | 🟡 |
| No animated layout props | 🔴 |

### Mobile

| Check | Severity |
|-------|----------|
| 44x44px minimum touch targets | 🔴 |
| Thumb zone awareness | 🔴 |
| No hover-only interactions | 🟡 |
| Inputs don't zoom on focus (≥16px) | 🟡 |

### Depth Strategy

Pick ONE and commit:
- Borders-only (clean, technical)
- Subtle shadows (soft lift)
- Layered shadows (premium)
- Surface color shifts (hierarchy without shadows)

**Anti-pattern:** Mixing approaches (borders AND shadows)

### Red Flags

**Visual (🟡):** Harsh borders, dramatic lightness jumps, pure white cards on colored bg, mixed depth strategies

**Structural (🔴/🟡):** Missing interaction states (🔴), missing data states (🔴), inconsistent spacing (🟡)

**Craft (🟡):** Hardcoded hex colors, default fonts, arbitrary spacing values

---

## Output Format

```markdown
## UX Review

### Interaction

⚠️ **Reversibility** — `src/components/ItemCard.tsx:42`
   Delete without undo. Add confirmation or soft delete.

⚠️ **Persistence** — `src/components/Form.tsx:15`
   Form state in useState only. Lost on refresh.

⚠️ **Forgiveness** — `src/components/SubmitButton.tsx:8`
   Button not disabled during async. Double-submit possible.

✓ **Transparency** — Error states show actionable messages
✓ **Escape** — Modal has close button and ESC handler
✓ **Consistency** — Delete behavior matches other screens

### Visual

⚠️ **States** — `src/components/UserList.tsx:23`
   No empty state. Show guidance when list is empty.

⚠️ **Accessibility** — `src/components/IconButton.tsx:5`
   Missing aria-label on icon-only button.

✓ **Motion** — prefers-reduced-motion respected
✓ **Layout** — Consistent spacing throughout

### Craft

⚠️ **Tokens** — `src/components/Card.tsx:12`
   Hardcoded colors (#3b82f6). Use design tokens.

⚠️ **Depth** — `src/components/Modal.tsx:8`
   Mixed strategies: borders AND shadows. Pick one.

✓ **Polish** — Hover and focus states present
```

---

## Format Rules

1. **Category header** — Group by principle type
2. **Status icon** — ⚠️ for issues, ✓ for passing
3. **Principle name in bold** — One word identifier
4. **File:line** — Clickable location reference
5. **One line problem + fix** — Minimal explanation

---

## What to Include

### Interaction (from interaction principles)

| Check | Pass/Fail Criteria |
|-------|-------------------|
| Reversibility | Delete handlers have confirmation/undo/trash |
| Forgiveness | Async buttons disabled during loading |
| Persistence | Important state survives refresh |
| Transparency | try/catch on async, errors explain next steps |
| Escape | Modals closeable, flows have back/cancel |
| Consistency | Same action = same behavior everywhere |
| Recognition | Options visible, not hidden behind memorization |

### Visual (from visual principles)

| Check | Pass/Fail Criteria |
|-------|-------------------|
| States | Loading, empty, error states present |
| Accessibility | aria-labels, keyboard nav, focus management |
| Hierarchy | Consistent typography, single accent |
| Layout | Consistent spacing, proper mobile handling |
| Motion | reduced-motion respected, compositor props only |

### Craft (from visual principles)

| Check | Pass/Fail Criteria |
|-------|-------------------|
| Tokens | Colors/spacing use tokens, not hardcoded values |
| Depth | ONE strategy (borders OR shadows), not mixed |
| Text hierarchy | Four levels defined, used consistently |
| Polish | Hover, focus, transition states present |

---

## Severity Markers

Use for serious issues only:

```markdown
🔴 **Blocker: Accessibility** — `src/Button.tsx:12`
   div with onClick. Use <button> for keyboard access.
```

Most issues are just ⚠️ warnings.

---

## What NOT to Include

- Long explanations (save for audit mode)
- Principle rationales (user can look them up)
- Multiple fix options (just state what's needed)
- Teaching content (this is for experienced reviewers)

---

## Example: Full Review

```markdown
## UX Review: PR #142 — Add item deletion

### Interaction

⚠️ **Reversibility** — `src/components/ItemCard.tsx:42`
   Delete without safeguard. Add confirmation dialog.

⚠️ **Reversibility** — `src/api/items.ts:28`
   Hard delete. Consider soft delete to trash.

✓ **Forgiveness** — Delete button styled distinctly from primary actions
✓ **Transparency** — Toast shown after deletion

### Visual

⚠️ **States** — `src/components/ItemList.tsx:15`
   No empty state after last item deleted.

✓ **Accessibility** — Delete button has aria-label
✓ **Motion** — No animations added

---

**Summary:** 3 issues (2 interaction, 1 visual). Main concern is delete without recovery path.
```

---

## Integration Note

This format is designed for:
- PR comments (GitHub, GitLab)
- CI output
- Slack summaries

Keep it scannable. Link to full docs if user wants to learn more.
