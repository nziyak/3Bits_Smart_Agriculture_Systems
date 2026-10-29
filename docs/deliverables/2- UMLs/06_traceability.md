## 6 Traceability

The traceability matrix establishes bi-directional mapping between the initial Project Definition specifications, the Functional Requirements (FR), the Use Cases (UC), and the Conceptual Object Model classes.

| Project Definition Section | Requirement ID (FR) | Associated Use Case | Conceptual Domain Classes |
| :--- | :--- | :--- | :--- |
| **3.1 Greenhouse & Zone Mgmt** | FR-1, FR-2, FR-3, FR-4, FR-5, FR-6 | UC-1, UC-2, UC-3 | `Greenhouse`, `Zone`, `GreenhouseComponent` |
| **3.2 Sensor Management** | FR-7, FR-8, FR-9, FR-11 | UC-2, UC-5 | `Sensor`, `SoilMoistureSensor`, `TemperatureSensor`, `SunlightSensor` |
| **3.3 Sensor Data Monitoring** | FR-9, FR-10, FR-30, FR-33 | UC-5, UC-8 | `Sensor`, `GreenhouseComponent`, `SimulationClock` |
| **3.4 Actuator Management** | FR-12, FR-13, FR-18 | UC-2, UC-10 | `Actuator`, `IrrigationPump`, `HeatingSystem`, `ShadeCurtain` |
| **3.5 Rule-Based Control** | FR-19, FR-21, FR-23, FR-24 | UC-8, UC-10 | `Rule`, `ThresholdRule`, `Actuator` |
| **3.6 Polymorphic Rule Processing** | FR-20, FR-21, FR-22 | UC-8 | `Rule`, `ThresholdRule`, `CompoundRule` |
| **3.7 Control Strategies** | FR-25, FR-26, FR-27, FR-28, FR-29 | UC-4, UC-8 | `ControlStrategy`, `EcoMode`, `HighYieldGrowth`, `FrostProtection` |
| **3.8 Event-Driven Automation** | FR-10, FR-19, FR-23, FR-30 | UC-7, UC-8, UC-10 | `Sensor`, `Rule`, `Actuator`, `SimulationClock` |
| **3.9 Manual Control** | FR-14, FR-15, FR-16, FR-17, FR-18 | UC-6 | `Actuator`, `GreenhouseComponent` |
| **3.10 Alerts & Notifications** | FR-31, FR-32, FR-33 | UC-9 | `Alert`, `Zone`, `Sensor` |
| **3.11 Simulation & Time Progression** | FR-34, FR-35, FR-36 | UC-7 | `SimulationClock`, `Greenhouse`, `Sensor` |
| **3.12 System Monitoring & Dashboard**| FR-37, FR-38 | UC-5 | `Greenhouse`, `Zone`, `Alert`, `ControlStrategy` |
| **4.0 Technical Architecture** | NFR-10, NFR-11, NFR-12, NFR-14 | All Use Cases | All Domain Model Classes |
