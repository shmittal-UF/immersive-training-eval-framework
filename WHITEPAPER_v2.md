# Open Evaluation Infrastructure for AI-Powered Immersive Training Systems
## A Technical Framework and Research Agenda
### Shivam Mittal | smittal992@gmail.com | 05/25/2026
### Working Paper — Version 0.1

---

## Abstract

Immersive VR and AR training systems have demonstrated measurable value across healthcare simulation, workforce reskilling, and accessible education. Despite this, institutional adoption at national scale has remained limited. This paper argues that the primary barrier is not technological immaturity but the absence of open, platform-independent infrastructure for measuring training interaction quality and competency outcomes in ways that external credentialing bodies, regulatory agencies, and multi-site institutions can use and compare. I propose a research agenda to develop this infrastructure: an open system comprising a natural interaction layer, a structured outcome measurement framework, and an accessibility-first design that reduces physical interface barriers. I describe the technical components, the design principles, and the institutional deployment model. This working paper is circulated to solicit feedback from researchers and institutional partners.

---

## 1. The Problem

The United States Department of Labor, the Health Resources and Services Administration, and the Department of Veterans Affairs have each endorsed immersive simulation training as a mechanism for addressing workforce and clinical training shortfalls. The technology has reached a level of maturity where this endorsement is credible. VR headset costs have fallen dramatically. Content quality has improved substantially. Large employers, healthcare systems, and workforce programs have run pilots.

Those pilots routinely fail to scale into durable institutional programs — not because the technology underperforms, but because the output of VR training is not currently legible to the institutional systems that make credentialing, hiring, and compliance decisions.

Every VR training system produces performance records in its own format, defined by its own metrics, anchored to its own internal standards. These records cannot be compared across systems, submitted to external credentialing bodies, integrated into HR management platforms, or used as regulatory evidence of workforce readiness. An institution that trains a nurse using System A and another that trains a nurse using System B cannot compare outcomes. A workforce development board that funds VR-based reskilling cannot produce outcome data that a certification body will recognize. A hospital system that deploys VR for procedural simulation cannot submit training records to its accrediting body.

This is a measurement infrastructure problem. It is not a problem any single VR company has commercial incentive to solve, because a truly open, platform-independent measurement standard would benefit competing platforms equally. It therefore requires independent research.

---

## 2. The Proposed Framework

I propose developing three interoperable components forming a middleware layer between any VR training platform and any institutional output system.

![System Architecture Overview](diagram_system_overview.svg)

*Figure 1 — System architecture: the Natural Interaction Layer (NIL), Structured Outcome Measurement Framework (SOMF), and Accessibility Compliance Layer (ACL) sit between VR training platforms and institutional output systems. Any VR platform can implement the input layer; any credentialing body or institution can consume the output layer without vendor-specific integration.*

### 2.1 Natural Interaction Layer (NIL)

Current VR training systems require precise physical controller input, limiting access for users with motor impairments, sensory differences, or physical disabilities. The NIL is a middleware system that interprets user intent through natural communication channels — voice, gesture, gaze, and behavioral cues — and translates that intent into VR system inputs without requiring controller precision.

![NIL Component Architecture](diagram_nil_architecture.svg)

*Figure 2 — NIL component architecture: four input modalities flow through individual classifiers into a Bayesian multimodal fusion engine. Adaptive calibration adjusts per-user tolerance bands. Output is platform-independent intent events consumed by both the VR system and the SOMF session log.*

**Core technical components:**
- Multimodal intent classification: a model ensemble that interprets concurrent speech, hand motion, and gaze signals and resolves them into a structured intent representation with a confidence score
- Uncertainty handling: when intent confidence falls below threshold, the system requests clarification through the least disruptive available modality rather than executing a low-confidence action
- Safe fallback behaviors: a predefined set of neutral-state actions the system executes when intent cannot be resolved, preventing training disruption
- Calibration protocol: an adaptive baseline-setting process that accounts for individual variation in movement range, speech patterns, and sensory processing

**Design principle:** The NIL is designed as a software layer that can be implemented above any VR platform's native input system, operating on processed sensor data rather than raw hardware inputs. This architecture allows it to function independently of platform-specific APIs.

**Output schema:**
```json
{
  "timestamp": "2026-05-30T14:23:11.342Z",
  "intent": "select",
  "target": "option_B",
  "modalities_used": ["gaze", "voice"],
  "confidence": 0.91,
  "accessibility_mode": "gaze_primary",
  "session_event_id": "evt_0042"
}
```

### 2.2 Structured Outcome Measurement Framework (SOMF)

The SOMF is a schema and associated tooling for recording, structuring, and exporting training performance data in formats compatible with external evaluation requirements.

![SOMF Data Flow](diagram_somf_flow.svg)

*Figure 3 — SOMF data flow: proprietary VR event streams from any platform pass through normalization, competency mapping, and xAPI statement generation to produce portable institutional records. The same training session produces records readable by any institution regardless of which VR platform generated them.*

