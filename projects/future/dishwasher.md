# Project: Dishwasher Robot

## Overview

**One-line description:** Robot that unloads (and potentially loads) a dishwasher

**Project Lead:** TBD
**Team Members:** TBD
**Status:** Future

## Description

Dishwasher Robot automates the tedious task of unloading clean dishes from a dishwasher and placing them in cabinets. Using an arm (potentially on a gantry for extended reach), the robot identifies dishes, determines their type, and places them in the appropriate location.

Extended functionality includes loading dirty dishes from the sink and coordinating with other kitchen robots (cleaning cart handoff).

## Viam Capabilities Demonstrated

- [x] Motion / Arm Control
- [x] Gripper Manipulation
- [x] Vision / ML
- [x] Data Management (dish tracking)
- [ ] Fleet Management
- [x] Remote Operation
- [ ] Modular Resources
- [ ] Multi-machine Coordination (stretch: sink handoff)
- [x] Cloud Integration
- [x] Configuration Management (cabinet positions)
- [x] Data Pipeline ← **Dish image capture for classifier training**
- [x] Triggers ← **Dishwasher cycle complete trigger**

## Hardware Requirements

| Component | Description | Options |
|-----------|-------------|---------|
| Arm | Dish manipulation | xArm 6, dual arms for efficiency |
| Gripper | Dish handling | Parallel jaw, soft gripper for fragile items |
| Camera | Dish detection | Overhead + side view, Intel RealSense |
| Gantry | Extended reach | Overhead rail system (post-MVP) |
| Mount | Installation | Counter-mounted, ceiling gantry |
| Compute | Main controller | Raspberry Pi 4, Jetson Nano |

**Estimated Hardware Cost:** $TBD (arm + gantry is significant)

**Remote-Friendly:** Partially - manipulation logic can be developed remotely, physical testing requires hardware and kitchen setup

---

## MVP Options

Select one for hackathon scope:

### Option A: Single Dish Type (Recommended)
Unload plates only, place in single cabinet location.
- **Complexity:** Medium
- **Demo Appeal:** High
- **Scope:** Plate detection, pick-and-place, single destination

### Option B: Multiple Dish Types
Detect and handle plates, bowls, cups - different destinations.
- **Complexity:** High
- **Demo Appeal:** Very High
- **Scope:** Multi-class detection, multiple place locations

### Option C: Utensil Sorting
Focus on utensil basket - sort forks, knives, spoons into drawer organizer.
- **Complexity:** Medium
- **Demo Appeal:** High
- **Scope:** Small object manipulation, fine classification

### Option D: Rack Extraction
Pull dishwasher rack out, enabling easier access for unloading.
- **Complexity:** Low-Medium
- **Demo Appeal:** Medium
- **Scope:** Single manipulation task, rack mechanism

**Selected MVP:** _______________

---

## Backlog

Select 3-5 items for post-hackathon development:

### Detection & Classification
- [ ] **Dish classification** - ML model identifies dish types (plate, bowl, cup, etc.)
- [ ] **Pose estimation** - Determine dish orientation for optimal grip
- [ ] **Clean detection** - Verify dishes are clean before unloading
- [ ] **Breakage detection** - Detect and alert on cracked/chipped dishes

### Manipulation & Placement
- [ ] **Cabinet mapping** - Learn cabinet locations for different items
- [ ] **Stacking logic** - Stack dishes properly in cabinets
- [ ] **Fragile handling** - Special handling for wine glasses, delicate items
- [ ] **Pot/pan handling** - Larger manipulation for cookware

### Extended Functions
- [ ] **Dishwasher loading** - Reverse workflow - load from sink
- [ ] **Sink handoff** - Receive dishes from cleaning cart robot
- [ ] **Cycle trigger** - Start unloading when dishwasher cycle ends
- [ ] **Gantry extension** - Add gantry for full kitchen reach

### Data & Monitoring
- [ ] **Inventory tracking** - Track dish counts, alert on low supplies
- [ ] **Cycle counting** - Track loads processed
- [ ] **Error logging** - Record drops, misses, jams

### Data Pipeline / ML Training (Gap Feature)
- [ ] **Dish image capture** - Capture images of each dish before handling
- [ ] **Dish type labeling** - Label images with dish type (plate, bowl, cup, etc.)
- [ ] **Grasp success tracking** - Record successful vs failed grasps with images
- [ ] **Train improved classifier** - Use captured data to train better dish detector
- [ ] **Deploy updated model** - Push improved model via Registry

### Triggers (Gap Feature)
- [ ] **Cycle complete trigger** - Smart dishwasher signals cycle done, robot starts unloading
- [ ] **Cabinet full trigger** - Detect when cabinet location is full, alert or use alternate
- [ ] **Drop detection trigger** - If dish dropped, alert and pause for inspection

---

## Stretch Goals

- [ ] Full kitchen integration (sink → dishwasher → cabinet workflow)
- [ ] Handle any dish type without pre-training
- [ ] Detergent level monitoring and reorder alerts
- [ ] Voice status updates ("Unloading complete")
- [ ] Integration with smart dishwasher (cycle completion signal)

---

## Success Criteria

**MVP Complete When:**
- [ ] Robot can detect dishes in dishwasher rack
- [ ] Robot can pick up a dish without dropping
- [ ] Robot can place dish in designated cabinet location
- [ ] Works reliably for 5+ dishes in sequence

**Project Complete When:**
- [ ] Handles all common dish types
- [ ] Can unload full dishwasher load
- [ ] All selected backlog items implemented
- [ ] Documentation complete

---

## Documentation Deliverables

- [ ] README with setup instructions
- [ ] Hardware assembly guide
- [ ] Kitchen installation guide
- [ ] Cabinet position configuration guide
- [ ] Supported dish types reference
- [ ] Troubleshooting guide

---

## Links

- **Jira Epic:** [TBD]
- **GitHub Repo:** [TBD]
- **Viam Organization:** [TBD]
- **Hardware BOM:** [TBD]

---

## Notes

**Considerations:**
- Gantry adds significant complexity - consider arm-only MVP
- Kitchen installation requires coordination with facilities
- Dishwasher model may affect approach (rack design varies)
- Could start with dish rack on counter (not actual dishwasher) for hackathon

**Gap Features This Project Addresses:**
- **Data Pipeline** - Dish image capture, grasp success tracking, classifier training
- **Triggers** - Dishwasher cycle complete, cabinet full alerts, drop detection
