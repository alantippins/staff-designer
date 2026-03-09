---
name: interface-teach
description: Learn the Laws of interface quality with examples and explanations.
---

# Interface Teach

Deep educational explanations. For learning UX principles, not reviewing code.

---

## When to Use

- User wants to understand a principle
- Learning UX concepts
- Building intuition, not fixing code

---

## How It Works

User asks about a principle → Full lesson with examples, counter-examples, and related concepts.

---

## Input Formats

```
/interface-teach Law of Reversibility
/interface-teach "Why do users need undo?"
/interface-teach forgiveness
/interface-teach "What makes good error handling?"
```

---

## The Laws of Interface Quality

### Law of Reversibility

**Every action should be undoable or recoverable.**

Users will make mistakes. They delete the wrong thing, edit when they meant to view, submit before they're ready. When actions are reversible, users explore freely. When they're not, users hesitate.

**What violation feels like:** "I just deleted that and there's no way to get it back." Heart-pounding panic followed by resignation.

**What to Check:**

| Check | What to Look For |
|-------|------------------|
| Delete has safeguard | Confirmation, undo toast, or soft delete (trash) |
| Bulk actions protected | "Delete all" / "Remove selected" has extra confirmation |
| State changes reversible | History/undo mechanism for important changes |
| Archive over delete | Soft delete when permanent removal isn't required |

**Severity:**

| Situation | Severity |
|-----------|----------|
| No safeguard at all | 🔴 Blocker |
| Confirmation dialog only (no undo) | 🟡 Warning |
| Undo toast or soft delete | ✅ Good |

---

### Law of Forgiveness

**Software should assume human error and prevent harm.**

Users aren't careful. They double-click, fat-finger, paste wrong values, forget to save. Robust software anticipates this and prevents damage rather than punishing mistakes.

**What violation feels like:** "I clicked twice and it charged me twice." "The form rejected my input but won't tell me why."

**What to Check:**

| Check | What to Look For |
|-------|------------------|
| Submit disabled during async | Button disabled while processing |
| Destructive actions distinct | Delete styled differently than Submit |
| Input parsing permissive | Accept variations, normalize internally |
| Forms preserve on error | Don't clear data after API failure |

**Examples:**

✗ **Violation: E-commerce checkout**
User clicks "Place Order" → no feedback → clicks again → charged twice.
No loading state, no disabled button. User blamed for "double-clicking."

✓ **Good: Stripe checkout**
Click submit → button shows spinner and disables → "Processing..." text.
Even if user frantically clicks, only one charge happens.

---

### Law of Persistence

**User work should survive navigation, refresh, failure, and closing.**

Lost work is the deepest betrayal. Users invest time and attention. When the app loses their work—whether through a bug, a refresh, or accidental navigation—they lose trust permanently.

**What violation feels like:** "I spent 20 minutes on that form and it's gone." "I refreshed and everything reset."

**What to Check:**

| Check | What to Look For |
|-------|------------------|
| Long forms have draft state | localStorage/sessionStorage/autosave |
| State survives refresh | Not just React state |
| Failed submissions preserve input | Don't clear form on API error |
| Unsaved changes warning | `onbeforeunload` or router guards |

**Examples:**

✗ **Violation: Job application form**
User spends 30 minutes filling out application → accidentally hits back button → everything gone. No draft, no warning, no recovery.

✓ **Good: Google Docs**
Type anything → "Saving..." appears → close browser → reopen → everything there.
Users never think about saving. The app just remembers.

✓ **Good: Notion**
Start typing → navigate away → browser warns "You have unsaved changes."
Even if ignored, draft is waiting when they return.

---

### Law of Transparency

**System state should be visible and understandable at all times.**

Users shouldn't have to guess what happened, what's happening, or what will happen. Invisible state creates anxiety and mistrust. Clear feedback builds confidence.

**What violation feels like:** "Did it save?" "Is this loading or broken?" "What does this error mean?"

**What to Check:**

| Check | What to Look For |
|-------|------------------|
| Actions confirm completion | Toast/feedback after async operations |
| Errors explain what to do | Not just "Error" — what happened and next steps |
| Pending states visible | Loading indicators, disabled states |
| Sync status shown | "Saved" / "Saving..." / "Offline" |

**Examples:**

