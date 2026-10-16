## Context

Signal Desk is a production-close operations queue for inspecting requests, finding waiting work, previewing replies and exporting records. Staff may be moving quickly between requests; lost ownership context or unreachable controls costs time and risks missed handoffs.

## First impressions

The desktop page feels orderly: a clear title, bordered request and reply panels, readable status labels and a separate next-action panel. Green and amber distinguish statuses with words as well as color. Mobile loses that confidence: the page extends beyond the viewport, cutting off filters and actions. Keep the established visual direction; the urgent work is making its existing tasks dependable.

## Findings

**Mobile actions fall outside the usable page.** At a 390px viewport, the measured document is 806px wide. The initial capture cuts through the table and omits its actions; the bottom capture still lacks the preview button, measured at x=643–773px. Source overrides force `.embed-inner` to a 720px minimum width and horizontal layout, while `.preview` hides overflow. The grid item's content sizing also needs attention: wrapping the toolbar alone will not restore the page width. Allow the main grid column and its children to shrink, restore the preview's mobile stack and confine any necessary table scrolling to the table. Verify both the panel contents and their placement in the whole page. Staff should reach every task without panning the entire interface.

**The first request excludes keyboard users.** “North wing access” uses a clickable `div`, confirmed as tabIndex −1, while the second row uses a button. It also appears as plain text beside the second row's outlined action. Replace it with the same native button so both requests offer the same visible affordance, keyboard activation and focus treatment. The existing shared focus outline is worth preserving.

**Filtering removes the promised owner.** The waiting capture and measurements confirm `ownerHidden: true`; `filter(on)` explicitly hides the owner along with the first request. This contradicts both the page's instruction to keep the next owner visible and Help's claim that waiting filters retain the owner. Keep Morgan Lee visible while filtering. The resulting height change comes partly from removing that 48px minimum-height owner row, not merely from text wrapping. The separate 32px status slot reserves feedback space; preserve that useful stability rather than removing all apparent whitespace.

**Preview feedback does not deliver a preview.** The supplied click handler only writes “Preview ready: North wing access.” into the status paragraph in the requests panel. It neither opens reply content nor changes the preview panel. For someone checking a reply, that reports completion without providing the thing to inspect. Show the reply in the panel or an accessible dialog, with feedback beside the action. The supplied source cannot establish whether a fuller reply exists elsewhere.

**Export looks unavailable despite being active.** Its 12px label and pale text on pale fill make it resemble a disabled control, although its handler creates a CSV. The supplied RGB pair yields approximately 2:1 contrast, below normal-text requirements. Give this enabled action readable neutral styling consistent with the other controls. Typography otherwise supports scanning: the shown page uses four sizes (12/16/18/28px), three weights and five text colors; the system sans, short copy and heading hierarchy fit an operations tool.

## User context and top opportunities

A hurried operator needs confidence about who owns the queue and what each action accomplished. First restore mobile reachability and keyboard access, then retain ownership through filtering and make preview completion tangible. These changes preserve the page's calm composition while addressing the points where it currently makes staff hesitate or work around it.

This review uses supplied captures, source and measurements. I did not run keyboard, screen-reader, download or native dialog/popover tests. Bundled data requires no network loading state; network failure behavior is outside this example.

## Sources inspected

Staff Designer: `/tmp/alan-os-designer-blind-packages/v2/SKILL.md`, `critique.md`, `references/interaction.md`, `references/checklists.md`, `references/typography.md`.

Artifact directory: `/tmp/alan-os-staff-designer-stage/tests/scoped-review/`. Read `artifact-request.txt`, `case-42.html`, `artifacts/case-42-measurements.json`; visually inspected `artifacts/case-42-desktop.jpg`, `case-42-mobile.jpg`, `case-42-mobile-bottom.jpg`, `case-42-mobile-waiting.jpg`.
