# Project: Retro Roomba Revival

## Overview

**One-line description:** Bring a Roomba 650/655 into the Viam ecosystem with a custom driver module

**Project Lead:** TBD
**Team Members:** TBD
**Status:** New

## Description

Retro Roomba Revival integrates a Roomba 650/655 with Viam by building a custom driver module from scratch. The project implements the Roomba Open Interface protocol over serial, exposes the robot's sensors and actuators through standard Viam component APIs, and demonstrates the full module development lifecycle from prototype to fleet deployment.

No computer vision—just serial communication, bump sensors, and clean abstractions.

## Viam Capabilities Demonstrated

### Core Capabilities
- [x] **Hardware Integration** — Roomba base, bump sensors, power sensor, movement sensor
- [ ] **Motion Planning** — Not applicable (simple base control)
- [ ] **Vision / ML Inference** — Not applicable (bump sensor based)
- [x] **Data Capture & Sync** — Sensor logs, battery cycles, patrol data
- [x] **Remote Operation** — Control through app and SDKs via WebRTC
- [x] **Module Development** — Primary: build driver module from scratch

### Scale & Fleet Capabilities
- [x] **Fragments** — Hardware fragment for Roomba configuration
- [ ] **Fleet Management** — Stretch: multiple Roombas
- [x] **OTA Updates** — Publish and version driver via Registry
- [ ] **Provisioning** — Stretch: streamlined multi-Roomba setup

### Operational Capabilities
- [x] **Event-Driven Automation** — Low battery, dock needed, bump detected
- [ ] **Scheduled Tasks** — Stretch: scheduled patrol times
- [ ] **Monitoring & Alerting** — Backlog: battery degradation alerts
- [ ] **Data Pipeline (ML Training)** — Not applicable

### Customer-Facing Capabilities
- [ ] **Customer Delivery** — Stretch: guest control interface
- [ ] **Web/Mobile Apps** — Backlog: TypeScript/Flutter control apps

### Primary Focus
- **Custom Module Development** — Build complete driver from scratch
- **Hardware Abstraction** — Implement base, sensor, power_sensor, movement_sensor APIs
- **Protocol Implementation** — Roomba Open Interface serial protocol

---

## Hardware Requirements

| Component | Description | Options |
|-----------|-------------|---------|
| Roomba | 600 series base | Roomba 650 or 655 |
| Compute | Main controller | Raspberry Pi 5 |
| Serial Adapter | Connect Pi to Roomba | Mini-DIN cable + logic level converter |

**Remote-Friendly:** Partially - protocol/module development remote, physical testing requires hardware

---

## MVP Options

Select one for hackathon scope:

### Option A: Basic Drive Control (Recommended)
Drive Roomba from Viam app, read sensors.
- **Complexity:** Medium
- **Demo Appeal:** Medium
- **Scope:** Serial protocol, base API, basic sensors

### Option B: Full Sensor Suite
All Roomba sensors exposed through Viam.
- **Complexity:** Medium-High
- **Demo Appeal:** Medium
- **Scope:** Complete sensor implementation

**Selected MVP:** _______________

---

## Backlog

### 1. Driver Module

Build the core Viam module that controls the Roomba.

#### 1.1 Module Structure
- [ ] Create module scaffold (main.go, meta.json, resource registration)
- [ ] Implement `base.Base` interface (SetVelocity, SetPower, Stop, IsMoving)
- [ ] Handle serial port configuration via attributes
- [ ] Implement `Reconfigure()` for config changes without restart
- [ ] Implement `Close()` for clean shutdown

#### 1.2 Additional Component APIs
- [ ] Implement `sensor.Sensor` for bump sensors
- [ ] Implement `power_sensor.PowerSensor` for battery state
- [ ] Implement `movement_sensor.MovementSensor` for wheel odometry
- [ ] Single config entry creates all Roomba resources

#### 1.3 Roomba Protocol
- [ ] OI initialization (Start, Safe, Full mode commands)
- [ ] Sensor packet parsing (decode binary data)
- [ ] Drive command encoding
- [ ] Error handling (timeouts, reconnection)

#### 1.4 Testing
- [ ] Unit tests for protocol encoding/decoding
- [ ] Mock serial port for module testing
- [ ] Integration tests using Python SDK

---

### 2. Configuration & Fragments

Set up reusable configuration for fleet deployment.

- [ ] Create machine config with Roomba module + components
- [ ] Define attributes schema (serial port, polling rate)
- [ ] Configure frame system for Roomba coordinate frame
- [ ] Extract hardware fragment (Roomba base + sensors)
- [ ] Add fragment variables (serial port, device name)
- [ ] Version the fragment (stable/dev tags)

---

### 3. Application Module

Build robot-side application logic as a Viam module.

- [ ] Create application module (separate from driver module)
- [ ] Implement patrol service (drive patterns, obstacle response)
- [ ] Implement return-to-dock behavior
- [ ] Expose DoCommand for manual activation of behaviors
- [ ] Configure as dependency of driver module

---

### 4. CLI Development

Set up local development workflow against remote hardware.

- [ ] Connect to remote Roomba from laptop via WebRTC
- [ ] Run application module locally during development
- [ ] Iterate without deploying (edit → build → test cycle)
- [ ] Use CLI for manual control and testing
- [ ] Package application module for deployment when ready

---

### 5. Data Pipeline

Configure Viam's built-in data capture and sync.

