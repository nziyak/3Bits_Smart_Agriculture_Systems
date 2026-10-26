# Smart Agriculture and Greenhouse IoT Controller System (3Bits)

## Overview

The **Smart Agriculture & Greenhouse IoT Controller System** is an event-driven software simulation and monitoring platform engineered to manage an automated greenhouse environment. The system models heterogeneous physical devices—such as sensors, actuators, environmental zones, automation rules, and control policies—as collaborating software objects following rigorous Object-Oriented Analysis and Design (OOAD) principles.

By leveraging decoupled event pipelines and industry-standard design patterns, the platform continuously acquires environmental telemetry, evaluates multi-condition operational rules, resolves policy conflicts via interchangeable strategies, and orchestrates physical actuators to maintain optimal growing conditions.

---

## Key Objectives

- **Model Physical Hardware as Software Abstractions**: Establish flexible, extensible object hierarchies for heterogeneous sensors and actuators.
- **Event-Driven Decoupled Architecture**: Eliminate direct dependencies between telemetry producers, business logic engines, and presentation layers.
- **Dynamic Policy Execution**: Support runtime interchangeability of greenhouse management objectives (e.g., resource conservation versus yield optimization).
- **Hierarchical Facility Management**: Model multi-zone greenhouse layouts where components can be addressed individually or collectively.
- **Comprehensive Virtual Simulation**: Provide virtual time progression to simulate environmental volatility, hardware faults, and automated mitigation.

---

## System Architecture

The system follows a modular multi-tier architecture to ensure high cohesion and loose coupling across components:

```
+-------------------------------------------------------------+
|                     User Interface / Dashboard              |
+-------------------------------------------------------------+
                              |
+-------------------------------------------------------------+
|                Monitoring & Event Bus Layer                 |
+-------------------------------------------------------------+
                              |
+-------------------------------------------------------------+
|             Rule Engine & Polymorphic Processing            |
+-------------------------------------------------------------+
                              |
+-------------------------------------------------------------+
|                 Control Strategy Pipeline                   |
+-------------------------------------------------------------+
                              |
+-------------------------------------------------------------+
|               Composite Zone & Hardware Layer               |
|            (Sensors, Actuators, Zones, Controllers)         |
+-------------------------------------------------------------+
                              |
+-------------------------------------------------------------+
|                     Persistence Layer                       |
|           (Configurations, Telemetry, Event Logs)           |
+-------------------------------------------------------------+
```

### Applied Design Patterns

- **Composite Pattern (Zone and Component Management)**:
  Greenhouse zones and device groupings are structured as composite hierarchies. This allows individual devices and aggregate zones to be managed uniformly through shared component interfaces (e.g., querying operational status or dispatching collective shutdown commands).

- **Observer Pattern (Event-Driven Telemetry Distribution)**:
  Sensors publish state transitions and measurement updates to registered subscribers without maintaining direct dependencies on consumers. Observers include monitoring services, alert dispatchers, rule evaluation engines, and real-time dashboard components.

- **Strategy Pattern (Interchangeable Control Policies)**:
  Alternative environmental management policies are encapsulated behind a common `ControlStrategy` interface. This allows dynamic switching between distinct operational modes at runtime without modifying core rule evaluation or greenhouse component logic.

---

## Functional Capabilities

### 1. Zone and Facility Management
- Multi-zone virtual greenhouse architecture supporting independently managed spatial zones.
- Configuration of distinct environmental targets and tolerances per zone.
- Dynamic association and grouping of sensors and actuators within target zones.
- Real-time global facility overview and detailed zone-level diagnostic inspection.

### 2. Sensor Telemetry Subsystem
- Common abstraction (`Sensor`) providing standardized telemetry interfaces across heterogeneous hardware:
  - **Soil Moisture Sensors**: Volumetric water content measurements.
  - **Ambient Temperature Sensors**: Thermal equilibrium tracking.
  - **Sunlight / Lux Sensors**: Solar irradiance and photometric monitoring.
- Telemetry metadata: Device identifier, sensor type, current measurement, engineering units, operational status, zone assignment, and update timestamps.

### 3. Actuator Subsystem and Manual Overrides
- Common abstraction (`Actuator`) implementing device-specific control behavior:
  - **Irrigation Pumps**: Soil hydration and water delivery management.
  - **Heating Coils / Systems**: Thermal regulation and frost mitigation.
  - **Automated Shade Curtains**: Sunlight attenuation and exposure regulation.
- Lifecycle commands: Activation, deactivation, status inspection, and operating parameter tuning.
- Priority manual control: Allows operators to override automated commands, inspect control provenance (manual vs. automated), and return actuators to automated regulation.

### 4. Polymorphic Rule Processing Engine
- Event-triggered evaluation of environmental conditions against operational thresholds.
- Specialized condition evaluators:
  - Low / High soil moisture thresholds.
  - Critical minimum / maximum temperature boundaries.
  - Excessive solar radiation levels.
  - Compound multi-variable environmental conditions.
- Polymorphic rule execution ensures extensible addition of new rule types without modifying core evaluation pipelines.

### 5. Dynamic Control Strategies
- **EcoMode**: Minimizes resource consumption (conserves water and energy by permitting wider operational tolerance bands).
- **HighYieldGrowth**: Prioritizes optimal micro-climate conditions to maximize crop yield and growth rates.
- **FrostProtection**: Prioritizes emergency thermal preservation and insulation to protect crops against low-temperature damage.

### 6. Event-Driven Workflow
1. Sensor generates a measurement update event upon state or reading changes.
2. Registered observers receive notifications across the event dispatch pipeline.
3. Rule evaluation engines assess environmental conditions against active thresholds.
4. Active control strategy resolves conflicting directives and dictates appropriate actions.
5. Target actuators are activated, deactivated, or reconfigured accordingly.
6. System telemetry and user interfaces update to reflect state transitions.

### 7. Simulation and Time Progression
- Virtual time engine supporting discrete time-step advancement or continuous scaled execution.
- Dynamic modeling of environmental fluctuations, weather changes, and device degradation.
- Verification and demonstration platform for automated control behavior under simulated conditions.

### 8. Monitoring Dashboard and Diagnostic Alerts
- Comprehensive system monitoring dashboard displaying zone health, sensor telemetry, active actuators, current control strategies, and triggered rules.
- Real-time alert notifications for critical conditions: extreme temperatures, soil drought, sensor/actuator faults, and rule conflicts.
- Separation of historical telemetry logs from live device state.

---

## Repository Structure

```
.
|-- docs/
|   |-- deliverables/
|   |   `-- 1-requirements-analysis/
|   |       |-- RAD.md                 # Requirements Analysis Document (Deliverable #1)
|   |       `-- *.pdf                  # Course assignment brief and RAD template
|   `-- project-definition/            # Formal project specification and requirements
`-- README.md                          # Project documentation and architectural overview
```

---

## Academic Information

- **Course**: CSE443 - Object-Oriented Analysis and Design
- **Deliverable**: Smart Agriculture & Greenhouse IoT Controller Systems
- **Team**: 3Bits
- **Team Members**:
  - Nuri Ziya Kırtepe
  - Muhammed Korkmaz
  - Derya Uysal
