---
name: validate
description: Review requirements for quality using Wiegers checklist. Use before handoff to development or stakeholder sign-off.
argument-hint: "[project-name] [optional: specific REQ-IDs to validate]"
---

# Requirements Validation

Review requirements against Wiegers quality criteria. This is the quality gate before development.

## Step 1: Load requirements

Read `projects/{project}/requirements.md`. If specific IDs given, focus on those. Otherwise validate all with status "Draft" or "Reviewed".

## Step 2: Individual requirement quality

For each requirement, check:

### Completeness
- [ ] Is the full behavior described?
- [ ] Are error conditions specified?
- [ ] Are boundary values defined?
- [ ] Is the expected response/output clear?

### Correctness
- [ ] Is this factually accurate?
- [ ] Does it match stakeholder intent?
- [ ] No contradictions with other requirements?

### Feasibility
- [ ] Is this technically achievable?
- [ ] Within budget/timeline constraints?
- [ ] Technology exists to implement this?

### Necessity
- [ ] Traces to a business need?
- [ ] Would anyone notice if removed?
- [ ] Is this a real requirement or a design decision?

### Unambiguity
- [ ] Only one possible interpretation?
- [ ] No vague terms? (fast, easy, user-friendly, flexible, appropriate, etc.)
- [ ] Quantified where possible?

### Verifiability
- [ ] Can you write a test for this?
- [ ] Are acceptance criteria specific enough?
- [ ] Pass/fail criteria are clear?

### Consistency
- [ ] No conflicts with other requirements?
- [ ] Terminology consistent with glossary?
- [ ] Uses "shall" (mandatory) vs "should" (optional) correctly?

## Step 3: Set-level quality

Check the requirements set as a whole:

- [ ] **Complete coverage** — Are all business requirements addressed by functional requirements?
- [ ] **No redundancy** — Any duplicate or overlapping requirements?
- [ ] **No conflicts** — Any requirements that contradict each other?
- [ ] **Traceable** — Every requirement has an ID, source, and priority?
- [ ] **Prioritized** — All requirements have MoSCoW priority?
- [ ] **Testable** — All requirements have acceptance criteria?

## Step 4: Common anti-patterns

Flag these if found:
1. **Gold plating** — Requirements beyond business need
2. **Solution masquerading as requirement** — "Use PostgreSQL" instead of "Persist data with ACID compliance"
3. **Compound requirements** — Multiple behaviors in one requirement (split them)
4. **Missing negative requirements** — What the system should NOT do
5. **Orphan requirements** — No trace to business need
6. **Untestable qualities** — "System shall be reliable" (how reliable?)

## Step 5: Generate report

Create a validation report:

```markdown
# Requirements Validation Report — {Project}
**Date**: YYYY-MM-DD
**Validated by**: BA Brain
**Scope**: [All / specific IDs]

## Summary
- Total requirements reviewed: X
- Passed: X
- Issues found: X
- Critical issues: X

## Issues

### Critical (must fix before development)
| REQ ID | Issue | Recommendation |
|--------|-------|----------------|
| REQ-F-xxx | [description] | [fix suggestion] |

### Warnings (should fix)
| REQ ID | Issue | Recommendation |
|--------|-------|----------------|

### Suggestions (nice to fix)
| REQ ID | Issue | Recommendation |
|--------|-------|----------------|

## Missing Coverage
- [Areas not covered by requirements]

## Recommendation
[Ready for development / Needs rework / Needs stakeholder review]
```

## Step 6: Update statuses

- Requirements that passed: update status to "Reviewed"
- Requirements with critical issues: keep as "Draft", add issue note
- Write the validation report to `projects/{project}/` as `validation-YYYY-MM-DD.md`

## Step 7: Present to user

Show the summary and critical issues. Suggest:
- Fix critical issues first
- Then run `/validate` again
- Once clean: ready for stakeholder approval and development handoff
