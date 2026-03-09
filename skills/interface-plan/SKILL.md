---
name: interface-plan
description: Surface interaction and craft concerns before you build. Asks the questions that prevent headaches later.
---

# Interface Plan

Question-driven spec refinement. Use **before** building to surface interaction and craft concerns early.

---

## When to Use

- Starting a new feature
- Refining a user story
- Before writing any code

---

## How It Works

1. User describes what they want to build
2. You ask questions that surface principle violations before they're coded
3. Output: refined spec with interaction concerns addressed

---

## Interaction Principles

The Laws of Interface Quality — understand these before asking questions.

### Law of Reversibility

**Every action should be undoable or recoverable.**

Users will make mistakes. They delete the wrong thing, edit when they meant to view, submit before they're ready. When actions are reversible, users explore freely. When they're not, users hesitate.

**What violation feels like:** "I just deleted that and there's no way to get it back."

| Check | What to Look For |
|-------|------------------|
| Delete has safeguard | Confirmation, undo toast, or soft delete (trash) |
| Bulk actions protected | "Delete all" / "Remove selected" has extra confirmation |
| State changes reversible | History/undo mechanism for important changes |
| Archive over delete | Soft delete when permanent removal isn't required |

| Situation | Severity |
|-----------|----------|
| No safeguard at all | 🔴 Blocker |
| Confirmation dialog only (no undo) | 🟡 Warning |
| Undo toast or soft delete | ✅ Good |

### Law of Forgiveness

**Software should assume human error and prevent harm.**

Users aren't careful. They double-click, fat-finger, paste wrong values, forget to save. Robust software anticipates this and prevents damage rather than punishing mistakes.

**What violation feels like:** "I clicked twice and it charged me twice." "The form rejected my input but won't tell me why."

| Check | What to Look For |
|-------|------------------|
| Submit disabled during async | Button disabled while processing |
| Destructive actions distinct | Delete styled differently than Submit |
| Input parsing permissive | Accept variations, normalize internally |
| Forms preserve on error | Don't clear data after API failure |

### Law of Persistence

**User work should survive navigation, refresh, failure, and closing.**

Lost work is the deepest betrayal. Users invest time and attention. When the app loses their work—whether through a bug, a refresh, or accidental navigation—they lose trust permanently.

**What violation feels like:** "I spent 20 minutes on that form and it's gone." "I refreshed and everything reset."

| Check | What to Look For |
|-------|------------------|
| Long forms have draft state | localStorage/sessionStorage/autosave |
| State survives refresh | Not just React state |
| Failed submissions preserve input | Don't clear form on API error |
| Unsaved changes warning | `onbeforeunload` or router guards |

### Law of Transparency

**System state should be visible and understandable at all times.**

Users shouldn't have to guess what happened, what's happening, or what will happen. Invisible state creates anxiety and mistrust. Clear feedback builds confidence.

**What violation feels like:** "Did it save?" "Is this loading or broken?" "What does this error mean?"

| Check | What to Look For |
|-------|------------------|
| Actions confirm completion | Toast/feedback after async operations |
| Errors explain what to do | Not just "Error" — what happened and next steps |
| Pending states visible | Loading indicators, disabled states |
| Sync status shown | "Saved" / "Saving..." / "Offline" |

### Law of Escape

**Users should always have a way out of any state.**

Trapped users become angry users. Whether it's a modal, a wizard, or a process they started accidentally—there should always be an exit. Forced completions breed resentment.

**What violation feels like:** "I can't close this dialog." "There's no back button." "How do I cancel?"

| Check | What to Look For |
|-------|------------------|
| Modals have escape routes | X button, ESC handler, backdrop click |
| Multi-step flows have back/cancel | Not just "Next" and "Submit" |
| Browser back works | Proper history management |
| Onboarding skippable | Skip option available |

### Law of Consistency

**The same action should work the same way everywhere.**

Users build mental models. When a swipe deletes in one place and archives in another, the model breaks. When your app works differently than every other app on the platform, users stumble.

**What violation feels like:** "Wait, why didn't that work?" "This button did something different last time."

| Check | What to Look For |
|-------|------------------|
| Platform conventions | iOS patterns on iOS, Android on Android, web standards on web |
| Internal consistency | Same gesture/action = same result everywhere in the app |
| Icon meanings | Trash means delete everywhere, not archive in one place |
| Terminology | Same words for same concepts throughout |

### Law of Craft

**The interface should show intentional design choices, not unexamined defaults.**

Generic interfaces feel cheap. Users notice when something was designed vs. assembled from defaults. Craft isn't about being flashy — it's about every choice being deliberate.

**What violation feels like:** "This looks like a template." "This could be any app."

**Where Defaults Hide:**

| Area | The Trap | Reality |
|------|----------|---------|
| Typography | "Pick something readable, move on" | Typography IS your design. The weight of a headline, the personality of a label — these shape feel before anyone reads a word. |
| Navigation | "Build the sidebar, get to real work" | Navigation IS your product. Where you are, where you can go, what matters most. |
| Data display | "You have numbers, show numbers" | A number on screen is not design. What does it mean? What will they do with it? |
| Token names | "Implementation detail" | Your CSS variables are design decisions. `--ink` and `--parchment` evoke a world. `--gray-700` evokes a template. |

### Law of Recognition

**Show users what they need — don't make them remember.**

Memory is unreliable. When users have to remember commands, navigate without landmarks, or recall what they did last time, friction builds. Recognition is easy. Recall is hard.

**What violation feels like:** "Where was that setting?" "What did I name that thing?"

