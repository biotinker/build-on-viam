# Build on Viam Program

## Program Overview

Build on Viam is an internal program where Viam engineers build real robotics projects using the Viam platform. These projects serve multiple purposes: they demonstrate Viam's capabilities to customers and visitors, provide reference implementations for common robotics patterns, surface platform issues through real-world usage, and give engineers hands-on experience with the full development lifecycle.

## Projects

| Project | Summary |
|---------|---------|
| [Apples](./applesauce.md) | Robotic system that picks, cores, and peels apples from a basket |
| [Automated Storage](./automated-storage.md) | Modular lab storage system that retrieves and returns bins on demand via a 3-axis gantry, with RFID identification and a searchable inventory |
| [Barista](./barista.md) | Single-arm robot that operates an espresso station like a human barista |
| [Chess](./chess.md) | Robot that plays chess against humans, physically moving pieces on a real board |
| [Dog](./dog.md) | Autonomous quadruped robot that uses computer vision to detect and follow a designated human operator |
| [Greenhouse](./greenhouse.md) | Automated growing environment with sensing, environmental control, and growth tracking |
| [Inventory Tracker](./inventory-tracker.md) | Track lab equipment checkout and return using RFID and cameras |
| [Irrigation Balancer](./irrigation.md) | Closed-loop orchard flood irrigation — actuated valves plus per-outlet flow-estimating cameras keep water balanced across outlets regardless of inlet pressure |
| [Retro Roomba](./retro-roomba.md) | Bring a Roomba 650/655 into the Viam ecosystem with a custom driver module and new capabilities |
| [Rod Hockey Robot](./rod-hockey-robot.md) | A robot controlled rod hockey game that plays against humans |
| [Salad Maker](./salad-maker.md) | Dual-arm robot that assembles custom salads from a refrigerated prep station |
| [Smart Lighting](./smart-lighting.md) | Intelligent lighting that responds to occupancy, daylight, and schedules |
| [Vino](./vino.md) | Wine service robot that pours and serves wine on demand |

## Viam Platform Capabilities

These are the Viam capabilities we want to exercise throughout this program.

### Core Capabilities

| Capability | Description |
|------------|-------------|
| **Hardware Integration** | Consistent APIs across cameras, arms, motors, sensors |
| **Motion Planning** | Arm movement, obstacle avoidance, frame system |
| **Vision / ML Inference** | Object detection, classification, custom models |
| **Data Capture & Sync** | Edge-to-cloud data pipelines with offline resilience |
| **Remote Operation** | Control and monitor robots through firewalls |
| **Module Development** | Custom components and services via Registry |
| **Fragments** | Reusable configuration blocks |

### Scale & Fleet Capabilities

| Capability | Description |
|------------|-------------|
| **Fleet Management** | Managing multiple machines with shared configs |
| **OTA Updates** | Deploying module and model updates to fleet |
| **Provisioning** | Using fragments to reuse machine config across a fleet |

### Operational Capabilities

| Capability | Description |
|------------|-------------|
| **Scheduled Tasks** | Periodic operations without custom schedulers |
| **Monitoring & Alerting** | Fleet health visibility and notifications |
| **Data Pipeline (ML Training)** | Capture → Label → Train → Deploy workflow |

### Customer-Facing Capabilities

| Capability | Description |
|------------|-------------|
| **Customer Delivery** | White-label auth, TypeScript/Flutter SDKs, billing |
| **Web/Mobile Apps** | Customer-facing interfaces using Viam SDKs |

## Current Feature Coverage

As of the current project portfolio, here's how capabilities are covered:

**Projects:** Apples, Chess, Vino, Salad Maker, Greenhouse, Barista, Inventory Tracker, Retro Roomba, Smart Lighting

| Capability | Projects |
|------------|----------|
| Hardware Integration | All projects |
| Motion Planning | Apples, Chess, Vino, Salad Maker, Barista |
| Vision / ML Inference | Apples, Chess, Vino, Salad Maker, Barista, Inventory Tracker, Greenhouse |
| Data Capture & Sync | All projects |
| Remote Operation | All projects |
| Module Development | Apples, Chess, Vino, Salad Maker, Barista, Inventory Tracker, Retro Roomba, Smart Lighting |
| Fragments | All projects |
| Fleet Management | Apples, Vino, Greenhouse, Barista, Inventory Tracker, Smart Lighting |
| OTA Updates | All projects |
| Provisioning | Apples, Greenhouse, Barista, Inventory Tracker, Smart Lighting, Cleaning Cart |
| Scheduled Tasks | Apples, Vino, Salad Maker, Greenhouse, Barista, Inventory Tracker, Smart Lighting |
| Monitoring & Alerting | Apples, Vino, Greenhouse, Barista |
| Data Pipeline (ML Training) | Vino, Salad Maker, Greenhouse, Barista, Inventory Tracker |
| Customer Delivery | Vino, Salad Maker, Barista, Inventory Tracker |
| Web/Mobile Apps | Vino, Salad Maker, Barista, Inventory Tracker |


## Proposing New Projects

When proposing a new project, consider:

### 1. Feature Coverage

- Does this project demonstrate a broad set of Viam capabilities?
- Does it emphasize any capability not well covered by other projects?

### 2. Demo Appeal

- Would visitors/customers be impressed?
- Is there a clear "wow" moment?

### 3. Feasibility

- What are the hardware needs?
- What is the MVP for the hackathon?
- Is the MVP achievable in hackathon timeframe?

### 4. Lifecycle Coverage

- Does this project exercise multiple lifecycle stages?
- Prototype → Deploy → Scale → Fleet → Maintain

### 5. Longevity

- Is there a well-defined backlog of work that will extend beyond the hackathon?
- Can this project be maintained long-term?
- Will someone own it after the hackathon?

To propose a new project, submit a pull request adding a new `.md` file to this directory following the [project template](./project-template.md).
