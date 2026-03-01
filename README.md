# BABOK Claude Toolkit

> Business Analysis toolkit for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) based on **BABOK v3** and **Karl Wiegers' requirements engineering** practices.

[Українська версія](README.uk.md)

Open this folder in Claude Code and get a full BA assistant with structured skills, templates, and a document converter — all grounded in industry-standard methodology.

## Quick Start

```bash
# Open in Claude Code
cd babok-claude-toolkit
claude

# Define a new project
/scope my-project

# Import existing documents
/import /path/to/requirements.pdf my-project

# Extract requirements from imported docs
/elicit my-project document-analysis

# Create a user story
/user-story my-project "User wants to reset their password"
```

## What's Inside

### Structure

```
babok-claude-toolkit/
├── CLAUDE.md                          # System prompt (role, rules, behavior)
├── convert.py                         # Document converter → Markdown
├── .claude/
│   ├── rules/
│   │   └── babok.md                   # BABOK v3 + Wiegers reference (auto-loaded)
│   └── skills/                        # 8 skills (slash commands)
│       ├── scope/SKILL.md
│       ├── import/SKILL.md
│       ├── elicit/SKILL.md
│       ├── analyze/SKILL.md
│       ├── specify/SKILL.md
│       ├── user-story/SKILL.md
│       ├── validate/SKILL.md
│       └── glossary/SKILL.md
├── templates/
│   ├── en/                            # English templates
│   │   ├── srs.md
│   │   ├── user-story.md
│   │   ├── use-case.md
│   │   ├── stakeholder-register.md
│   │   └── requirements-checklist.md
│   └── uk/                            # Ukrainian templates
│       ├── srs.md
│       ├── user-story.md
│       ├── use-case.md
│       ├── stakeholder-register.md
│       └── requirements-checklist.md
└── projects/                          # Your project work goes here
    └── _example/                      # Example project structure
```

### Per-Project Structure

Each project lives in `projects/{project-name}/`:

```
projects/my-project/
├── requirements.md      # All requirements with IDs, priorities, statuses
├── glossary.md           # Domain terms and definitions
├── stakeholders.md       # Stakeholder register
├── decisions.md          # Key decisions and rationale
├── sources/              # Imported documents (converted to Markdown)
├── use-cases/            # Detailed use case files
└── archive/              # Completed/deprecated items
```

---

## Skills

Skills follow the BABOK workflow — from scope definition through validation.

### `/scope` — Scope Definition

Starting point for any new project. Asks sequentially:

1. **Problem statement** — what's broken or missing
2. **Business objectives** — how we measure success
3. **Stakeholders** — decision makers, users, technical team
4. **Scope boundaries** — what's IN, what's OUT
5. **Constraints** — technical, budget, timeline
6. **Assumptions** — what we're taking as true
7. **Risks** — what could go wrong

**Output**: populated `stakeholders.md`, `requirements.md` (business requirements), `glossary.md`.

### `/import` — Document Import

Converts PDF, DOCX, DOC, XLSX, XLS files to Markdown and saves them to `sources/`.

```bash
/import /path/to/spec.pdf my-project
/import "/path/to/docs/*.pdf" my-project
```

What happens:
1. Verifies file exists
2. Converts via `convert.py`
3. Saves to `projects/{project}/sources/{filename}.md` with metadata header
4. Shows summary (headings count, tables count)
5. Suggests running `/elicit` for analysis

**Auto-detection**: if you give Claude a file path ending in `.pdf`, `.docx`, `.doc`, `.xlsx`, or `.xls`, it will automatically suggest `/import`.

### `/elicit` — Requirements Elicitation

Structured requirements gathering session. Supports 4 techniques:

| Technique | When to use |
|-----------|-------------|
| **Interview** | 1-on-1 conversation with a stakeholder/SME |
| **Brainstorm** | Idea generation, exploring the solution space |
| **Document analysis** | Analyzing existing documents (after `/import`) |
| **Meeting notes** | Structuring meeting notes into requirements |

For each discovered requirement:
- Assigns an ID (`REQ-F-001`, `REQ-NF-003`, etc.)
- Formulates in "The system shall..." style
- Challenges ambiguity (vague terms flagged)
- Identifies source and suggests priority
- Points out gaps — what wasn't discussed but should be

### `/analyze` — Requirements Analysis

Structures and models requirements after gathering:

