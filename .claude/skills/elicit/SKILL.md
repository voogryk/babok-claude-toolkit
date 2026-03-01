---
name: elicit
description: Run a structured requirements elicitation session. Use when gathering new requirements from stakeholders or analyzing meeting notes.
argument-hint: "[project-name] [optional: technique - interview|brainstorm|document-analysis]"
---

# Requirements Elicitation

Conduct a structured elicitation session following BABOK Elicitation & Collaboration.

## Step 1: Load context

Read the project files:
- `projects/{project}/requirements.md` — existing requirements
- `projects/{project}/stakeholders.md` — who we're working with
- `projects/{project}/glossary.md` — domain terms

If no project specified, ask which project.

## Step 2: Choose technique

Ask the user which technique fits this session:

1. **Interview** — "I'm talking to a stakeholder, help me structure the conversation"
2. **Brainstorm** — "Let's explore ideas and requirements freely"
3. **Document analysis** — "Here are existing docs/notes, extract requirements from them"
4. **Meeting notes** — "Here are notes from a meeting, structure them into requirements"

If the user provides raw text (meeting notes, email, etc.), default to **document analysis**.

## Step 3: Conduct elicitation

### For Interview:
Provide a structured question set based on context:
- Open-ended questions first ("Tell me about your workflow...")
- Probing questions ("What happens when X fails?")
- Confirming questions ("So if I understand correctly, you need...")
- Edge cases ("What about [unusual scenario]?")

### For Brainstorm:
- Capture all ideas without judgment first
- Then categorize: Must Have / Nice to Have / Out of Scope
- Identify dependencies and conflicts

### For Document Analysis / Meeting Notes:
- Extract every statement that implies a requirement
- Flag ambiguous statements (ask for clarification)
- Identify gaps — what's NOT mentioned but probably needed
- Categorize into: Business / User / Functional / Non-Functional

## Step 4: Structure into requirements

For each requirement discovered:

1. Assign an ID (check existing requirements.md for next available number)
2. Write in "The system shall..." format for functional requirements
3. Challenge ambiguity — if any trigger words found (fast, easy, flexible, etc.), ask for specifics
4. Identify the source stakeholder
5. Suggest initial priority

## Step 5: Write to files

Append new requirements to `projects/{project}/requirements.md`.
Add any new terms to `projects/{project}/glossary.md`.

## Step 6: Confirm and identify gaps

Show the user:
- List of new requirements captured (ID + title)
- Any ambiguous items that need follow-up
- Potential gaps: "I notice we haven't discussed [error handling / security / performance / edge cases] — should we?"
- Suggest next step: `/analyze` to decompose, or another `/elicit` session for gaps
