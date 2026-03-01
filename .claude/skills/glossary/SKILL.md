---
name: glossary
description: Add or update domain terms in the project glossary. Use when new terminology comes up or definitions need clarification.
argument-hint: "[project-name] [term to define]"
---

# Glossary Management

Maintain a consistent domain glossary following BABOK best practices.

## Step 1: Load glossary

Read `projects/{project}/glossary.md`.

## Step 2: Add or update term

If the user provides a term and definition, add it directly.

If only a term is given, help define it:
1. Ask the user for the definition in their words
2. Refine it to be precise and unambiguous
3. Identify synonyms (terms that mean the same thing — pick one canonical term)
4. Identify homonyms (same word, different meanings in different contexts — clarify which)

## Step 3: Write to glossary

Format:
```markdown
| Term | Definition | Context | Synonyms |
|------|-----------|---------|----------|
| [term] | [precise definition] | [where/how used] | [other names for same concept] |
```

Rules:
- One canonical term per concept (list others as synonyms)
- Definitions must be understandable by non-technical stakeholders
- Include context to disambiguate (e.g., "User" in auth context vs. "User" in billing context)
- Keep alphabetically sorted

## Step 4: Check for inconsistency

After adding a term, scan `projects/{project}/requirements.md` for:
- Uses of the term that don't match the definition
- Uses of synonyms that should be replaced with the canonical term
- Ambiguous uses that need clarification

Report any inconsistencies to the user.

## Step 5: Confirm

Show the updated glossary entry and any inconsistencies found.
