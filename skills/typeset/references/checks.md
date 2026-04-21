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
