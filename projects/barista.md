# Project: Barista

## Overview

**One-line description:** Single-arm robot that operates an espresso station like a human barista

**Project Lead:** TBD
**Team Members:** TBD
**Status:** New

## Description

Barista is a robotic coffee preparation system where a single UFACTORY 850 arm performs all the steps a human barista would: grabbing the portafilter, holding it under the grinder, placing it on an auto-tamper, locking it into the espresso machine, brewing the shot, steaming milk, and assembling drinks. Customers order via a tablet interface and watch their drink being prepared.

Unlike systems that use fully-automatic espresso machines, this project uses a semi-automatic machine with a robot performing the manipulation. This approach mirrors commercial robotic baristas like [Rozum Cafe](https://cafe.rozum.com/) while demonstrating advanced manipulation skills.

This project combines manipulation complexity (multi-step beverage preparation), customer-facing interaction (ordering interface), and operational features (inventory tracking, scheduling, quality monitoring).

## Viam Capabilities Demonstrated

### Core Capabilities
- [x] **Hardware Integration** — Arm, gripper, espresso machine, grinder, auto-tamper, cameras
- [x] **Motion Planning** — Complex multi-step manipulation workflow
- [x] **Vision / ML Inference** — Cup detection, fill level, foam quality assessment
- [x] **Data Capture & Sync** — Order history, drink analytics synced to cloud
- [x] **Remote Operation** — Develop control logic remotely
- [x] **Module Development** — Custom barista service module

### Scale & Fleet Capabilities
- [x] **Fragments** — Hardware configuration as reusable fragment
- [x] **Fleet Management** — Multiple coffee stations with centralized monitoring
- [ ] **OTA Updates** — Backlog: push recipe updates to all stations
- [ ] **Provisioning** — Backlog: automated new station setup

### Operational Capabilities
- [x] **Event-Driven Automation** — Order received, brew complete, low beans alert
- [x] **Scheduled Tasks** — Morning warmup, cleaning cycles, inventory check
- [x] **Monitoring & Alerting** — Bean level, water, temperature, usage metrics
- [x] **Data Pipeline (ML Training)** — Drink quality images, shot timing for grind tuning

### Customer-Facing Capabilities
- [x] **Customer Delivery** — Tablet ordering interface, guest profiles
- [x] **Web/Mobile Apps** — TypeScript/Flutter SDK ordering apps

## Hardware Requirements

| Component | Description | Specific Model |
|-----------|-------------|----------------|
| Arm | 6-DOF robot arm | UFACTORY 850 (850mm reach, 5kg payload) |
| Gripper | Portafilter/pitcher handling | UFACTORY Gripper |
| Auto-tamper | Consistent 30lb tamp pressure | Puqpress Q2 |
| Espresso Machine | Semi-automatic, physical buttons | Gaggia Classic Pro |
| Grinder | Portafilter-activated | Eureka Atom |
| Wrist Camera | Close-up detection | Intel RealSense D405 |
| Overview Camera | Workspace monitoring | USB webcam |
| Tablet | Order interface | Android tablet |
| Cup Dispenser | Cup staging | Gravity dispenser |
| Knockbox | Puck disposal | Standard knockbox |
| Milk Pitcher | Steaming vessel | Standard 12oz pitcher |
| Compute | Main controller | System76 Meerkat |

**Remote-Friendly:** Partially - control logic can be developed remotely, physical testing requires hardware

---

## MVP Options

Select one for hackathon scope:

### Option A: Espresso Only (Recommended)
Pull espresso shots - grind, tamp, brew, serve.
- **Complexity:** Medium
- **Demo Appeal:** High
- **Scope:** Full portafilter workflow, no milk

### Option B: Espresso + Americano
Espresso plus hot water addition.
- **Complexity:** Medium
- **Demo Appeal:** High
- **Scope:** Adds water dispensing step

### Option C: Full Milk Drinks
Espresso, Latte, Cappuccino with steamed milk.
- **Complexity:** High
- **Demo Appeal:** Very High
- **Scope:** Adds milk steaming with pitcher handling

### Option D: Order Interface Focus
Simple espresso + polished ordering experience.
- **Complexity:** Medium
- **Demo Appeal:** High
- **Scope:** Focus on customer experience

**Selected MVP:** _______________

---

## Backlog

Select 3-5 items for post-hackathon development:

### Core Workflow
- [ ] **Portafilter handling** - Grab, hold, lock-in, remove
- [ ] **Grinder operation** - Position under grinder, activate, dose
- [ ] **Auto-tamper integration** - Place on Puqpress, retrieve
- [ ] **Shot pulling** - Lock portafilter, start brew, monitor
- [ ] **Puck disposal** - Knock out puck, clean portafilter

### Milk Steaming
- [ ] **Pitcher handling** - Grab pitcher, position under wand
- [ ] **Steam wand operation** - Hold during steaming
- [ ] **Pour milk** - Pour steamed milk into cup
- [ ] **Foam quality detection** - ML model assesses microfoam

### Drink Variations
- [ ] **Multiple drink types** - Espresso, Americano, Latte, Cappuccino
- [ ] **Size variations** - Small, Medium, Large cups
- [ ] **Strength options** - Single, double shots
- [ ] **Milk alternatives** - Different pitchers for oat, almond

### Customer Delivery (Gap Feature)
- [ ] **Tablet ordering interface** - TypeScript SDK app
- [ ] **Mobile app** - Flutter SDK for remote ordering
- [ ] **Guest profiles** - Remember regular orders
- [ ] **Order queue display** - Show pending orders
- [ ] **Order status** - Real-time prep progress

### Event-Driven Automation (Gap Feature)
- [ ] **Order received** - Start preparation sequence
- [ ] **Brew complete** - Detect shot done, proceed to next step
- [ ] **Low beans alert** - Weight sensor activates refill alert
- [ ] **Temperature alert** - Alert if brew temp out of range

### Scheduled Tasks (Gap Feature)
- [ ] **Morning warmup** - Pre-heat machine before office opens
- [ ] **Cleaning cycle** - Daily backflush routine
- [ ] **Inventory check** - Daily bean/water level report

### Data Pipeline (Gap Feature)
- [ ] **Drink image capture** - Photo of every finished drink
- [ ] **Shot time tracking** - Extraction times for grind tuning
- [ ] **Quality labeling** - Rate drinks for training data

---

## Stretch Goals

- [ ] Voice ordering ("Hey Barista, make me a latte")
- [ ] Latte art pour patterns
- [ ] Grind size auto-adjustment based on shot timing
- [ ] Multiple bean hoppers with selection
- [ ] Calendar integration (coffee ready when meeting ends)

---

## Success Criteria

**MVP Complete When:**
- [ ] Robot grabs portafilter and holds under grinder
- [ ] Robot places portafilter on Puqpress
- [ ] Robot locks portafilter into group head
- [ ] Robot activates brew and waits for completion
- [ ] Robot serves cup to pickup location
- [ ] Works reliably for 5+ drinks in sequence

**Project Complete When:**
- [ ] Milk steaming workflow complete
- [ ] Multiple drink types available
- [ ] Customer ordering interface working
- [ ] Monitoring dashboard operational
- [ ] Documentation complete

---

## Documentation Deliverables

- [ ] README with setup instructions
- [ ] Hardware assembly and mounting guide
- [ ] Espresso machine integration guide
- [ ] Arm calibration procedure
- [ ] Drink recipe configuration
- [ ] Customer app setup guide
- [ ] Operations and maintenance guide

---

## Links

- **Jira Epic:** [TBD]
- **GitHub Repo:** [TBD]
- **Viam Organization:** [TBD]
- **Hardware BOM:** [TBD]

---

## Technical Details

### Single-Arm Workflow Sequence

```
1. RECEIVE ORDER
   └── Event: Order placed via tablet

2. PREPARE PORTAFILTER
   ├── Grab portafilter from holder
   ├── Move to grinder
   ├── Push portafilter against fork (auto-activates grind)
   └── Hold until dose complete

3. TAMP
   ├── Move to Puqpress
   ├── Place portafilter on tamper
   ├── Wait for tamp completion (~1.3 sec)
   └── Retrieve portafilter

4. BREW
   ├── Move to espresso machine group head
   ├── Lock portafilter (twist motion)
   ├── Position cup under spout
   ├── Activate brew (button or lever)
   └── Wait for shot completion (~25-30 sec)

5. STEAM MILK (if latte/cappuccino)
   ├── Grab milk pitcher
   ├── Position under steam wand
   ├── Activate steam
   ├── Hold for steaming duration
   └── Pour milk into cup

6. SERVE
   ├── Move cup to pickup location
   └── Signal order ready

7. CLEANUP
   ├── Remove portafilter from group head
   ├── Knock out puck into knockbox
   └── Return portafilter to holder
```

### Workspace Layout

```
        [Grinder]     [Espresso Machine]
            │              │
            ▼              ▼
    ┌───────────────────────────────────┐
    │                                   │
    │           [UFACTORY 850]          │
    │                │                  │
    │    ┌───────────┼───────────┐      │
    │    │           │           │      │
    │    ▼           ▼           ▼      │
    │ [Puqpress]  [Cups]    [Knockbox]  │
    │                                   │
    │         [Milk Pitcher]            │
    │                                   │
    │      [Pickup] ← Customer          │
    └───────────────────────────────────┘
```

### Key Manipulation Challenges

| Task | Challenge | Solution |
|------|-----------|----------|
| Portafilter lock-in | Requires twist motion under spring pressure | Compliant motion, force feedback |
| Grinder activation | None - portafilter-activated | Push against fork, auto-grinds |
| Tamping | None - auto-tamps | Place on Puqpress, auto-tamps |
| Steam wand positioning | Hold steady during steaming | Fixed wand angle, move pitcher |
| Puck knockback | Firm tap required | Controlled velocity impact |

### Minimal Button Workflow

Both the Eureka Atom grinder and Puqpress Q2 are sensor-activated:
- **Grinder:** Portafilter fork switch triggers grinding when pressed
- **Tamper:** Sensor detects portafilter placement, auto-tamps in 1.3 sec

The only button the robot needs to press is the **Gaggia Classic Pro brew rocker switch**. The rocker switch design is easier for a robot arm to actuate than push buttons.

### Espresso Machine Options

| Machine | Pros | Cons |
|---------|------|------|
| Gaggia Classic Pro | Rocker switches (easy for robot), 58mm portafilter, Pi mods available | No PID (can add aftermarket) |
| Rancilio Silvia | Professional build, toggle switches | No PID built-in |
| Rancilio Silvia Pro X | PID built-in, reliable | More complex |
| Breville Bambino Plus | Compact, PID | 54mm portafilter (non-standard) |

**Recommendation:** Gaggia Classic Pro - rocker switches are easy for robot to press, 58mm commercial portafilter, well-documented mods.

### References

- [Rozum Cafe](https://cafe.rozum.com/) - Commercial robotic barista
- [Cafe X](https://www.cafexapp.com/) - Single-arm robotic coffee bar
- [Artly Coffee](https://artly.coffee/) - AI-trained robotic barista
- [Eureka Atom](https://www.eureka.co.it/en/products/espresso_line_home/atom.aspx) - Portafilter-activated grinder
- [Puqpress Q2](https://puq.coffee/) - Automatic tamper with 22-66lb adjustable pressure
- [Gaggia Classic Pro](https://www.gaggia.com/manual-machines/new-classic/) - Semi-automatic with rocker switches
- [Gaggia Classic Pi Mods](https://github.com/esrice/piggia) - Open source Pi control for Gaggia

---

## Notes

**Why single arm works:**
- Sequential workflow is natural for coffee making
- One arm is sufficient for all manipulation tasks
- Simpler development
- Commercial systems (Cafe X) use single arm successfully

**Why Puqpress instead of robot tamping:**
- UFACTORY 850 payload (5kg/11lb) < required tamp force (30lb)
- Auto-tamper ensures consistent pressure
- This is what commercial robotic baristas do
- Robot still does all other manipulation

**Gap Features This Project Addresses:**
- **Customer Delivery** - Ordering interface with TypeScript/Flutter SDKs
- **Event-Driven Automation** - Order received, brew complete, inventory alerts
- **Scheduled Tasks** - Morning warmup, cleaning cycles
- **Monitoring/Alerting** - Bean level, water, temperature, usage
- **Data Pipeline** - Drink quality images, shot timing data

**Risk Factors:**
- Portafilter lock-in requires precise force control
- Steam wand manipulation is complex
- Hot liquids require safety considerations
- Espresso quality depends on many variables
