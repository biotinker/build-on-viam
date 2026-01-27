# Project: Lab Inventory Tracker

## Overview

**One-line description:** Track lab equipment with RFID/vision, manage checkouts, alert on low stock or overdue items

**Project Lead:** TBD
**Team Members:** TBD
**Status:** New

## Description

Lab Inventory Tracker is a system for tracking shared lab equipment - who has what, when it's due back, and what needs reordering. Engineers check out items via an app (scan RFID or select from list), and the system tracks everything. Cameras periodically audit shelves to detect discrepancies between what's checked out and what's actually there.

This project solves a real problem (missing equipment, stockouts) while demonstrating Viam capabilities that manipulation-heavy projects don't emphasize: data capture, triggers, scheduled tasks, and customer-facing apps.

## Viam Capabilities Demonstrated

- [ ] Motion / Arm Control
- [x] Vision / ML ← **Item detection, shelf audit**
- [x] Data Management ← **Primary demo: checkout logs, inventory state**
- [x] Fleet Management ← **Multiple storage locations**
- [x] Remote Operation
- [x] Modular Resources ← **RFID reader module**
- [x] Multi-machine Coordination ← **Shelf stations report to central system**
- [x] Cloud Integration
- [x] Customer Delivery ← **Checkout app with user auth**
- [x] Triggers ← **Overdue alerts, low stock, discrepancy detection**
- [x] Scheduled Tasks ← **Daily audit, weekly reports**

## Hardware Requirements

| Component | Description | Options |
|-----------|-------------|---------|
| Compute | Per-shelf controller | Raspberry Pi 5 |
| Camera | Shelf monitoring | USB webcam, Pi Camera |
| RFID Reader | Item/badge scanning | RC522 (~$5), PN532 (~$10) |
| RFID Tags | Item identification | 13.56MHz stickers (~$0.10 ea) |
| Barcode Scanner | Alternative to RFID | USB barcode scanner (~$30) |
| Weight Sensors | Detect item removal (optional) | HX711 + load cells |
| Tablet | Checkout kiosk | Android tablet or iPad |
| Shelving | Storage display | Wire shelving or existing |

**Estimated Hardware Cost:** $300-800 (depending on approach)

**Remote-Friendly:** Yes - app development fully remote, ML training remote, physical setup minimal

---

## MVP Options

Select one for hackathon scope:

### Option A: Barcode Checkout (Recommended)
Scan barcode to check in/out, web app shows inventory state.
- **Complexity:** Low-Medium
- **Demo Appeal:** Medium
- **Scope:** Checkout flow, basic triggers, dashboard

### Option B: RFID Checkout
RFID badge + item tags for faster scanning.
- **Complexity:** Medium
- **Demo Appeal:** Medium-High
- **Scope:** RFID module development, same checkout flow

### Option C: Vision Audit
Camera detects items on shelf, compares to checkout records.
- **Complexity:** Medium-High
- **Demo Appeal:** High
- **Scope:** ML model training, discrepancy detection

### Option D: Full System
RFID checkout + vision audit + multiple locations.
- **Complexity:** High
- **Demo Appeal:** Very High
- **Scope:** Complete inventory management system

**Selected MVP:** _______________

---

## Backlog

Select 3-5 items for post-hackathon development:

### Checkout & Tracking
- [ ] **RFID checkout** - Tap badge, tap item, done
- [ ] **Mobile app** - Flutter SDK checkout from phone
- [ ] **Self-service kiosk** - Tablet-based checkout station
- [ ] **Bulk checkout** - Check out multiple items at once
- [ ] **Transfer between locations** - Move item from Lab A to Lab B

### Vision & ML
- [ ] **Item detection model** - Train model to recognize common lab items
- [ ] **Shelf audit** - Compare ML detection vs. checkout records
- [ ] **Discrepancy alerts** - Item on shelf but checked out, or vice versa
- [ ] **New item detection** - Flag unknown items for cataloging

### Triggers (Gap Feature)
- [ ] **Overdue trigger** - Item checked out > N days, send reminder
- [ ] **Escalating reminders** - 1 day, 3 days, 7 days, then manager
- [ ] **Low stock trigger** - Quantity below threshold, alert to reorder
- [ ] **Missing item trigger** - Expected on shelf but not detected
- [ ] **Return reminder** - Notify when leaving building (stretch: BLE beacon)

