# Signal Desk: assignment flow plan

This is an implementation plan awaiting review, not a built screen. Review it as a staff designer. Do not implement it or invent screenshots.

Operations coordinators assign a waiting request to an available colleague. They work on desktop and mobile, often interrupted. Keep the existing Signal Desk palette, type and navigation. The scope is one assignment flow, not a portfolio redesign.

## Proposed flow
1. Open a request from the queue.
2. Edit the request's reply and choose an assignee in a side panel.
3. Click Assign. The panel closes immediately, the queue says Assigned, and the server request begins.
4. If the server fails, show a toast. No retry or reconciliation design is specified.

## State and navigation
The headline promise is: users can leave and return without losing edits.
The proposed implementation keeps reply and assignee in the side panel's local component state. Closing or leaving the route unmounts the panel and clears this state. The next open begins with the saved server values. There is no draft write until Assign is clicked.

## Interaction details
The Assign control remains enabled while the network call is in flight. Duplicate requests can create duplicate handoff notifications. No cancellation or in-flight state is designed yet.

The plan calls for a small title, reply field, assignee selector and Assign control. Screenshots, dimensions, rendered color values and final visual composition are not available yet. No decision has been made about preserving edits on close, distinguishing pending from confirmed assignment, or recovering from failure.

Please identify unresolved decisions and propose bounded defaults where the plan supports them. Do not evaluate unprovided visual details as observed defects.