| Check | What to Look For |
|-------|------------------|
| Recent items visible | Show what they worked on last |
| Options discoverable | Common actions visible, not buried in menus |
| Context preserved | Return to where they left off |
| Search over navigation | Let users find instead of browse for large sets |

### Related Laws (from Laws of UX)

- **Jakob's Law** — Users expect your app to work like others they've used
- **Fitts's Law** — Small, far targets are hard to hit (44px minimum touch targets)
- **Hick's Law** — More choices = slower decisions (one clear primary CTA per view)
- **Postel's Law** — Be liberal in what you accept, conservative in what you produce
- **Peak-End Rule** — Experiences are judged by peak and end moments
- **Doherty Threshold** — Response under 400ms keeps users in flow

---

## Question Framework

For each feature, work through these categories.

### Intent Questions (ask first)

Before any implementation questions, establish intent:

- **Who is this human?** Not "users." The actual person. Where are they when they open this? What's on their mind?
- **What must they accomplish?** Not "use the feature." The verb. What action, what outcome?
- **What should this feel like?** Say it in words that mean something. "Clean and modern" means nothing. Warm like a notebook? Cold like a terminal? Dense like a trading floor? Calm like a reading app?

If you can't answer these with specifics, ask the user. Don't guess.

### Craft Questions (decisions to make early)

These decisions shape everything downstream. Make them explicit:

- **Depth strategy:** Borders-only, subtle shadows, layered shadows, or surface color shifts? Pick ONE.
- **Typography:** What typeface fits the feel? Don't default — select.
- **Color temperature:** Warm, cool, neutral? What colors exist in this product's world?
- **Information density:** Spacious or dense? What serves the user's task?

### Where Defaults Hide

Defaults sneak into these areas. Name them before they win:

| Area | The Trap | Ask Instead |
|------|----------|-------------|
| Typography | "Pick something readable" | What typeface fits this product's personality? |
| Navigation | "Build sidebar, add links" | How should users think about this space? |
| Data display | "Show the number" | What does this number mean? What will they do with it? |
| Token names | "Implementation detail" | Do these names evoke the product or a template? |

---

### Reversibility Questions
- Will users need to recover deleted items? How long should recovery be available?
- Are there bulk operations? What happens if they select the wrong items?
- Can changes be undone? History, version control, undo button?

### Forgiveness Questions
- What happens if users double-click submit?
- Can they put bad data in and recover gracefully?
- Are destructive actions distinguishable from safe ones?

### Persistence Questions
- If they refresh mid-form, what happens?
- If the API fails, is their input preserved?
- Should there be a draft/autosave?

### Transparency Questions
- How will they know it worked?
- What does the loading state look like?
- If it fails, what do they see? What can they do?

### Escape Questions
- Can they cancel at any point?
- If there's a modal, how do they close it?
- For multi-step flows, can they go back?

### Consistency Questions
- Does this action work the same way elsewhere in the app?
- Are we following platform conventions (iOS/Android/web)?
- Will users expect this to behave like similar features they've used?

### Recognition Questions
- Can users see their options, or must they remember commands?
- Should we show recent items, suggestions, or search?
- How do users find this feature if they forget where it is?

---

## Output Format

Return a refined spec that includes:

```markdown
## Feature: [Name]

### Intent
- **Who:** [The actual person using this]
- **Task:** [What they must accomplish]
- **Feel:** [How it should feel — specific, not generic]

### Craft Decisions
- **Depth:** [borders-only / subtle shadows / layered / surface shifts]
- **Typography:** [Selected typeface and why]
- **Density:** [spacious / balanced / dense]

### Happy Path
[Normal flow]

### Interaction Safeguards

**Reversibility:**
- [How delete/changes are recoverable]

**Forgiveness:**
- [How double-submit is prevented]
- [How errors preserve input]

**Persistence:**
- [What survives refresh/failure]

**Transparency:**
- [Loading, success, error feedback]

**Escape:**
- [How users can exit any state]

**Consistency:**
- [How this matches existing patterns]

### Questions Still Open
- [Anything that needs user decision]
```

---

## Example

**User says:** "I want to add a delete button to each item in my list."

**Plan mode response:**

> A few questions before we build this:
>
> **Reversibility:**
> - Should deleted items go to trash (recoverable) or be permanently removed?
> - If permanent, do you want a confirmation dialog, undo toast, or both?
>
> **Forgiveness:**
> - Should the delete button be visually distinct from other actions (red, icon only, positioned separately)?
>
> **Transparency:**
> - What feedback should users see after deleting? Toast notification? List animation?
>
> **Bulk operations:**
> - Will you eventually support multi-select delete? If so, we should design for it now.

After user answers:

```markdown
## Feature: Delete Items

### Happy Path
Click delete → confirmation dialog → item removed → toast confirmation

### Interaction Safeguards

**Reversibility:**
- Soft delete to trash (recoverable 30 days)
- Confirmation dialog: "Delete [item name]? [Cancel] [Delete]"
- Undo toast for 5 seconds after deletion

**Forgiveness:**
- Delete button: outline style, smaller than primary actions
- Positioned right side, away from edit/view buttons

**Persistence:**
- N/A (list is server state)

**Transparency:**
- Loading: button shows spinner during API call
- Success: toast "Item deleted" with undo link
- Error: toast "Couldn't delete. Try again." + item stays in list

**Escape:**
- Confirmation dialog has Cancel button and closes on ESC/backdrop
```

---

## Key Principles

1. **Ask, don't assume** — Surface decisions before coding
2. **Name the principle** — "For reversibility..." helps users learn
3. **Offer good defaults** — Suggest the safest approach as default
4. **Keep it conversational** — This is planning, not auditing
