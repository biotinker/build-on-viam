# Project: Smart Office Lighting

## Overview

**One-line description:** Intelligent lighting that responds to occupancy, daylight, and schedules

**Project Lead:** TBD
**Team Members:** TBD
**Status:** New

## Description

Smart Office Lighting integrates Lutron Caseta lighting controls with Viam, creating an intelligent lighting system that responds to multiple inputs: occupancy sensors, ambient light levels, and time schedules. The system automatically adjusts lighting based on who's in the office, how much natural light is available, and what time of day it is.

This project demonstrates event-driven automation, scheduled tasks, IoT integration, and custom module development - capabilities that manipulation-heavy projects don't emphasize.

## Viam Capabilities Demonstrated

### Core Capabilities
- [ ] **Hardware Integration** — Lutron Bridge, dimmers, switches, motion sensors, light sensor
- [ ] **Motion Planning** — Not applicable
- [ ] **Vision / ML Inference** — Not applicable
- [x] **Data Capture & Sync** — Lighting events, energy usage synced to cloud
- [x] **Remote Operation** — Full remote control and development
- [x] **Module Development** — Primary: Lutron Telnet protocol module

### Scale & Fleet Capabilities
- [x] **Fragments** — Zone configurations as reusable fragments
- [x] **Fleet Management** — Multiple light zones managed as fleet
- [ ] **OTA Updates** — Not primary focus
- [ ] **Provisioning** — Not primary focus

### Operational Capabilities
- [x] **Event-Driven Automation** — Primary: occupancy, daylight thresholds, after-hours behavior
- [x] **Scheduled Tasks** — Primary: time-based scenes, daylight harvesting loop
- [ ] **Monitoring & Alerting** — Backlog: zone status dashboard
- [ ] **Data Pipeline (ML Training)** — Not applicable

### Customer-Facing Capabilities
- [ ] **Customer Delivery** — Not applicable
- [ ] **Web/Mobile Apps** — Backlog: lighting control dashboard

## Hardware Requirements

| Component | Description | Options |
|-----------|-------------|---------|
| Lutron Bridge | Central controller | Smart Bridge PRO (L-BDGPRO2-WH) - required for API |
| Dimmers | Light control | Caseta In-Wall Dimmer (PD-6WCL) |
| Switches | On/off control | Caseta Switch (PD-5ANS) |
| Plug Dimmers | Lamp control | Caseta Plug-in (PD-3PCL) |
| Motion Sensors | Occupancy detection | Caseta Motion Sensor (PD-OSENS) |
| Pico Remotes | Manual override | Pico Remote (PJ2-3BRL) |
| Compute | Viam machine | Raspberry Pi 5 |
| Light Sensor | Daylight harvesting | BH1750 |

**Remote-Friendly:** Yes - module development fully remote, physical install minimal

---

## MVP Options

Select one for hackathon scope:

### Option A: Basic Control + Scenes (Recommended)
Control lights from Viam, implement scene presets.
- **Complexity:** Medium
- **Demo Appeal:** Medium
- **Scope:** Telnet module, zone control, scenes

### Option B: Occupancy Response
Lights respond to Lutron motion sensors.
- **Complexity:** Medium
- **Demo Appeal:** Medium-High
- **Scope:** Adds sensor integration, automatic control

### Option C: Daylight Harvesting
Automatically adjust artificial lighting based on ambient light levels.
- **Complexity:** Medium-High
- **Demo Appeal:** High
- **Scope:** Light sensor integration, continuous adjustment loop

### Option D: Full Smart Office
Occupancy + daylight + schedules.
- **Complexity:** High
- **Demo Appeal:** Very High
- **Scope:** Complete intelligent lighting system

**Selected MVP:** _______________

---

## Backlog

Select 3-5 items for post-hackathon development:

### Core Control
- [ ] **Telnet connection** - Connect to Lutron Bridge PRO
- [ ] **Individual light control** - Set any dimmer level
- [ ] **Zone grouping** - Control multiple lights together
- [ ] **Scene activation** - Preset lighting configurations
- [ ] **Fade transitions** - Smooth level changes

