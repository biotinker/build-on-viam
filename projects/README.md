# Build on Viam Projects

This directory contains all projects for the Build on Viam program.

## Active Projects

| Project | Status | Primary Capabilities | MVP Options |
|---------|--------|---------------------|-------------|
| [Vino](vino.md) | Existing | Arm, gripper, **customer delivery** | Pour on demand, glass detection |
| [Chess](chess.md) | Existing | Arm, vision, ML, **data pipeline** | Full game play, move execution |
| [Salad Maker](salad-maker.md) | New | **Dual-arm**, vision, **customer delivery**, **multi-machine** | Single arm fixed recipe |
| [Greenhouse](greenhouse.md) | New | Data, ML, **fleet**, **triggers** | Monitor + auto-water |
| [Barista](barista.md) | New | Arm, **customer delivery**, **fleet**, **triggers** | Espresso only |
| [Inventory Tracker](inventory-tracker.md) | New | RFID, vision, **triggers**, **customer delivery** | Barcode checkout |
| [Retro Roomba](retro-roomba.md) | New | **Custom module**, protocol, SLAM | Basic drive control |
| [Smart Lighting](smart-lighting.md) | New | IoT, **triggers**, **multi-machine**, **scheduled tasks** | Basic control + scenes |

See also: [Future Projects](future-projects.md) - Cleaning Cart, Dishwasher, Box Bot

## Project Comparison

| Project | Platform Coverage | Feasibility | Cool Factor | Assessment Score |
|---------|------------------|-------------|-------------|------------------|
| Salad Maker | 5 | 3 | 5 | **4.6** |
| Greenhouse | 5 | 3 | 5 | **4.6** |
| Barista | 5 | 3 | 5 | **4.5** |
| Inventory Tracker | 5 | 4 | 4 | **4.3** |
| Smart Lighting | 4 | 4 | 4 | **4.2** |
| Vino | 4 | 4 | 5 | **4.0** |
| Chess | 4 | 4 | 5 | **4.0** |
| Retro Roomba | 4 | 4 | 4 | **4.0** |

## Project Categories

### Manipulation (Arm-based)
- **Salad Maker** - Dual-arm salad assembly
- **Vino** - Wine pouring and service
- **Chess** - Chess piece manipulation
- **Barista** - Coffee preparation

### Mobile/Navigation
- **Retro Roomba** - Legacy Roomba with custom driver

### IoT/Sensing
- **Greenhouse** - Environmental monitoring and control
- **Inventory Tracker** - RFID/vision asset tracking
- **Smart Lighting** - Lutron integration, cross-machine triggers

## Viam Capabilities by Project

| Capability | Vino | Chess | Salad | GH | Bar | Inv | RR | Light |
|------------|------|-------|-------|-----|-----|-----|-----|-------|
| Arm Control | x | x | x | | x | | | |
| Gripper | x | x | x | | x | | | |
| Vision/ML | x | x | x | x | x | x | | |
| Navigation/SLAM | | | | | | | x | |
| Data Capture | x | x | x | x | x | x | x | x |
| Remote Operation | x | x | x | x | x | x | x | x |
| **Custom Module** | | | | | | x | x | x |
| **Triggers** | x | x | x | x | x | x | x | x |
| **Data Pipeline** | | x | x | x | x | x | | |
| **Scheduled Tasks** | x | | x | x | x | x | | x |
| **Customer Delivery** | x | | x | | x | x | | |
| **Fleet Management** | | | | x | x | x | | x |
| **Multi-machine** | | | x | x | | | | x |
| **Monitoring/Alerting** | | | x | x | x | x | | x |

**Legend:** Salad=Salad Maker, GH=Greenhouse, Bar=Barista, Inv=Inventory Tracker, RR=Retro Roomba, Light=Smart Lighting

## Gap Feature Coverage

