# Build on Viam Program

## Program Overview

Build on Viam is an internal program where Viam engineers build real robotics projects using the Viam platform. These projects serve multiple purposes: they demonstrate Viam's capabilities to customers and visitors, provide reference implementations for common robotics patterns, surface platform issues through real-world usage, and give engineers hands-on experience with the full development lifecycle.

## Projects

| Project | Summary |
|---------|---------|
| [Barista](../projects/barista.md) | Single-arm robot that operates an espresso station like a human barista |
| [Chess](../projects/chess.md) | Robot that plays chess against humans, physically moving pieces on a real board |
| [Greenhouse](../projects/greenhouse.md) | Automated growing environment with sensing, environmental control, and growth tracking |
| [Inventory Tracker](../projects/inventory-tracker.md) | Track lab equipment with zero-tagging vision - just hold up an item and go
| [Retro Roomba](../projects/retro-roomba.md) | Bring a Roomba 650/655 into the Viam ecosystem with a custom driver module and new capabilities |
| [Salad Maker](../projects/salad-maker.md) | Dual-arm robot that assembles custom salads from a refrigerated prep station |
| [Smart Lighting](../projects/smart-lighting.md) | Intelligent lighting that responds to occupancy, daylight, and schedules |
| [Vino](../projects/vino.md) | Wine service robot that pours and serves wine on demand |

## Viam Platform Capabilities

These are the Viam capabilities we want to exercise throughout this program.

### Core Capabilities (must be covered)

| Capability | Description |
|------------|-------------|
| **Hardware Integration** | Consistent APIs across cameras, arms, motors, sensors |
| **Motion Planning** | Arm movement, obstacle avoidance, frame system |
| **Vision / ML Inference** | Object detection, classification, custom models |
| **Data Capture & Sync** | Edge-to-cloud data pipelines with offline resilience |
| **Remote Operation** | Control and monitor robots through firewalls |
| **Module Development** | Custom components and services via Registry |
| **Fragments** | Reusable configuration blocks for fleet management |

### Scale & Fleet Capabilities

| Capability | Description |
|------------|-------------|
| **Fleet Management** | Managing multiple machines with shared configs |
| **OTA Updates** | Deploying module and model updates to fleet |
| **Provisioning** | Using fragments to reuse configurations across a fleet |

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

**Projects:** Chess, Vino, Salad Maker, Greenhouse, Barista, Inventory Tracker, Retro Roomba, Smart Lighting

| Capability | Projects |
|------------|----------|
| Hardware Integration | All projects |
| Motion Planning | Chess, Vino, Salad Maker, Barista |
| Vision / ML Inference | Chess, Vino, Salad Maker, Barista, Inventory Tracker, Greenhouse |
| Data Capture & Sync | All projects |
| Remote Operation | All projects |
| Module Development | Chess, Vino, Salad Maker, Barista, Inventory Tracker, Retro Roomba, Smart Lighting |
| Fragments | All projects |
| Fleet Management | Vino, Greenhouse, Barista, Inventory Tracker, Smart Lighting |
| OTA Updates | All projects |
| Provisioning | Greenhouse, Barista, Inventory Tracker, Smart Lighting, Cleaning Cart |
| Scheduled Tasks | Vino, Salad Maker, Greenhouse, Barista, Inventory Tracker, Smart Lighting |
| Monitoring & Alerting | Vino, Greenhouse, Barista |
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

If you have a project you'd like to propose, write it up following the template used by the projects already defined and submit as a pull request to this repo.
