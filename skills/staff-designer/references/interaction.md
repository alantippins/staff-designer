# The 8 Interaction Principles

What makes software feel solid, intentional, and trustworthy.

**Where these come from.** These eight principles are a distillation of [Nielsen Norman Group's 10 Usability Heuristics](https://www.nngroup.com/articles/ten-usability-heuristics/) and [Laws of UX](https://lawsofux.com/) into the ones that fire at the moment a user actually touches an interface — plus Craft as the intentionality lens. Nielsen's Match/Error Recovery/Help fold into adjacent principles; Craft adds the "was this decided or defaulted?" check that the classic heuristics don't cover. The editorial pass is the contribution, not the concepts. Credits inline below.

Severity: 🔴 Blocker | 🟡 Warning | 🟢 Suggestion

---

## Reversibility

**Every action should be undoable or recoverable.**

*Based on: [User Control and Freedom (Nielsen Heuristic 3)](https://www.nngroup.com/articles/user-control-and-freedom/).*

Users will make mistakes. They delete the wrong thing, edit when they meant to view, submit before they're ready. When actions are reversible, users explore freely. When they're not, users hesitate.

**What violation feels like:** "I just deleted that and there's no way to get it back." Heart-pounding panic followed by resignation.

### What to Check

| Check | What to Look For |
|-------|------------------|
| Delete has safeguard | Confirmation, undo toast, or soft delete (trash) |
| Bulk actions protected | "Delete all" / "Remove selected" has extra confirmation |
| State changes reversible | History/undo mechanism for important changes |
| Archive over delete | Soft delete when permanent removal isn't required |

### Severity

| Situation | Severity |
|-----------|----------|
| No safeguard at all | 🔴 Blocker |
| Confirmation dialog only (no undo) | 🟡 Warning |
| Undo toast or soft delete | ✅ Good |

---

## Forgiveness

**Software should assume human error and prevent harm.**

*Based on: [Error Prevention (Nielsen Heuristic 5)](https://www.nngroup.com/articles/ten-usability-heuristics/) + [Postel's Law (Laws of UX)](https://lawsofux.com/postels-law/).*

Users aren't careful. They double-click, fat-finger, paste wrong values, forget to save. Robust software anticipates this and prevents damage rather than punishing mistakes.

**What violation feels like:** "I clicked twice and it charged me twice." "The form rejected my input but won't tell me why."

### What to Check

| Check | What to Look For |
|-------|------------------|
| Submit disabled during async | Button disabled while processing |
| Destructive actions distinct | Delete styled differently than Submit |
| Input parsing permissive | Accept variations, normalize internally |
| Forms preserve on error | Don't clear data after API failure |

---

## Persistence

**User work should survive navigation, refresh, failure, and closing.**

*Based on: [Zeigarnik Effect (Laws of UX)](https://lawsofux.com/zeigarnik-effect/). Nielsen's heuristics don't address persistence directly — it's a distinct 2010s-onward concern added to the canon because lost work is such a common trust-breaker.*

Lost work is the deepest betrayal. Users invest time and attention. When the app loses their work—whether through a bug, a refresh, or accidental navigation—they lose trust permanently.

**What violation feels like:** "I spent 20 minutes on that form and it's gone." "I refreshed and everything reset."

### What to Check

| Check | What to Look For |
|-------|------------------|
| Long forms have draft state | localStorage/sessionStorage/autosave |
| State survives refresh | Not just React state |
| Failed submissions preserve input | Don't clear form on API error |
| Unsaved changes warning | `onbeforeunload` or router guards |

---

## Transparency

**System state should be visible and understandable at all times.**

*Based on: [Visibility of System Status (Nielsen Heuristic 1)](https://www.nngroup.com/articles/visibility-system-status/) + [Doherty Threshold (Laws of UX)](https://lawsofux.com/doherty-threshold/).*

Users shouldn't have to guess what happened, what's happening, or what will happen. Invisible state creates anxiety and mistrust. Clear feedback builds confidence.

**What violation feels like:** "Did it save?" "Is this loading or broken?" "What does this error mean?"

### What to Check

| Check | What to Look For |
|-------|------------------|
| Actions confirm completion | Toast/feedback after async operations |
| Errors explain what to do | Not just "Error" — what happened and next steps |
| Pending states visible | Loading indicators, disabled states |
| Sync status shown | "Saved" / "Saving..." / "Offline" |

---

## Escape

**Users should always have a way out of any state.**

*Based on: [User Control and Freedom (Nielsen Heuristic 3)](https://www.nngroup.com/articles/user-control-and-freedom/). Pairs with Reversibility — where Reversibility is about undoing after, Escape is about exiting during.*

Trapped users become angry users. Whether it's a modal, a wizard, or a process they started accidentally—there should always be an exit. Forced completions breed resentment.

**What violation feels like:** "I can't close this dialog." "There's no back button." "How do I cancel?"

### What to Check

| Check | What to Look For |
|-------|------------------|
| Modals have escape routes | X button, ESC handler, backdrop click |
| Multi-step flows have back/cancel | Not just "Next" and "Submit" |
| Browser back works | Proper history management |
| Onboarding skippable | Skip option available |

---

## Consistency

**The same action should work the same way everywhere.**

*Based on: [Consistency and Standards (Nielsen Heuristic 4)](https://www.nngroup.com/articles/consistency-and-standards/) + [Jakob's Law (Laws of UX)](https://lawsofux.com/jakobs-law/).*

Users build mental models. When a swipe deletes in one place and archives in another, the model breaks. When your app works differently than every other app on the platform, users stumble. Consistency lets users transfer what they've learned.

**What violation feels like:** "Wait, why didn't that work?" "This button did something different last time." "This doesn't feel like an iPhone app."

### What to Check

| Check | What to Look For |
|-------|------------------|
| Platform conventions | iOS patterns on iOS, Android on Android, web standards on web |
| Internal consistency | Same gesture/action = same result everywhere in the app |
| Icon meanings | Trash means delete everywhere, not archive in one place |
| Terminology | Same words for same concepts throughout |

### Severity

| Situation | Severity |
|-----------|----------|
| Conflicts with platform conventions | 🔴 Blocker |
| Same action behaves differently within app | 🟡 Warning |
| Minor terminology inconsistencies | 🟢 Suggestion |

---

## Craft

**The interface should show intentional design choices, not unexamined defaults.**

*Based on: [Aesthetic and Minimalist Design (Nielsen Heuristic 8)](https://www.nngroup.com/articles/ten-usability-heuristics/) + [Aesthetic-Usability Effect (Laws of UX)](https://lawsofux.com/aesthetic-usability-effect/). Added to the core eight because Nielsen's heuristics measure usability compliance but don't measure whether something was decided or defaulted — the intentionality gap that separates designed from assembled.*

Generic interfaces feel cheap. Users notice when something was designed vs. assembled from defaults. Craft isn't about being flashy — it's about every choice being deliberate. A minimal interface can show craft. A complex one can lack it.

**What violation feels like:** "This looks like a template." "This could be any app." "It works but feels unfinished."

### Where Defaults Hide

Defaults don't announce themselves. They disguise themselves as infrastructure — parts that feel like they "just need to work."

| Area | The Trap | Reality |
|------|----------|---------|
| **Typography** | "Pick something readable, move on" | Typography is the foundation of interface design. It carries the majority of information. When it's wrong, the whole interface reads as wrong regardless of execution quality elsewhere — it's the highest-leverage fix. Assess: font fit (does the typeface match the product's register?), hierarchy (are the needed content roles distinct without color?), signal (does weight track semantic importance?). For deep analysis, delegate to `/typeset`. |
| **Navigation** | "Build the sidebar, get to real work" | Navigation IS your product. Where you are, where you can go, what matters most. A screen floating in space is a component demo, not software. |
| **Data display** | "You have numbers, show numbers" | A number on screen is not design. What does it mean? What will they do with it? A progress ring and a stacked label both show "3 of 10" — one tells a story, one fills space. |
| **Token names** | "Implementation detail" | Check what tokens mean and how they are used. Generic or expressive names can both support an intentional product. |

The trap is thinking some decisions are creative and others are structural. Everything is design. The moment you stop asking "why this?" is when defaults take over.

### What to Check

| Check | What to Look For |
|-------|------------------|
| Typography intentional | Fonts selected for purpose, not defaulted |
| Color coherent | Defined palette with tokens, not random hex values |
| Spacing systematic | Consistent scale (4px/8px), not arbitrary numbers |
| Depth strategy coherent | Borders, shadows and surface shifts serve clear, consistent grouping and layering roles |
| Details finished | Hover states, focus rings, transitions polished |

### Quality Tests

Run these during review:

**Swap Test**
> Replace the typeface and colors with generic alternatives. Does it feel different?
> Assess whether the choices fit the intended experience; a familiar typeface or palette can be deliberate.

**Token Test**
> Are values hardcoded or using a system?
> Inspect whether the actual values and roles form a coherent system. Tokenization alone does not prove design quality.

### Severity

| Situation | Severity |
|-----------|----------|
| No design tokens, all hardcoded values | 🟡 Warning |
| Missing hover/focus/transition states | 🟡 Warning |
| Generic with no distinctive character | 🟢 Suggestion |

---

## Recognition

**Show users what they need — don't make them remember.**

*Based on: [Recognition rather than Recall (Nielsen Heuristic 6)](https://www.nngroup.com/articles/ten-usability-heuristics/) + [Hick's Law (Laws of UX)](https://lawsofux.com/hicks-law/).*

Memory is unreliable. When users have to remember commands, navigate without landmarks, or recall what they did last time, friction builds. Recognition is easy. Recall is hard. Show, don't tell.

**What violation feels like:** "Where was that setting?" "What did I name that thing?" "How do I do that again?"

### What to Check

| Check | What to Look For |
|-------|------------------|
| Recent items visible | Show what they worked on last |
| Options discoverable | Common actions visible, not buried in menus |
| Context preserved | Return to where they left off |
| Search over navigation | Let users find instead of browse for large sets |

### Severity

| Situation | Severity |
|-----------|----------|
| Critical features only accessible via hidden gestures/shortcuts | 🔴 Blocker |
| No recent items in content-heavy apps | 🟡 Warning |
| No search in apps with 50+ items | 🟡 Warning |

---

## Reporting principles

Use applicable principles to explain observable findings and what works. Skip principles with no useful signal. Report the evidence, impact and uncertainty in prose; do not manufacture a numeric Design Score, percentage or shipping band.

---

## Related Principles (from Laws of UX)

These inform the eight core principles above.

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
