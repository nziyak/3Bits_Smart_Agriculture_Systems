### 3.4 System models

#### 3.4.1 Scenarios

##### Scenario 1: Low Soil Moisture Event and Automated Irrigation in EcoMode
- **Context**: Zone 1 contains tomato crops. The active control strategy is set to **EcoMode**. Virtual time advances to 14:00.
- **Execution**:
  1. The Soil Moisture Sensor in Zone 1 measures 22% volumetric water content (below the configured 25% threshold).
  2. The sensor generates a `SensorUpdateEvent` and broadcasts it to registered observers.
  3. The Rule Engine evaluates the `LowMoistureRule`.
  4. The active strategy (**EcoMode**) evaluates the condition: because EcoMode is designed for resource conservation, it checks if the reading is below the absolute safety limit (20%) or if off-peak evaporation hours apply. It approves a short, pulsed irrigation cycle.
  5. The Irrigation Pump actuator for Zone 1 is activated with a 5-minute duty cycle.
  6. The dashboard updates, displaying the active pump and an audit notice: *"Zone 1 Irrigation Pump activated by LowMoistureRule under EcoMode"*.

##### Scenario 2: Sudden Temperature Drop and FrostProtection Intervention
- **Context**: Nighttime simulation in Zone 2. Ambient temperature drops rapidly due to a simulated cold front.
- **Execution**:
  1. Ambient Temperature Sensor records a decline from 6°C to 1.5°C (falling below the 3°C frost hazard threshold).
  2. The sensor fires an urgent event notification.
  3. The Rule Engine evaluates the `FrostHazardRule`.
  4. The active strategy (**FrostProtection**) preempts all other non-critical operations and immediately commands:
     - Heating coils in Zone 2 are activated to 100% capacity.
     - Automated shade/thermal curtains are closed to retain ambient radiant heat.
  5. The notification subsystem dispatches a high-priority `CRITICAL_ALERT: Frost Condition Detected in Zone 2`.
  6. The dashboard highlights Zone 2 in red and presents the active heating intervention.

##### Scenario 3: Manual Actuator Override and Mode Synchronization
- **Context**: A human greenhouse supervisor inspects Zone 1 and observes maintenance work requiring dry soil.
- **Execution**:
  1. The operator selects Zone 1's Irrigation Pump on the dashboard console.
  2. The operator selects "Manual Override: FORCE OFF".
  3. The system sets the pump's operational mode to `MANUAL_OVERRIDE` and forces the actuator state to `INACTIVE`.
  4. A subsequent sensor update triggers the automated `LowMoistureRule`.
  5. The rule engine inspects the actuator status, identifies the `MANUAL_OVERRIDE` lock, and suppresses the automated turn-on signal.
  6. The system logs: *"Automated activation suppressed for Zone 1 Irrigation Pump (Manual Override Active)"*.
  7. When maintenance completes, the operator toggles the pump back to `AUTOMATIC`. Automated rule processing resumes.

---
