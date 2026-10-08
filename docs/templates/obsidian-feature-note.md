# {{Feature Name}}

> Module: {{module}}
> Feature: {{Feature Name}}
> Status: 🚧 In Progress / ✅ Completed
> Version: v1.0
> Last Updated: {{YYYY-MM-DD}}

<!--
LEARNING NOTE TEMPLATE — cloud-based-chat-app
Canonical copy. Vault mirror: ...\cloud-based-chat-app\templates\Feature-Template.md

WHAT THIS NOTE IS FOR
This is a LEARNING note, not formal documentation. When the developer reopens it months later
they must be able to (1) understand the feature quickly, (2) revise it fast, (3) rebuild it from
scratch, (4) explain it confidently in an interview.

WRITING STYLE — the rules that matter
- Bullets and short sections. Never a wall of prose.
- MEDIUM-length bullets. One clear idea per bullet, explained enough to learn from.
    TOO SHORT:  "Calls the service."
    TOO LONG:   a five-clause sentence you must read twice.
    RIGHT:      "Receives the login request and hands the credentials to AuthenticationManager,
                 instead of verifying the password inside the controller itself."
- Use simple vertical ↓ flows, never UML sequence diagrams.
- Use tables for fields, methods, and status codes.
- Explain cause → action → result.
- Every claim must come from the real code. Never invent an endpoint, port, table, column,
  field, method, Redis key, STOMP destination, or log line.
- Sections that do not apply: write "Not applicable — {reason}". Never delete a section.

THE VERIFICATION BOUNDARY (CLAUDE.md §16)
- §10.1 automated tests: Claude runs them and reports real output.
- §10.2–§10.6 manual verification: Claude writes the guide, the DEVELOPER runs it.
  Claude never fills an "Actual Result" and never sets ✅ Fully Verified.

Delete this comment block in the real note.
-->

---

# 1. Overview

## What is this feature?

Two or three plain sentences. Someone who has never seen this code should understand what it does.

## Why do we need it?

State the problem as simple points, not academic prose.

- Point about what was missing or broken.
- Point about what that prevented.
- Point about who or what it affects.

## Goal

What the feature must actually achieve, as a checklist of outcomes.

- Accept X.
- Verify Y.
- Produce Z.
- Return it to the client.

## Concepts involved

| Concept | Where it shows up here |
|---|---|
| e.g. Spring Security | Filter chain that authenticates the request |
| e.g. BCrypt | Password verification |

## Classes at a glance

| Class | Module | One-line role |
|---|---|---|
| `X` | `auth` | What it does |

---

# 2. API

Endpoint, request, response, errors. If the feature adds no endpoint, write
"Not applicable — {reason}" and say what the observable surface is instead.

## Endpoint

```http
METHOD /api/...
```

## Headers

```text
Content-Type: application/json
```

## Request

```json
{
}
```

## Success Response

```json
{
}
```

```text
200 OK
```

## Error Responses

| Status | When it happens |
|---|---|
| 400 | ... |
| 401 | ... |
| 409 | ... |

---

# 3. Request Flow

## The path

Simple vertical chain of the real components. No UML.

```text
Client
   ↓
Controller
   ↓
Service
   ↓
Repository
   ↓
PostgreSQL
   ↓
Response
```

## Step by step

Numbered steps. For each one: **what happens**, **which class does it**, and **why the step
exists** when that is not obvious.

1. **Client sends the request** — `POST /api/...` with the JSON body above.
2. **Security filter chain runs first** — `SecurityConfig` decides whether the request needs a
   credential before any controller code executes.
3. **Controller receives it** — `XController` binds the JSON to a request DTO and triggers
   validation. It does no business logic.
4. **Service performs the work** — `XService` owns the use case and the transaction boundary.
5. **Repository loads or saves** — `XRepository` runs the query.
6. **Response is built** — a response DTO, never the entity.

---

# 4. Implementation (Class Walkthrough)

