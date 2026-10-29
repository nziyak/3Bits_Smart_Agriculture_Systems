#### 3.4.4 Dynamic model

##### Sequence Diagram 1: Telemetry Event, Rule Evaluation, and Actuator Dispatch

```mermaid
sequenceDiagram
    autonumber
    actor Sim as SimulationClock
    participant S as TemperatureSensor
    participant EB as EventDispatcher (Observer)
    participant RE as RuleEngine
    participant CS as ControlStrategy (FrostProtection)
    participant A as HeatingSystem
    participant UI as DashboardUI

    Sim->>S: advanceTime(step)
    S->>S: sampleEnvironment() [Reading: 1.2 C]
    S->>EB: publish(SensorUpdateEvent)
    
    activate EB
    EB->>UI: notifyTelemetryUpdate(S)
    EB->>RE: onSensorEvent(SensorUpdateEvent)
    activate RE
    
    RE->>RE: evaluateRule(FrostHazardRule)
    Note over RE: Condition Met: 1.2 C < 3.0 C Threshold
    
    RE->>CS: arbitrateAction(FrostHazardRule, HeatingSystem)
    activate CS
    CS-->>RE: approvedCommand(ACTIVATE, capacity=1.0)
    deactivate CS
    
    RE->>A: executeCommand(ACTIVATE)
    activate A
    A->>A: setActive(true)
    A-->>RE: commandAcknowledged(isActive=true)
    deactivate A
    
    RE->>EB: publish(ActuatorStateChangeEvent)
    RE->>EB: publish(AlertEvent: CRITICAL_FROST)
    deactivate RE
    
    EB->>UI: notifyActuatorUpdate(A)
    EB->>UI: displayAlert(CRITICAL_FROST)
    deactivate EB
```

##### Sequence Diagram 2: Manual Operator Override and Automation Suppression

```mermaid
sequenceDiagram
    autonumber
    actor Op as Greenhouse Operator
    participant UI as DashboardUI
    participant Ctrl as ActuatorController
    participant Act as IrrigationPump
    participant RE as RuleEngine

    Op->>UI: click "Force Inactive" on IrrigationPump
    UI->>Ctrl: submitManualOverride(pumpId, FORCE_OFF)
    activate Ctrl
    
    Ctrl->>Act: setControlMode(MANUAL_OVERRIDE)
    Ctrl->>Act: setActive(false)
    Act-->>Ctrl: confirmed(mode=MANUAL_OVERRIDE, active=false)
    
    Ctrl->>UI: renderManualLockIndicator(pumpId)
    deactivate Ctrl

    Note over RE: Subsequent Telemetry Triggers LowMoistureRule
    RE->>Act: inspectStatus()
    Act-->>RE: returnStatus(mode=MANUAL_OVERRIDE)
    Note over RE: Command Suppressed: Actuator under Operator Lock
    RE->>UI: logSuppressedActionNotice(pumpId)
```

##### State Machine Diagram: Actuator Lifecycle & Control State

```mermaid
stateDiagram-v2
    [*] --> Inactive_Auto : Initialize

    state Automatic_Control {
        Inactive_Auto --> Active_Auto : Rule Condition Met [Strategy Approved]
        Active_Auto --> Inactive_Auto : Target Reached / Rule Expired
    }

    state Manual_Override {
        Active_Manual --> Inactive_Manual : Operator Commands Force Off
        Inactive_Manual --> Active_Manual : Operator Commands Force On
    }

    Automatic_Control --> Inactive_Manual : Operator Manual Override [Force Off]
    Automatic_Control --> Active_Manual : Operator Manual Override [Force On]

    Manual_Override --> Inactive_Auto : Operator Releases Override [Condition Normal]
    Manual_Override --> Active_Auto : Operator Releases Override [Condition Critical]

    Automatic_Control --> Fault_State : Hardware Malfunction Detected
    Manual_Override --> Fault_State : Hardware Malfunction Detected
    Fault_State --> Inactive_Auto : Fault Cleared & Re-initialized
```

---
