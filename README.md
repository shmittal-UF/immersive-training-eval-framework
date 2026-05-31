# Open Evaluation Infrastructure for AI-Powered Immersive Training Systems

Open, platform-independent AI evaluation and accessibility infrastructure
for institutional VR/AR training systems.

**Author:** Shivam Mittal | smittal992@gmail.com  
**Status:** Working Paper v0.1 — May 2026

---

## The Problem

VR training systems deployed across U.S. healthcare, workforce development,
and special education programs generate performance data in proprietary
formats that cannot be compared across platforms, submitted to credentialing
bodies, or integrated into institutional accreditation workflows. This
project proposes open infrastructure to address that gap.

## Three Components

| Component | Function |
|---|---|
| **NIL** — Natural Interaction Layer | Voice, gesture, gaze interpretation — no controller precision required |
| **SOMF** — Structured Outcome Measurement Framework | xAPI-compatible portable competency records across any VR platform |
| **ACL** — Accessibility Compliance Layer | WCAG 2.1 Level AA compliance documentation for ADA Title II obligations |

## Documentation

- [Working Paper v0.1](WHITEPAPER_v2.md) — full framework description,
  research plan, and institutional partners (05/25/2026)
- [Technical Architecture Specification](TECHNICAL_ARCHITECTURE.md) —
  component specs, schemas, and code samples

## Architecture Diagrams

| Diagram | Description |
|---|---|
| [System Overview](diagram_system_overview.svg) | NIL → SOMF → ACL stack between VR platforms and institutional systems |
| [NIL Architecture](diagram_nil_architecture.svg) | Multimodal input processing pipeline |
| [SOMF Data Flow](diagram_somf_flow.svg) | VR events → xAPI competency records transformation |

## Standards

xAPI (ADL) · IMS Global CASE · IEEE P2048 · WCAG 2.1 Level AA ·
DOJ ADA Title II (April 2024) · W3C XR Accessibility User Requirements · IDEA

## Institutional Collaborators

- **V-ARE Lab, University of Illinois Chicago** (Dr. Mohan Zalake) —
  healthcare VR training evaluation methodology
- **Rising Star SPED Academy, San Jose, CA** —
  special education accessibility pilot

## Current Status

```
[x] System architecture defined
[x] xAPI output schema specified
[x] Architecture diagrams published
[x] Working paper circulated for feedback
[ ] NIL reference implementation — in progress
[ ] SOMF reference implementation — in progress
[ ] ACL test protocol — in progress
[ ] Institutional pilot evaluations — in discussion
```

## Contact

smittal992@gmail.com | [LinkedIn](https://www.linkedin.com/in/shmittal-uf/)

## License

Specification: CC-BY 4.0 · Implementations (when released): Apache 2.0
