---
name: analyze
description: Analyze, decompose, prioritize, and model requirements. Use after elicitation to structure raw requirements into actionable specs.
argument-hint: "[project-name]"
---

# Requirements Analysis

Analyze and structure requirements following BABOK Requirements Analysis & Design Definition.

## Step 1: Load all requirements

Read `projects/{project}/requirements.md` and `projects/{project}/glossary.md`.

## Step 2: Decomposition

For each high-level requirement, ask:
- Can this be broken into smaller, independent requirements?
- Does this requirement describe multiple behaviors? (Split it)
- Is there an implicit "and" hiding multiple requirements?

Example:
```
BAD:  "The system shall allow users to register, login, and manage their profile"
GOOD: REQ-F-001: "The system shall allow users to register with email and password"
      REQ-F-002: "The system shall allow users to login with email and password"
      REQ-F-003: "The system shall allow users to update their profile information"
```

## Step 3: Categorization

Ensure every requirement is categorized:
- **Business** (REQ-B): Why we're doing this
- **User** (REQ-U): What users need to do
- **Functional** (REQ-F): What the system does
- **Non-Functional** (REQ-NF): Quality attributes
- **Constraint** (REQ-C): Limitations
- **Interface** (REQ-IF): Integration points

## Step 4: Dependency mapping

Identify dependencies between requirements:
- Which requirements block others?
- Which can be developed in parallel?
- Are there conflicts between requirements?

Add `**Dependencies**: REQ-F-xxx` to affected requirements.

## Step 5: Prioritization

If not already prioritized, run MoSCoW prioritization:
- **Must Have**: System doesn't work without it
- **Should Have**: Important but has workaround
- **Could Have**: Nice to have, low impact if missing
- **Won't Have (this release)**: Acknowledged but deferred

Ask the user to confirm priorities for Must Have items.

## Step 6: Gap analysis

Check for common gaps:
- [ ] Error handling — what happens when things fail?
- [ ] Authentication & authorization — who can do what?
- [ ] Data validation — what input is valid?
- [ ] Performance — response times, throughput, capacity?
- [ ] Security — data protection, encryption, audit trail?
- [ ] Accessibility — WCAG compliance needed?
- [ ] Internationalization — multiple languages/locales?
- [ ] Migration — data migration from existing system?
- [ ] Reporting — what reports/analytics are needed?
- [ ] Audit trail — what actions need logging?

Flag any gaps to the user.

## Step 7: Write updates

Update `projects/{project}/requirements.md` with:
- New decomposed requirements
- Updated categories and priorities
- Dependencies
- Gap items as new Draft requirements

## Step 8: Summary

Show:
- Total requirements by category and priority
- Dependency graph (text-based)
- Identified gaps
- Suggest next: `/specify` for formal specs, or `/validate` for quality review
