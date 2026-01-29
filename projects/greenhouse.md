# Project: Greenhouse

## Overview

**One-line description:** Automated growing environment with sensing, environmental control, and growth tracking

**Project Lead:** TBD
**Team Members:** TBD
**Status:** New

## Description

Greenhouse is an automated plant growing system that monitors environmental conditions (temperature, humidity, soil moisture, light), controls actuators (pumps, lights, fans), and tracks plant growth over time. The system demonstrates Viam's data capture, cloud sync, remote monitoring, and ML capabilities.

This project naturally exercises the full robotics lifecycle - from prototype through fleet deployment - as it can scale from a single plant pod to multiple grow stations with centralized monitoring.

## Viam Capabilities Demonstrated

### Core Capabilities
- [ ] **Hardware Integration** — Sensors (temp, humidity, soil, light), actuators (pump, lights, fans)
- [ ] **Motion Planning** — Stretch: harvesting arm
- [ ] **Vision / ML Inference** — Backlog: ripeness detection, growth tracking
- [x] **Data Capture & Sync** — Environmental data synced to cloud with offline resilience
- [x] **Remote Operation** — Full remote monitoring and control
- [ ] **Module Development** — Backlog: custom sensor/actuator modules

### Scale & Fleet Capabilities
- [x] **Fragments** — Environment recipes as reusable configurations
- [x] **Fleet Management** — Primary demo: multiple grow stations with centralized monitoring
- [ ] **OTA Updates** — Backlog: push recipe updates to all stations
- [ ] **Provisioning** — Backlog: automated new station setup

### Operational Capabilities
- [x] **Event-Driven Automation** — Threshold-based: humidity, temperature, soil moisture, light
- [x] **Scheduled Tasks** — Periodic readings, daily reports, time-lapse capture
- [x] **Monitoring & Alerting** — Environmental alerts, fleet health dashboard
- [x] **Data Pipeline (ML Training)** — Growth images → labeling → ripeness model → deploy

### Customer-Facing Capabilities
- [ ] **Customer Delivery** — Not applicable
- [ ] **Web/Mobile Apps** — Backlog: environmental dashboard

### Multi-Machine Coordination
- [x] **Multiple sensor stations** — Centralized monitoring, cross-station comparison

## Hardware Requirements

| Component | Description | Options |
|-----------|-------------|---------|
| Sensors | Environmental monitoring | DHT22 (temp/humidity), soil moisture, light sensor, pH |
| Actuators | Environment control | Relay-controlled pump, solenoid, grow lights, fans |
| Camera | Time-lapse & monitoring | USB camera, RPi camera |
| Compute | Main controller | Raspberry Pi 4, Jetson Nano (if ML) |
| Enclosure | Growing environment | IKEA cabinet, grow tent, custom build |
| Growing medium | Plant support | Soil pots, hydroponics, AeroGarden-style |

**Remote-Friendly:** Yes - sensors can be monitored from anywhere, development can be fully remote

---

## MVP Options

Select one for hackathon scope:

### Option A: Monitor + Dashboard
Sensors track temp/humidity/soil moisture, display on web dashboard.
- **Complexity:** Low
- **Demo Appeal:** Medium
- **Scope:** Sensor integration, data capture, basic visualization

### Option B: Monitor + Auto-Water (Recommended)
Above plus automated watering based on soil moisture thresholds.
- **Complexity:** Low-Medium
- **Demo Appeal:** Medium-High
- **Scope:** Adds actuation, threshold logic, closed-loop control

### Option C: Monitor + Water + Lights
Full environment control including grow lights on schedule.
- **Complexity:** Medium
- **Demo Appeal:** High
- **Scope:** Multiple actuators, scheduling, light cycles

### Option D: Single Plant Pod
Small self-contained unit (like AeroGarden) with full monitoring.
- **Complexity:** Low-Medium
- **Demo Appeal:** High
- **Scope:** Compact, portable, good for demos

**Selected MVP:** _______________

---

## Backlog

Select 3-5 items for post-hackathon development:

### Environmental Control
- [ ] **Multi-zone control** - Different settings for different plant types
- [ ] **Recipe management** - Saved profiles for different crops (via fragments)
- [ ] **Climate scheduling** - Day/night cycles, seasonal adjustments
- [ ] **Fan/ventilation control** - Humidity and temperature regulation

