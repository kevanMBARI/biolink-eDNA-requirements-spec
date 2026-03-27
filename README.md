# biolink-eDNA-requirements-spec
Open repository for sharing, reviewing, and refining the functional requirements and interface specification for the Biolink eDNA middleware platform. This repository contains the functional requirements specification for the BioLink Middleware system — a modular interface layer designed to bridge autonomous ocean samplers with microfluidic analytical devices for in situ environmental DNA (eDNA) processing.

---

## About This Document

The BioLink Functional Requirements Specification defines *what* the middleware system must do, not *how* it does it. Requirements are written as solution-agnostic "shall" statements with quantitative bounds (minimum, target, maximum) to allow independent implementation while ensuring interface compatibility.

The document covers three functional blocks and their critical interfaces:

- **Sampler** — Collects and processes water samples into a native homogenate
- **Middleware** — Bridges sampler output to analytical device input through lab-on-chip-based sample modification
- **Analytical Device** — Converts modified sample into actionable biological information

---

## Document Structure

The specification is organized into the following sections:

| Section | Description |
|---------|-------------|
| Sampler | Primary function, functional requirements, key inputs/outputs |
| Middleware | Primary function, functional requirements, key inputs/outputs, operating environmental requirements (ENV-1.x) |
| Analytical Device | Primary function, functional requirements, key inputs/outputs |
| Middleware Architecture | Purpose, functional architecture (translation, resource management, contamination prevention, standardization, orchestration, scalability) |
| Critical Interface Requirements | Eight interface specifications (IF-1 through IF-11) covering fluidic, pneumatic, reagent, waste, electrical, thermal, and mechanical docking interfaces |

### Requirement ID Scheme

- **ENV-x.x** — Environmental operating requirements (temperature, humidity, mechanical, pressure, deployment duration)
- **IF-1.x** — Sampler to Middleware Interface
- **IF-2.x** — Gas and Pneumatic Chip Interface
- **IF-3.x** — Middleware Reagent Interface
- **IF-4.x** — Middleware and Chip Waste Management
- **IF-5.x** — Middleware to Analytical Device Interface
- **IF-6.x / IF-7.x** — Electrical (Power and Control) Interface
- **IF-9.x** — Thermal Management Interface
- **IF-11.x** — Mechanical Docking (Middleware to Chip)

---

## File

```
BioLink_Functional_Requirements_Release_v1.md
```

---

## Usage

This document is intended to serve as the baseline requirements reference for all downstream design, prototyping, and testing activities. Requirements should be traced forward into interface control documents, test plans, and design reviews.

When referencing a specific requirement, use its ID (e.g., IF-9.2) for traceability.

---

## Formatting Conventions

- **Formal requirements** are presented in blockquote format with bold requirement IDs:
  > **IF-1.1:** The MW shall receive and retain a usable homogenate sample volume...

- **Clarifying notes** appear as bullet points below the requirement they modify. Notes provide context, caveats, or identify items subject to future refinement — they are not requirements themselves.

- **Functional purpose** statements at the beginning of each interface section describe the intent of that interface in plain language.

---

## License

See institutional agreements for terms of use and distribution.
