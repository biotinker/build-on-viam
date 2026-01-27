# Build on Viam Projects

This directory contains all projects for the Build on Viam program.

## Active Projects

| Project | Status | Primary Capabilities | MVP Options |
|---------|--------|---------------------|-------------|
| [Vino](vino.md) | Existing | Arm, gripper, **customer delivery** | Pour on demand, glass detection |
| [Chess](chess.md) | Existing | Arm, vision, ML, **data pipeline** | Full game play, move execution |
| [Greenhouse](greenhouse.md) | New | Data, ML, **fleet**, **triggers** | Monitor + auto-water |
| [Barista](barista.md) | Proposed | Arm, **customer delivery**, **fleet**, **triggers** | Espresso only |
| [Inventory Tracker](inventory-tracker.md) | New | RFID, vision, **triggers**, **customer delivery** | Barcode checkout |
| [Retro Roomba](retro-roomba.md) | New | **Custom module**, protocol, SLAM | Basic drive control |
| [Smart Lighting](smart-lighting.md) | New | IoT, **triggers**, **multi-machine**, **scheduled tasks** | Basic control + scenes |

See also: [Future Projects](future-projects.md) - Cleaning Cart, Dishwasher, Box Bot

## Project Comparison

| Project | Platform Coverage | Feasibility | Cool Factor | Assessment Score |
|---------|------------------|-------------|-------------|------------------|
| Greenhouse | 5 | 3 | 5 | **4.6** |
| Barista | 5 | 3 | 5 | **4.5** |
| Inventory Tracker | 5 | 4 | 4 | **4.3** |
| Smart Lighting | 4 | 4 | 4 | **4.2** |
| Vino | 4 | 4 | 5 | **4.0** |
| Chess | 4 | 4 | 5 | **4.0** |
| Retro Roomba | 4 | 4 | 4 | **4.0** |

## Project Categories

### Manipulation (Arm-based)
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

| Capability | Vino | Chess | GH | Bar | Inv | RR | Light |
|------------|------|-------|-----|-----|-----|-----|-------|
| Arm Control | x | x | | x | | | |
| Gripper | x | x | | x | | | |
| Vision/ML | x | x | x | x | x | | |
| Navigation/SLAM | | | | | | x | |
| Data Capture | x | x | x | x | x | x | x |
| Remote Operation | x | x | x | x | x | x | x |
| **Custom Module** | | | | | x | x | x |
| **Triggers** | x | x | x | x | x | x | x |
| **Data Pipeline** | | x | x | x | x | | |
| **Scheduled Tasks** | x | | x | x | x | | x |
| **Customer Delivery** | x | | | x | x | | |
| **Fleet Management** | | | x | x | x | | x |
| **Multi-machine** | | | x | | | | x |
| **Monitoring/Alerting** | | | x | x | x | | x |

**Legend:** GH=Greenhouse, Bar=Barista, Inv=Inventory Tracker, RR=Retro Roomba, Light=Smart Lighting

## Gap Feature Coverage

| Gap Feature | Primary Projects | Secondary Projects |
|-------------|------------------|-------------------|
| **Triggers** | Inventory Tracker, Smart Lighting | Greenhouse, Barista |
| **Scheduled Tasks** | Smart Lighting, Inventory Tracker | Greenhouse, Barista |
| **Customer Delivery** | Inventory Tracker, Vino | Barista |
| **Data Pipeline** | Chess, Greenhouse | Inventory Tracker, Barista |
| **Fleet Management** | Greenhouse, Smart Lighting | Barista, Inventory Tracker |
| **Multi-machine Coordination** | Smart Lighting | Greenhouse |
| **Custom Module Development** | Retro Roomba, Smart Lighting | Inventory Tracker |

## Cost Comparison

| Project | Hardware Cost | Arm Required | Remote-Friendly |
|---------|--------------|--------------|-----------------|
| Vino | $$$$$ | Yes | Partial |
| Chess | $$$$$ | Yes | Partial |
| Barista | $$$$$ | Yes | Partial |
| Greenhouse | $$ | No | Yes |
| Inventory Tracker | $$ | No | Yes |
| Smart Lighting | $$ | No | Yes |
| Retro Roomba | $ | No | Partial |

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
| Greenhouse | 1 | 5 | 5 |
| Inventory Tracker | 1 | 5 | 5 |
| Smart Lighting | 1 | 5 | 5 |
| Retro Roomba | 1 | 5 | 5 |

**Note:** Adjust based on interest and hardware availability.

## Next Steps

For each project:
1. [ ] Select MVP option
2. [ ] Select 3-5 backlog items
3. [ ] Confirm hardware availability
4. [ ] Assign project lead
5. [ ] Create Jira epic
