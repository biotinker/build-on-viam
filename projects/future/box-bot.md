# Project: Box Bot

## Overview

**One-line description:** Stationary robot that breaks down cardboard boxes for recycling

**Project Lead:** TBD
**Team Members:** TBD
**Status:** Future (suggested by Andrea)

## Description

Box Bot is a stationary recycling assistant that accepts cardboard boxes, flattens them, and stacks them for recycling pickup. Mounted in a convenient location (kitchen, mail room), employees simply drop boxes in front of it. The robot handles the tedious task of breaking down boxes.

Extended functionality includes restocking kitchen supplies by unpacking boxes and tracking inventory.

## Viam Capabilities Demonstrated

- [x] Motion / Arm Control
- [x] Gripper Manipulation
- [x] Vision / ML
- [x] Data Management
- [ ] Fleet Management
- [x] Remote Operation
- [ ] Modular Resources
- [ ] Multi-machine Coordination
- [x] Cloud Integration
- [x] Triggers ← **Box detection, jam alerts, bin full**
- [x] Data Pipeline ← **Box image capture for classifier training**

## Hardware Requirements

| Component | Description | Options |
|-----------|-------------|---------|
| Arm | Box manipulation | xArm 6, custom flattening mechanism |
| Gripper | Box grabbing | Wide parallel jaw, vacuum pads |
| Camera | Box detection | Overhead camera for detection |
| Mount | Station structure | Wall-mounted, freestanding station |
| Flattening | Box breakdown | Arm pressure, roller mechanism, press |
| Bin | Output storage | Stacking area, binding station |
| Compute | Main controller | Raspberry Pi 4, Intel NUC |

**Estimated Hardware Cost:** $TBD (depends on arm vs custom mechanism)

**Remote-Friendly:** Partially - vision/logic can be developed remotely, physical testing requires hardware

---

## MVP Options

Select one for hackathon scope:

### Option A: Flatten Only (Recommended)
Detect box, grab it, flatten it, place in pile.
- **Complexity:** Medium
- **Demo Appeal:** High
- **Scope:** Detection, manipulation, single motion sequence

### Option B: Flatten + Stack
Flatten boxes and stack neatly by size category.
- **Complexity:** Medium-High
- **Demo Appeal:** High
- **Scope:** Adds size classification, organized stacking

### Option C: Flatten + Bind
Flatten, stack, and bundle with twine or tape when stack is full.
- **Complexity:** High
- **Demo Appeal:** Very High
- **Scope:** Adds binding mechanism, stack counting

### Option D: Sort + Flatten
Detect box size/type, sort into categories, then flatten.
- **Complexity:** Medium-High
- **Demo Appeal:** High
- **Scope:** ML classification, multiple output bins

**Selected MVP:** _______________

---

## Backlog

Select 3-5 items for post-hackathon development:

### Processing & Manipulation
- [ ] **Size classification** - ML model classifies box sizes
- [ ] **Multi-size handling** - Adjust technique for different box sizes
- [ ] **Tape removal** - Detect and remove packing tape before flattening
- [ ] **Binding** - Bundle flattened boxes with twine/tape

### Data & Monitoring
- [ ] **Box counting** - Track boxes processed per day/week
- [ ] **Recycling metrics** - Dashboard showing environmental impact
- [ ] **Processing time tracking** - Measure efficiency over time
- [ ] **Jam detection** - Detect and alert when mechanism jams

### Operations
- [ ] **Scheduled operation** - Run during off-hours to reduce noise
- [ ] **Remote monitoring** - Check status and metrics from anywhere
- [ ] **Bin full detection** - Alert when output bin needs emptying
- [ ] **Maintenance alerts** - Notify when service needed

### Extended Functions
- [ ] **Restock mode** - Unpack boxes to restock kitchen supplies
- [ ] **Multi-material sorting** - Separate cardboard from other recyclables
- [ ] **QR scanning** - Track supplies via package codes (restock mode)

### Triggers (Gap Feature)
- [ ] **Box detected trigger** - When box placed in intake, start flatten sequence
- [ ] **Jam detection trigger** - Detect mechanism jam, alert and pause
- [ ] **Bin full trigger** - When output bin full, alert facilities team
- [ ] **Scheduled operation trigger** - Only operate during off-hours (noise)

### Data Pipeline / ML Training (Gap Feature)
- [ ] **Box image capture** - Capture images of each box before processing
- [ ] **Size/type labeling** - Label boxes by size category and type
- [ ] **Train classifier** - Train model to classify box types (small/medium/large, cardboard/plastic)
- [ ] **Deploy improved model** - Push updated classifier via Registry
- [ ] **Rejection tracking** - Capture images of rejected items for training

---

## Stretch Goals

- [ ] Integration with recycling pickup schedule
- [ ] Compactor integration for volume reduction
- [ ] Multi-station deployment (different floors/buildings)
- [ ] Gamification - department competition for recycling
- [ ] Carbon offset tracking and reporting

---

## Success Criteria

**MVP Complete When:**
- [ ] Robot detects box placed in input area
- [ ] Robot successfully flattens box
- [ ] Robot places flattened box in output area
- [ ] Works reliably for 3+ different box sizes

**Project Complete When:**
- [ ] All selected backlog items implemented
- [ ] Runs unsupervised for full workday
- [ ] Metrics dashboard operational
- [ ] Documentation complete

---

## Documentation Deliverables

- [ ] README with setup instructions
- [ ] Hardware assembly guide
- [ ] Station mounting guide
- [ ] Supported box sizes reference
- [ ] Troubleshooting guide (jams, errors)
- [ ] Metrics dashboard guide

---

## Links

- **Jira Epic:** [TBD]
- **GitHub Repo:** [TBD]
- **Viam Organization:** [TBD]
- **Hardware BOM:** [TBD]

---

## Notes

**Why this project works well:**
- Stationary mount simplifies vs mobile robots
- Clear, bounded problem (boxes in → flat cardboard out)
- High visibility location drives engagement
- Solves actual office annoyance
- Easy to measure success (boxes processed)
- Andrea's suggestion adds internal validation

**Gap Features This Project Addresses:**
- **Triggers** - Box detection to start processing, jam alerts, bin full notifications
- **Data Pipeline** - Capture box images, train size/type classifier, deploy improvements
