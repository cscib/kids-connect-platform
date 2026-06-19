Maltese Quest V1 — Architecture Addendum

1. Shared Flows
1.1 Child Login Flow
- App opens.
- Profile picker shows child profile cards.
- Child selects profile.
- If PIN exists, child enters PIN.
- If no PIN exists, parent-approved entry path is used.
- Child lands on quest map.
- First-time experience flag is handled separately and cleared only after quest map unlock.

1.2 Lesson Flow
- Child opens quest map.
- Selects an available lesson node.
- Enters activity sequence with match, tap, listen, and speak activities.
- Completes lesson.
- XP and reward animation play.
- Child returns to quest map with progress updated.

1.3 First-Time Child Experience Flow
- On first launch, system detects a new child profile.
- Benni introduces the experience before any security or lesson step.
- Child still follows the normal login path.
- First-time tutorial sequence appears once.
- Flag clears on quest map unlock, not before.

2. MQ Product Flows
2.1 Speaking Practice Flow
- Child reaches first speak activity.
- App checks microphone permission status before showing any UI.
- If permission already granted, child goes directly to record screen.
- If permission not yet asked, child sees a pre-permission explanation screen before the native device dialog.
- If permission is permanently denied, child sees a denial explanation and fallback guidance.
- Child records voice, hears playback, and can retry.
- Incorrect or denied states never shame the child.
- Fallback activity is available so lesson completion remains possible.

2.2 Contact Request Initiation Flow
- Child sees invite-a-friend prompt from one of several entry points.
- Child chooses from suggestions or asks a grown-up to help.
- Child cannot enter contact details independently.
- Parent-assisted entry screen collects contact details.
- System creates a contact request object.
- Request must be approved by the requesting parent before being sent.
- Receiving parent then approves or rejects.
- If approved, both children can exchange challenges.

2.3 Send Challenge Flow
- Child opens challenge inbox or starts from quest map.
- Child selects approved contact.
- System checks permission level in the background.
- If challenge sending is allowed, child selects a preset prompt.
- Child records a challenge and submits it.
- Challenge is packaged as a challenge object.
- Both parents receive a background notification.
- Child sees a confirmation and returns to the map or inbox.
- If the contact is blocked or not permitted, child is routed to a fallback path silently.

2.4 Receive and Respond to Challenge Flow
- Child opens challenge inbox or notification.
- Child plays the sender's recording.
- Child records a response.
- Child reviews and submits.
- A preset reaction is sent to the original challenger in the background.
- XP is awarded and the child returns to the map or inbox.

2.5 Reward and Badge Flow
- Lesson or challenge completion triggers XP calculation.
- XP animation is shown.
- Badge unlock is evaluated in parallel.
- Minor routine completions get a small Benni reaction.
- Badge unlock gets a stronger celebration.
- Milestone completion may unlock a narrative moment.
- Full rewards screen is optional and browsable, not forced.

2.6 Progress Review Flow
- Parent opens dashboard.
- Parent selects a child if the household has more than one profile.
- Parent reviews lesson completions, speaking history, streak and XP summary, and badges.
- Parent can drill into detail screens for each section.
- Child-facing emotion or character framing is absent.
- Analytics data comes from shared infrastructure.

2.7 Streak and Return Flow
- System detects return after absence.
- Benni greets the child before streak information is shown.
- System checks whether streak is maintained or reset.
- Child sees the result in a confidence-preserving way.
- Parent can review streak history in the progress dashboard.

3. KCP Platform Flows
3.1 Parent Onboarding and Child Access
- Parent account is created.
- Consent is recorded.
- Household and child profile records are created.
- Child PIN or parent-approved entry is configured.
- Child login uses the same profile model.
- Tokens must support future federation with Kids Connect.

3.2 Contact Approval Flow
- A system event creates a pending request.
- Parent receives a neutral notification or sees a dashboard badge.
- Parent opens request detail.
- Parent can review limited details in V1.
- Parent approves or rejects.
- Reject is private and consequence-free.
- Approve requires selecting a permission level.
- Confirmation updates the approved contacts graph immediately.
- Requesting family gets a neutral acceptance notification.
- Parent dashboard shows the new contact afterward.

3.3 Permissions Management Flow
- Parent opens dashboard and selects a child.
- Parent opens a contact card.
- System notes current permission level silently.
- Parent selects a new level.
- Same-level changes are blocked.
- Upgrade uses a simpler confirm step.
- Downgrade uses a stronger confirm step.
- Updated permission is written to the graph and both parent logs.
- Other parent gets a neutral notification.

3.4 Alert and Activity Review Flow
- Safety rules trigger an alert.
- Alert is classified into informational, warning, or action required.
- Parent gets a matching notification.
- Parent opens alert detail.
- Parent can dismiss, block contact, revoke permission, or pause the child account where allowed.
- Alerts stay unresolved until action is taken.
- Blocking and pausing must execute immediately.
- Revoke permission routes into the permissions flow.

3.5 Revoke Contact Flow
- Parent opens contact list.
- Parent selects a contact.
- Parent confirms revocation.
- Contact is removed immediately.
- Pending challenges from that contact are removed.
- No reason is shown to the removed family.
- Activity log records the action for audit.

4. Shared System Events
- SHSYS handles push notifications, email delivery, and shared event logging.
- PSYS handles neutral system-side processes like graph updates, approval notifications, permission updates, and reaction notifications.
- MQ and KCP must not directly access each other’s databases.
- Background updates must never fail silently.
- Retention and premium gating still need final policy decisions.

5. Implementation Rules
- Parent-facing notifications remain neutral and low-detail.
- Child-facing rejection or block reasons are never shown in V1.
- All graph updates, pauses, blocks, and revocations are background actions.
- Challenge-scoped recording access is mandatory.
- First-time and streak logic must be session-safe and profile-scoped.
- Parent review of recordings remains a product decision, not a UI-only gate.
- Benni never appears on parent screens.

6. Remaining Open Questions
- Voice recording retention: temporary or permanent.
- Absence threshold for streak reset.
- Two-parent co-management rules.
- Parent challenge-review entitlement.
- Sibling account handling in V1.
- Free versus premium feature boundary.
- Event retention by type.
- Hosting region and cloud provider choice.
- Exact curriculum mapping source.
