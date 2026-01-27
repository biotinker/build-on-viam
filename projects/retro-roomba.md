# Project: Retro Roomba Revival

## Overview

**One-line description:** Bring a 2005-era Roomba into the Viam ecosystem with custom drivers and DIY IR beacons

**Project Lead:** TBD
**Team Members:** TBD
**Status:** New

## Description

Retro Roomba Revival takes a cheap, old Roomba (500/600 series, ~$30 on eBay) and integrates it with Viam by building a custom driver module. Engineers implement the Roomba Open Interface protocol, handle serial communication, and create DIY IR beacons for navigation. Optional upgrades include adding a camera and LiDAR for modern SLAM capabilities.

This project teaches WHY Viam's abstractions exist by making engineers build them from scratch. It's the deepest hardware integration learning experience in the portfolio.

## Viam Capabilities Demonstrated

- [x] Custom Module Development ← **Primary learning: build driver from scratch**
- [x] Hardware Abstraction ← **Implement base, sensor, power_sensor APIs**
- [x] Protocol Implementation ← **Roomba Open Interface serial protocol**
- [x] Data Capture ← **Sensor logs, battery cycles, patrol data**
- [x] Triggers ← **Low battery, dock needed, bump detected**
- [x] Remote Operation
- [ ] Fleet Management
- [x] SLAM (with LiDAR upgrade) ← **Add modern nav to retro hardware**
- [ ] Customer Delivery
- [x] Modular Resources

## Hardware Requirements

| Component | Description | Options |
|-----------|-------------|---------|
| Roomba | 2005-2010 era base | 500 series (~$30), 600 series (~$40) |
| Compute | Main controller | Raspberry Pi 5 |
| Serial Adapter | Connect Pi to Roomba | Mini-DIN cable + logic level converter |
| Camera | Vision (optional) | USB webcam |
| LiDAR | SLAM upgrade (optional) | RPLidar A1 (~$100) |
| IR LEDs | DIY beacons | 940nm IR LEDs |
| Beacon Controller | DIY virtual walls | Arduino Nano or ATtiny85 |

**Estimated Hardware Cost:**
- Basic: ~$150 (Roomba + Pi + wiring)
- With LiDAR: ~$290
- With beacons: ~$50 additional

**Remote-Friendly:** Partially - protocol/module development remote, physical testing requires hardware

---

## MVP Options

Select one for hackathon scope:

### Option A: Basic Drive Control (Recommended)
Drive Roomba from Viam app, read sensors.
- **Complexity:** Medium
- **Demo Appeal:** Medium
- **Scope:** Serial protocol, base API, basic sensors

### Option B: Full Sensor Suite
All Roomba sensors exposed through Viam.
- **Complexity:** Medium-High
- **Demo Appeal:** Medium
- **Scope:** Complete sensor implementation

### Option C: DIY Beacons
Build virtual walls and dock beacon.
- **Complexity:** High
- **Demo Appeal:** High
- **Scope:** IR protocol reverse engineering, beacon builds

### Option D: SLAM Upgrade
Add LiDAR, implement modern navigation.
- **Complexity:** High
- **Demo Appeal:** Very High
- **Scope:** Full modern capabilities on retro hardware

**Selected MVP:** _______________

---

## Backlog

Select 3-5 items for post-hackathon development:

### Protocol & Control
- [ ] **Drive command** - SetVelocity, Stop, SetPower
- [ ] **Sensor polling** - All Roomba sensor packets
- [ ] **Safe mode** - Cliff/bump protection active
- [ ] **Full mode** - No safety limits (for testing)
- [ ] **Song playback** - Roomba beep patterns

### Sensor Integration
- [ ] **Bump sensors** - Left/right bump detection
- [ ] **Cliff sensors** - Edge detection (4 sensors)
- [ ] **Wheel encoders** - Odometry data
- [ ] **Battery state** - Charge level, voltage, current
- [ ] **IR receivers** - Detect virtual walls and dock

### DIY Beacons
- [ ] **Virtual wall** - IR transmitter blocks Roomba path
- [ ] **Dock beacon** - Red/green buoy + force field signals
- [ ] **Lighthouse** - Room-to-room navigation beacons
- [ ] **Custom zones** - Define patrol areas with beacons

### Vision & SLAM Upgrade
- [ ] **Mount camera** - Top-mounted USB webcam
- [ ] **Mount LiDAR** - RPLidar A1 on top
- [ ] **Cartographer SLAM** - Map building with LiDAR
- [ ] **Fused odometry** - Wheel encoders + LiDAR
- [ ] **Autonomous navigation** - Navigate mapped space

### Triggers
- [ ] **Low battery** - Alert and return to dock
- [ ] **Bump detected** - Log obstacle encounters
- [ ] **Cliff detected** - Emergency stop, alert
- [ ] **Dock signal lost** - Alert if beacon down

### Data Capture
- [ ] **Patrol logs** - Route taken, time, events
- [ ] **Sensor data** - Continuous capture for analysis
- [ ] **Battery cycles** - Track charge/discharge patterns
- [ ] **Error events** - Stuck, bump, cliff occurrences

---

## Stretch Goals

- [ ] Voice control ("Roomba, clean the lab")
- [ ] Multi-Roomba fleet
- [ ] Integration with Smart Lighting (lights follow Roomba)
- [ ] Custom cleaning patterns
- [ ] ROS 2 bridge (for comparison)

---

## Success Criteria

**MVP Complete When:**
- [ ] Roomba drives from Viam app (SetVelocity works)
- [ ] Battery level readable as sensor
- [ ] Bump sensors trigger stops
- [ ] Module published to registry (private)

