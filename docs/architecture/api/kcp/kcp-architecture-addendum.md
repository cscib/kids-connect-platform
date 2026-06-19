KCP Architecture Addendum

1. Contact Approval Flow
- System event starts when another parent initiates a contact request.
- Parent receives a push notification or alert badge; no approve/reject action is available from the notification.
- Parent opens request detail to review requesting child's first name, avatar, and household name only.
- Parent may dismiss for later; dismissed requests remain in alerts for 30 days.
- Parent may approve or reject.
- Reject is private, neutral, and consequence-free; the requesting family receives only a neutral acceptance-failure message.
- Approve requires a selected permission level.
- Permission levels: Challenge only, Learning companion, Future chat enabled (placeholder in V1).
- On confirm, the approved contacts graph is updated immediately and both parents are notified neutrally.
- Parent dashboard shows the new contact and allows edit or revoke.

2. Permissions Management Flow
- Parent-initiated action from dashboard.
- Parent selects child, then contact, then a new permission level.
- Current permission level is read silently by the system to determine upgrade or downgrade.
- Same-level selection is blocked.
- Upgrade: single confirm.
- Downgrade: stronger confirmation with two-step acknowledgment.
- Update is immediate, logged in both parent activity logs, and reflected in the approved contacts graph.
- Other parent receives a neutral notification that the permission level changed.
- Parent returns to contact list and then dashboard.

3. Alert and Activity Review Flow
- System detects unusual activity automatically via safety rules.
- Alert is classified as Informational, Warning, or Action required before notification.
- Parent gets a severity-matched notification, but not the detailed incident.
- Parent opens alert detail with severity, description, timestamp, affected child, and contact involved if relevant.
- Parent may dismiss, block contact, revoke permission, or pause child account if severity is Action required.
- Dismiss marks alert reviewed and resolved.
- Block removes the contact immediately and permanently.
- Revoke routes into the Permissions Management Flow.
- Pause suspends social and challenge features but keeps learning active.
- All actions are written to the activity log.

4. Revoke Contact Flow
- Parent opens child's contact list and selects a contact.
- Revoke is immediate and does not notify the removed family.
- Any pending unseen challenges from that contact are removed.
- Approved contacts graph is updated immediately.
- Parent activity log records the event for audit.

5. Implementation Notes
- Parent-facing notifications must remain neutral and low-detail.
- Child-facing rejection or block reasons are never shown in V1.
- All graph updates, pauses, blocks, and revocations are background actions that must not fail silently.
- Resolved alerts remain visible for 30 days.
- Contact requests and alert items should support deferred review.
- Permission changes need explicit audit history and timestamping.
