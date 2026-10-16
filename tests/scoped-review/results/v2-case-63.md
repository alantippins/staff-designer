## Signal Desk assignment flow

This is an implementation plan for coordinators assigning waiting requests on desktop and mobile. They are often interrupted; success means returning to their work and knowing whether a colleague actually received the handoff. Losing a reply costs repeated work. Reporting an assignment too early risks a waiting request being treated as handled.

The proposed sequence is compact: open a request, edit its reply, choose someone, then Assign. Its immediate closure promises certainty that the server has not yet earned. The main work before implementation is settling persistence, submission and recovery behavior. There is no rendered interface here, so visual hierarchy, typography, contrast and spacing remain unassessed.

### Unresolved decisions and bounded defaults

**Persistence: what does “leave and return” cover?** The plan explicitly clears reply and assignee when the panel unmounts, and reopening restores server values. That contradicts the headline promise even for closing and reopening the panel. Default to restoring both edits for the same request after panel closure and route navigation, without assigning it. Decide explicitly whether refresh, browser closure and another device are also covered. Choose the draft lifetime and ownership before choosing storage; the supplied plan does not establish an existing draft mechanism. Clear a draft only after confirmed submission or an explicit discard. Make any “Draft saved” message reflect actual durability, so an interrupted coordinator can trust it.

**Transparency: when is the assignment real?** The queue says Assigned before the request begins. This gives the coordinator a false completion signal if the request fails. Default to keeping the panel open with “Assigning…” until confirmation, then closing it and updating the queue. If leaving during submission is allowed, retain a visible pending status on the request and reconcile it when they return. Pending and confirmed must remain distinct wherever the request appears.

**Forgiveness: what counts as one submission?** Assign remains enabled during the call, and the plan says duplicate requests can produce duplicate notifications. Default to disabling repeated submission while pending and showing progress immediately. Also require duplicate protection at the operation boundary: a disabled button alone cannot settle retries or an uncertain network result. The contract for recognizing one handoff is an implementation decision still to resolve.

**Recovery: how does the coordinator finish after failure?** A toast alone offers neither a durable place to recover nor a specified next step. Default to preserving the edited reply and assignee, showing a persistent error beside the action and offering Retry when failure is confirmed. If the connection drops without a definitive result, check the assignment before inviting another submission. Reconcile the queue with confirmed server state; never leave Assigned standing after a confirmed failure. A toast can supplement that recovery surface.

**Escape and correction: what does closing mean?** Distinguish closing the editor from discarding a draft, and leaving a pending operation from cancelling it. Default to allowing departure with preserved work; do not label departure “Cancel assignment” unless cancellation is supported. Separately decide how a coordinator corrects a confirmed wrong assignee. Reassignment may be enough, but its notification consequences are unspecified; an Undo promise would be premature.

**Craft across devices.** Retain Signal Desk’s palette, type and navigation. At implementation, establish labelled controls, keyboard access, focus return after closing, announced pending/error states and a mobile layout that keeps the reply, assignee and action usable with the keyboard open. These are acceptance questions, not observed defects. The phrase “small title” alone does not establish a hierarchy problem.

The strongest opportunity is a complete interrupted journey: edit, leave, return, submit once, encounter failure and recover without retyping or guessing who owns the request. Review that sequence before visual polish; it directly tests the promise this flow makes.

### Sources inspected

Read the supplied `case-63.md`, plus `/tmp/alan-os-designer-blind-packages/v2/SKILL.md`, `critique.md`, `references/interaction.md`, `references/checklists.md` and `references/typography.md`. Evidence is limited to the supplied plan; no implementation or rendered screens were available.
