## 5 Priority

Priorities are established using the industry-standard MoSCoW methodology:
- **Must Have (M)**: Mandatory core functionality required for project deliverable baseline.
- **Should Have (S)**: High-priority capabilities essential for complete automation and pattern fidelity.
- **Could Have (C)**: Desirable enhancements to expand simulation realism if time permits.
- **Won't Have (W)**: Excluded from this deliverable scope (deferred to future milestones).

| Req ID | Requirement Summary | Category | Priority | Justification |
| :--- | :--- | :--- | :--- | :--- |
| **FR-1 - FR-6** | Greenhouse and Zone Management | Functional | **Must Have** | Fundamental structural domain model needed to host components. |
| **FR-7 - FR-11** | Sensor Management & Telemetry | Functional | **Must Have** | Required data source for environmental monitoring and event triggering. |
| **FR-12 - FR-15** | Actuator Management & Abstractions | Functional | **Must Have** | Core mechanism to enact environmental modifications. |
| **FR-16 - FR-18** | Manual Override & Provenance Logging | Functional | **Must Have** | Critical requirement specified in project definition section 3.9. |
| **FR-19 - FR-24** | Polymorphic Rule Engine | Functional | **Must Have** | Key educational objective demonstrating polymorphism and decoupled logic. |
| **FR-25 - FR-29** | Interchangeable Control Strategies | Functional | **Must Have** | Mandatory application of the Strategy Pattern (EcoMode, HighYield, Frost). |
| **FR-30 - FR-33** | Observer-Based Event Pipeline | Functional | **Must Have** | Mandatory application of the Observer Pattern for telemetry distribution. |
| **FR-34 - FR-36** | Virtual Time & Environmental Simulation | Functional | **Should Have** | Essential for automated demonstration of dynamic environmental cycles. |
| **FR-37 - FR-38** | Monitoring Dashboard & Diagnostics | Functional | **Should Have** | Required for user visibility and explaining rule actuation rationales. |
| **NFR-1 - NFR-3** | Usability & Metric Standardization | Non-Functional | **Should Have** | Ensures clear user comprehension and unambiguous operator commands. |
| **NFR-4 - NFR-6** | System Reliability & Graceful Fallback | Non-Functional | **Must Have** | Prevents system crashes during unexpected sensor anomalies or fast simulation. |
| **NFR-7 - NFR-9** | Event Pipeline & UI Performance | Non-Functional | **Should Have** | Guarantees timely rule processing without UI thread blocking. |
| **NFR-10 - NFR-11**| Extensibility & Pattern Adherence | Non-Functional | **Must Have** | Primary grading criteria for OOAD principles (Open/Closed Principle). |
| **NFR-12 - NFR-15**| Object-Oriented Architecture Standards | Non-Functional | **Must Have** | Core academic deliverable requirement. |
| **NFR-16 - NFR-19**| Packaging, Git, and Academic Integrity | Non-Functional | **Must Have** | Deliverable submission criteria. |

---