### Event-Driven Automation (Gap Feature)
- [ ] **Occupancy detection** - Motion sensor activates lights
- [ ] **Vacancy timeout** - Dim/off after no motion for N minutes
- [ ] **Daylight threshold** - Adjust artificial light based on ambient
- [ ] **After hours behavior** - Different behavior outside work hours
- [ ] **Manual override detection** - Detect Pico remote use, pause automation

### Scheduled Tasks (Gap Feature)
- [ ] **Morning startup** - Lights to work mode at 7 AM
- [ ] **Evening shutdown** - Lights off at 8 PM
- [ ] **Weekend mode** - Reduced lighting Sat/Sun
- [ ] **Daylight harvesting loop** - Continuous adjustment based on light sensor
- [ ] **Cleaning mode** - Full brightness for cleaning crew (scheduled)

### Scenes
- [ ] **Work mode** - Standard office lighting (80%)
- [ ] **Meeting** - Conference room preset (60%)
- [ ] **Presentation** - Front low, back very low
- [ ] **Away** - All lights off
- [ ] **Emergency** - All lights 100%

### Daylight Harvesting
- [ ] **Ambient light sensor** - BH1750 integration
- [ ] **Per-zone adjustment** - Window zones dim more than interior
- [ ] **Target lux maintenance** - Maintain consistent light level regardless of outside conditions
- [ ] **Energy tracking** - Log savings from harvesting

### Data & Analytics
- [ ] **Event logging** - All light changes captured
- [ ] **Energy usage** - Estimate based on levels and time
- [ ] **Occupancy patterns** - When are zones used
- [ ] **Dashboard** - Real-time lighting status

---

## Stretch Goals

- [ ] Color temperature control (if using tunable fixtures)
- [ ] Circadian rhythm lighting (warm morning/evening, cool midday)
- [ ] Voice control integration
- [ ] Calendar integration (meeting room auto-adjust based on bookings)
- [ ] Energy reporting and optimization recommendations

---

## Success Criteria

**MVP Complete When:**
- [ ] Lutron module connects to bridge via Telnet
- [ ] Can control individual lights from Viam
- [ ] Zone grouping works
- [ ] Basic scene activation works
- [ ] One automation working: occupancy or daylight threshold

**Project Complete When:**
- [ ] Daylight harvesting working
- [ ] Scheduled scenes operational
- [ ] Occupancy sensor integration complete
- [ ] Dashboard showing lighting status
- [ ] Documentation complete

---

## Documentation Deliverables

- [ ] README with setup instructions
- [ ] Lutron Bridge PRO configuration guide
- [ ] Wiring and installation guide
- [ ] Zone configuration reference
- [ ] Scene programming guide
- [ ] Event-driven automation configuration guide

---

## Links

- **Jira Epic:** [TBD]
- **GitHub Repo:** [TBD]
- **Viam Organization:** [TBD]
- **Hardware BOM:** [TBD]

---

## Technical Details

### Lutron Integration Protocol

