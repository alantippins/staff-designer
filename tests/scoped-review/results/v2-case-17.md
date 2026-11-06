## Context

Signal Desk is a production-close operations queue for inspecting requests, filtering waiting work, previewing a reply and exporting. Staff are likely scanning between other tasks; unclear request context costs time and risks reviewing the wrong reply. The existing panel, help and status treatments are intentional and worth preserving.

## First impressions

The page feels calm and legible. A clear title leads into bordered request and preview panels, with green and amber labels separating readiness from waiting. Desktop keeps guidance alongside the queue; mobile preserves readable controls by stacking the page. The strongest opening is to make the relationship between the queue and reply preview equally clear.

## Findings

**Make the preview’s scope explicit.** In the supplied Waiting capture, Loading dock schedule is the only visible request, while the next panel still offers a North wing access reply marked “Ready for review.” Source confirms that filtering only hides the first table row; opening either request does not change the fixed preview (`case-17.html:1`). The request name prevents complete ambiguity, but a hurried operator still has to infer why an excluded request remains here. If this is an intentionally pinned reply, label the panel “Pinned reply: North wing access” and explain that it remains across filters. If it is meant to follow the inspected request, connect it to that request and show an explicit state when no reply exists. Which model is intended is not established by the supplied material.

**Name who is expected to reply.** “Waiting requests need a reply before they can be assigned” leaves responsibility unresolved. The loading dock dialog’s source is more precise: Morgan is awaiting the delivery team’s reply. Bring that specificity into the queue or guidance, such as “Awaiting delivery team reply,” so staff can distinguish their next action from someone else’s obligation. This improves Transparency without adding a new workflow.

**Keep the mobile layout’s useful restraint.** The 390px measurements report a 390px document width and zero horizontal scroll. The bottom capture shows the preview button fully visible after scrolling; its measured height is approximately 44px. This is a reachable preview, not a clipped embedded control. Request names and “Open request” wrap, but remain readable. The owner stays present in Waiting, confirmed by both the capture and measurements. The shorter panel follows removal of a request row, rather than evidence of owner loss or unexplained wrapping. The owner’s 48px minimum slot and status region’s 32px minimum also reserve real space; do not remove those gaps indiscriminately.

**Typography and grouping support scanning.** The visible type uses three sizes, 16/18/28px, three weights, 400/600/700, and five text colors across body, supporting copy, export and status labels. System-ui fits a practical queue. Short measures, consistent text rhythm and weighted headings establish the necessary hierarchy. Bordered content and shadowed floating help serve different layers; their combination alone is no inconsistency.

## Top opportunities and limits

Clarify the preview’s relationship to the queue first, then expose who owes the waiting reply. Those changes would let a busy operator trust the page’s sequence without interpreting hidden relationships.

Source provides native modal dialogs with close forms, pressed filter states, visible-focus styling, a live status region and CSV export logic. I inspected those implementations but did not execute them. Dialog rendering, keyboard focus restoration, help placement, assistive-technology announcements and actual download completion remain unverified. Local bundled data makes a network-loading critique inappropriate here.

## Sources inspected

Read the supplied user request, complete `case-17.html` and `artifacts/case-17-measurements.json` under `/tmp/alan-os-staff-designer-stage/tests/scoped-review/`. Viewed `case-17-desktop.jpg`, `case-17-mobile.jpg`, `case-17-mobile-bottom.jpg` and `case-17-mobile-waiting.jpg` in that directory’s `artifacts/` folder. Applied `/tmp/alan-os-designer-blind-packages/v2/SKILL.md`, its complete `critique.md`, and its interaction, checklists and typography references.