1. **Decomposition** — breaks complex requirements into atomic ones
2. **Categorization** — Business / User / Functional / Non-Functional / Constraint / Interface
3. **Dependency mapping** — what blocks what, what can be done in parallel
4. **Prioritization** — MoSCoW (Must / Should / Could / Won't)
5. **Gap analysis** — checks for:
   - Error handling
   - Authentication/authorization
   - Data validation
   - Performance
   - Security
   - Data migration
   - Reporting

### `/specify` — Formal Specification

Writes formal specs in Wiegers SRS style:

- **Functional requirements** — "The system shall..." with error conditions
- **Non-functional requirements** — with measurable criteria (ms, %, count)
- **Use cases** — Actor/System table with main, alternative, and exception flows
- **Cross-references** — traceability from business to functional requirements

Uses `templates/{lang}/srs.md` as a base.

### `/user-story` — User Stories

Quick user story creation with acceptance criteria:

```
As a [specific role],
I want [capability],
So that [business value].

Acceptance Criteria:
1. Given [context], when [action], then [result]
```

Checks every story against **INVEST** criteria:
- **I**ndependent — can be developed separately
- **N**egotiable — details open for discussion
- **V**aluable — delivers value to user or business
- **E**stimable — team can estimate effort
- **S**mall — fits in one sprint
- **T**estable — has clear acceptance criteria

Proactively adds edge cases (invalid input, cancellation, load, permissions).

### `/validate` — Requirements Validation

Quality gate before development handoff. Checks against Wiegers checklist:

**Per requirement:**
- Completeness — nothing missing?
- Correctness — factually accurate?
- Feasibility — technically achievable?
- Necessity — traces to business need?
- Unambiguity — only one interpretation?
- Verifiability — can write a test?
- Consistency — no contradictions?

**For the requirement set:**
- Full coverage of business requirements
- No duplicates
- No conflicts
- Everything has an ID and priority

**Flags anti-patterns:**
- Gold plating — requirements without business need
- Solution as requirement — "Use PostgreSQL" instead of "ACID compliance"
- Compound requirements — multiple behaviors in one
- Untestable qualities — "System shall be reliable"

Generates a **Validation Report** with Critical/Warning/Suggestion issues.

### `/glossary` — Glossary Management

Domain glossary maintenance:
- Adds/updates terms with definitions and context
- Identifies synonyms (picks one canonical term)
- Detects homonyms (same word, different meanings)
- Scans `requirements.md` for inconsistent term usage

---

## Templates

Templates are available in **English** (`templates/en/`) and **Ukrainian** (`templates/uk/`).

| File | Description | Based on |
|------|-------------|----------|
| `srs.md` | Software Requirements Specification — full structure with 9 sections + traceability | Wiegers SRS |
| `user-story.md` | User story with acceptance criteria, INVEST checklist, edge cases | Agile + INVEST |
| `use-case.md` | Use case with main/alternative/exception flows, postconditions | UML / Cockburn |
| `stakeholder-register.md` | Stakeholder register with RACI matrix | BABOK |
| `requirements-checklist.md` | Requirements quality checklist with anti-patterns and sign-off | Wiegers |

Skills use templates automatically. You can also open them manually as reference.

---

## Document Converter

`convert.py` converts documents to Markdown for analysis.

### Supported Formats

| Format | Library | What it preserves |
|--------|---------|-------------------|
| PDF | `pymupdf4llm` | Headings, tables, lists, structure. LLM-optimized. |
| DOCX | `mammoth` | Formatting, lists, tables. Shows conversion warnings. |
| DOC | `antiword` / `LibreOffice` | Via antiword (plain text) or LibreOffice → DOCX → mammoth. |
| XLSX / XLS | `openpyxl` | Each sheet as a separate Markdown table. |

### Usage

```bash
cd babok-claude-toolkit
.venv/bin/python convert.py input.pdf                  # Output to stdout
.venv/bin/python convert.py input.pdf output.md        # Save to file
```

### Installing Dependencies

```bash
cd babok-claude-toolkit
python3 -m venv .venv
.venv/bin/pip install pymupdf4llm mammoth openpyxl
```

For legacy `.doc` files, you also need `antiword` or `libreoffice` (system package).

---

## Rules

### `.claude/rules/babok.md`

Auto-loads when working with any project (`projects/**`). Contains:

- **6 BABOK v3 knowledge areas** with actionable guidance
- **Elicitation techniques table** — when to use which
- **Requirement types hierarchy** (Wiegers): Business → User → Functional / NF / Constraints
- **Quality checklist** with bad/good examples
- **Ambiguity trigger words** — "fast", "easy", "flexible", etc.
- **ID convention** — `REQ-{type}-{number}`
- **Requirement template** and **user story template**
- **INVEST criteria**

---

## Language

- **Conversation**: Claude responds in Ukrainian by default (configurable in CLAUDE.md)
- **Documentation & requirements**: written in English (working language for specs)
- **Templates**: available in both English and Ukrainian

---

## Typical Workflow

```
/scope          Define project, stakeholders, business objectives
    │
/import         Import existing documents (PDF, DOCX, XLSX)
    │
/elicit         Gather requirements (interview, document analysis, meeting notes)
    │
/analyze        Decompose, categorize, prioritize, gap analysis
    │
/specify        Formal specification (SRS, use cases)
    │
/user-story     User stories with acceptance criteria
    │
/validate       Quality gate — Wiegers checklist review
    │
/glossary       Glossary maintenance (at any stage)
```

Skills can be used in any order and repeated. The workflow is iterative.

---

## Methodology

### BABOK v3 (Business Analysis Body of Knowledge)
Standard from IIBA (International Institute of Business Analysis). Defines 6 knowledge areas, techniques, and competencies for business analysts.

### Karl Wiegers — Software Requirements
From "Software Requirements" and "More About Software Requirements". Defines:
- Requirement types hierarchy
- SRS document structure
- Requirements quality checklist
- Requirements engineering process

---

## License

MIT
