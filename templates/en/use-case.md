# Use Case Template

## UC-{number}: {Use Case Title}

**Actor**: {Primary actor — specific role}
**Level**: User goal | Subfunction | Summary
**Status**: Draft | Reviewed | Approved

---

### Description
{One paragraph summary of what this use case achieves.}

### Preconditions
1. {What must be true before this use case starts}
2. {System state, user state, data state}

### Trigger
{What initiates this use case — user action, system event, time-based}

---

### Main Success Scenario (Happy Path)

| Step | Actor | System |
|------|-------|--------|
| 1 | {Actor does X} | |
| 2 | | {System responds with Y} |
| 3 | {Actor provides Z} | |
| 4 | | {System validates and processes} |
| 5 | | {System confirms success} |

---

### Alternative Flows

**2a. {Condition — e.g., "Validation fails"}**
1. System displays specific error message
2. System highlights invalid fields
3. Return to step 1

**3a. {Condition — e.g., "Actor cancels"}**
1. System prompts for confirmation
2. If confirmed: discard changes, return to main screen
3. If not confirmed: return to step 3

**4a. {Condition — e.g., "External service unavailable"}**
1. System retries once after 5 seconds
2. If still unavailable: queue request, notify user, show estimated time

---

### Exception Flows

**E1. {Condition — e.g., "Session expired"}**
1. System redirects to login
2. After login: return user to step where they left off

---

### Postconditions

**Success:**
- {What is true after successful completion}
- {Data changes, notifications sent, state transitions}

**Failure:**
- {What happens if use case fails}
- {Data rollback, error state}

---

### Business Rules
- BR-{number}: {Rule that applies to this use case}

### Data Requirements
- {What data is needed — input fields, formats, constraints}

### Non-Functional Requirements
- {Performance: response time for this use case}
- {Security: authentication/authorization needed}
- {Usability: accessibility requirements}

### Related
- **Implements**: REQ-U-{xxx}
- **Related Use Cases**: UC-{xxx}
- **User Stories**: US-{xxx}