### Vision & ML
- [ ] **Ripeness detection** - ML model detects when produce is ready to harvest
- [ ] **Growth tracking** - Measure plant size/health over time
- [ ] **Pest detection** - Identify pests or disease via vision
- [ ] **Growth time-lapse** - Capture images on schedule, compile into video

### Data & Monitoring
- [ ] **Alerting** - Notify when conditions out of range or harvest ready
- [ ] **Historical analysis** - Track growth rates, correlate with conditions
- [ ] **Yield tracking** - Track harvests over time, optimize for yield
- [ ] **Environmental dashboard** - Rich visualization of all metrics

### Scale & Fleet
- [ ] **Multi-station fleet** - Multiple grow stations with centralized monitoring
- [ ] **Cross-station comparison** - Compare growth across different setups
- [ ] **Centralized recipes** - Push environment profiles to all stations

### Event-Driven Automation (Gap Feature)
- [ ] **Humidity threshold** - When humidity < 40%, activate mister automatically
- [ ] **Temperature threshold** - When temp > 85°F, activate fans and send alert
- [ ] **Soil moisture threshold** - When soil dry, start watering cycle
- [ ] **Light level threshold** - Adjust grow lights based on ambient light sensor

### Data Pipeline / ML Training (Gap Feature)
- [ ] **Automated data capture** - Capture images on schedule for training data
- [ ] **Growth stage labeling** - Label images with growth stage for ML training
- [ ] **Train ripeness model** - Use captured data to train harvest-ready detector
- [ ] **Deploy trained model** - Push updated model to all stations via Registry
- [ ] **Model performance tracking** - Compare model accuracy across versions

### Monitoring & Alerting (Gap Feature)
- [ ] **Threshold alerts** - Configure alerts for out-of-range conditions
- [ ] **Fleet health dashboard** - Single view of all station statuses
- [ ] **Daily digest** - Scheduled summary of all station metrics
- [ ] **Anomaly detection** - Alert on unusual patterns (sensor drift, failures)

---

## Stretch Goals

- [ ] Harvesting arm on gantry (complex mechanical addition)
- [ ] Seed planting automation
- [ ] Integration with weather API for outdoor greenhouses
- [ ] Produce delivery handoff to mobile robot
- [ ] Nutrient dosing for hydroponics
- [ ] CO2 monitoring and injection

---

## Success Criteria

**MVP Complete When:**
- [ ] Sensors reading and logging to Viam cloud
- [ ] Dashboard shows current and historical data
- [ ] Automated watering activates correctly (if Option B+)
- [ ] System runs unattended for 24+ hours

**Project Complete When:**
- [ ] Plants successfully grown from seed to harvest
- [ ] All selected backlog items implemented
- [ ] Time-lapse video created
- [ ] Documentation complete

---

## Documentation Deliverables

- [ ] README with setup instructions
- [ ] Hardware wiring guide
- [ ] Sensor calibration guide
- [ ] Fragment templates for different crops
- [ ] Dashboard configuration
- [ ] Time-lapse setup guide

---

## Links

- **Jira Epic:** [TBD]
- **GitHub Repo:** [TBD]
- **Viam Organization:** [TBD]
- **Hardware BOM:** [TBD]

---

## Notes

**Why this project scores highly:**
- Naturally exercises all 5 lifecycle stages (prototype → deploy → scale → fleet → maintain)
- Data capture, cloud sync, remote monitoring are Viam strengths
- Remote-friendly for distributed team members
- Tangible output (actual vegetables/herbs)
- Great content potential (time-lapses, growth data)
- Easy to scale from 1 station to many (fleet demo)

**Gap Features This Project Addresses:**
- **Fleet Management** - Primary demo of multi-machine coordination with 2-3 sensor stations
- **Event-Driven Automation** - Threshold-based automation (humidity, temperature, soil moisture)
- **Data Pipeline** - End-to-end capture → label → train → deploy workflow
- **Monitoring/Alerting** - Environmental alerts and fleet health dashboard
- **Scheduled Tasks** - Periodic sensor readings, daily reports, time-lapse capture
