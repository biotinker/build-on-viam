# Project: Vino

## Overview

**One-line description:** Wine service robot that pours and serves wine on demand

**Project Lead:** TBD
**Team Members:** TBD
**Status:** Existing (has backlog)

## Description

Vino is a robotic wine service system using an arm and gripper to handle bottles and pour wine. The robot can retrieve bottles from a rack, identify wines, pour measured amounts, and potentially serve guests.

This project demonstrates manipulation capabilities, vision-based detection, and creates a highly engaging demo suitable for events and visitors.

## Viam Capabilities Demonstrated

### Core Capabilities
- [x] **Hardware Integration** — Arm, gripper, camera, sensors
- [x] **Motion Planning** — Motion service for bottle/glass handling
- [x] **Vision / ML Inference** — Pour level detection, glass detection
- [x] **Data Capture & Sync** — Pour analytics synced to cloud
- [x] **Remote Operation** — Develop control logic remotely
- [x] **Module Development** — Custom vino service module

### Scale & Fleet Capabilities
- [x] **Fragments** — Hardware configuration as reusable fragment
- [ ] **Fleet Management** — Stretch: multi-station deployment
- [ ] **OTA Updates** — Not primary focus
- [ ] **Provisioning** — Not primary focus

### Operational Capabilities
- [x] **Event-Driven Automation** — Glass placement, bottle empty, order received
- [x] **Scheduled Tasks** — Cleaning cycles
- [ ] **Monitoring & Alerting** — Backlog: bottle levels, temperature
- [ ] **Data Pipeline (ML Training)** — Not primary focus

### Customer-Facing Capabilities
- [x] **Customer Delivery** — Primary demo: TypeScript SDK web ordering
- [x] **Web/Mobile Apps** — Web ordering interface for guests

## Hardware Requirements

| Component | Description | Options |
|-----------|-------------|---------|
| Arm | 6-DOF robot arm | xArm 6, xArm 5 Lite, UFactory Lite 6 |
| Gripper | Bottle/glass handling | Parallel jaw, soft gripper |
| Camera | Bottle/glass detection | Intel RealSense, USB camera |
| Wine Rack | Bottle storage | Custom with known positions, or vision-based |
| Compute | Main controller | Raspberry Pi 4, Intel NUC |

**Remote-Friendly:** Partially - can develop control logic remotely, physical testing requires hardware

---

## MVP Options

Select one for hackathon scope:

### Option A: Pour on Demand (Recommended)
Arm picks bottle from rack, pours measured amount into glass at fixed location.
- **Complexity:** Medium
- **Demo Appeal:** High
- **Scope:** Single bottle type, fixed glass position, timed pour

### Option B: Glass Detection Pour
Vision detects glass placement, arm pours into detected glass.
- **Complexity:** Medium-High
- **Demo Appeal:** High
- **Scope:** Adds vision requirement, flexible glass positioning

### Option C: Wine Selector
User selects wine via app/voice, arm retrieves correct bottle from rack.
- **Complexity:** Medium
- **Demo Appeal:** Medium
- **Scope:** Multiple bottles, selection interface, retrieval logic

### Option D: Sommelier Display
Camera reads wine label, displays pairing suggestions and tasting notes.
- **Complexity:** Low-Medium
- **Demo Appeal:** Medium
- **Scope:** Vision + ML for label reading, database integration

**Selected MVP:** _______________

---

## Backlog

### Technical Improvements
- [ ] **Graceful error recovery** - `reset()` should determine current state and recover appropriately
- [ ] **Failed grab recovery** - If bottle grab fails, put glass back before retrying
- [ ] **Config from app** - Pull configuration from Viam app instead of hardcoding
- [ ] **April tag localization** - Auto-determine arm 2 location using April tags
- [ ] **Remove hardcoded positions** - Eliminate hardcoded joint positions throughout
- [ ] **Motion refactoring** - Clean up hacks in motion.go, use proper motion service patterns