- [ ] Enable data capture for all sensor components
- [ ] Configure capture frequency per component
- [ ] Set up sync rules (schedule, conditions)
- [ ] View captured data in Viam app
- [ ] Query data via CLI (`viam data` commands)
- [ ] Query data via SDK (DataClient)
- [ ] Analyze battery degradation over time
- [ ] Track patrol efficiency metrics
- [ ] Correlate error patterns (bumps, cliffs, stuck events)

---

### 6. Event-Driven Automation

Configure event-driven behaviors.

- [ ] Low battery alert
- [ ] Bump detection response
- [ ] Cliff detection response
- [ ] Webhook notifications (Slack/Discord)
- [ ] Email alerts
- [ ] Conditional data capture on events
- [ ] Scheduled patrol times

---

### 7. Module Registry

Publish and maintain both modules (driver + application).

- [ ] Write README for each module
- [ ] Complete meta.json (all fields, models)
- [ ] Add example configurations
- [ ] Publish to registry (private first)
- [ ] Semantic versioning and changelog
- [ ] Publish publicly
- [ ] OTA updates to fleet
- [ ] Rollback procedures

---

### 8. Fleet Operations

Scale to multiple Roombas.

- [ ] Deploy second Roomba using same fragments
- [ ] Consistent naming conventions
- [ ] Location-based organization
- [ ] Fleet dashboard view
- [ ] Bulk configuration updates via fragment
- [ ] Fleet-wide data queries
- [ ] Streamlined provisioning flow
- [ ] Viam agent setup

---

### 9. End-User Applications

Build customer-facing interfaces using Viam SDKs.

#### Web Application (TypeScript SDK)
- [ ] Custom control UI
- [ ] Real-time sensor display
- [ ] User authentication
- [ ] Permission scoping (operator roles)

#### Mobile Application (Flutter SDK)
- [ ] Control interface
- [ ] Push notifications

#### Voice Control
- [ ] Voice command integration
- [ ] Natural language → action mapping

---

### 10. Cross-Project Integration

Connect with other Build on Viam projects.

- [ ] Smart Lighting integration (lights follow Roomba)
- [ ] Inventory Tracker integration (report floor items)
- [ ] Home Assistant integration
- [ ] Calendar-based scheduling
- [ ] Multi-Roomba zone assignment
- [ ] Inter-robot collision avoidance

---

## Success Criteria

**MVP Complete When:**
- [ ] Roomba drives from Viam app (SetVelocity works)
- [ ] Battery level readable as sensor
- [ ] Bump sensors cause stops
- [ ] Module published to registry (private)

**v1.0 Complete When:**
- [ ] All Roomba sensors exposed through Viam
- [ ] Module has unit tests
- [ ] Documentation complete
- [ ] Hardware fragment created and versioned

**Full Project Complete When:**
- [ ] Fleet of 2+ Roombas managed together
- [ ] Custom web or mobile control interface
- [ ] Event-driven automation configured
- [ ] Data capture and analysis pipeline working

---

## Documentation Deliverables

- [ ] README with setup instructions
- [ ] Wiring diagram (Pi to Roomba)
- [ ] Configuration examples
- [ ] Roomba Open Interface command reference
- [ ] Module development notes
- [ ] Testing guide
- [ ] Parts list with purchase links

---

## Links

- **Jira Epic:** [TBD]
- **GitHub Repo:** [TBD]
- **Viam Organization:** [TBD]
- **Hardware BOM:** [TBD]

---

## Technical Reference

### Roomba Open Interface

**Connection:**
- Mini-DIN connector on Roomba
- TXD, RXD, GND, battery power
- 5V logic (needs level shifter for 3.3V Pi)
- Default baud: 115200 (Roomba 650/655)

**Key commands:**

| Command | Opcode | Data | Description |
|---------|--------|------|-------------|
| Start | 128 | none | Initialize OI |
| Safe | 131 | none | Safe mode (cliff/bump protection) |
| Full | 132 | none | Full mode (no limits) |
| Drive | 137 | velocity (2), radius (2) | Drive wheels |
| Sensors | 142 | packet ID | Request sensor data |
| Dock | 143 | none | Seek dock |

**Sensor packets:**

| Packet | ID | Bytes | Description |
|--------|----|----|-------------|
| Bump/Wheeldrop | 7 | 1 | Bump and wheel drop flags |
| Cliff Left | 9 | 1 | Left cliff sensor |
| Battery Charge | 25 | 2 | Current charge (mAh) |
| Distance | 19 | 2 | Distance since last (mm) |
| Angle | 20 | 2 | Angle since last (degrees) |

### Module Structure

**Driver Module** (hardware interface):
```
roomba-driver/
├── main.go              # Entry point, resource registration
├── roomba_base.go       # Implements base.Base
├── roomba_sensor.go     # Implements sensor.Sensor (bump)
├── roomba_power.go      # Implements powersensor.PowerSensor
├── roomba_movement.go   # Implements movementsensor.MovementSensor
├── protocol.go          # OI protocol implementation
├── protocol_test.go     # Protocol unit tests
├── meta.json
└── README.md
```

**Application Module** (behaviors):
```
roomba-app/
├── main.go              # Entry point, resource registration
├── patrol.go            # Patrol service implementation
├── behaviors.go         # Return-to-dock, obstacle response
├── meta.json
└── README.md
```

---

## References

- [Roomba Open Interface Specification](https://edu.irobot.com/what-we-offer/create3-resources)
- [iRobot Create 2 OI Spec](https://www.irobot.com/about-irobot/stem/create-2)
