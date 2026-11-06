## Context

Signal Desk is a production-close queue for operations staff inspecting requests, filtering waiting work, previewing replies and exporting. A staff member moving quickly needs reliable access and visible ownership; failures cost time and confidence in handoffs. The established panels, floating help, neutral actions and status palette remain appropriate.

## First impressions

The desktop capture presents a clear title, a dominant requests panel, a reply preview below and a narrow next-action sidebar. Green and amber labels distinguish status without relying on color alone. It feels orderly on desktop, but the mobile captures replace that confidence with uncertainty: request names remain visible while filters, statuses and actions extend beyond the viewport.

## Findings

**Mobile task access is the first priority.** The supplied measurement records an 806px document inside a 390px viewport. The initial and vertically scrolled mobile captures both leave the preview action outside the visible area; its measured left edge is 643px. The horizontally shifted waiting capture exposes controls while losing the request names. Staff must pan between the item and its action. Source fixes `.embed-inner` at 720px after the responsive rules, overriding the intended mobile column, while grid items retain their automatic minimum sizing (`case-42.html:1`). Constrain the grid children, let the preview fit its container and restore the mobile stacking rule. Keep any necessary table scrolling within the table region. Simply clipping overflow would conceal the task.

**The first request is inaccessible by keyboard.** “North wing access” uses a clickable `div`; the other row uses a button. Measurements confirm the first action has `tabIndex: -1`, and source supplies neither keyboard handling nor button semantics (`case-42.html:1`). Visually, its plain text also lacks the neighboring action’s clear boundary. Use the same native button for both rows so keyboard users can inspect every request and everyone can recognize the action consistently.

**Filtering removes ownership.** The waiting capture and measurements show the owner hidden, and `filter(on)` explicitly sets `owner.hidden=on` (`case-42.html:1`). This contradicts both the introductory promise and the help text. It also removes a 48px minimum-height row, alongside hiding the ready request; the resulting height change is not merely text wrapping. Retain the owner across filters so the handoff context survives when staff focus on waiting work. The status announcement and pressed filter states are useful existing feedback.

**Preview feedback does not deliver a preview.** The handler only writes “Preview ready: North wing access.” into the queue’s status area; it reveals no reply content (`case-42.html:1`). On mobile that announcement sits above the preview panel. Show the reply beside its trigger or in an accessible dialog with a clear return path, so staff can actually check it before continuing.

**Export looks unavailable despite being enabled.** Its measured text and background colors produce approximately 1.99:1 contrast, below 4.5:1 for its 12px label. The muted fill resembles a disabled control, although its handler creates a CSV. Restore readable neutral-action contrast rather than changing the status palette. The captured page uses four type sizes, three weights and five text colors; the system sans, 28px title, 18px section headings and 16px content otherwise establish useful hierarchy and readable short text groups.

## User context and top opportunities

Preserve the calm grouping and explicit status words. First make each mobile task visible beside its context, then standardize request buttons, retain ownership and deliver the promised preview. These changes give a rushed operator confidence about what they can do and who owns the next step.

This review uses supplied captures, measurements and source. I did not operate the page, inspect open help/dialog states, verify downloaded file handling or test assistive technology. Bundled local data does not warrant speculative network-loading findings.

## Sources inspected

Staff Designer v3: `SKILL.md`, `critique.md`, `references/interaction.md`, `references/checklists.md`, `references/typography.md`. Fixture: `artifact-request.txt`, `case-42.html`, `artifacts/case-42-measurements.json`, and all four supplied desktop/mobile JPG captures, viewed directly.
