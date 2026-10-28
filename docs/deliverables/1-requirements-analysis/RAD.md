# REQUIREMENTS ANALYSIS DOCUMENT

**For:** Smart Agriculture and Greenhouse IoT Controller System (3Bits)  
**Document Issue No:** 1.0  
**Issue Date:** October 2026  

**Prepared by:**  
- Nuri Ziya Kırtepe  
- Muhammed Korkmaz  
- Derya Uysal  

**Course:** CSE443 - Object-Oriented Analysis and Design  
**Project Team:** 3Bits  
**Target Repository:** `nziyak/3Bits_Smart_Agriculture_Systems`  

---

## TABLE OF CONTENTS

1. [Introduction](#1-introduction)  
   1.1 [Purpose of the system](#11-purpose-of-the-system)  
   1.2 [Scope of the system](#12-scope-of-the-system)  
   1.3 [Objectives and success criteria of the project](#13-objectives-and-success-criteria-of-the-project)  
   1.4 [Definitions, acronyms, and abbreviations](#14-definitions-acronyms-and-abbreviations)  
   1.5 [References](#15-references)  
   1.6 [Overview](#16-overview)  
2. [Current system](#2-current-system)  
3. [Proposed system](#3-proposed-system)  
   3.1 [Overview](#31-overview)  
   3.2 [Functional requirements](#32-functional-requirements)  
   3.3 [Nonfunctional requirements](#33-nonfunctional-requirements)  
       3.3.1 [Usability](#331-usability)  
       3.3.2 [Reliability](#332-reliability)  
       3.3.3 [Performance](#333-performance)  
       3.3.4 [Supportability](#334-supportability)  
       3.3.5 [Implementation](#335-implementation)  
       3.3.6 [Interface](#336-interface)  
       3.3.7 [Packaging](#337-packaging)  
       3.3.8 [Legal](#338-legal)  
   3.4 [System models](#34-system-models)  
       3.4.1 [Scenarios](#341-scenarios)  
       3.4.2 [Use case model](#342-use-case-model)  
       3.4.3 [Object model](#343-object-model)  
       3.4.4 [Dynamic model](#344-dynamic-model)  
       3.4.5 [User interfaces and Mock-ups](#345-user-interfaces-and-mock-ups)  
4. [Glossary of Terms](#4-glossary-of-terms)  
5. [Priority](#5-priority)  
6. [Traceability](#6-traceability)  

---

## 1 Introduction

### 1.1 Purpose of the system
The Smart Agriculture and Greenhouse IoT Controller System is an event-driven software simulation and monitoring platform engineered to automate environmental regulation within a modern greenhouse facility. The system models heterogeneous hardware devices—including soil moisture, ambient temperature, and sunlight sensors, alongside irrigation pumps, heating coils, and automated shade curtains—as interacting software abstractions. 

The software collects environmental telemetry, applies configurable evaluation rules, executes dynamic control policies, and coordinates actuators to maintain ideal agronomic conditions without human intervention, while supporting manual supervisor overrides and historical diagnostic observation.

### 1.2 Scope of the system
The scope of this project encompasses:
- Modeling a virtual greenhouse partitioned into one or more independently managed environmental zones.
- Establishing extensible abstractions for sensors and actuators.
- Providing an event-driven publish-subscribe telemetry pipeline.
- Implementing a polymorphic rule evaluation engine capable of evaluating single-variable and multi-variable boundary conditions.
- Implementing dynamic control strategies (EcoMode, HighYieldGrowth, FrostProtection) to resolve policy trade-offs.
- Supporting priority manual operator overrides with explicit provenance tracking.
- Simulating virtual time progression and dynamic environmental phenomena (weather changes, soil absorption, crop transpiration).
- Providing an operator dashboard displaying live system health, alerts, and operational telemetry.

**Out of Scope:**
- Physical hardware deployment, direct embedded micro-controller firmware programming, or electrical sensor calibration in the real physical world.
- Commercial billing, accounting, and supply chain inventory management modules.

### 1.3 Objectives and success criteria of the project
- **Object-Oriented Design Excellence**: Adhere to core object-oriented principles (Abstraction, Encapsulation, Inheritance, Polymorphism, Composition).
- **Design Pattern Utilization**: Correctly apply the Composite Pattern for hierarchical zone management, the Observer Pattern for telemetry event distribution, and the Strategy Pattern for interchangeable control policies.
- **Decoupled Architecture**: Eliminate direct dependencies between sensors, rule evaluators, actuators, and user-interface layers.
- **Extensibility**: Facilitate the integration of new sensor types, actuator models, rule evaluation logic, or control policies without altering existing core engine logic.
- **Simulation Fidelity**: Accurately simulate time-stepped or continuous environmental changes and demonstrate timely automated corrective responses.

### 1.4 Definitions, acronyms, and abbreviations
- **EARS**: Easy Approach to Requirements Syntax
- **GUI**: Graphical User Interface
- **IoT**: Internet of Things
- **NFR**: Non-Functional Requirement
- **FR**: Functional Requirement
- **OOAD**: Object-Oriented Analysis and Design
- **RAD**: Requirements Analysis Document
- **UML**: Unified Modeling Language
- **Zone**: An isolated spatial section of a greenhouse maintaining dedicated environmental parameters.
- **Telemetry**: Automated measurement data generated by sensors and transmitted across the event pipeline.

### 1.5 References
- CSE443 Course Syllabus and Lecture Notes on Object-Oriented Analysis and Design.
- Project Definition Specification: *Smart Agriculture and Greenhouse IoT Controller Systems*, Department of Computer Engineering.
- Gamma, E., Helm, R., Johnson, R., & Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley.
- IEEE Std 830-1998: *IEEE Recommended Practice for Software Requirements Specifications*.

### 1.6 Overview
The remainder of this document outlines the current state of greenhouse management systems (Section 2), describes the functional and non-functional requirements of the proposed platform alongside UML analysis models (Section 3), provides a glossary of domain terminology (Section 4), establishes requirement priorities (Section 5), and maps requirements to use cases and architecture components via a traceability matrix (Section 6).

---

## 2 Current system

Traditional greenhouse management relies on manual labor, localized standalone controllers, or rudimentary timer-based relays:
1. **Manual Inspection and Sampling**: Operators manually measure soil moisture using handheld probes, read wall-mounted thermometers, and observe sunlight levels. This approach is labor-intensive, error-prone, and incapable of continuous 24/7 monitoring.
2. **Delayed Intervention**: Because physical readings are taken periodically, micro-climate anomalies—such as unexpected cold snaps, heatwaves, or rapid soil desiccation—are frequently detected only after crop damage or stress has occurred.
3. **Siloed and Inflexible Equipment**: Existing analog thermostats, pump timers, and mechanical roof vents operate independently without central coordination. For instance, a heater may operate simultaneously with ventilation curtains, resulting in extreme energy waste.
4. **Lack of Policy Flexibility**: Conventional automation systems operate on static, hard-coded thresholds. They cannot dynamically balance resource conservation (e.g., water/energy restrictions) against high-yield commercial objectives based on external context.
5. **Absence of Centralized Provenance**: When equipment fails or operates unexpectedly, operators have no centralized event audit trail to diagnose whether the action was triggered by an automation fault or a manual command.

The proposed software replaces these disparate and manual workflows with a unified, event-driven, intelligent object-oriented controller platform.

---

## 3 Proposed system

### 3.1 Overview
The proposed Smart Agriculture and Greenhouse IoT Controller System models physical greenhouse infrastructure as an interconnected hierarchy of software abstractions. The system monitors multiple micro-climate zones in real time via simulated sensor networks, processes environmental updates through a polymorphic rule engine, applies specialized control strategies to arbitrate actuator actions, and provides supervisors with a comprehensive monitoring and manual override console.

### 3.2 Functional requirements
All functional requirements are organized by functional subsystem and authored according to the Easy Approach to Requirements Syntax (EARS) standard using the *"The system shall..."* formulation.

#### Subsystem 1: Greenhouse and Zone Management
- **FR-1**: The system shall allow operators to create, configure, and remove virtual greenhouse instances.
- **FR-2**: The system shall allow operators to add, reconfigure, and delete greenhouse zones within a greenhouse instance.
- **FR-3**: The system shall allow operators to configure target environmental parameter ranges (soil moisture, temperature, light levels) for each individual zone.
- **FR-4**: The system shall allow operators to associate sensors and actuators with specific greenhouse zones.
- **FR-5**: The system shall maintain zone components in a composite structure capable of aggregating operational status across all contained devices.
- **FR-6**: The system shall provide visual zone summaries and detailed individual zone diagnostics upon operator request.

#### Subsystem 2: Sensor Management and Telemetry
- **FR-7**: The system shall support heterogeneous sensor models including soil moisture sensors, ambient temperature sensors, and sunlight/lux sensors through a common sensor abstraction.
- **FR-8**: The system shall maintain identifying metadata, operational status, engineering units, associated zone, and timestamped readings for each registered sensor.
- **FR-9**: The system shall periodically acquire telemetry readings from all operational sensors as virtual simulation time advances.
- **FR-10**: The system shall generate an update event and broadcast telemetry whenever a sensor measurement changes or exceeds configured boundary values.
- **FR-11**: The system shall detect and record sensor failure states when a sensor produces invalid readings or becomes unresponsive.

#### Subsystem 3: Actuator Management and Manual Override
- **FR-12**: The system shall model heterogeneous actuators including irrigation pumps, heating coils/systems, and automated shade curtains through a common actuator abstraction.
- **FR-13**: The system shall allow authorized automation rules and operators to activate, deactivate, and configure operational parameters of any registered actuator.
- **FR-14**: The system shall allow operators to issue priority manual override commands to force an actuator into an active or inactive state.
- **FR-15**: The system shall maintain an explicit operational mode indicator (Automatic vs. Manual Override) for every actuator.
- **FR-16**: When an actuator is placed under manual override, the system shall suppress automated rule activations directed at that specific actuator until manual control is relinquished.
- **FR-17**: The system shall allow operators to return a manually overridden actuator back to automatic regulation.
- **FR-18**: The system shall log all actuator state transitions along with the commanding provenance (Rule Engine vs. Manual Operator).

#### Subsystem 4: Rule Engine and Polymorphic Processing
- **FR-19**: The system shall provide an extensible rule evaluation engine that processes environmental events dispatched by sensors.
- **FR-20**: The system shall evaluate environmental conditions polymorphically through specialized condition subclasses without inspecting concrete device types.
- **FR-21**: The system shall evaluate boundary conditions including low soil moisture, excessive heat, sub-threshold frost conditions, and excessive solar irradiance.
- **FR-22**: The system shall evaluate compound multi-variable conditions combining multiple environmental metrics simultaneously.
- **FR-23**: The system shall trigger corresponding environmental correction actions when evaluation rule conditions evaluate to true.
- **FR-24**: The system shall deactivate triggered actuators when environmental metrics return within acceptable target ranges.

#### Subsystem 5: Control Strategy Management
- **FR-25**: The system shall support interchangeable environmental control policies via a common strategy abstraction.
- **FR-26**: The system shall implement an **EcoMode** strategy that minimizes water and electricity consumption by extending acceptable environmental tolerances and deferring non-critical actuation.
- **FR-27**: The system shall implement a **HighYieldGrowth** strategy that prioritizes optimal micro-climate conditions to maximize crop growth rates.
- **FR-28**: The system shall implement a **FrostProtection** strategy that prioritizes heating and enclosure protection over power conservation during low-temperature events.
- **FR-29**: The system shall allow operators to switch the active control strategy at runtime without restarting the application or modifying core rule engine components.

#### Subsystem 6: Event-Driven Pipeline and Notifications
- **FR-30**: The system shall distribute telemetry notifications from sensors to subscribers via an asynchronous publish-subscribe observer mechanism.
- **FR-31**: The system shall dispatch high-priority alert notifications to the user interface when critical environmental conditions (drought, frost, extreme overheating) are detected.
- **FR-32**: The system shall dispatch warning alerts when device faults or conflicting rule directives are detected.
- **FR-33**: The system shall maintain historical telemetry measurements and system alert logs separated from current device states.

#### Subsystem 7: Simulation and Virtual Time Progression
- **FR-34**: The system shall provide a virtual simulation clock supporting discrete step-by-step advancement and continuous scaled-time progression.
- **FR-35**: As virtual time progresses, the system shall dynamically calculate environmental changes including soil moisture evaporation, thermal dissipation, and solar diurnal cycles.
- **FR-36**: The system shall allow operators to pause, resume, and adjust the execution speed factor of the virtual simulation clock.

#### Subsystem 8: Monitoring Dashboard and User Interface
- **FR-37**: The system shall render a centralized monitoring dashboard presenting real-time zone states, sensor readings, active actuators, and the currently active control strategy.
- **FR-38**: The system shall provide visual indications explaining the rationalization behind each automated actuator command (e.g., triggered rule, initiating sensor, active strategy).

### 3.3 Nonfunctional requirements

#### 3.3.1 Usability
- **NFR-1**: The user interface shall provide clear visual separation between automatic system activations and manual operator overrides.
- **NFR-2**: All critical environmental alerts (e.g., frost hazard, severe drought) shall be visually prominent within the monitoring dashboard within 1 second of occurrence.
- **NFR-3**: The dashboard shall display all environmental metrics using standardized engineering units (Celsius for temperature, percentage for moisture, Lux for illumination).

#### 3.3.2 Reliability
- **NFR-4**: The software engine shall handle individual sensor failure events without crashing or corrupting adjacent zone monitoring routines.
- **NFR-5**: Conflicting rule evaluations (e.g., simultaneous heat and vent requests) shall fail gracefully into safe fallback states governed by the active control strategy.
- **NFR-6**: The system state shall remain consistent under rapid simulation clock speed multipliers (up to 100x real-time speed).

#### 3.3.3 Performance
- **NFR-7**: The event dispatch pipeline shall deliver a sensor state update to all registered observers within 50 milliseconds in a simulated execution environment.
- **NFR-8**: The rule engine shall complete evaluation of all registered zone rules within 100 milliseconds following a telemetry update event.
- **NFR-9**: The dashboard user interface shall maintain a minimum rendering refresh rate of 30 frames per second during continuous simulation.

#### 3.3.4 Supportability
- **NFR-10**: The architecture shall allow adding new sensor models or actuator types by subclassing base abstractions without modifying existing zone or rule engine classes (Open/Closed Principle).
- **NFR-11**: The strategy pipeline shall allow integration of new specialized control policies without recompilation or alteration of the domain model.

#### 3.3.5 Implementation
- **NFR-12**: The application shall be designed following strict object-oriented paradigms using a strongly-typed object-oriented language.
- **NFR-13**: The system shall strictly decouple domain model classes from presentation components and concrete persistence stores.

#### 3.3.6 Interface
- **NFR-14**: All device abstractions (Sensor, Actuator) shall expose standardized, contract-based programming interfaces.
- **NFR-15**: The presentation tier shall interact with domain models exclusively through defined controller and facade interfaces.

#### 3.3.7 Packaging
- **NFR-16**: The complete deliverable shall be packaged and version-controlled within the official team GitHub repository according to course guidelines.
- **NFR-17**: The project repository shall contain all documentation, architectural diagrams, and build configuration files required for execution.

#### 3.3.8 Legal
- **NFR-18**: The software and documentation shall comply with academic honesty regulations and the course project collaboration guidelines.
- **NFR-19**: Any third-party software libraries utilized shall adhere to open-source licenses compatible with educational and commercial development.

### 3.4 System models
*TBD*

---

## 4 Glossary of Terms

*Section 4 content to be detailed in subsequent revision.*

---

## 5 Priority

*Section 5 content to be detailed in subsequent revision.*

---

## 6 Traceability

*Section 6 content to be detailed in subsequent revision.*