### Scheduled Tasks (Gap Feature)
- [ ] **Daily inventory snapshot** - Capture shelf images at 6 AM
- [ ] **Weekly utilization report** - Most used items, longest checkouts
- [ ] **Monthly audit** - Full physical vs. system reconciliation
- [ ] **Expiration check** - Alert on items past calibration/expiry date

### Customer Delivery (Gap Feature)
- [ ] **Web checkout app** - TypeScript SDK, user authentication
- [ ] **Mobile app** - Flutter SDK for checkout on the go
- [ ] **Per-team views** - Each team sees their checked-out items
- [ ] **Admin dashboard** - Full inventory visibility, user management
- [ ] **Slack integration** - Checkout notifications to channel

### Data & Analytics
- [ ] **Usage trends** - Which items are most requested
- [ ] **Predict stockouts** - ML-based reorder suggestions
- [ ] **Item lifecycle** - New → in-use → retired tracking
- [ ] **Export for procurement** - Generate purchase requests

### Fleet & Scale
- [ ] **Multiple locations** - Hardware lab, supply closet, main office
- [ ] **Centralized dashboard** - All locations in one view
- [ ] **Fragment for shelf config** - Reusable configuration per shelf
- [ ] **Cross-location search** - "Where's the RealSense?"

---

## Stretch Goals

- [ ] Integration with procurement system (auto-reorder)
- [ ] QR code generation for new items
- [ ] Voice assistant ("Where's the soldering iron?")
- [ ] Reservation system for high-demand items
- [ ] Calibration tracking and reminders

---

## Success Criteria

**MVP Complete When:**
- [ ] User can check out an item via app
- [ ] User can check in an item via app
- [ ] Dashboard shows current inventory state
- [ ] Overdue alert triggers correctly
- [ ] Low stock alert triggers correctly

**Project Complete When:**
- [ ] RFID checkout working
- [ ] ML model detects common lab items
- [ ] Automated audit compares detection vs. records
- [ ] Multiple locations configured as fleet
- [ ] 30 days of usage data captured

---

## Documentation Deliverables

- [ ] README with setup instructions
- [ ] Hardware wiring guide (RFID, cameras)
- [ ] Item tagging guide
- [ ] Checkout app user guide
- [ ] Admin dashboard guide
- [ ] Adding new items guide

---

## Links

- **Jira Epic:** [TBD]
- **GitHub Repo:** [TBD]
- **Viam Organization:** [TBD]
- **Hardware BOM:** [TBD]

---

## Technical Details

### RFID Integration

**Hardware:** RC522 module (~$5) connected via SPI to Raspberry Pi

**Python library:** [pi-rc522](https://github.com/ondryaso/pi-rc522)

**Viam module structure:**
```
rfid-reader/
├── main.go (or main.py)
├── rfid_sensor.go
└── meta.json
```

**Component type:** `sensor` - returns UID of scanned tag

**Example reading:**
```json
{
  "tag_present": true,
  "tag_uid": "04:A2:B3:C4:D5:E6:F7",
  "tag_type": "MIFARE Classic 1K",
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### Vision-Based Audit

**Approach:**
1. Camera captures shelf image on schedule
2. ML model detects items present
3. Compare to checkout database
4. Alert on discrepancies

**Model training:**
- Capture images of items during normal operation
- Label with item IDs
- Train classifier in Viam
- Deploy to shelf machines

### Database Schema

```
items:
  - id: string (barcode/RFID UID)
  - name: string
  - category: string
  - location: string
  - quantity: int
  - reorder_threshold: int

checkouts:
  - id: string
  - item_id: string
  - user_id: string
  - checked_out_at: timestamp
  - due_at: timestamp
  - returned_at: timestamp (nullable)

users:
  - id: string
  - name: string
  - email: string
  - team: string
```

---

## Notes

**Gap Features This Project Addresses:**
- **Customer Delivery** - Primary demo of checkout app with TypeScript SDK
- **Triggers** - Overdue alerts, low stock, discrepancy detection
- **Scheduled Tasks** - Daily snapshots, weekly reports, audits
- **Data Capture** - All checkout events logged and queryable
- **Fleet** - Multiple storage locations managed centrally

**Why this project is valuable:**
- Solves real problem the team faces daily
- Low hardware cost, high learning value
- Remote-friendly development
- Demonstrates capabilities manipulation projects don't
- System will actually be used after hackathon

**RFID vs Barcode:**
- RFID: Faster, works through packaging, more expensive tags
- Barcode: Simpler, requires line-of-sight, cheaper
- Recommendation: Start with barcode for MVP, add RFID later
