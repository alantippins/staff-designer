# Typography Code Checks

Patterns to flag when reviewing code. Each check maps to one of the four jobs.

---

## Hierarchy

**Multiple semantic levels sharing one class**
`text-sm` used for labels, body copy, and error messages with no weight or color distinction. Result: the hierarchy is invisible to the eye even though the content has clear importance levels.

**Too many sizes without semantic purpose**
More than 6 distinct sizes in a single view with no clear mapping to hierarchy levels. Complexity without structure.

**One or two sizes for everything**
Every text element at `text-sm` and `text-base` with no differentiation at heading or muted levels. Flat hierarchy.

**Hardcoded sizes instead of scale steps**
`font-size: 13px` or `text-[13px]` — arbitrary values outside the defined scale. Breaks rhythm and makes the scale untrustworthy.

---

## Rhythm

**Hardcoded line-height values**
`leading-[1.6]` or `line-height: 22px` — magic numbers outside the Tailwind scale. A sign the type system isn't being respected.

**No line-height distinction between heading and body**
Both using `leading-normal` or `leading-relaxed` — headings should be tighter than body copy. `leading-tight` or `leading-snug` for headings; `leading-relaxed` or `leading-loose` for body.

**Inconsistent spacing between text blocks**
`mb-3` on one paragraph, `mb-5` on another, `mt-4` on a third — no consistent rhythm between text elements.

**Mixed font families without clear role**
Two or more font families applied inconsistently — one on headings, one on labels, one on a random callout. Role should be clear: serif for editorial, mono for code, sans for UI.

---

## Measure

**No max-width on body copy**
Paragraphs or long-form text with no `max-w-*` or `max-ch-*` constraint. At full container width, body copy routinely exceeds 100 characters per line.

**Missing text-balance on headings**
Multi-line headings without `text-balance` — orphaned words or uneven line breaks that could be fixed with one class.

**Missing text-pretty on body**
Long-form body copy without `text-pretty` — avoids widows and orphans in paragraph text.

**Measure too narrow**
Body copy inside a constrained column (< 45ch) forcing uncomfortable line breaks and a choppy reading experience.

---

## Signal

**font-bold applied decoratively**
Bold weight used on UI chrome, borders, or decoration rather than to signal importance. When everything bold is important, nothing is.

**Color used as the only signal**
Muted text differentiated only by color, not size or weight — invisible in low-contrast environments and inaccessible to users who can't distinguish colors.

**Passive text colored like interactive elements**
Descriptive or supporting text using the same color as links, buttons, or active states — reads as clickable when it isn't. Check any non-heading text that uses the brand or accent color: is it interactive? If not, it should use a neutral text color instead.

**Hardcoded text color hex values**
`color: #6B7280` instead of a token like `text-muted` or `--color-text-secondary`. Breaks theming and makes signal rules impossible to maintain.

**Weight contradiction**
A supporting label in `font-semibold` outweighs a primary value in `font-normal` next to it. The visual weight inverts the semantic importance.

**Decorative size hierarchy**
A large decorative number or display text visually dominates over the primary action or heading it supports. Decoration outranking function.

---

## Missing Polish

**No tabular-nums on numeric data**
Numbers in tables or data displays without `tabular-nums` — digits don't align vertically across rows, making comparison harder.

**Inconsistent capitalization**
`uppercase` on some labels, sentence case on others, title case on a third group — no consistent rule for label capitalization.

**Missing font-feature-settings for ligatures**
Long-form reading contexts without `font-feature-settings: "liga" 1` where the typeface supports it. Minor, but part of craft.

---

## Hard Stops

These aren't edge cases — they're the decisions that make a type system untrustworthy. Each one is recoverable, but only with a full audit.

**Too many families.** Three font families is the ceiling, and most products don't need more than one or two. Every additional family is a relationship you have to manage: pairing contrast, weight equivalence, size matching. The complexity compounds fast.

**Arbitrary sizes.** A size that isn't on the scale isn't a decision — it's a gap in the system. The next person who needs something "between" those two sizes will add another arbitrary value, and the scale collapses.

**Body text below 16px.** Below 1rem, you're not setting type for your users — you're setting it for users with perfect vision in ideal lighting. Use rem, not px. Respect the browser's font size setting.

**Display fonts in body.** A font chosen for personality at 48px falls apart at 16px. Display and text fonts solve different problems at different sizes.

**Too many weights.** Four weights (Regular, Medium, Semibold, Bold) is the full working set. Loading a fifth weight adds page weight and tempts misuse. If you can't solve the problem with four, the problem is hierarchy, not weights.

**Pairing fonts that are almost the same.** Two geometric sans-serifs, two humanists — the pairing reads as inconsistency, not intention. Pair for contrast: a serif with a sans, a condensed with a regular, a high-contrast with a low-contrast.

**Defaulting on font choice.** Inter is not a design decision. Neither is Roboto. They're placeholders. Using them is fine when the interface is the product. When the brand needs personality, the typeface is the first place to build it.

---

## Whether It's Working

These questions reveal whether the system holds, not just whether it was defined.

**Does hierarchy read without color?** Cover the screen and remove color mentally. Can you still rank elements by importance? If hierarchy only works because blue means "important," it breaks in grayscale, in low vision, in screenshots.

**Does weight track what matters?** The heaviest weight on screen should be on the most important content. If something decorative or structural is bolder than the primary action or value, the signal is inverted.

**Do same-role elements look the same?** Every label, every body paragraph, every heading at the same level — if they're visually identical, the system is working. If you can tell which component built them, it isn't.

**Does the type fit the product?** If you swapped in a generic system font, would the product feel different? If the answer is no, the type choice wasn't a decision.

---

## Reference Values

These are defaults worth reaching for, not rules worth defending.

**Scale:** 5 levels cover most products — caption, secondary, body, subheading, heading. Ratio: 1.25 for dense tools and apps, 1.333 when headings need more presence, 1.5 for expressive or marketing contexts. App UIs want a fixed rem-based scale — fluid sizing (`clamp()`) makes sense for marketing headings, not for interface labels.

**Measure:** `max-width: 65ch` on body containers. Below 45ch lines break too often. Above 80ch the eye loses the return. Labels and headings don't need measure constraints — paragraphs do.

**Line-height:** 1.1–1.2 on headings (tight reads as confident). 1.5–1.7 on body (open reads as readable). Go slightly looser on light-on-dark — dark backgrounds compress apparent spacing.

**Details that compound:** `tabular-nums` on any number that shares a column with another number. Letter-spacing slightly open on uppercase and small caps, tight-to-default on display. Token names that mean something (`--text-body`, not `--font-16`) — the name is the contract.
