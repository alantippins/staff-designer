## Context

Signal Desk is a production-close queue for operations staff inspecting requests, finding waiting work, previewing a reply and exporting the queue. Someone moving through this between other tasks needs confidence about which request they are acting on; a context mistake costs time and could produce the wrong reply.

## First impressions

The page feels calm and legible. The title leads into a bordered request panel, with readable green and amber statuses, a separate reply preview and a short next-action panel. Those borders explain grouping; the shadow reserved for floating help serves a different role. Keep this visual direction. The supplied evidence supports a focused refinement pass, rather than a broad redesign.

## Findings

**Keep the reply's context explicit when filtering.** The waiting capture shows only “Loading dock schedule” in the queue, while the reply panel still presents “North wing access.” The source confirms that filtering hides the first row without changing the preview, and its dialog always opens the north-wing reply. The request name remains visible, so this is not a falsely labeled reply. Nevertheless, a hurried operator can reasonably expect the preview beneath a filtered queue to relate to that queue. If this is intentionally an independent preview, label that relationship, for example “Reply preview: North wing access,” with a brief indication that it sits outside the current filter. If it is meant to follow the request being inspected, connect that selection explicitly. The intended relationship is not established by the supplied request.

**Give waiting work a more direct route on mobile.** Desktop puts “Next action” beside Requests. On mobile it follows the entire reply panel; the lower capture only reaches the beginning of that section. The toolbar's Waiting button already makes filtering reachable, so the workflow is not blocked. There is an opportunity to place the short explanation beside that filter, where someone deciding what to do next can use it immediately. Preserve the existing filter rather than adding another action.

**The responsive behavior holds.** The mobile document measures 390px wide at a 390px viewport, and the lower capture shows the preview button fully reachable. Its measured height is approximately 44px. The preview stacks its text and button at the mobile breakpoint. The change in queue height under Waiting follows the removal of a request row and the appearance of status text; the owner remains visible. There is no evidence here of a lost owner or an unreachable preview.

**Typography and feedback support scanning.** The source uses system-ui with three explicit sizes, 16/18/28px, and weights of normal, 600 and 700, plus native heading/strong bold. Main text, muted explanation, status labels and inverse action text have distinct color roles. Heading size and weight establish hierarchy without depending on color; short copy and consistent line spacing keep the rhythm comfortable. Buttons have visible focus styling, filters expose pressed state, and the status region announces filter/export feedback. Native dialogs provide a sound starting point for modal interaction.

## User context and top opportunity

The page respects an operator's attention through stable ownership, named requests and plain actions. The highest-value refinement is clarifying what the reply preview belongs to after filtering. Bringing the waiting explanation closer to its mobile control is secondary.

These conclusions cover supplied captures and source inspection. I did not exercise keyboard/focus behavior, assistive technology, the dialogs or an actual downloaded CSV. The local-data example does not establish network failure handling, persistence or behavior with a larger queue.

## Sources inspected

Read the supplied artifact request, case-17.html and artifacts/case-17-measurements.json; visually inspected case-17-desktop.jpg, case-17-mobile.jpg, case-17-mobile-bottom.jpg and case-17-mobile-waiting.jpg. Applied the supplied Staff Designer SKILL.md, critique.md, and interaction, checklists and typography references.
