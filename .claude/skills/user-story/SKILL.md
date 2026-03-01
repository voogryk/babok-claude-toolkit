---
name: user-story
description: Create user stories with acceptance criteria. Quick way to capture requirements in agile format.
argument-hint: "[project-name] [description of what the user needs]"
---

# User Story Creation

Create user stories following INVEST criteria with Given/When/Then acceptance criteria.

## Step 1: Load context

Read `projects/{project}/requirements.md` and `projects/{project}/glossary.md`.

## Step 2: Capture the need

If the user provided a description, parse it. Otherwise ask:
1. "Who is the user/role?" (be specific — not just "user", but "registered customer", "admin", "guest")
2. "What do they want to accomplish?"
3. "Why? What business value does this deliver?"

## Step 3: Write the story

Format:
```markdown
### US-{number}: [Short title]

**Story**: As a [specific role], I want [capability], so that [business value].

**Priority**: Must / Should / Could / Won't
**Estimate**: [leave blank for team to fill]
**Source**: [stakeholder or requirement ID]

**Acceptance Criteria**:
1. Given [precondition], when [action], then [expected result]
2. Given [precondition], when [action], then [expected result]
3. Given [edge case], when [action], then [expected result]

**Out of scope**: [What this story does NOT cover]
**Dependencies**: [Other stories or requirements]
**Notes**: [Technical notes, design considerations]
```

## Step 4: INVEST quality check

Verify the story against INVEST:
- [ ] **Independent** — Can be developed without waiting for other stories?
- [ ] **Negotiable** — Details can be discussed with the team?
- [ ] **Valuable** — Delivers clear value to user or business?
- [ ] **Estimable** — Team has enough info to estimate?
- [ ] **Small** — Can be completed in one sprint?
- [ ] **Testable** — Acceptance criteria are specific and verifiable?

If any check fails, suggest improvements. Common fixes:
- Too big → Split into smaller stories
- Not independent → Identify and document the dependency
- Not testable → Add specific Given/When/Then criteria
- Not valuable → Rewrite "so that" with concrete business value

## Step 5: Edge cases

For each story, proactively suggest edge cases:
- What if the input is invalid?
- What if the user cancels midway?
- What if the system is under load?
- What if permissions are insufficient?
- What about empty states (first use, no data)?

Add relevant edge cases as additional acceptance criteria.

## Step 6: Write to files

Append the story to `projects/{project}/requirements.md` under a "## User Stories" section.

If the story relates to an existing requirement, add cross-reference:
- Add `**Related**: US-xxx` to the requirement
- Add `**Implements**: REQ-F-xxx` to the story

## Step 7: Confirm

Show the complete story to the user. Ask:
- "Does this capture what you need?"
- "Any acceptance criteria missing?"
- "Should I create more stories for related functionality?"
