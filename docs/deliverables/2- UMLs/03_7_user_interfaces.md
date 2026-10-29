#### 3.4.5 User interfaces and Mock-ups

##### Screen 1: Master Dashboard & Zone Overview
```
+----------------------------------------------------------------------------------------------------+
| SMART AGRICULTURE & GREENHOUSE IOT CONTROLLER SYSTEM                  [Sim Time: 14:32:00 | 10x]   |
+----------------------------------------------------------------------------------------------------+
| ACTIVE STRATEGY: [ EcoMode (Resource Conservation) ]  [ Change Policy ]   | Alerts: [2 Critical]  |
+----------------------------------------------------------------------------------------------------+
| ZONE 1: TOMATO GREENHOUSE (Sector A)              | ZONE 2: NURSERY & SEEDLINGS (Sector B)         |
| Status: NORMAL                                    | Status: ALERT (FROST HAZARD WARNING)           |
|---------------------------------------------------|------------------------------------------------|
| Soil Moisture:    28.4 %   [ OK ]                 | Soil Moisture:    42.1 %   [ OK ]              |
| Temperature:      23.1 C   [ OK ]                 | Temperature:       1.8 C   [ CRITICAL LOW ]    |
| Sunlight Level:   850 Lux  [ OK ]                 | Sunlight Level:   120 Lux  [ LOW ]             |
|---------------------------------------------------|------------------------------------------------|
| ACTUATORS:                                        | ACTUATORS:                                     |
|  - Irrigation Pump:   [ OFF ] (AUTO)              |  - Irrigation Pump:   [ OFF ] (AUTO)           |
|  - Heating Coils:     [ OFF ] (AUTO)              |  - Heating Coils:     [ ON  ] (AUTO - Frost)   |
|  - Shade Curtains:    [ OPEN] (AUTO)              |  - Shade Curtains:    [ CLOSED] (AUTO)         |
| [ View Zone Details ]   [ Manual Controls ]       | [ View Zone Details ]   [ Manual Controls ]    |
+----------------------------------------------------------------------------------------------------+
| RECENT SYSTEM ALERTS & EVENT LOG:                                                                  |
| [14:31:45] CRITICAL: Zone 2 Temperature dropped to 1.8 C (Threshold: 3.0 C).                       |
| [14:31:46] ACTION: Zone 2 Heating Coils forced ON by FrostProtection strategy.                     |
| [14:28:10] NOTICE: Zone 1 Irrigation completed. Soil moisture recovered to 28.4%.                 |
+----------------------------------------------------------------------------------------------------+
```

##### Screen 2: Zone Detail and Actuator Manual Override Console
```
+----------------------------------------------------------------------------------------------------+
| ZONE 1: DETAILED CONTROLS & TELEMETRY                                          [ Return to Master ]|
+----------------------------------------------------------------------------------------------------+
| SENSOR TELEMETRY                                  | TARGET THRESHOLDS                              |
| - Soil Moisture Sensor #1: 24.2 %                 | - Moisture Target: 30% (+/- 5%)                |
| - Ambient Temp Sensor #1:  22.8 C                 | - Temperature Target: 24 C (+/- 2 C)           |
| - Sunlight Sensor #1:      740 Lux                | - Sunlight Target: 800 Lux (+/- 100 Lux)       |
+---------------------------------------------------+------------------------------------------------+
| ACTUATOR HARDWARE & MANUAL OVERRIDE CONSOLE                                                        |
|----------------------------------------------------------------------------------------------------|
| ACTUATOR NAME       | CURRENT STATE | MODE             | MANUAL ACTION CONTROLS                    |
|---------------------|---------------|------------------|-------------------------------------------|
| Irrigation Pump #1  | [ ON  ]       | MANUAL OVERRIDE  | [ FORCE ON ]  [ FORCE OFF ]  [ RELEASE ]  |
| Heating Coils #1    | [ OFF ]       | AUTOMATIC        | [ FORCE ON ]  [ FORCE OFF ]  [ RELEASE ]  |
| Shade Curtains #1   | [ OPEN]       | AUTOMATIC        | [ FORCE ON ]  [ FORCE OFF ]  [ RELEASE ]  |
+----------------------------------------------------------------------------------------------------+
| RECENT RULE EVALUATIONS FOR ZONE 1:                                                                |
| - LowMoistureRule: TRIGGERED -> Action SUPPRESSED due to active Manual Override.                   |
| - HighTempVentRule: NOT TRIGGERED (Temperature within optimal window).                             |
+----------------------------------------------------------------------------------------------------+
```

##### Navigational Paths & Screen Transitions

```mermaid
flowchart TD
    S1[Screen 1: Master Dashboard] -->|Click Zone Card| S2[Screen 2: Zone Details & Override]
    S1 -->|Click Change Policy| S3[Screen 3: Strategy Selection Modal]
    S1 -->|Click View All Logs| S4[Screen 4: Historical Log & Alert Archive]
    S2 -->|Click Return| S1
    S3 -->|Confirm Policy| S1
    S4 -->|Click Return| S1
```

---
