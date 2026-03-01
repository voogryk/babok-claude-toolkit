# Requirements Quality Checklist (Wiegers)

Use this checklist before development handoff or stakeholder sign-off.

---

## Individual Requirement Quality

For each requirement, verify:

### Content
- [ ] **Complete** — All necessary details present (inputs, outputs, behavior, errors)
- [ ] **Correct** — Accurately reflects stakeholder intent (verified with source)
- [ ] **Necessary** — Traces to a business need (has rationale)
- [ ] **Feasible** — Technically achievable within constraints

### Clarity
- [ ] **Unambiguous** — Only one possible interpretation
- [ ] **No vague terms** — No "fast", "easy", "user-friendly", "flexible", "appropriate"
- [ ] **Quantified** — Measurable where applicable (ms, %, count)
- [ ] **Consistent terminology** — Uses glossary terms consistently

### Quality
- [ ] **Verifiable** — Can write a test / acceptance criteria exist
- [ ] **Prioritized** — Has MoSCoW or numeric priority
- [ ] **Traceable** — Has unique ID, source, and rationale
- [ ] **Atomic** — Describes single behavior (no "and" combining multiple requirements)

---

## Requirement Set Quality

For the complete set of requirements:

### Coverage
- [ ] All business requirements have supporting functional requirements
- [ ] Error handling is specified (not just happy path)
- [ ] Security requirements are addressed
- [ ] Performance/scalability requirements are defined
- [ ] Data migration requirements exist (if applicable)
- [ ] Reporting/analytics requirements exist (if applicable)

### Consistency
- [ ] No contradictions between requirements
- [ ] Terminology is consistent throughout
- [ ] Priority levels are applied consistently
- [ ] ID numbering is sequential with no gaps

### Completeness
- [ ] All stakeholder needs are represented
- [ ] All user roles are covered
- [ ] All interfaces are specified (UI, API, external)
- [ ] Non-functional requirements cover: performance, security, usability, reliability
- [ ] Constraints and assumptions are documented

### Traceability
- [ ] Every requirement has a unique ID
- [ ] Business → User → Functional trace exists
- [ ] Traceability matrix is up to date
- [ ] Orphan requirements are identified (no business justification)

---

## Common Anti-Patterns to Flag

| Anti-Pattern | Example | Fix |
|-------------|---------|-----|
| Gold plating | Feature no one asked for | Remove or get explicit stakeholder approval |
| Solution as requirement | "Use React for frontend" | "Frontend shall render in < 2s on mobile" |
| Compound requirement | "System shall X and Y and Z" | Split into 3 separate requirements |
| Missing negatives | No "shall NOT" requirements | Add security/access restrictions |
| Implicit requirements | Assumed but not written | Make explicit, get confirmation |
| Moving target | Requirement changed 3 times | Lock scope, log changes |

---

## Sign-off Record

| Reviewer | Role | Date | Verdict | Comments |
|----------|------|------|---------|----------|
| {name} | {role} | YYYY-MM-DD | Approved / Needs rework | {notes} |
