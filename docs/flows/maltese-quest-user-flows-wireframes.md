# Maltese Quest V1
# User Flows and Wireframes

## Purpose

This document defines the first-product user flows and low-fidelity wireframe structure for Maltese Quest V1. It is meant to support design, development, and parent-pilot testing by showing the critical path for both the parent and child experiences. User flows should stay simple and focused on one goal at a time, especially for a child-directed product with parent-controlled onboarding.

## Product goals

- Enable a parent to create and supervise a child account.
- Let a child complete short Maltese learning sessions on desktop and mobile.
- Support challenge-based voice recording exchange with approved contacts.
- Keep the child experience playful, warm, and quest-like.
- Preserve a reusable structure for the future Kids Connect platform.

## Key design principles

- One flow, one goal.
- Parent-first onboarding.
- Clear separation between adult controls and child actions.
- Minimal steps for the child.
- Quiet, supportive feedback over noisy reward bursts.
- Responsive layouts for both desktop and mobile.

## Personas

### Parent
The adult who owns the account, grants consent, creates the child profile, approves contacts, and monitors progress.

### Child
A child aged 7–9 who logs in to complete lessons, record short spoken answers, and send or receive challenge-based practice from approved family or friends.

## Flow 1: Parent onboarding

### Goal
Create the parent account and establish consent before any child profile can be activated.

### Entry point
App landing page or invite link.

### Steps
1. Parent opens app.
2. Parent sees clear explanation of product purpose.
3. Parent signs up.
4. Parent completes consent and verification step.
5. Parent creates household.
6. Parent creates child profile.
7. Parent reaches dashboard.

### Decision points
- Does the parent agree to the terms and consent flow?
- Does the parent want to add a second guardian?
- Does the parent want to create the child profile now or later?

### Success state
Parent is able to access the dashboard and manage child settings.

## Flow 2: Contact approval

### Goal
Let the parent approve who the child can interact with.

### Entry point
Parent dashboard.

### Steps
1. Parent opens contacts screen.
2. Parent chooses add contact.
3. Parent enters or selects a trusted family/friend contact.
4. Parent assigns permission level.
5. Parent approves relationship.
6. System logs approval.
7. Contact becomes available for challenge exchange.

### Permission levels
- Learning-only.
- Challenge-only.
- Follow / broader contact access for later versions.

### Success state
Approved contacts appear in the child’s safe network.

## Flow 3: Child login and map

### Goal
Let the child enter the app and start a lesson with minimal friction.

### Entry point
Child profile picker.

### Steps
1. Child opens app.
2. Child chooses profile or is auto-signed in from the parent device.
3. Child lands on the home quest map.
4. Child sees current island/section and next task.
5. Child taps a lesson node.
6. Lesson screen opens.

### Success state
Child is ready to start a 3–5 minute session.

## Flow 4: Lesson completion

### Goal
Guide the child through a small learning loop.

### Entry point
Selected lesson node.

### Steps
1. Mascot welcomes the child.
2. Child completes tap, listen, match, reorder, or repeat task.
3. Child reaches speaking step if included.
4. System gives feedback.
5. Lesson ends with progress update.
6. Child returns to map.

### Success state
Lesson node completes and a reward/progress signal is shown.

## Flow 5: Speaking challenge

### Goal
Let the child record a short spoken answer or challenge response.

### Entry point
Lesson step or challenge inbox.

### Steps
1. Mascot frames a mission.
2. Child hears or reads the prompt.
3. Child records a short answer.
4. System plays back the recording or stores it in the challenge.
5. Child receives response feedback.
6. Challenge may be sent to an approved contact.

### Rules
- Recording is short.
- Only preset prompts are allowed in V1.
- No open chat or free conversation.

### Success state
A completed speaking challenge is stored and linked to the correct lesson or contact.

## Flow 6: Friend challenge exchange

### Goal
Allow a child to send or receive a structured language challenge.

