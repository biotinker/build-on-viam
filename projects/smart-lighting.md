# Project: Smart Office Lighting

## Overview

**One-line description:** Intelligent lighting that responds to occupancy, daylight, schedules, and robot activity

**Project Lead:** TBD
**Team Members:** TBD
**Status:** New

## Description

Smart Office Lighting integrates Lutron Caseta lighting controls with Viam, creating an intelligent lighting system that responds to multiple inputs: occupancy sensors, ambient light levels, time schedules, and crucially - robot locations. When a rover enters an area, lights in that zone activate. When all robots dock at night, the building shifts to night mode.

This project demonstrates multi-machine coordination, triggers, scheduled tasks, and IoT integration - capabilities that manipulation-heavy projects don't emphasize. It also creates tangible cross-project integration where robots interact with building infrastructure.

## Viam Capabilities Demonstrated

- [x] Custom Module Development ← **Lutron Telnet protocol module**
- [x] Multi-machine Coordination ← **Rovers trigger lighting changes**
- [x] Triggers ← **Primary demo: robot location, occupancy, thresholds**
- [x] Scheduled Tasks ← **Time-based scenes, daylight harvesting**
- [x] Data Capture ← **Lighting events, energy usage**
- [x] Fleet Management ← **Multiple light zones as fleet**
- [x] Remote Operation
- [x] Modular Resources
- [ ] Motion / Arm Control
- [ ] Vision / ML
- [x] Cloud Integration

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
| Light Sensor | Daylight harvesting | BH1750 (~$5) |

**Estimated Hardware Cost:** $500-1,000 (depending on number of zones)

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

### Option C: Robot-Triggered Lighting
Lights follow rovers around the office.
- **Complexity:** Medium-High
- **Demo Appeal:** High
- **Scope:** Cross-machine triggers, zone mapping

### Option D: Full Smart Office
Occupancy + daylight + schedules + robot integration.
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

### Multi-Machine Coordination
- [ ] **Rover zone detection** - Map rover SLAM position to light zones
- [ ] **Lights follow rover** - Activate zone when rover enters
- [ ] **Night patrol mode** - Only light the rover's current zone
- [ ] **All docked = night mode** - When all rovers dock, dim building
- [ ] **Cross-machine triggers** - Rover events trigger light changes

### Triggers (Gap Feature)
- [ ] **Occupancy trigger** - Motion sensor activates lights
- [ ] **Vacancy timeout** - Dim/off after no motion
- [ ] **Daylight threshold** - Adjust artificial light based on ambient
- [ ] **Rover entered zone** - Trigger from rover location data
- [ ] **After hours trigger** - Different behavior outside work hours

### Scheduled Tasks (Gap Feature)
- [ ] **Morning startup** - Lights to work mode at 7 AM
- [ ] **Evening shutdown** - Lights off at 8 PM
- [ ] **Weekend mode** - Reduced lighting Sat/Sun
- [ ] **Daylight harvesting loop** - Continuous adjustment
- [ ] **Cleaning mode** - Full brightness for cleaning crew

### Scenes
- [ ] **Work mode** - Standard office lighting (80%)
- [ ] **Meeting** - Conference room preset (60%)
- [ ] **Presentation** - Front low, back very low
- [ ] **Night patrol** - Only rover zone lit
- [ ] **Away** - All lights off
- [ ] **Emergency** - All lights 100%

### Daylight Harvesting
- [ ] **Ambient light sensor** - BH1750 integration
- [ ] **Per-zone adjustment** - Window zones dim more
- [ ] **Target lux maintenance** - Maintain consistent light level
- [ ] **Energy tracking** - Log savings from harvesting

### Data & Analytics
- [ ] **Event logging** - All light changes captured
- [ ] **Energy usage** - Estimate based on levels and time
- [ ] **Occupancy patterns** - When are zones used
- [ ] **Dashboard** - Real-time lighting status

---

## Stretch Goals

- [ ] Color temperature control (if using tunable fixtures)
- [ ] Circadian rhythm lighting (warm morning/evening)
- [ ] Voice control integration
- [ ] Calendar integration (meeting room auto-adjust)
- [ ] Energy reporting and optimization

---

## Success Criteria

**MVP Complete When:**
- [ ] Lutron module connects to bridge via Telnet
- [ ] Can control individual lights from Viam
- [ ] Zone grouping works
- [ ] Basic scene activation works
- [ ] One trigger: rover enters zone -> lights on

**Project Complete When:**
- [ ] Full integration with Cleaning Cart location
- [ ] Daylight harvesting working
- [ ] Scheduled scenes operational
- [ ] Occupancy sensor integration complete
- [ ] Dashboard showing lighting status

---

## Documentation Deliverables

- [ ] README with setup instructions
- [ ] Lutron Bridge PRO configuration guide
- [ ] Wiring and installation guide
- [ ] Zone configuration reference
- [ ] Scene programming guide
- [ ] Cross-machine trigger setup guide

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

### Robot-Triggered Lighting Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                      VIAM CLOUD                              │
└─────────────────────────────────────────────────────────────┘
         │                              │
         ▼                              ▼
┌─────────────────┐          ┌─────────────────────┐
│  Cleaning Cart  │          │  Lighting Machine   │
│                 │          │                     │
│  SLAM position  │─────────▶│  Zone Manager       │
│  data capture   │  query   │       │             │
└─────────────────┘          │       ▼             │
                             │  Lutron Bridge      │
                             │       │             │
                             └───────┼─────────────┘
                                     │
                                     ▼
                             ┌───────────────┐
                             │ Lutron Caseta │
                             │   Dimmers     │
                             └───────────────┘
```

**Zone mapping:**
```python
ZONE_MAP = {
    # SLAM coordinates -> lighting zone
    "x:-5to0,y:0to5":    "zone-a",  # Lab area
    "x:0to5,y:0to5":     "zone-b",  # Main office
    "x:0to5,y:5to10":    "zone-c",  # Conference
    "x:-5to0,y:5to10":   "zone-d",  # Kitchen
}

def position_to_zone(x, y):
    for bounds, zone in ZONE_MAP.items():
        if in_bounds(x, y, bounds):
            return zone
    return None
```

### Cross-Project Integration

| Project | Integration Point |
|---------|-------------------|
| Cleaning Cart | SLAM position → zone activation |
| Retro Roomba | IR beacon zones → light zones |
| Dishwasher | Kitchen lights on when active |
| Box Bot | Recycling area lights when processing |
| Inventory Tracker | Lab lights when equipment checked out |

---

## Notes

**Gap Features This Project Addresses:**
- **Triggers** - Primary demo of cross-machine triggers
- **Scheduled Tasks** - Time-based scenes, daylight harvesting
- **Multi-machine Coordination** - Rovers and lighting work together
- **IoT Integration** - Extends Viam beyond robotics

**Why this project is valuable:**
- Creates visible cross-project integration
- Lights literally follow the robots around
- Demonstrates IoT and building automation
- Practical energy savings in the office
- Different skillset than manipulation projects

**Hardware notes:**
- Smart Bridge PRO required - standard bridge doesn't support API
- Lutron uses Clear Connect RF (not WiFi/Zigbee)
- Motion sensors report to bridge, not directly to Pi
- Consider starting with plug-in dimmers (easier install)

**References:**
- [Lutron Integration Protocol (PDF)](https://assets.lutron.com/a/documents/040249.pdf)
- [Lutron Caseta - Home Assistant](https://www.home-assistant.io/integrations/lutron_caseta/)
- [Custom PRO Bridge Component](https://github.com/upsert/lutron-caseta-pro)
