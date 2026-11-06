Signal Desk has a clear desktop structure, but the supplied build needs corrections before release on mobile and for keyboard users. This is a production-close operations queue: staff need to inspect requests, identify waiting work and check replies without losing ownership context. Mistakes here cost time and confidence in the queue.

The desktop capture feels orderly. The title leads into the request table, status labels combine words with color, and the reply panel follows below. The bordered panels and floating help treatment fit the stated direction. On mobile, that order breaks: the page extends sideways, leaving essential controls outside the initial view.

**Make the mobile page fit before refining its spacing.** At a 390px viewport, the measured document width is 806px. The initial capture cuts off status information and request actions, while the filters sit beyond the visible right edge. The source forces `.embed-inner` to a minimum width of 720px, overriding its mobile column layout; the grid also lacks a constraint that lets its content shrink. Contain the grid, restore the stacked preview and keep any necessary table scrolling inside the table region. Staff should be able to read a request and reach its action without moving the entire page sideways.

**Give both request actions the same accessible behavior.** “North wing access” uses a clickable `div`; “Loading dock schedule” uses a button. The first action has a measured tab index of −1 and no keyboard handler or button semantics. Visually, it also looks like ordinary text beside an outlined control that performs the same job. Use native buttons for both. This fixes a keyboard access blocker and makes the interaction predictable.

**Keep ownership visible when filtering.** Both Waiting controls invoke `filter(true)`, which explicitly hides the queue owner. The waiting-state receipt confirms this. That contradicts the page’s promise to “keep the next owner visible” and the help text saying filters retain the owner. Preserve Morgan Lee’s ownership row while changing the request list. Staff should not have to clear a useful filter to recover assignment context.

**Make “Preview reply” show something staff can inspect.** Its handler only writes “Preview ready: North wing access.” into the queue’s status region; it neither reveals reply content nor opens a preview. The existing preview box contains a readiness label and request name, rather than the reply. Show the actual reply in that panel or an accessible dialog, with a clear return path. A completion message cannot support the promised check.

**Let Export CSV look available.** The enabled export button has 12px text in `#93a59b` on `#d8e4e0`, approximately 1.99:1 contrast, and appears disabled in the desktop capture. Restore readable text contrast and the established neutral action treatment. It need not become the dominant action to be discoverable.

The system font suits a scanning task. Four declared text sizes—12, 16, 18 and 28px—and three weights provide a workable hierarchy; five visible text colors distinguish content, supporting copy, statuses and export. The main typography opportunity is the export label, rather than replacing the type system. Likewise, the existing panel and status vocabulary can stay.

For staff moving quickly, the desktop offers calm orientation, but mobile cropping and inconsistent actions introduce hesitation at the moment they need to act. The highest-impact work is to restore mobile access, keyboard access and truthful preview behavior, then preserve ownership and correct export contrast.

These conclusions combine the supplied captures, measurements and source inspection. I did not run the page, test assistive technology, verify downloaded CSV contents or inspect an opened dialog. Network loading and failure behavior cannot be assessed from this bundled-data example.

Sources inspected: supplied request; `case-42.html`; all four case-42 captures; case-42 measurements in `capture-receipts.json`; Staff Designer skill, critique methodology, interaction principles, checklists and typography reference.
