---
name: typeset
description: "Typography review and planning. Works on code, screenshots, or briefs."
argument-hint: "[--plan]"
---

# Typeset

By Alan Tippins

Review existing typography or plan a system from scratch. Give it code and it reads the classes. Give it a screenshot and it reads the hierarchy. Give it a brief and it builds the system.

## How It Works

| Input          | Output                                             |
| -------------- | -------------------------------------------------- |
| Code           | Audit classes, catch inconsistencies, flag magic numbers |
| Screenshot     | Read the hierarchy, assess rhythm and signal       |
| Spec / Brief   | Generate a typography system                       |

Detect from context. If `--plan` is passed, or the input is a brief with no existing typography to review, generate a system. Otherwise, critique what's there.

---

## The Four Jobs

Typography has four jobs. Every finding traces back to one.

**Hierarchy.** Can you identify four distinct levels — primary, secondary, tertiary, muted — without relying on color? Count the distinct sizes. Count the distinct weights. If everything lands at one or two levels, there's no scale. If there are six levels that look nearly identical, there's no hierarchy either.

**Rhythm.** Does the type scale have internal logic? Steps should have a mathematical relationship — a ratio or a defined set — not arbitrary jumps. Line-height should be consistent within context: tighter for headings, more open for body, tightest for labels. Spacing between text blocks should feel like it comes from the same system as the type itself.

**Measure.** Line length determines readability. 65–75 characters is the target for body copy. Shorter feels cramped. Longer forces the eye to track across too much ground. Headings can run shorter. Labels can run longer. The issue is when body copy runs wall-to-wall with no constraint.

**Signal.** Does weight, size, and color reinforce what's semantically important — or contradict it? A bold label competing with a bolder value reads as noise. A large decorative heading visually outranking a smaller primary action inverts the priority. Signal is about whether the visual language matches the semantic hierarchy.

---

## Review Methodology

### Step 0: Orient

Before critiquing, establish:
- What kind of interface is this? (data-dense tool, marketing page, onboarding flow, content reading)
- What's the primary reading task? (scan, read, fill in, decide)

This sets the bar. A data table tolerates tighter measure and smaller type than a long-form article.

### Step 1: Count

Before judging, count:
- How many distinct font sizes are used?
- How many distinct weights?
- How many distinct text colors?

State the counts. "6 sizes, 2 weights, 4 colors" gives you the raw material for the critique. Counts prevent vague claims.

### Step 2: Audit by Job

Run each of the four jobs. For each finding, state: what you see, why it matters, what it could be instead.

**Reviewing code** — read the actual classes. See [references/checks.md](references/checks.md) for patterns to flag.

**Reviewing a screenshot** — read the visual hierarchy. Does the squint test pass? (Blur your vision — can you still identify 4 levels?) Is the measure constrained? Does weight track importance?

### Step 3: Score

Score each job 0–4:

| Score | Meaning |
| ----- | ------- |
| 0 | Broken — job isn't being done |
| 1 | At risk — partially addressed, breaks under real content |
| 2 | Uneven — works in some places, not others |
| 3 | Solid — job is done, minor gaps |
| 4 | Elevated — intentional craft, nothing wasted |

Mark N/A where a job doesn't apply (e.g. Measure on a one-word label component).

---

## Review Output

```
## Typography Score

| Job       | Score | Note |
| --------- | ----- | ---- |
| Hierarchy | 0–4   |      |
| Rhythm    | 0–4   |      |
| Measure   | 0–4   |      |
| Signal    | 0–4   |      |
| **Total** | /16   | Band |
```

Bands: ≥87% Solid · 68–86% Needs Work · <68% Broken

Then:

**Findings** — Prose by job. Bolded issue name. Specific and quantitative. Name the actual sizes, classes, counts.

**Code Flags** — (code input only) Specific class names or values to change. See [references/checks.md](references/checks.md).

**Top Opportunities** — 3 highest-impact changes, one sentence each, ordered by impact.

---

## Plan Methodology

When `--plan` is passed or the input is a brief:

1. **Identify the reading context** — What's the primary interface type? This determines base size and density.
2. **Set the scale** — Choose a base size and ratio. Modular scale (1.25 Minor Third, 1.333 Perfect Fourth, 1.5 Perfect Fifth) for expressive UIs. Custom increments (12/14/16/20/24/32) for dense tools.
3. **Map hierarchy** — Assign scale steps to the four levels. Name them semantically, not by size.
4. **Set rhythm** — Line-height per context. Spacing relationships.
5. **Define measure** — Max-width for body. Constraints for narrow columns.
6. **Write signal rules** — How weight, size, and color map to importance for this system specifically.

Make decisions. State the ratio, state the base, state why it fits the context. A confident recommendation is more useful than a list of options.

---

## Plan Output

```
## Scale
Base: [size]px · Ratio: [ratio or named increment]

| Step | Size  | Semantic Name | Use               |
| ---- | ----- | ------------- | ----------------- |
| xs   | [px]  | muted         | captions, labels  |
| sm   | [px]  | secondary     | supporting text   |
| base | [px]  | primary       | body copy         |
| lg   | [px]  | subheading    | section headers   |
| xl   | [px]  | heading       | page headings     |
| 2xl  | [px]  | display       | hero, emphasis    |

## Hierarchy Map
Primary: [step] · [weight] · [color token]
Secondary: [step] · [weight] · [color token]
Tertiary: [step] · [weight] · [color token]
Muted: [step] · [weight] · [color token]

## Rhythm
Body line-height: [value]
Heading line-height: [value]
Label line-height: [value]
Section spacing: [value]

## Measure
Body max-width: [ch or rem]
Narrow column: [value]
Use text-balance on headings. Use text-pretty on body.
Use tabular-nums on numeric data.

## Signal Rules
[How weight, size, and color reinforce semantic importance for this specific system]

## Tailwind / CSS
[Concrete implementation — classes or custom properties, ready to copy]
```

---

## Voice

Same posture as staff-designer — direct, specific, quantitative. Name the actual sizes. Count the distinct levels. Quote the class names.

"There are six uses of `text-sm` across this component: three are labels, two are body copy, one is an error message. No weight or color distinction separates them. The hierarchy is invisible." That's a finding.

"The hierarchy is unclear" is not.

For plan mode: make decisions, don't present options. "Use a 1.333 ratio — Perfect Fourth — because this is a reading-heavy product and the intervals give headings enough presence without needing large sizes" is useful. A table of five ratios asking the user to choose is not.

---

## Foundation

- [references/checks.md](references/checks.md) — Code patterns to flag when reviewing
