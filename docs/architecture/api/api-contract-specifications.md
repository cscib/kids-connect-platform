# API Contract Specifications

## 1. Conventions

### 1.1 Global rules
- Base path: `/v1`.
- Auth: `Bearer` access token unless an endpoint is marked public or internal.
- Parent tokens can access only their own household and children.
- Child tokens are scoped to one child profile and cannot access parent data.
- All mutation endpoints must be idempotent where retries are likely.
- All list endpoints use cursor pagination unless otherwise stated.
- All responses use JSON unless the endpoint explicitly returns binary or stream data.

### 1.2 Standard error object
```json
{
  "code": "STRING_CODE",
  "message": "Human readable message",
  "details": {},
  "requestId": "req_123"
}
```

### 1.3 Common status codes
- `200 OK` success.
- `201 Created` resource created.
- `204 No Content` successful empty response.
- `400 Bad Request` validation or malformed input.
- `401 Unauthorized` missing or invalid token.
- `403 Forbidden` authenticated but not allowed.
- `404 Not Found` resource not found or hidden.
- `409 Conflict` duplicate or state conflict.
- `422 Unprocessable Entity` domain rule violation.
- `429 Too Many Requests` rate limited.
- `500 Internal Server Error` unexpected failure.

### 1.4 Event naming
- Use dotted lowercase names, for example `contact.request.created`.
- Emitted events must include `eventId`, `eventType`, `timestamp`, `sourceService`, and `metadata`.

## 2. Identity and Consent Service

### POST /auth/signup
**Auth:** Public

Creates a parent account and sends verification email.

**Request**
```json
{
  "email": "parent@example.com",
  "password": "secret-password",
  "displayName": "Parent Name"
}
```

**Response 201**
```json
{
  "parentId": "par_123",
  "verificationRequired": true
}
```

**Errors**: `400 INVALID_EMAIL`, `409 EMAIL_EXISTS`, `422 PASSWORD_WEAK`

### POST /auth/verify-email
**Auth:** Public

Confirms email token and activates parent account.

### POST /auth/login
**Auth:** Public

Authenticates parent and returns access and refresh tokens.

### POST /auth/social
**Auth:** Public

Signs in with Google or Apple identity tokens.

### POST /consent/record
**Auth:** Parent token

Stores the consent record and stamps checkbox state, IP address, and timestamp.

### GET /consent/status
**Auth:** Parent token

Returns current consent state for the parent account.

### POST /auth/child-token
**Auth:** Parent token or approved parent path

Issues a child session token after PIN verification or parent approval.

### POST /auth/refresh
**Auth:** Refresh token

Rotates refresh token and returns new access token.

## 3. Parent and Child Profile Service

### POST /households
**Auth:** Parent token

Creates a household.

### GET /households/{householdId}
**Auth:** Parent token

Returns household detail for the caller’s own household.

### POST /households/{householdId}/children
**Auth:** Parent token

Creates a child profile under the household.

### GET /children/{childId}
**Auth:** Parent or child token

Returns child profile detail if authorized.

### PATCH /children/{childId}
**Auth:** Parent token

Updates child profile fields, including age band and avatar.

### POST /children/{childId}/pin
**Auth:** Parent token

Creates or updates the child PIN hash.

### POST /children/{childId}/pin/verify
**Auth:** Public or parent token depending on flow

Verifies PIN and returns child token.

### POST /children/{childId}/parent-approval
**Auth:** Parent token or child session start flow

Triggers parent approval login path.

### GET /children/{childId}/first-time
**Auth:** Parent or child token

Returns first-time experience flag.

### DELETE /children/{childId}/first-time
**Auth:** Child or parent token

Clears first-time flag after tutorial completion.

## 4. Contact and Permissions Service

### POST /contacts/requests
**Auth:** Parent token

Creates a contact request.

### GET /contacts/requests/{requestId}
**Auth:** Parent token

Returns request detail.

### POST /contacts/requests/{requestId}/approve
**Auth:** Parent token

Approves request and sets permission level.

