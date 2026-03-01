---
name: specify
description: Write formal requirement specifications (SRS sections, use cases). Use when requirements need to be documented for development handoff.
argument-hint: "[project-name] [optional: section or REQ-ID to specify]"
---

# Formal Specification

Write formal specs following Wiegers SRS structure.

## Step 1: Load context

Read:
- `projects/{project}/requirements.md`
- `projects/{project}/glossary.md`
- `projects/{project}/stakeholders.md`
- `templates/srs.md` for structure reference

## Step 2: Determine scope

Ask the user:
- "Do you want a full SRS or specific sections?"
- "Which requirements should I formalize?" (all, specific IDs, specific category)

## Step 3: Write specifications

For each requirement, write using the Wiegers style:

### Functional requirements
Use "The system shall..." format. Be specific:
```
REQ-F-001: User Registration

The system shall allow new users to create an account by providing:
- Email address (valid format, unique in system)
- Password (minimum 8 characters, at least 1 uppercase, 1 digit)
- Display name (2-50 characters, alphanumeric + spaces)

Upon successful registration:
- The system shall send a verification email within 30 seconds
- The system shall create the account in "pending verification" status
- The system shall redirect the user to the "check your email" page

Error conditions:
- If email already exists: display "Email already registered" error
- If password doesn't meet criteria: display specific validation errors
- If email service unavailable: create account, queue verification email, show warning
```

### Non-functional requirements
Always include measurable criteria:
```
REQ-NF-003: API Response Time

The system shall respond to all API requests within:
- 200ms at p50 (median)
- 500ms at p95
- 1000ms at p99

Measured under: 1000 concurrent users, standard workload.
Excluded: File upload/download operations, report generation.
```

### Use cases
If the requirement involves user interaction, create a use case file in `projects/{project}/use-cases/`:

```markdown
# UC-001: [Use Case Title]

**Actor**: [Primary actor]
**Preconditions**: [What must be true before]
**Trigger**: [What starts this use case]

## Main Flow
1. Actor does X
2. System responds with Y
3. Actor does Z
4. System validates and confirms

## Alternative Flows
- 2a. If validation fails: System displays error, returns to step 1
- 3a. If actor cancels: System discards changes, returns to main screen

## Postconditions
- [What is true after successful completion]

## Business Rules
- BR-001: [Relevant business rule]
```

## Step 4: Cross-reference

- Ensure every functional requirement traces to a user/business requirement
- Ensure every non-functional requirement has measurable criteria
- Flag any requirements that can't be verified with a test

## Step 5: Write to files

- Update `projects/{project}/requirements.md` with formalized text
- Create use case files in `projects/{project}/use-cases/` if applicable
- Update status of specified requirements to "Reviewed"

## Step 6: Summary

Show:
- Requirements formalized (list of IDs)
- Use cases created
- Any items that need stakeholder clarification
- Suggest: `/validate` to run quality checklist