**Core technical components:**
- Event telemetry capture: timestamped recording of trainee actions, system states, and environmental conditions during training sessions
- Competency mapping: a configurable schema that maps raw event telemetry to competency dimensions defined by the training domain (e.g., procedural steps in a clinical simulation, safety protocols in a manufacturing context)
- Standardized output format: a JSON-LD schema for structured competency records, designed for compatibility with xAPI (Experience API / Tin Can) and IMS Global standards already adopted in some credentialing contexts
- Remediation signals: automated identification of performance patterns associated with skill gaps, structured for use by instructors in targeted remediation planning

**xAPI output schema (excerpt):**
```json
{
  "verb": {
    "id": "https://w3id.org/xapi/adl/verbs/demonstrated",
    "display": {"en-US": "demonstrated"}
  },
  "result": {
    "score": {"scaled": 0.84, "raw": 84, "min": 0, "max": 100},
    "success": true,
    "duration": "PT8M32S",
    "extensions": {
      "somf:task_completion_sequence": ["prep", "site_selection", "insertion", "securement"],
      "somf:nil_modalities": ["voice", "gaze"],
      "somf:accessibility_compliance": "wcag_2_1_aa"
    }
  }
}
```

**Design principle:** The SOMF is designed to be configurable by domain without altering its core data structure. A healthcare institution and a workforce training program can define different competency frameworks while producing records in a format that the same external evaluation tools can process.

### 2.3 Accessibility Compliance Layer (ACL)

The ACL is a design specification and testing protocol ensuring that VR training systems implementing the NIL and SOMF satisfy ADA and WCAG accessibility standards as applied to immersive environments. Its development is motivated in part by the DOJ ADA Title II Final Rule (89 Fed. Reg. 31,320, April 24, 2024), which establishes firm compliance deadlines for public institutions deploying digital training environments.

**Core components:**
- Input modality redundancy: every training interaction must be completable through at least two distinct input modalities (e.g., voice and gaze; gesture and switch-access)
- Sensory accommodation: configurable display, audio, and haptic parameters to accommodate visual and auditory processing differences
- Compliance documentation: automated generation of WCAG 2.1 Level AA accessibility conformance records as part of the SOMF output structure

**Standards alignment:**

| Standard | Role |
|---|---|
| xAPI (Experience API) — ADL | SOMF output data transport |
| IMS Global CASE | Competency framework interoperability |
| IEEE P2048 | VR/AR standards alignment target |
| WCAG 2.1 Level AA | ACL compliance baseline |
| DOJ ADA Title II (April 2024) | ACL compliance obligation context |
| IDEA | Education schema IEP alignment |

---

## 3. Research Plan

### Phase 1 (Q3–Q4 2026): Architecture and Pilot Design
- Finalize technical specifications for NIL, SOMF, and ACL components
- Identify 2–3 institutional pilot partners across healthcare, workforce, and special education domains
- Establish research collaboration agreements with academic partners for evaluation methodology co-development
- Submit architecture documentation for peer review via workshop or preprint

### Phase 2 (Q1–Q2 2027): Prototype Development and Initial Evaluation
- Develop NIL prototype implementing voice and gesture intent classification
- Develop SOMF prototype with configurable competency schema and xAPI-compatible output
- Deploy in controlled pilot settings at 1–2 partner institutions
- Collect evaluation data on interaction quality, outcome measurement accuracy, and institutional usability

### Phase 3 (Q3–Q4 2027): Refinement and Dissemination
- Refine components based on pilot evaluation findings
- Publish findings in peer-reviewed venue
- Release open documentation supporting institutional and researcher adoption
- Engage with relevant standards bodies (IEEE, IMS Global, xAPI community) on integration pathways

---

## 4. Institutional Partners and Collaborators

This research is designed to be developed in collaboration with institutional partners across sectors. Current discussions are underway with:

- **V-ARE Lab, University of Illinois Chicago** (Dr. Mohan Zalake): Healthcare VR training evaluation methodology and clinical deployment
- **Rising Star SPED Academy, San Jose, CA**: Special education deployment for students with autism — accessibility evaluation

Additional academic and healthcare institution partnerships are being developed.

---

## 5. Note on Independence

This research agenda is being developed independently of my current employment. The proposed framework is designed as open infrastructure — not as a product for any employer — and its value depends on its independence from any single commercial interest. All research activities described here are conducted on my own time, using my own resources, and will be disseminated publicly.

---

## References

[1] U.S. Department of Labor. "Apprenticeship and Registered Apprenticeship." Employment and Training Administration.  
[2] Health Resources and Services Administration. "Health Workforce Shortage Areas." HRSA Data Warehouse, 2025.  
[3] White House Office of Science and Technology Policy. "Critical and Emerging Technologies List Update." February 2024.  
[4] xAPI Specification, ADL Initiative. https://adlnet.gov/projects/xapi/  
[5] IMS Global Learning Consortium. Competencies and Academic Standards Exchange (CASE) Framework.  
[6] Bihorac, A. et al. "MySurgeryRisk: Development and Validation of a Machine-Learning Risk Algorithm for Major Complications and Death after Surgery." Annals of Surgery, 2019.  
[7] Department of Justice. "Nondiscrimination on the Basis of Disability; Accessibility of Web Information and Services of State and Local Government Entities." 89 Fed. Reg. 31,320 (April 24, 2024).

---

*This is a working paper circulated for feedback. Comments and collaboration inquiries welcome at smittal992@gmail.com.*

*Version 0.1 | 05/25/2026*