### POST /contacts/requests/{requestId}/reject
**Auth:** Parent token

Rejects request.

### GET /contacts/{childId}
**Auth:** Child or parent token

Returns approved contacts for a child.

### PATCH /contacts/{contactId}/permission
**Auth:** Parent token

Updates permission level and stores audit trail.

### DELETE /contacts/{contactId}
**Auth:** Parent token

Revokes contact immediately.

### POST /contacts/{contactId}/block
**Auth:** Parent token

Blocks a contact permanently.

## 5. Safety and Alerting Service

### POST /events/log
**Auth:** Internal service token

Logs interaction events from MQ or KCP.

### GET /alerts/{parentId}
**Auth:** Parent token

Returns alerts for the parent.

### GET /alerts/{alertId}
**Auth:** Parent token

Returns alert detail.

### POST /alerts/{alertId}/resolve
**Auth:** Parent token

Marks alert as resolved and records action taken.

### POST /children/{childId}/pause
**Auth:** Parent token

Pauses child account.

### POST /children/{childId}/resume
**Auth:** Parent token

Reactivates paused child account.

### GET /activity-log/{childId}
**Auth:** Parent token

Returns child activity log, subject to entitlement.

## 6. Learning Content and Progression Service

### GET /quest-map/{childId}
**Auth:** Child token

Returns quest map with node states.

### GET /lessons/{lessonId}
**Auth:** Child token

Returns lesson detail and activity sequence.

### POST /progress/lesson-complete
**Auth:** Child token

Records lesson completion and triggers XP/badge evaluation.

### POST /progress/activity-complete
**Auth:** Child token

Records activity completion with accuracy and retry metadata.

### GET /progress/{childId}
**Auth:** Parent or child token

Returns progress summary.

### GET /streak/{childId}
**Auth:** Parent or child token

Returns streak history and current status.

### POST /streak/check-absence
**Auth:** Internal service token

Evaluates absence and updates streak state.

### GET /badges/{childId}
**Auth:** Parent or child token

Returns earned badges.

### GET /review/{childId}
**Auth:** Child token

Returns weak-content review loop.

## 7. Challenge and Recording Service

### GET /prompts
**Auth:** Child token

Returns preset prompts.

### POST /recordings/upload
**Auth:** Child token

Uploads a recording and returns recording reference.

### POST /challenges
**Auth:** Child token

Creates and sends a challenge.

### GET /challenges/inbox/{childId}
**Auth:** Child token

Returns challenge inbox for the child.

### GET /challenges/{challengeId}
**Auth:** Child or parent token

Returns challenge detail, permission-checked.

### POST /challenges/{challengeId}/respond
**Auth:** Child token

Attaches a response recording to the challenge.

### POST /challenges/{challengeId}/react
**Auth:** Child token

Sends preset reaction on completed challenge.

### GET /recordings/{recordingId}
**Auth:** Child or parent token

Streams recording only within challenge context.

### POST /mic-permission
**Auth:** Child token

Logs microphone permission status for a device.

### GET /mic-permission/{childId}
**Auth:** Child or parent token

Returns current microphone permission state.

## 8. Analytics and Event Logging Service

### POST /events
**Auth:** Internal service token

Ingests events from MQ and KCP services.

### GET /analytics/progress/{childId}
**Auth:** Parent token

Returns aggregated progress data.

### GET /analytics/dashboard/{childId}
**Auth:** Parent token

Returns headline metrics for parent dashboard.

### GET /analytics/speaking/{childId}
**Auth:** Parent token

Returns speaking challenge history.

### GET /analytics/streak/{childId}
**Auth:** Parent token

Returns streak history and heatmap data.

### GET /analytics/badges/{childId}
**Auth:** Parent token

Returns badge history and trigger events.

## 9. Open decisions
- Recording retention: temporary or permanent.
- Exact premium boundaries.
- Two-parent co-management rules.
- Sibling support model.
- Data retention by event type.

## 10. Suggested next spec fields
For each endpoint, add request schema, response schema, error codes, idempotency, side effects, and emitted events.