| Gap Feature | Primary Projects | Secondary Projects |
|-------------|------------------|-------------------|
| **Triggers** | Inventory Tracker, Smart Lighting | Greenhouse, Salad Maker, Barista |
| **Scheduled Tasks** | Smart Lighting, Inventory Tracker | Greenhouse, Salad Maker, Barista |
| **Customer Delivery** | Inventory Tracker, Vino, Salad Maker | Barista |
| **Data Pipeline** | Chess, Greenhouse, Salad Maker | Inventory Tracker, Barista |
| **Fleet Management** | Greenhouse, Smart Lighting | Barista, Inventory Tracker |
| **Multi-machine Coordination** | Salad Maker, Smart Lighting | Greenhouse |
| **Custom Module Development** | Retro Roomba, Smart Lighting | Inventory Tracker |

## Hardware Requirements by Build

### Arm-Based Projects

| Build | Arm | Gripper | Compute | Cameras | Other |
|-------|-----|---------|---------|---------|-------|
| Vino 1 | xArm 6 (2) | xArm Gripper G2 (2) | Meerkat (1) | D435 wrist (2), webcam glass (1) | — |
| Vino 2 | xArm 6 (2) | xArm Gripper G2 (2) | Meerkat (1) | D435 wrist (2), webcam glass (1) | — |
| Vino 3 | xArm 6 (2) | xArm Gripper G2 (2) | Meerkat (1) | D435 wrist (2), webcam glass (1) | — |
| Vino 4 | xArm 6 (2) | xArm Gripper G2 (2) | Meerkat (1) | D435 wrist (2), webcam glass (1) | — |
| Chess 1 | xArm 7 (1) | xArm Gripper G2 (1) | Meerkat (1) | D435 wrist (1) | Board (1), pieces (1) |
| Chess 2 | xArm 7 (1) | xArm Gripper G2 (1) | Meerkat (1) | D435 wrist (1) | Board (1), pieces (1) |
| Salad 1 | UFACTORY 850 (2) | xArm Gripper G2 + tongs (2) | Meerkat (1) | D435 wrist (2), webcam overview (1) | Prep station (1), dispenser (1) |
| Salad 2 | UFACTORY 850 (2) | xArm Gripper G2 + tongs (2) | Meerkat (1) | D435 wrist (2), webcam overview (1) | Prep station (1), dispenser (1) |
| Barista 1 | UFACTORY 850 (1) | xArm Gripper G2 (1) | Meerkat (1) | D435 wrist (1), webcam overview (1) | Eureka Atom (1), Puqpress Q2 (1), Gaggia (1), tablet (1), Viam mugs |
| Barista 2 | UFACTORY 850 (1) | xArm Gripper G2 (1) | Meerkat (1) | D435 wrist (1), webcam overview (1) | Eureka Atom (1), Puqpress Q2 (1), Gaggia (1), tablet (1), Viam mugs |

### IoT/Sensing Projects

| Build | Compute | Cameras | Sensors | Other |
|-------|---------|---------|---------|-------|
| Greenhouse 1 | TBD | TBD | TBD | TBD |
| Inventory 1 | Pi 5 (6) | webcam (6) | RFID reader (2) | RFID tags, tablet kiosk (1) |
| Lighting 1 | Pi 5 (4) | — | BH1750 light (4) | Lutron Bridge PRO (4) |

### Mobile Projects

| Build | Compute | Cameras | Sensors | Base | Other |
|-------|---------|---------|---------|------|-------|
| Roomba 1 | Pi 5 (1) | webcam (1) | (internal) | Roomba 500/600 (1) | Serial adapter (1), IR beacons |
| Roomba 2 | Pi 5 (1) | webcam (1) | (internal) | Roomba 500/600 (1) | Serial adapter (1), IR beacons |

### Hardware Totals

