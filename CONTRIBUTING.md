# Contributing

Guidelines for proposing changes, additions, or corrections to the BioLink Functional Requirements Specification.

---

## Scope

This document governs contributions to the functional requirements specification only. It does not cover design implementation, test procedures, or other project artifacts.

---

## How to Propose a Change

1. **Open an issue** describing the proposed change. Include:
   - The requirement ID(s) affected (e.g., IF-9.2, ENV-1.5), or indicate if this is a new requirement
   - The rationale for the change — grounded in test data, design constraints, or interface dependencies
   - The proposed new or revised text

2. **Submit a pull request** with the change applied to the markdown file. The PR description should reference the issue number and summarize the change.

3. **Review** — Changes will be reviewed for:
   - Consistency with the solution-agnostic "shall" statement format
   - Impact on adjacent requirements and interface dependencies
   - Completeness of quantitative bounds (minimum, target, maximum where applicable)

4. **Approval** — Changes to baseline requirements require approval from the document owner. Changes that affect cross-institutional interfaces require agreement from all affected parties.

---

## Requirements Writing Guidelines

### Format

All formal requirements must follow this structure:

```markdown
> **IF-X.X:** The MW shall [do something measurable], with [quantitative bounds].
```

- Use blockquote format with a bold requirement ID prefix
- Begin the requirement with "The MW shall..." (or the applicable subsystem)
- Include minimum, target, and maximum values where the parameter has a defined range

### Clarifying Notes

Context, caveats, or items subject to future refinement go below the requirement as bullet points:

```markdown
> **IF-X.X:** The MW shall deliver reagents at a pressure within the chip tolerance range, with a minimum of 50 kPa, a target of 380 kPa, and a maximum of 500 kPa.

- Reagent delivery pressure limits and targets are subject to change as chip pressure tolerance and fluidic interface characteristics are refined through ongoing development and validation.
```

Notes are not requirements. They provide context but do not carry "shall" statement weight.

### Principles

- **Solution-agnostic** — Describe *what* the system must do, not *how*. Avoid specifying particular components, vendors, or implementation approaches in the requirement statement itself. Solution-specific context may appear in notes.
- **Quantitative where possible** — Vague requirements ("sufficient," "adequate," "reasonable") are difficult to verify. Provide numbers.
- **Traceable** — Every requirement must have a unique ID that can be referenced in downstream documents (ICD, test plans, design reviews).
- **Testable** — Write requirements that can be verified through inspection, analysis, demonstration, or test.

---

## Requirement ID Assignment

New requirements should follow the established numbering scheme:

| Prefix | Interface |
|--------|-----------|
| ENV-1.x | Environmental Operating Requirements |
| IF-1.x | Sampler to Middleware Interface |
| IF-2.x | Gas and Pneumatic Chip Interface |
| IF-3.x | Middleware Reagent Interface |
| IF-4.x | Middleware and Chip Waste Management |
| IF-5.x | Middleware to Analytical Device Interface |
| IF-6.x / IF-7.x | Electrical (Power and Control) Interface |
| IF-9.x | Thermal Management Interface |
| IF-11.x | Mechanical Docking (Middleware to Chip) |

Append the next available number within the relevant prefix. Do not reuse IDs from deleted or superseded requirements — mark them as deprecated instead.

---

## Types of Changes

### Minor (no issue required)
- Typo corrections
- Formatting fixes
- Clarifying note updates that do not alter requirement intent

### Standard (issue required)
- Revising quantitative bounds on an existing requirement
- Adding a new requirement within an existing interface section
- Adding or modifying clarifying notes that change interpretation

### Major (issue + discussion required)
- Adding a new interface section
- Removing or deprecating a requirement
- Changes that affect multiple interface sections or cross-institutional boundaries

---

## Versioning

This document uses simple version numbering (v1.0, v1.1, v2.0, etc.):

- **Patch (v1.0 → v1.1):** Minor corrections, clarifying note updates, formatting
- **Minor (v1.1 → v1.2):** New requirements, revised bounds, added notes
- **Major (v1.x → v2.0):** Structural changes, new interface sections, requirement removals, or changes resulting from decision gate reviews

All changes must be recorded in `CHANGELOG.md` under the appropriate version heading.