✗ **Violation: Settings page**
User toggles a setting → nothing happens → did it save? User refreshes to check.
No confirmation, no feedback. Anxiety on every interaction.

✓ **Good: Linear**
Change anything → subtle "Saved" appears briefly → user knows it worked.
Every action has feedback. Users develop trust.

✗ **Violation: Generic error**
API fails → "Error" toast appears → user has no idea what went wrong or what to do.

✓ **Good: Specific error**
"Couldn't save — you're offline. We'll retry when connected."
User understands the problem AND knows it's being handled.

---

### Law of Escape

**Users should always have a way out of any state.**

Trapped users become angry users. Whether it's a modal, a wizard, or a process they started accidentally—there should always be an exit. Forced completions breed resentment.

**What violation feels like:** "I can't close this dialog." "There's no back button." "How do I cancel?"

**What to Check:**

| Check | What to Look For |
|-------|------------------|
| Modals have escape routes | X button, ESC handler, backdrop click |
| Multi-step flows have back/cancel | Not just "Next" and "Submit" |
| Browser back works | Proper history management |
| Onboarding skippable | Skip option available |

**Examples:**

✗ **Violation: Onboarding wizard**
App forces 5-step onboarding → no skip button → user wants to explore first.
Forced completions feel like hostage situations.

✓ **Good: Slack onboarding**
"Set up your profile" with clear "Skip for now" link.
Users who want guidance get it. Users who don't aren't trapped.

✗ **Violation: Modal with no close**
Modal appears → no X button → ESC doesn't work → backdrop click does nothing.
User has to refresh the page to escape.

✓ **Good: Any well-built modal**
X button visible → ESC closes → clicking outside closes.
Three escape routes. User never feels trapped.

---

### Law of Consistency

**The same action should work the same way everywhere.**

Users build mental models. When a swipe deletes in one place and archives in another, the model breaks. When your app works differently than every other app on the platform, users stumble. Consistency lets users transfer what they've learned.

**What violation feels like:** "Wait, why didn't that work?" "This button did something different last time." "This doesn't feel like an iPhone app."

**What to Check:**

| Check | What to Look For |
|-------|------------------|
| Platform conventions | iOS patterns on iOS, Android on Android, web standards on web |
| Internal consistency | Same gesture/action = same result everywhere in the app |
| Icon meanings | Trash means delete everywhere, not archive in one place |
| Terminology | Same words for same concepts throughout |

**Severity:**

| Situation | Severity |
|-----------|----------|
| Conflicts with platform conventions | 🔴 Blocker |
| Same action behaves differently within app | 🟡 Warning |
| Minor terminology inconsistencies | 🟢 Suggestion |

**Examples:**

✗ **Violation: Custom gestures**
App uses swipe-left to archive → every other app uses swipe-left to delete.
Users delete things by accident, then blame themselves.

✓ **Good: Following conventions**
Swipe-left reveals delete (red). Matches iOS Mail, every todo app, user expectations.
Users transfer knowledge. No learning curve.

✗ **Violation: Internal inconsistency**
Trash icon deletes in list view → same trash icon archives in detail view.
User's mental model breaks. "Wait, why didn't that delete?"

✓ **Good: Internal consistency**
Trash icon always deletes. Archive icon always archives. Same action = same result.

---

### Law of Craft

**The interface should show intentional design choices, not unexamined defaults.**

Generic interfaces feel cheap. Users notice when something was designed vs. assembled from defaults. Craft isn't about being flashy — it's about every choice being deliberate. A minimal interface can show craft. A complex one can lack it.

**What violation feels like:** "This looks like a template." "This could be any app." "It works but feels unfinished."

**Where Defaults Hide:**

| Area | The Trap | Reality |
|------|----------|---------|
| **Typography** | "Pick something readable, move on" | Typography IS your design. The weight of a headline, the personality of a label — these shape feel before anyone reads a word. |
| **Navigation** | "Build the sidebar, get to real work" | Navigation IS your product. Where you are, where you can go, what matters most. A screen floating in space is a component demo, not software. |
| **Data display** | "You have numbers, show numbers" | A number on screen is not design. What does it mean? What will they do with it? A progress ring and a stacked label both show "3 of 10" — one tells a story, one fills space. |
| **Token names** | "Implementation detail" | Your CSS variables are design decisions. `--ink` and `--parchment` evoke a world. `--gray-700` and `--surface-2` evoke a template. |

