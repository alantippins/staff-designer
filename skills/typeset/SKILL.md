---
name: typeset
description: "Formal typography audit. Works on code, screenshots, or briefs."
argument-hint: "[--plan]"
---

# Typeset

By Alan Tippins

Formal typography audit with four-job scoring, code flags, and generative directions. Install alongside staff-designer — they share a methodology.

## How It Works

| Input          | Output                                             |
| -------------- | -------------------------------------------------- |
| Code           | Four-job score, code flags, top opportunities      |
| Screenshot     | Four-job score, visual findings, directions        |
| Spec / Brief   | Generate a typography system                       |

Detect from context. If `--plan` is passed, or the input is a brief with no existing typography to review, generate a system. If the input is a screenshot or image, review visually — no code flags. Otherwise, run the full audit.

---

## Methodology

The four-job framework lives in staff-designer. Load it before proceeding:

→ Read `~/.claude/skills/staff-designer/references/typography.md`

Apply the Orient → Count → Audit → Score sequence from that file.

For code input, also reference [references/checks.md](references/checks.md) for implementation-level flags.

---

## Audit Output

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

**Score only what the user experiences.** Token mismatches that currently render correctly, off-system class names that produce the right visual output — none of these move the score. Score the screen, flag the code separately.

**Findings** — Prose by job. Bolded issue name. Specific and quantitative. Name what's working and what isn't. For every problem, show what great looks like.

**Where this could go** — Three specific directions:

1. **Font direction** — Is the current typeface a ceiling or a foundation? Name what a personality shift would unlock. Specific: not "try a serif" but "a humanist display type at the heading level would give this the warmth that Inter can't carry — something like DM Serif Display or Fraunces would shift the product from tool to trusted advisor."

2. **Hierarchy vision** — What would intentional craft look like at scale, with real content under pressure?

3. **System maturity** — What structural work would make this scale reliably? Naming, tokens, constraints.

**Code Flags** — (code input only) Token inconsistencies, missing constraints, off-system values. Advisory — don't tank the score. See [references/checks.md](references/checks.md).

**Top Opportunities** — 3 highest-impact changes, one sentence each. Visual issues first, code flags second.

---

## Plan Methodology

When `--plan` is passed or the input is a brief:

1. **Identify the reading context** — Use the context table from the typography methodology to set defaults.
2. **Choose base size** — 13–14px for data tools. 15–16px for apps. 16–18px for reading-heavy products. 18–22px for display-first marketing.
3. **Set the scale** — Choose a ratio:
   - Dense tools: custom increments (12/14/16/20/24)
   - Apps and task flows: 1.25 (Minor Third)
   - Reading products: 1.333 (Perfect Fourth)
   - Expressive / marketing: 1.5 (Perfect Fifth) or higher
4. **Map hierarchy** — Assign scale steps to the four levels. Name them semantically.
5. **Set rhythm** — Line-height per context. Spacing relationships.
6. **Define measure** — Max-width for body. Constraints for narrow columns.
7. **Write signal rules** — How weight, size, and color map to importance for this system.

Make decisions. State the ratio, state the base, state why it fits the context.

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
[How weight, size, and color reinforce semantic importance for this system]

## Tailwind / CSS
[Concrete implementation — classes or custom properties, ready to copy]
```

---

## Voice

Same posture as staff-designer — direct, specific, quantitative, but oriented toward the upside. Typeset is the typography depth layer: it goes where staff-designer's Craft principle points but doesn't follow.

Name what's actually there before naming what's wrong. Frame findings as what the typography could be doing, not just what it isn't. "The description text sits at the same weight and line-height as the label above it — one level is doing two jobs, and the user has to work harder to parse the card" is a finding. "The hierarchy is unclear" is not.

Show what great looks like. After naming a problem, describe the better version specifically. Not "increase line-height on descriptions" — "giving descriptions a looser line-height would let them breathe as supporting copy instead of competing with the label for attention."

For plan mode: make decisions. "Use a 1.333 ratio — Perfect Fourth — because this is a reading-heavy product and the intervals give headings enough presence without needing large sizes" is useful. A table of options asking the user to choose is not.

---

## Foundation

- [references/checks.md](references/checks.md) — Implementation-level patterns to flag when reviewing code
