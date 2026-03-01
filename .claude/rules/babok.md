---
paths:
  - "projects/**"
---

# BABOK v3 + Wiegers — Quick Reference

This rule auto-loads when working with any project. Use it as a reference for requirements engineering best practices.

## BABOK Knowledge Areas

### 1. Business Analysis Planning & Monitoring
- Define BA approach, stakeholder engagement, governance
- Decide which techniques to use for this project
- Plan how requirements will be managed (tools, traceability, change control)

### 2. Elicitation & Collaboration
**Techniques** (use the right one for the situation):

| Technique | When to use |
|-----------|-------------|
| Interview | 1-on-1 deep dive with SME or stakeholder |
| Workshop | Multiple stakeholders, need consensus |
| Observation | Understanding current workflow ("as-is") |
| Document Analysis | Existing docs, regulations, legacy systems |
| Survey/Questionnaire | Large audience, quantitative data |
| Brainstorming | Generating ideas, exploring solution space |
| Prototyping | UI/UX requirements, unclear user needs |
| Interface Analysis | System integration points |

**Elicitation flow**: Prepare → Conduct → Confirm → Communicate

### 3. Requirements Life Cycle Management
- **Trace**: Every requirement links to business need (upstream) and test/design (downstream)
- **Maintain**: Requirements evolve — track status: Draft → Reviewed → Approved → Implemented → Verified
- **Prioritize**: Use MoSCoW, or numeric (1-5), or value/effort matrix
- **Manage changes**: Every scope change goes through impact analysis

### 4. Strategy Analysis
- **Current state**: Document how things work now ("as-is")
- **Future state**: Define desired outcome ("to-be")
- **Gap analysis**: What's missing between current and future
- **Risk assessment**: What can go wrong, likelihood, impact, mitigation

### 5. Requirements Analysis & Design Definition
**Requirement types** (Wiegers classification):

```
Business Requirements (WHY)
  └── User Requirements (WHO does WHAT)
       └── Functional Requirements (system SHALL)
       └── Non-Functional Requirements (quality attributes)
       └── Constraints (technical/business limitations)
```

**Modeling techniques**:
- **Process models**: Flowcharts, BPMN, activity diagrams
- **Data models**: ERD, data dictionary
- **State models**: State machines for entities with lifecycle
- **Use cases**: Actor → System interaction sequences
- **User stories**: As a [role], I want [goal], so that [benefit]

### 6. Solution Evaluation
- Validate solution meets business requirements
- Assess organizational readiness
- Identify gaps and improvement opportunities

---

## Wiegers Requirements Quality Checklist

Every requirement MUST be:

| Quality | Test | Bad example | Good example |
|---------|------|-------------|--------------|
| **Complete** | Nothing missing? | "System handles errors" | "System displays error code and message for all API failures" |
| **Correct** | Factually accurate? | (verify with stakeholder) | (verified) |
| **Feasible** | Technically possible? | "Real-time translation of all languages" | "Support EN, UK, DE translation with <2s latency" |
| **Necessary** | Traces to business need? | "Add dark mode" (why?) | "Add dark mode (REQ-B-003: reduce eye strain for night-shift operators)" |
| **Unambiguous** | One interpretation only? | "System should be fast" | "API response time < 200ms at p95 under 1000 concurrent users" |
| **Verifiable** | Can write a test for it? | "System is user-friendly" | "New user completes onboarding in < 3 minutes without assistance" |
| **Prioritized** | MoSCoW or numeric? | (no priority) | Must Have |
| **Traceable** | Has ID and source? | (floating text) | REQ-F-042, Source: Product Owner, Sprint 5 |

### Ambiguity triggers — ALWAYS challenge these words:
- "fast", "quick", "responsive" → Ask: how many ms/seconds?
- "user-friendly", "intuitive", "easy" → Ask: measurable how?
- "flexible", "configurable" → Ask: what exactly can be changed?
- "support", "handle" → Ask: what specific behavior?
- "etc.", "and so on", "and more" → Ask: list all items explicitly
- "should", "may", "might" → Ask: is this a MUST or a NICE-TO-HAVE?
- "appropriate", "adequate", "reasonable" → Ask: by what criteria?

---

## Requirement ID Convention

```
REQ-{type}-{number}

Types:
  B  = Business requirement
  U  = User requirement
  F  = Functional requirement
  NF = Non-functional requirement
  C  = Constraint
  IF = Interface requirement

Examples:
  REQ-B-001  = First business requirement
  REQ-F-042  = 42nd functional requirement
  REQ-NF-007 = 7th non-functional requirement
```

## Requirement Template

```markdown
### REQ-F-001: [Short title]

**Description**: [Full requirement text using "The system shall..."]
**Priority**: Must Have | Should Have | Could Have | Won't Have
**Source**: [Stakeholder name, meeting date, or document reference]
**Rationale**: [Why this requirement exists]
**Status**: Draft | Reviewed | Approved | Implemented | Verified
**Acceptance Criteria**:
1. [Given/When/Then or checklist item]
2. [...]
**Dependencies**: [Other REQ IDs this depends on]
**Notes**: [Any additional context]
```

## User Story Format

```
As a [role],
I want [capability/goal],
So that [business value/benefit].

Acceptance Criteria:
- Given [context], when [action], then [expected result]
- Given [context], when [action], then [expected result]
```

**INVEST criteria** for good user stories:
- **I**ndependent — can be developed separately
- **N**egotiable — details can be discussed
- **V**aluable — delivers value to user/business
- **E**stimable — team can estimate effort
- **S**mall — fits in one sprint
- **T**estable — has clear acceptance criteria