| Component | Count | Notes |
|-----------|-------|-------|
| **Arms** | | |
| xArm 6 | 8 | Vino (4 builds × 2) |
| xArm 7 | 2 | Chess (2 builds × 1) |
| UFACTORY 850 | 6 | Salad (2 builds × 2), Barista (2 builds × 1) |
| **Grippers** | | |
| xArm Gripper G2 | 16 | Vino (8), Chess (2), Salad (4), Barista (2) |
| Tongs extension | 4 | Salad (2 builds × 2) |
| **Compute** | | |
| System76 Meerkat | 10 | Vino (4), Chess (2), Salad (2), Barista (2) |
| Raspberry Pi 5 | 12 | Inventory (6), Lighting (4), Roomba (2) |
| **Cameras** | | |
| Intel RealSense D435 | 16 | Vino (8), Chess (2), Salad (4), Barista (2) |
| Webcam | 16 | Vino (4), Salad (2), Barista (2), Inventory (6), Roomba (2) |
| **Bases** | | |
| Roomba 500/600 | 2 | Retro Roomba (2 builds × 1) |
| **Barista Equipment** | | |
| Eureka Atom grinder | 2 | Barista (2 builds × 1) |
| Puqpress Q2 | 2 | Barista (2 builds × 1) |
| Gaggia Classic Pro | 2 | Barista (2 builds × 1) |
| **Other** | | |
| Lutron Smart Bridge PRO | 4 | Lighting (1 build × 4) |
| RFID reader | 2 | Inventory (1 build × 2) |
| Tablet | 3 | Barista (2), Inventory (1) |

### Arm Summary

| Arm Model | Projects | Per Build | Builds | Total |
|-----------|----------|-----------|--------|-------|
| xArm 6 | Vino | 2 | 4 | 8 |
| xArm 7 | Chess | 1 | 2 | 2 |
| UFACTORY 850 | Salad Maker | 2 | 2 | 4 |
| UFACTORY 850 | Barista | 1 | 2 | 2 |
| **Total** | | | | **16** |

## Cost Comparison

| Project | Hardware Cost | Arm Required | Remote-Friendly |
|---------|--------------|--------------|-----------------|
| Salad Maker | ~$19k | Yes (2x UFACTORY 850) | Partial |
| Barista | ~$13k | Yes (UFACTORY 850) | Partial |
| Vino | ~$9k | Yes (xArm 6) | Partial |
| Chess | ~$10k | Yes (xArm 7) | Partial |
| Greenhouse | ~$400 | No | Yes |
| Inventory Tracker | ~$500 | No | Yes |
| Smart Lighting | ~$700 | No | Yes |
| Retro Roomba | ~$150 | No | Partial |

## Cross-Project Integration

Several projects can work together:

| Integration | Projects | Description |
|-------------|----------|-------------|
| **Lights follow rover** | Smart Lighting + Retro Roomba | Lights activate when rover enters zone |
| **Checkout triggers lights** | Inventory Tracker + Smart Lighting | Lab lights on when equipment checked out |
| **Robot fleet dashboard** | All mobile robots | Centralized monitoring of all rovers |

## Reference Documents

- [Project Assessment Criteria](../docs/project-assessment-criteria.md) - How projects are evaluated
- [Project Template](../templates/project-template.md) - Template for new projects
- [Submission Guidelines](../docs/submission-guidelines.md) - How to propose new projects

## Selecting a Project

During the hackathon kickoff, engineers will select which project to join. Consider:

- Which capabilities do you want to learn?
- What hardware is available to you?
- Which team members do you want to collaborate with?
- Do you prefer manipulation, navigation, or IoT projects?

**Requirement:** Every engineer must join a project team.

## Team Sizes (50 Engineers)

Current build configuration for 50 engineers:

| Project | Builds | Team Size | Total Engineers |
|---------|--------|-----------|-----------------|
| Vino | 4 | 5 | 20 |
| Chess | 2 | 5 | 10 |
| Salad Maker | 2 | 5 | 10 |
| Barista | 2 | 5 | 10 |
| Greenhouse | 1 | 5 | 5 |
| Inventory Tracker | 1 | 5 | 5 |
| Smart Lighting | 1 | 5 | 5 |
| Retro Roomba | 2 | 5 | 10 |

**Note:** Adjust based on interest and hardware availability.

## Next Steps

For each project:
1. [ ] Select MVP option
2. [ ] Select 3-5 backlog items
3. [ ] Confirm hardware availability
4. [ ] Assign project lead
5. [ ] Create Jira epic