One block per important class. Enough that the developer can rebuild it from the note.

## `ClassName`

**Purpose**

One or two sentences: what this class is and why it exists.

**Fields**

| Field | Type | Purpose |
|---|---|---|
| `x` | `TypeX` | What it is used for |

**Methods**

| Method | Purpose |
|---|---|
| `doThing()` | What it does and what it returns |

**Responsibilities**

- Medium-length bullet describing one real responsibility.
- Another one, including *why* it belongs here rather than elsewhere.

**Connects to**

- Calls `OtherClass` for X.
- Is called by `CallerClass` when Y happens.

**Implementation detail worth remembering**

Anything subtle: an annotation that changes behavior, a default that matters, an ordering
constraint. Skip this sub-heading when there is nothing to say.

---

# 5. Key Concepts Explained

For each important concept this feature actually uses. Keep it tied to this project — not a
textbook chapter.

## {{Concept}}

- **What it means** — plain definition.
- **Why we use it here** — the specific reason in this feature.
- **What happens internally** — useful depth, not source-code archaeology.
- **Where it is in our code** — real class and file.
- **Why this design** — the trade-off that was chosen.
- **Without it** — what would break or get worse.

---

# 6. Database

## Tables

Which tables the feature touches, and whether it reads, writes, or both.

## Columns used

| Column | Type | Why this feature cares |
|---|---|---|

## Operations

```text
SELECT ...
   ↓
No INSERT / UPDATE      ← or describe the write
```

## Relationships and indexes

Only what applies. Say which index backs which lookup, and why it matters.

---

# 7. Security

- **Authentication required?** — yes/no, and why.
- **What is protected** — the paths and rules that apply.
- **Password / token handling** — how credentials are stored and verified.
- **What is deliberately not done yet** — and which task will do it.

---

# 8. Validation

## Input validation

| Field | Rule | Message |
|---|---|---|

## Business validation

- Rule enforced in the service, and what happens when it fails.

## Where validation runs

Say explicitly whether invalid input reaches the service or is rejected before it.

---

# 9. Exception Handling

## Exceptions

| Exception | Thrown when | Status |
|---|---|---|

## Where it is handled

Name the handler. If the failure happens in the filter chain and never reaches
`GlobalExceptionHandler`, say so — that distinction matters.

---

# 10. Testing & Verification

## 10.1 Automated Tests

Keep this short. What exists, what it proves, the real result.

| Test class | Tests | What it verifies |
|---|---|---|
| `XTest` | n | ... |

```text
Command: apps/api/mvnw -B test

Tests Run:
Passed:
Failed:
Errors:
Skipped:
```

## 10.2 Manual Testing (Postman)

### Prerequisites

```text
[ ] PostgreSQL running on localhost:5432, database "chatapp"
[ ] Env vars exported: DB_URL, DB_USERNAME, DB_PASSWORD
[ ] Backend running: cd apps/api && ./mvnw spring-boot:run
[ ] Health check: GET http://localhost:8080/actuator/health -> {"status":"UP"}
[ ] Redis running        (only if this feature uses Redis)
```

### Test 1 — {{Happy path}}

**Request**

Method: `POST`
URL: `http://localhost:8080/api/...`

**Body**

```json
{
}
```

**Expected result**

- HTTP `200 OK`
- Response contains X.
- Response does **not** contain Y.

**Actual result**

```text
[To be filled after manual verification]
```

### Test 2 — {{Negative case}}

Same shape. Include only cases this feature can actually reach: invalid credentials, missing
field, duplicate resource, invalid/expired token, unauthorized, malformed body.

**Why this case matters** — one line, so the test is not just a ritual.

**Actual result**

```text
[To be filled after manual verification]
```

## 10.3 Database Verification

Never assume HTTP 200 means the feature works. Check the row.

**Before**

```sql
```

What the state should be before the request.

**Run**

Which Postman test from 10.2 to send.

**After**

```sql
```