**Connection:**
- Smart Bridge PRO required (standard bridge doesn't support Telnet)
- Enable Telnet in Lutron app: Settings → Advanced → Integration
- Default credentials: username `lutron`, password `integration`
- Port 23 (Telnet)

**Command format:**
```
#<operation>,<integration_id>,<action>,<parameters>
```

**Common commands:**

| Command | Description |
|---------|-------------|
| `#OUTPUT,5,1,75` | Set device 5 to 75% |
| `#OUTPUT,5,1,0` | Turn device 5 off |
| `#OUTPUT,5,1,100` | Turn device 5 to 100% |
| `#DEVICE,2,3,3` | Press button 3 on keypad 2 |

**Event format (incoming):**
```
~OUTPUT,5,1,50    # Device 5 is now at 50%
~DEVICE,10,2,3    # Occupancy detected on device 10
```

**Python connection:**
```python
import telnetlib

class LutronBridge:
    def __init__(self, host, username="lutron", password="integration"):
        self.tn = telnetlib.Telnet(host, 23)
        self.tn.read_until(b"login: ")
        self.tn.write(f"{username}\n".encode())
        self.tn.read_until(b"password: ")
        self.tn.write(f"{password}\n".encode())
        self.tn.read_until(b"GNET> ")

    def set_level(self, device_id, level):
        cmd = f"#OUTPUT,{device_id},1,{level}\n"
        self.tn.write(cmd.encode())

    def get_level(self, device_id):
        cmd = f"?OUTPUT,{device_id},1\n"
        self.tn.write(cmd.encode())
        response = self.tn.read_until(b"\n")
        # Parse response: ~OUTPUT,5,1,75
        return int(response.split(b",")[3])
```

### Viam Module Structure

```
lutron-lighting/
├── main.go
├── bridge.go           # Connection management
├── zone.go             # Zone grouping logic
├── scene.go            # Scene definitions
├── occupancy_sensor.go # Sensor integration
└── meta.json
```

**Component types:**

| Name | Type | Purpose |
|------|------|---------|
| `lutron-bridge` | `generic` | Connection to Lutron |
| `lutron-zone` | `generic` | Group of lights |
| `lutron-sensor` | `sensor` | Occupancy sensor |

**DoCommand API:**
```go
// Set zone level
DoCommand(ctx, map[string]interface{}{
    "command": "set_level",
    "zone":    "lab",
    "level":   75,
})

// Activate scene
DoCommand(ctx, map[string]interface{}{
    "command": "scene",
    "name":    "work-mode",
})

// Get status
DoCommand(ctx, map[string]interface{}{
    "command": "get_state",
})
```

### Daylight Harvesting Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    Lighting Machine                          │
│                                                              │
│  ┌──────────────┐     ┌──────────────┐     ┌─────────────┐  │
│  │ BH1750       │────▶│ Harvesting   │────▶│ Lutron      │  │
│  │ Light Sensor │     │ Logic        │     │ Bridge      │  │
│  └──────────────┘     └──────────────┘     └─────────────┘  │
│                              │                     │         │
│                              ▼                     ▼         │
│                    ┌──────────────┐        ┌─────────────┐  │
│                    │ Data Capture │        │ Caseta      │  │
│                    │ (lux levels) │        │ Dimmers     │  │
│                    └──────────────┘        └─────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

**Harvesting logic:**
```python
TARGET_LUX = 500  # Target workspace illumination

def calculate_dimmer_level(ambient_lux, current_level):
    """Adjust artificial light to maintain target lux."""
    # Estimate artificial contribution at current level
    artificial_lux = current_level * 5  # ~500 lux at 100%

    total_lux = ambient_lux + artificial_lux
    lux_deficit = TARGET_LUX - ambient_lux

    if lux_deficit <= 0:
        return 0  # Enough natural light

    # Calculate needed artificial level
    needed_level = min(100, int(lux_deficit / 5))
    return needed_level
```

---

## Notes

**Gap Features This Project Addresses:**
- **Event-Driven Automation** - Occupancy detection, daylight thresholds, after-hours behavior
- **Scheduled Tasks** - Time-based scenes, daylight harvesting loop
- **Custom Module Development** - Lutron Telnet protocol integration
- **IoT Integration** - Extends Viam beyond robotics into building automation

**Why this project is valuable:**
- Demonstrates IoT and building automation use case
- Practical energy savings in the office
- Different skillset than manipulation projects
- Immediately useful - lights actually work better

**Hardware notes:**
- Smart Bridge PRO required - standard bridge doesn't support API
- Lutron uses Clear Connect RF (not WiFi/Zigbee)
- Motion sensors report to bridge, not directly to Pi
- Consider starting with plug-in dimmers (easier install)

**References:**
- [Lutron Integration Protocol (PDF)](https://assets.lutron.com/a/documents/040249.pdf)
- [Lutron Caseta - Home Assistant](https://www.home-assistant.io/integrations/lutron_caseta/)
- [Custom PRO Bridge Component](https://github.com/upsert/lutron-caseta-pro)