**Project Complete When:**
- [ ] All sensors exposed through Viam
- [ ] DIY virtual wall beacon working
- [ ] DIY dock beacon working (Roomba finds and docks)
- [ ] Camera mounted and streaming
- [ ] SLAM working with LiDAR

---

## Documentation Deliverables

- [ ] README with setup instructions
- [ ] Wiring diagram (Pi to Roomba)
- [ ] Roomba Open Interface command reference
- [ ] Beacon build guide with schematics
- [ ] Module development tutorial
- [ ] SLAM upgrade guide

---

## Links

- **Jira Epic:** [TBD]
- **GitHub Repo:** [TBD]
- **Viam Organization:** [TBD]
- **Hardware BOM:** [TBD]

---

## Technical Details

### Roomba Open Interface

**Connection:**
- Mini-DIN connector on Roomba
- TXD, RXD, GND, battery power
- 5V logic (needs level shifter for 3.3V Pi)
- Default baud: 115200 (500/600 series)

**Key commands:**

| Command | Opcode | Data | Description |
|---------|--------|------|-------------|
| Start | 128 | none | Initialize OI |
| Safe | 131 | none | Safe mode (cliff/bump protection) |
| Full | 132 | none | Full mode (no limits) |
| Drive | 137 | velocity (2), radius (2) | Drive wheels |
| Sensors | 142 | packet ID | Request sensor data |
| Dock | 143 | none | Seek dock |

**Sensor packets:**

| Packet | ID | Bytes | Description |
|--------|----|----|-------------|
| Bump/Wheeldrop | 7 | 1 | Bump and wheel drop flags |
| Cliff Left | 9 | 1 | Left cliff sensor |
| Battery Charge | 25 | 2 | Current charge (mAh) |
| Distance | 19 | 2 | Distance since last (mm) |
| Angle | 20 | 2 | Angle since last (degrees) |

### Viam Module Structure

```
roomba-legacy/
├── main.go
├── roomba_base.go      # Implements base.Base
├── roomba_sensor.go    # Implements sensor.Sensor
├── roomba_power.go     # Implements powersensor.PowerSensor
├── protocol.go         # OI protocol implementation
└── meta.json
```

**Base implementation sketch:**

```go
type RoombaBase struct {
    resource.Named
    port   io.ReadWriteCloser
    logger logging.Logger
    mu     sync.Mutex
}

func (r *RoombaBase) SetVelocity(ctx context.Context,
    linear, angular r3.Vector, extra map[string]interface{}) error {

    r.mu.Lock()
    defer r.mu.Unlock()

    // Convert to Roomba drive command
    velocity := int16(linear.Y * 500)  // mm/s, max 500
    radius := calculateRadius(angular.Z)

    cmd := []byte{
        137,  // DRIVE opcode
        byte(velocity >> 8), byte(velocity & 0xFF),
        byte(radius >> 8), byte(radius & 0xFF),
    }

    _, err := r.port.Write(cmd)
    return err
}

func (r *RoombaBase) Stop(ctx context.Context, extra map[string]interface{}) error {
    return r.SetVelocity(ctx, r3.Vector{}, r3.Vector{}, nil)
}
```

### DIY IR Beacon Protocol

**Virtual Wall (code 162):**
- 38kHz carrier
- Each bit: 1ms pulse for 1, 3ms pulse for 0
- Send byte 3 times with 100ms gaps
- 150ms pause after sequence

**Dock beacon signals:**

| Signal | Code | Purpose |
|--------|------|---------|
| Red Buoy | 168 | Right side of dock |
| Green Buoy | 164 | Left side of dock |
| Force Field | 161 | Center approach |
| Red+Green | 172 | Combined (close) |
| Red+Force | 169 | Right + center |
| Green+Force | 165 | Left + center |
| All | 173 | Very close to dock |

**Arduino beacon sketch:**

```cpp
#define IR_PIN 3
#define CARRIER_FREQ 38000

void sendRoombaCode(uint8_t code) {
    for (int rep = 0; rep < 3; rep++) {
        for (int bit = 7; bit >= 0; bit--) {
            int duration = (code & (1 << bit)) ? 1 : 3;
            tone(IR_PIN, CARRIER_FREQ);
            delay(duration);
            noTone(IR_PIN);
            delay(duration);
        }
        delay(100);
    }
    delay(150);
}

void loop() {
    sendRoombaCode(162);  // Virtual Wall
}
```

### Cost Comparison

| Platform | Cost | Driver Work | Learning Depth |
|----------|------|-------------|----------------|
| Retro Roomba | ~$150 | Build from scratch | Very High |
| Create 3 | $299 | Configure ROS 2 bridge | Medium |
| TurtleBot 4 | $1,850 | Configure existing | Low |

---

## Notes

**Gap Features This Project Addresses:**
- **Custom Module Development** - Primary demo of building a driver from scratch
- **Hardware Abstraction** - Implement base, sensor, power_sensor APIs
- **Protocol Implementation** - Serial protocol, IR beacon protocol

**Why this project is valuable:**
- Cheapest mobile base option ($30-50)
- Forces deep understanding of Viam abstractions
- IR beacon system teaches signal protocols
- Can be upgraded incrementally (camera, LiDAR)
- Creates reusable module for community

**Skills developed:**
- Serial communication
- Protocol implementation
- Viam module development
- Hardware interfacing (voltage levels)
- IR signal encoding
- SLAM integration (with upgrade)

**References:**
- [Roomba SCI Specification (PDF)](https://cdn.hackaday.io/files/1747287475562752/Roomba_SCI_manual.pdf)
- [Hacking a Broken Roomba](https://www.royvanrijn.com/blog/2015/12/hacking-a-broken-roomba/)
- [DIY Virtual Wall - GitHub](https://github.com/MKme/Roomba)
- [pi-rc522 RFID Library](https://github.com/ondryaso/pi-rc522)