**Verify**

- What must have changed.
- What must **not** have changed.
- Any security-sensitive column (e.g. a password column must hold a BCrypt hash, never plaintext).

**Actual result**

```text
[To be filled after manual verification]
```

## 10.4 Redis / WebSocket / Storage Verification

Only when the feature uses them. Use the real key structure, destination, or bucket.

```text
PING
GET <key>
TTL <key>
```

State which key should exist, why, expected TTL, and what it proves. Otherwise:
"Not applicable — {reason}".

**Actual result**

```text
[To be filled after manual verification]
```

## 10.5 Log Verification

Which log lines should appear, and what each one proves. Only output the code actually emits — if
no class in the feature declares a logger, say that plainly instead of inventing messages.

Look for framework signals too: a startup line that should now be *absent*, a bean name that
confirms the right wiring, or the SQL printed by `spring.jpa.show-sql` in `dev`.

**Actual result**

```text
[To be filled after manual verification]
```

## 10.6 Verification Checklist

```text
[ ] Application starts
[ ] Happy path works in Postman
[ ] Negative cases behave correctly
[ ] Database state verified
[ ] Redis / WebSocket verified   (or n/a)
[ ] Logs checked
[ ] Automated tests passed
```

```text
Verification Status:

⏳ Implementation Complete — Manual Verification Pending
```

> Changes to `✅ Fully Verified` only after the developer reports the manual results.
> Passing automated tests are never grounds for changing it.

---

# 11. Files Modified

| File | Change |
|---|---|
| `path/X.java` | New — what it does |
| `path/Y.java` | Modified — what changed |

---

# 12. Implementation Order (Rebuild From Scratch)

The answer to *"if you had to build this again, what would you do?"* Adapt the order to the
feature — do not copy this list blindly.

1. Create the entity and its columns.
2. Create the repository method(s).
3. Create the service that owns the use case.
4. Add the DTOs and validation.
5. Add the controller.
6. Wire the security configuration.
7. Write the unit tests.
8. Write the integration test.
9. Run the suite.
10. Start the app and verify through Postman.
11. Verify the database state.

---

# 13. Engineering Decisions

Short "Why X?" blocks — the questions an interviewer would actually ask.

### Why {{decision}}?

- The reason, in one or two bullets.
- The alternative that was rejected, and why.
- The trade-off accepted.

---

# 14. Lessons Learned

- Concept worth remembering, phrased so it is still useful in six months.
- Something surprising about how the framework behaves.
- A distinction that is easy to get wrong.

---

# 15. Common Mistakes

Realistic mistakes someone would make implementing this — including ones that still compile and
still pass tests.

- **Mistake** — why it is wrong and what it breaks.

---

# 16. Future Improvements

- Improvement, and the task ID that will do it when one exists.

---

# 17. Interview Questions

Write these as a **real conversation**, not textbook Q&A. The answers should sound like a strong
engineering student explaining their own project — confident, specific, and reproducible from
memory. Use "I chose X because…", "Instead of X I used Y because…", "The trade-off is…".

Cover the categories that apply: basic understanding · architecture · code · framework · design
decisions · failure cases · security · scalability · testing · follow-ups.

Include follow-up questions — the second thing an interviewer asks after the first answer.

## Basic Understanding

**Interviewer:** {{question}}

**Me:** {{answer in natural spoken English, 3–6 sentences, with reasoning}}

**Interviewer:** {{follow-up that digs into the first answer}}

**Me:** {{answer}}

## Architecture

**Interviewer:** ...

**Me:** ...

## Design Decisions

**Interviewer:** ...

**Me:** ...

## Failure Cases

**Interviewer:** ...

**Me:** ...

## Security

**Interviewer:** ...

**Me:** ...

## Scalability

**Interviewer:** ...

**Me:** ...

## Testing

**Interviewer:** ...

**Me:** ...

---

# 18. References

- Official docs used.
- Related notes: `[[other-note]]`.
