## Signal Desk assignment flow

This implementation plan needs its recovery behavior settled before build. Coordinators must hand a waiting request to an available colleague while moving between desktop, mobile and interruptions. Losing a reply costs them time; an assignment shown as complete before confirmation can leave a request unattended. The existing palette, type and navigation are settled constraints.

The proposed sequence is compact: open the request, edit a reply, choose a colleague, assign. Its intended feeling is quick completion. The specified behavior would instead create false certainty: the panel disappears and the queue says “Assigned” before the server has accepted anything. These are concerns in the plan, not observed defects in a built interface.

### Questions and bounded defaults

**Persistence: what does “leave and return” cover?** The promise directly conflicts with the proposed state lifetime. Reply and assignee live only in the panel; closing it or leaving the route unmounts it and clears both. Reopening reads saved server values. Decide whether the promise includes refresh, closing the browser and returning on another device. As a minimum default, retain a draft keyed to this request and coordinator outside the panel, restore it on return, and clear it only after confirmed success or explicit discard. Navigation alone should not discard it. The durable storage choice still needs agreement; moving state to a mounted parent would cover panel closure but would not establish refresh or cross-device survival. Show “Draft saved” only when the chosen persistence mechanism has actually saved it.

**Transparency: when is an assignment complete?** Default to keeping the panel open with “Assigning…” and a matching pending queue state until the server confirms success. Then close it and show the confirmed assignee in the queue. This gives immediate feedback without asking a coordinator to treat an unconfirmed handoff as finished. If leaving during submission is allowed, the pending operation and its eventual result must remain reachable from the queue.

**Forgiveness: what prevents a second handoff?** The plan explicitly leaves Assign enabled during the call, and duplicate requests can send duplicate notifications. Disable repeat submission immediately and retain the in-flight state across panel reopening. Server-side duplicate protection is also needed for retries or lost responses; a disabled control alone does not cover those cases. Confirm what protection the assignment endpoint supports before settling the retry behavior.

**Failure recovery: what should the coordinator do next?** A toast can announce a failure, but an interrupted person can miss it, and the panel has already gone away. Default to a persistent error beside the assignment controls, with the reply and assignee intact and a clear retry action. Distinguish a definite rejection from an unknown outcome after a timeout. For an unknown outcome, check the request’s current assignment before retrying so the recovery action does not generate another notification. Define what happens if the selected colleague is no longer available when submission reaches the server.

**Escape and correction: what does closing mean?** Let closing or Back preserve the draft. Keep “Discard draft” explicit and separate. Once submission starts, do not label closing the panel “Cancel” unless it actually cancels the server operation. After confirmation, can a mistaken assignee be changed, and what happens to the original notification? That remains unresolved; use an existing reassignment path if one exists, rather than promising undo without known support.

**Craft and mobile: what still needs verification?** Keep the existing visual system. “Small title” alone does not establish weak hierarchy, and no evidence supports claims about contrast, spacing or typography. At implementation, verify that request identity, reply, assignee and action remain legible with the mobile keyboard open; define accessible labels, pending/error announcements, keyboard close behavior and focus return. If the panel is modal, define its focus containment too.

The highest-value next step is to agree on draft lifetime, authoritative assignment status and safe failure recovery. Those decisions let this flow feel dependable when a coordinator’s attention moves elsewhere.

### Sources inspected

`/tmp/alan-os-staff-designer-stage/tests/scoped-review/case-63.md`; `/tmp/alan-os-designer-blind-packages/v3/SKILL.md`; its `critique.md`, `references/interaction.md`, `references/checklists.md`, and `references/typography.md`. No built screen, screenshot or implementation was supplied or inspected.