### Point Cloud & Detection
- [ ] **Separate surface and object segmentation** - obstacles-pointcloud conflates table segmentation with object detection; these need to be separate concerns
- [ ] **Single object detection** - Demo fails when detecting multiple point clouds instead of one; need reliable single-object isolation
- [ ] **Auto-find bottle** - Vision-based bottle detection (not just glass)
- [ ] **Detection UI feedback** - Show on screen when "no objects found" or "too many found"

### Pour Quality
- [ ] **Pour stopping detection** - Better detection of when to stop pouring
- [ ] **Pour consistency** - More reliable pour amounts
- [ ] **Dynamic pour amounts** - Adjust pour based on glass size and drink type

### Manipulation & Gripping
- [ ] **Grab verification** - Confirm successful grab (pressure sensor at back of gripper, or camera-based)
- [ ] **Multiple bottle types** - Handle different bottle shapes/sizes
- [ ] **Multiple glass types** - Support different glass sizes and shapes
- [ ] **Person interference handling** - Better timing/detection when person reaches into workspace
- [ ] **Funnel refill workflow** - Get funnel, put on bottle, pick up glass, pour water, put funnel back

### Control Interface
- [ ] **Streamdeck integration** - Physical button control for demo
- [ ] **Mode switching** - DoCommand to switch between manual and auto modes
- [ ] **Dynamic button states** - Streamdeck buttons reflect current system state
- [ ] **Default to manual mode** - Start in manual mode for safety

### Customer Delivery
- [ ] **Web ordering interface** - TypeScript SDK web app for ordering pours
- [ ] **Order queue display** - Show pending orders on screen
- [ ] **Event mode** - Pre-configured settings for specific events/tastings

### Event-Driven Automation
- [ ] **Glass placement detection** - Sensor detects glass, starts pour sequence
- [ ] **Bottle empty alert** - Alert when bottle weight indicates empty
- [ ] **Order received** - Start pour sequence when order placed via app

### Data & Monitoring
- [ ] **Inventory tracking** - Track bottles consumed, sync to cloud
- [ ] **Pour analytics** - Track pours by wine type, time, etc.

---

## Stretch Goals

- [ ] Voice commands ("Pour me a glass of the Pinot")
- [ ] Guest preferences and history tracking
- [ ] Wine recommendation engine based on preferences
- [ ] Multi-station fleet with centralized inventory
- [ ] Per-pour billing demonstration
- [ ] Label scanning with vintage database lookup
- [ ] Decanting with timed aeration
- [ ] Temperature monitoring and alerts
- [ ] Integration with wine cellar management systems

---

## Success Criteria

**MVP Complete When:**
- [ ] Robot can pick up a bottle from rack
- [ ] Robot can pour wine into a glass
- [ ] Pour amount is reasonably consistent
- [ ] Demo runs reliably 3+ times in a row

**Project Complete When:**
- [ ] All selected backlog items implemented
- [ ] Documentation complete
- [ ] Can be operated by someone not on the team

---

## Documentation Deliverables

- [ ] README with setup instructions
- [ ] Hardware assembly guide
- [ ] Configuration reference
- [ ] Demo operation guide
- [ ] Video of system in operation

---

## Links

- **Existing Code:** ~/viam/vino
- **Jira Epic:** [TBD]
- **GitHub Repo:** [TBD]
- **Viam Organization:** [TBD]
- **Hardware BOM:** [TBD]

---

## Notes

**Gap Features This Project Addresses:**
- **Customer Delivery** - Primary demo of customer-facing SDK (TypeScript web app for ordering)
- **Event-Driven Automation** - Glass placement sensor, bottle empty alerts, order-received events

**Key Technical Challenges:**
- **Point cloud segmentation** - Current obstacles-pointcloud module conflates surface/table segmentation with object segmentation, causing false positives when multiple objects detected
- **Error recovery** - Demo needs graceful recovery from failed states without manual intervention
- **Pour consistency** - Reliable pour amounts across different glass types and fill levels

**Why customer delivery fits here:**
- Vino has natural guest appeal - visitors want to interact
- Web ordering interface demonstrates TypeScript SDK
- Event mode shows configuration for specific use cases
