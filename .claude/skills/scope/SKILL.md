---
name: scope
description: Define project scope, stakeholders, and high-level business requirements. Use at project start or when scope changes.
---

# Scope Definition

Define or update the project scope following BABOK Strategy Analysis.

## Step 1: Identify or load the project

Ask the user which project this is for. If the project folder doesn't exist under `projects/`, create it:
```
projects/{project-name}/
├── requirements.md
├── glossary.md
├── stakeholders.md
└── decisions.md
```

If the project exists, read all files first.

## Step 2: Business context (ask one by one)

Ask these questions sequentially. Wait for each answer before asking the next.

1. **Problem statement**: "What problem are we solving? What's broken or missing today?"
2. **Business objectives**: "What does success look like? How will we measure it?"
3. **Stakeholders**: "Who are the key stakeholders? (decision makers, users, technical team, external parties)"
4. **Scope boundaries**: "What's IN scope? What's explicitly OUT of scope?"
5. **Constraints**: "Any technical, budget, timeline, or regulatory constraints?"
6. **Assumptions**: "What are we assuming to be true?"
7. **Risks**: "What could go wrong? What are the biggest unknowns?"

## Step 3: Write stakeholders

For each stakeholder identified, write to `projects/{project}/stakeholders.md` using this format:

```markdown
# Stakeholders

## {Name/Role}
- **Role**: [Their role in the project]
- **Interest**: [What they care about]
- **Influence**: High / Medium / Low
- **Engagement**: [How to engage them — meetings, reviews, sign-off]
```

## Step 4: Write business requirements

Create initial business requirements in `projects/{project}/requirements.md`:

```markdown
# Requirements — {Project Name}

## Business Requirements

### REQ-B-001: [Title]
**Description**: [...]
**Priority**: Must Have
**Source**: [Stakeholder]
**Rationale**: [Why]
**Status**: Draft
**Acceptance Criteria**:
1. [...]
```

## Step 5: Initialize glossary

Create `projects/{project}/glossary.md` with any domain terms that came up:

```markdown
# Glossary — {Project Name}

| Term | Definition | Context |
|------|-----------|---------|
| [term] | [definition] | [where/how it's used] |
```

## Step 6: Summarize

Show the user a summary:
- Number of stakeholders identified
- Number of business requirements captured
- Scope boundaries (in/out)
- Key risks and assumptions
- What to do next (suggest `/elicit` for detailed requirements)
