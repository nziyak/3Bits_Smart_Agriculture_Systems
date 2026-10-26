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

*Section 2 content to be detailed in subsequent revision.*

---

## 3 Proposed system

*Section 3 content to be detailed in subsequent revision.*

### 3.1 Overview
*TBD*

### 3.2 Functional requirements
*TBD*

### 3.3 Nonfunctional requirements
*TBD*

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
