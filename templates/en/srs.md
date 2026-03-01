# Software Requirements Specification (SRS)
## {Project Name}

**Version**: 1.0
**Date**: YYYY-MM-DD
**Author**: {name}
**Status**: Draft | In Review | Approved

---

## 1. Introduction

### 1.1 Purpose
{What this document covers and who it's for.}

### 1.2 Scope
{What the system does, who uses it, what's NOT included.}

### 1.3 Definitions & Acronyms
{Reference to glossary.md or inline definitions.}

### 1.4 References
{Related documents, standards, external specs.}

---

## 2. Overall Description

### 2.1 Product Perspective
{How this system fits in the bigger picture. Is it standalone? Part of a larger system? Replacing something?}

### 2.2 User Classes and Characteristics
{Who uses this system? What do they know? How often do they use it?}

| User Class | Description | Technical Level | Frequency |
|-----------|-------------|----------------|-----------|
| {role} | {description} | Low / Medium / High | Daily / Weekly / Occasional |

### 2.3 Operating Environment
{Where it runs — browsers, mobile, servers, OS requirements.}

### 2.4 Design and Implementation Constraints
{Technology choices, regulatory requirements, legacy integration.}

### 2.5 Assumptions and Dependencies
{What we assume to be true. What we depend on externally.}

---

## 3. Business Requirements

### REQ-B-001: {Title}
**Description**: {Why this project exists. Business objective.}
**Priority**: Must Have
**Source**: {Stakeholder}
**Acceptance Criteria**:
1. {Measurable success criterion}

---

## 4. User Requirements

### REQ-U-001: {Title}
**Description**: {What the user needs to accomplish.}
**Priority**: Must Have
**Source**: {Stakeholder}
**Related**: REQ-B-001

---

## 5. Functional Requirements

### 5.1 {Feature Area}

#### REQ-F-001: {Title}
**Description**: The system shall {specific behavior}.
**Priority**: Must Have
**Source**: REQ-U-001
**Rationale**: {Why}
**Status**: Draft
**Acceptance Criteria**:
1. Given {context}, when {action}, then {result}
2. Given {error condition}, when {action}, then {error handling}
**Dependencies**: {other REQ IDs}

---

## 6. Non-Functional Requirements

### 6.1 Performance
#### REQ-NF-001: {Title}
**Description**: {Measurable performance criterion}
**Measurement**: {How to test it}

### 6.2 Security
#### REQ-NF-010: {Title}
**Description**: {Security requirement}

### 6.3 Usability
#### REQ-NF-020: {Title}
**Description**: {Usability requirement with measurable criteria}

### 6.4 Reliability
#### REQ-NF-030: {Title}
**Description**: {Uptime, error rates, recovery}

---

## 7. Interface Requirements

### 7.1 User Interfaces
{Wireframes, UI principles, responsive requirements.}

### 7.2 API Interfaces
#### REQ-IF-001: {Title}
**Description**: {API contract, endpoints, data formats.}

### 7.3 External Interfaces
{Third-party integrations, data feeds.}

---

## 8. Constraints

### REQ-C-001: {Title}
**Description**: {Limitation on design or implementation}
**Rationale**: {Why this constraint exists}

---

## 9. Appendices

### A. Traceability Matrix

| Business Req | User Req | Functional Req | Test Case |
|-------------|----------|---------------|-----------|
| REQ-B-001 | REQ-U-001 | REQ-F-001, REQ-F-002 | TC-001 |

### B. Change History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | YYYY-MM-DD | {name} | Initial version |