### Entry point
Approved contact card or challenge inbox.

### Steps
1. Child opens approved friend or relative.
2. Child selects available challenge.
3. Child records response.
4. System attaches recording to challenge thread.
5. Approved contact receives the challenge.
6. Contact responds inside the same challenge object.

### Success state
Challenge exchange is completed with only parent-approved contacts.

## Flow 7: Parent review and alerts

### Goal
Keep the parent informed and in control.

### Entry point
Parent dashboard notification or activity screen.

### Steps
1. Parent receives alert about new contact request or unusual activity.
2. Parent opens alert.
3. Parent reviews context.
4. Parent approves, rejects, or revokes access.
5. System logs the decision.

### Success state
Parent remains the authority for access and communication.

## Flow 8: Recovery after absence

### Goal
Re-engage the child without guilt or shame.

### Entry point
Child returns after a gap.

### Steps
1. Child opens app.
2. Mascot greets child warmly.
3. App offers a small easy win.
4. Child resumes with a short task.
5. Progress updates quietly.

### Success state
Child feels welcome back and can re-enter the learning loop.

## Parent wireframe structure

### 1. Landing / sign-up
- Product name.
- One-line value proposition.
- Parent CTA.
- Safety explanation.

### 2. Consent and household setup
- Adult verification.
- Consent text.
- Household creation.
- Optional second guardian.

### 3. Child profile creation
- Child name.
- Avatar selection.
- Age band selection.
- Permission defaults.

### 4. Dashboard
- Child progress summaries.
- Contact approvals.
- Alerts.
- Recent activity.

### 5. Contacts and permissions
- Approved contacts list.
- Permission levels.
- Revoke access.
- Add new contact flow.

### 6. Alerts and activity
- Contact request alerts.
- Unusual activity notices.
- Challenge history.
- Optional recording history.

## Child wireframe structure

### 1. Profile picker
- Avatar button.
- Child name.
- Simple sign-in affordance.

### 2. Quest map
- Current path.
- Completed nodes.
- Next lesson highlighted.
- Reward indicators.

### 3. Lesson screen
- Mascot area.
- Instruction text.
- Task area.
- Audio controls.
- Progress bar.

### 4. Speaking challenge screen
- Prompt text.
- Record button.
- Replay button.
- Submit button.
- Encouraging mascot feedback.

### 5. Inbox
- Approved friend or family challenge list.
- New challenge cards.
- Completion status.

### 6. Progress screen
- Badges.
- Streak or practice history.
- Lesson map completion.
- Encouraging summary.

## Desktop layout notes

- Left side can hold navigation or map context.
- Main area should hold lesson content and mascot.
- Child tasks should stay centered and large enough for mouse use.
- Parent dashboard should use more information density.

## Mobile layout notes

- Navigation should collapse into simple tabs.
- One primary action per screen.
- Large buttons and readable text.
- Mascot and prompt should remain visible above the fold.

## Accessibility notes

- Keyboard navigation must work.
- Focus states must be visible.
- Reduced-motion mode must suppress unnecessary animation.
- Audio cues must have text equivalents.
- Contrast must remain readable in light and dark themes.

## Critical path summary

### Parent critical path
Landing -> consent -> household -> child profile -> contact approval -> dashboard.

### Child critical path
Login -> quest map -> lesson -> speaking challenge -> reward -> return to map.

### Social critical path
Parent approves contact -> child sends challenge -> approved contact responds -> parent can review if needed.

## Open questions for design review

- Final mascot placement on map and lesson screens.
- Whether the child home screen shows one main quest or multiple islands.
- Whether challenge inbox is a tab or a map overlay.
- Whether rewards appear as stars, XP, gems, or story fragments.
- Whether parent dashboard includes a daily summary by default.

## Wireframe handoff notes

This document is intentionally low-fidelity. It should be used to create first-pass wireframes in Figma, Miro, or similar tools. Each flow should be prototyped with one goal and one success state before adding more branches.
