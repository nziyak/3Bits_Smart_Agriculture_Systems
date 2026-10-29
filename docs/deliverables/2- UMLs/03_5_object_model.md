#### 3.4.3 Object model

The Conceptual Domain Model represents domain concepts, attributes, and relationships without implementation details (such as concrete class methods or database foreign keys), adhering strictly to the analysis activity standards.

```mermaid
classDiagram
    direction TB

    class Greenhouse {
        String greenhouseId
        String name
        String location
    }

    class Zone {
        String zoneId
        String name
        String cropType
        Float targetTemperature
        Float targetMoisture
        Float targetSunlight
    }

    class GreenhouseComponent {
        <<Abstract>>
        String componentId
        String name
        Boolean operationalStatus
    }

    class Sensor {
        <<Abstract>>
        String sensorId
        String sensorType
        Float currentReading
        String unitOfMeasure
        DateTime lastUpdated
    }

    class SoilMoistureSensor {
        Float depthCentimeters
    }

    class TemperatureSensor {
        Float calibrationOffset
    }

    class SunlightSensor {
        Float spectrumRangeNm
    }

    class Actuator {
        <<Abstract>>
        String actuatorId
        String actuatorType
        Boolean isActive
        String controlMode
        DateTime stateChangedAt
    }

    class IrrigationPump {
        Float flowRateLitersPerMin
    }

    class HeatingSystem {
        Float maxHeatOutputKw
    }

    class ShadeCurtain {
        Float opacityPercentage
    }

    class Rule {
        <<Abstract>>
        String ruleId
        String ruleName
        Boolean isEnabled
    }

    class ThresholdRule {
        String metricType
        String comparisonOperator
        Float thresholdValue
    }

    class CompoundRule {
        String logicalOperator
    }

    class ControlStrategy {
        <<Abstract>>
        String strategyName
        String description
    }

    class EcoMode {
        Float conservationFactor
    }

    class HighYieldGrowth {
        Float toleranceWindow
    }

    class FrostProtection {
        Float criticalThresholdCelsius
    }

    class Alert {
        String alertId
        String severityLevel
        String message
        DateTime timestamp
        Boolean isAcknowledged
    }

    class SimulationClock {
        DateTime virtualTime
        Float timeScaleMultiplier
        Boolean isRunning
    }

    class RuleEngine {
        String engineId
        Boolean isEnabled
    }

    class EventDispatcher {
        String dispatcherId
    }

    class ActuatorController {
        String controllerId
    }

    class DashboardUI {
        String dashboardId
    }

    %% Relationships
    Greenhouse "1" *-- "1..*" Zone : contains
    Zone --|> GreenhouseComponent
    Sensor --|> GreenhouseComponent
    Actuator --|> GreenhouseComponent

    Zone "1" *-- "0..*" GreenhouseComponent : aggregates (Composite)

    Sensor <|-- SoilMoistureSensor
    Sensor <|-- TemperatureSensor
    Sensor <|-- SunlightSensor

    Actuator <|-- IrrigationPump
    Actuator <|-- HeatingSystem
    Actuator <|-- ShadeCurtain

    Zone "1" o-- "0..*" Rule : evaluates
    Rule <|-- ThresholdRule
    Rule <|-- CompoundRule

    Rule "0..*" --> "1" Actuator : targets
    Rule "0..*" ..> ControlStrategy : arbitrated by

    ControlStrategy <|-- EcoMode
    ControlStrategy <|-- HighYieldGrowth
    ControlStrategy <|-- FrostProtection

    Zone "1" o-- "0..*" Alert : generates
    SimulationClock "1" ..> Greenhouse : drives
    Sensor "0..*" ..> EventDispatcher : publishes readings
    EventDispatcher "1" --> "1" RuleEngine : notifies
    EventDispatcher "1" --> "1" DashboardUI : updates
    RuleEngine "1" --> "0..*" Rule : evaluates
    RuleEngine "1" --> "1" ControlStrategy : consults
    RuleEngine "1" ..> Actuator : issues approved commands
    DashboardUI "1" ..> ActuatorController : submits override
    ActuatorController "1" --> "0..*" Actuator : controls
```

---