**What to Check:**

| Check | What to Look For |
|-------|------------------|
| Typography intentional | Fonts selected for purpose, not defaulted |
| Color coherent | Defined palette with tokens, not random hex values |
| Spacing systematic | Consistent scale (4px/8px), not arbitrary numbers |
| Depth strategy consistent | ONE approach: borders-only, subtle shadows, layered, or surface shifts |
| Details finished | Hover states, focus rings, transitions polished |

**Quality Tests:**

- **Swap Test:** Replace typeface and colors with generic alternatives. Does it feel different? If no → you defaulted.
- **Token Test:** Are values hardcoded or using a system? Hardcoded hex colors and pixel values = no design system.

**Severity:**

| Situation | Severity |
|-----------|----------|
| No design tokens, all hardcoded values | 🟡 Warning |
| Missing hover/focus/transition states | 🟡 Warning |
| Generic with no distinctive character | 🟢 Suggestion |

**Examples:**

✗ **Violation: Default everything**
System font, blue links, gray borders, 16px padding everywhere.
"This could be any app." No personality, no intention, no craft.

✓ **Good: Linear**
Custom typography, considered color palette, consistent spacing system.
You know you're in Linear. The interface has a voice.

✗ **Violation: Template tokens**
`--gray-100`, `--gray-200`, `--primary`, `--secondary`.
Implementation details masquerading as design decisions.

✓ **Good: Intentional tokens**
`--ink`, `--paper`, `--accent-warm`, `--surface-raised`.
Names that evoke the product's world. Design decisions, not defaults.

---

### Law of Recognition

**Show users what they need — don't make them remember.**

Memory is unreliable. When users have to remember commands, navigate without landmarks, or recall what they did last time, friction builds. Recognition is easy. Recall is hard. Show, don't tell.

**What violation feels like:** "Where was that setting?" "What did I name that thing?" "How do I do that again?"

**What to Check:**

| Check | What to Look For |
|-------|------------------|
| Recent items visible | Show what they worked on last |
| Options discoverable | Common actions visible, not buried in menus |
| Context preserved | Return to where they left off |
| Search over navigation | Let users find instead of browse for large sets |

**Severity:**

| Situation | Severity |
|-----------|----------|
| Critical features only accessible via hidden gestures/shortcuts | 🔴 Blocker |
| No recent items in content-heavy apps | 🟡 Warning |
| No search in apps with 50+ items | 🟡 Warning |

**Examples:**

✗ **Violation: Hidden features**
Power feature only accessible via keyboard shortcut → users never discover it.
"I didn't know you could do that!" after months of use.

✓ **Good: Figma**
Keyboard shortcuts shown in menus. Users learn by seeing.
Command palette (Cmd+/) surfaces everything. Nothing hidden.

✗ **Violation: No recent items**
Document app with hundreds of files → no "Recent" section → user must remember file names.
"What did I call that thing?"

✓ **Good: VS Code**
"Recent" front and center on launch. User picks up where they left off.
Recognition over recall. Show, don't make them remember.

---

## Related Laws (from Laws of UX)

These principles inform the eight core laws above.

### Jakob's Law
Users expect your app to work like others they've used.
- Standard icons for standard actions (pencil for edit, trash for delete)
- Conventional keyboard shortcuts (ESC closes, Enter submits)
- Platform-native gestures

### Fitts's Law
Small, far targets are hard to hit.
- Destructive actions smaller/further from primary actions
- 44px minimum touch targets
- Primary actions in thumb zones

### Hick's Law
More choices = slower decisions.
- One clear primary CTA per view
- Group long menus
- Smart defaults that work for 80%

### Postel's Law
Be liberal in what you accept, conservative in what you produce.
- Accept phone number variations
- Parse multiple date formats
- Unicode in name fields

### Peak-End Rule
Experiences are judged by peak and end moments.
- Errors at the end feel worse than errors in the middle
- Success states should feel satisfying
- Clear completion feedback

### Doherty Threshold
Response under 400ms keeps users in flow.
- Optimistic UI for immediate feedback
- Loading states within 100ms
- Progress indicators for long operations

### Tesler's Law
Complexity can't be eliminated, only moved.
- Don't hide essential features behind "simple" UI
- Predictable behaviors over "magic"
- Progressive disclosure for power features

### Zeigarnik Effect
Incomplete tasks nag at the mind.
- Draft saves for long forms
- Progress indicators
- "Continue where you left off"

---

## Output Format

When teaching a principle:

```markdown
# [Principle Name]

## The Core Idea
[One memorable sentence]

---

## Why This Matters

[2-3 paragraphs explaining:]
- The user psychology behind this
- What happens when it's violated
- What happens when it's done well

---

## Examples

### ✗ Violation
[Concrete example of doing it wrong]
- What the user experiences
- Why it fails

### ✓ Good Implementation
[Concrete example of doing it right]
- What the user experiences
- Why it works

---

## Detection

**What to look for in code:**
- [Pattern 1]
- [Pattern 2]

**What to look for in the UI:**
- [Manual check 1]
- [Manual check 2]

---

## Related Principles

- [Related Law 1] — [How they connect]
- [Related Law 2] — [How they connect]

---

## Quick Reference

| Severity | When |
|----------|------|
| 🔴 | [Blocker criteria] |
| 🟡 | [Warning criteria] |
| 🟢 | [Suggestion criteria] |

---

## Further Reading

- [Link or reference 1]
- [Link or reference 2]
```

---

## Example: Law of Reversibility

```markdown
# Law of Reversibility

## The Core Idea
Every action should be undoable or recoverable.

---

## Why This Matters

Users make mistakes. They click the wrong button, delete the wrong item,
submit before they're ready. This is not user error—it's human nature.
The question isn't whether mistakes happen, but what happens when they do.

When actions are irreversible, users develop anxiety. They hesitate before
clicking. They double-check obsessively. They lose trust in your app. Every
interaction carries risk, and risk creates friction.

When actions are reversible, users gain confidence. They explore freely.
They try things without fear. The cognitive load of "what if I mess up?"
disappears. Your app becomes a safe space to work, not a minefield.

---

## Examples

### ✗ Violation: Gmail circa 2004
Click delete → Email gone forever.
Users had to fish through trash. Accidental deletions caused panic.
The cost of a mistake was permanent loss.

### ✓ Good Implementation: Gmail today
Click delete → Email moves to trash → Toast: "Message deleted. [Undo]"
Users can immediately undo. Trash auto-purges after 30 days.
Accidents become minor inconveniences, not disasters.

### ✗ Violation: Form without confirmation
Click submit on wrong form → Data sent, no take-backs.
User realizes mistake immediately, but it's too late.
Anxiety on every submit button going forward.

### ✓ Good Implementation: Slack message editing
Send message → Can edit for hours → Can delete anytime.
Typos, wrong channels, regrettable messages—all fixable.
Users send freely without proofreading anxiety.

---

## Detection

**What to look for in code:**
- `onClick={() => delete(id)}` without confirmation/undo nearby
- Hard delete API calls (`DELETE /items/:id`) without soft delete option
- State changes with no history/undo mechanism
- Bulk operations without extra confirmation

**What to look for in the UI:**
- Delete buttons with no confirmation dialog
- No "undo" option after destructive actions
- No trash/archive as alternative to permanent delete
- Actions that immediately modify server state

---

## Related Principles

- **Law of Forgiveness** — Prevent mistakes from happening; Reversibility handles them after
- **Law of Transparency** — Users need to see what was undone and what state they're in
- **Peak-End Rule** — A recoverable mistake feels okay; an unrecoverable one ruins the experience

---

## Quick Reference

| Severity | When |
|----------|------|
| 🔴 Blocker | Delete with no safeguard at all |
| 🟡 Warning | Confirmation only (no undo or trash) |
| 🟢 Good | Undo toast, soft delete, or version history |

---

## Further Reading

- Laws of UX: https://lawsofux.com/
- Gmail's undo feature case study
- "Don't Make Me Think" by Steve Krug (Chapter on user mistakes)
```

---

## Key Principles for Teaching

1. **Start with the memorable version** — One sentence they'll remember
2. **Explain the psychology** — Why users feel this way
3. **Concrete examples** — Real products, real scenarios
4. **Both sides** — What bad looks like AND what good looks like
5. **Connect to other principles** — Build a mental model
6. **Make it actionable** — What to look for in their own work
