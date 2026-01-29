# Project: Lab Inventory Tracker

## Overview

**One-line description:** Track lab equipment with zero-tagging vision - just hold up an item and go

**Project Lead:** TBD
**Team Members:** TBD
**Status:** New

## Description

Lab Inventory Tracker solves the "where's the RealSense?" problem without requiring barcodes, RFID tags, or any tagging of objects. The core interaction is simple: hold an item up in front of a camera, and the system captures the moment for tracking.

**Phase 1 (MVP):** Detect checkout events and capture a photo of who took what. Notifications go to Slack with the image - providing an immediate audit trail even before any ML is trained.

**Phase 2:** Train the system to recognize common lab items from the captured images, automatically identifying WHAT was taken.

**Phase 3:** Add face recognition to identify WHO took the item, enabling fully automatic checkout logging.

This approach is pragmatic - it works on day one with zero training, builds its own training data through normal use, and evolves toward full automation incrementally.

## Viam Capabilities Demonstrated

### Core Capabilities
- [ ] **Hardware Integration** — Camera, optional button, display
- [ ] **Motion Planning** — Not applicable
- [x] **Vision / ML Inference** — Item recognition, face recognition (phased)
- [x] **Data Capture & Sync** — Checkout images synced to cloud with offline resilience
- [x] **Remote Operation** — Full remote monitoring and development
- [x] **Module Development** — Checkout station module

### Scale & Fleet Capabilities
- [x] **Fragments** — Checkout station configuration as reusable fragment
- [x] **Fleet Management** — Multiple checkout stations with centralized view
- [ ] **OTA Updates** — Backlog: push model updates to all stations
- [ ] **Provisioning** — Backlog: automated new station setup

### Operational Capabilities
- [x] **Event-Driven Automation** — Checkout detection, overdue alerts, escalating notifications
- [x] **Scheduled Tasks** — Daily summaries, weekly utilization reports
- [ ] **Monitoring & Alerting** — Backlog: station health, low activity alerts
- [x] **Data Pipeline (ML Training)** — Primary: captured images → labeling → item/face models → deploy

### Customer-Facing Capabilities
- [x] **Customer Delivery** — Dashboard for viewing checkouts and audit trail
- [x] **Web/Mobile Apps** — Web dashboard, mobile-friendly checkout status

### Multi-Machine Coordination
- [x] **Stations report to central system** — Centralized view across all locations

## Hardware Requirements

| Component | Description | Options |
|-----------|-------------|---------|
| Compute | Checkout station controller | Raspberry Pi 5 |
| Camera | Capture person + item | USB webcam, Pi Camera |
| Display (optional) | Feedback to user | Small LCD or status LEDs |
| Mounting | Camera position | Shelf-mounted, wall-mounted, or freestanding kiosk |

**Estimated Cost per Station:** ~$100-150

**Remote-Friendly:** Yes - ML training fully remote, app development remote, physical setup minimal

---

## MVP Options

### Phase 1: Capture the Moment (Recommended MVP)

Detect checkout events and capture photos for audit trail.

**Flow:**
1. Person approaches checkout station
2. Holds item up in front of camera (in designated "checkout zone")
3. System detects the gesture/motion and captures photo
4. Photo saved to cloud with timestamp
5. Notification sent to Slack with image: "Checkout at 10:32am - [photo]"
6. Human review if needed - photo serves as audit trail

**Detection options:**
- Motion detection in designated zone
- "Person holding object" pose detection
- Physical button press (simplest)
- Continuous monitoring with ML detecting checkout gesture

- **Complexity:** Low-Medium
- **Demo Appeal:** Medium-High
- **Scope:** Vision-based detection, data capture, notifications, basic dashboard

### Phase 2: Item Recognition

Add ML to identify WHAT was taken.

- Train model on captured images from Phase 1
- System auto-labels checkout with item name
- "Checkout at 10:32am - Intel RealSense D435 - [photo]"
- Unknown items flagged for manual labeling (feeds training)

- **Complexity:** Medium
- **Demo Appeal:** High
- **Scope:** ML training pipeline, model deployment, item database

### Phase 3: Face Recognition

Add ML to identify WHO took the item.

- Build face database from Phase 1/2 photos (with consent)
- System auto-identifies person
- "Shannon checked out Intel RealSense D435 at 10:32am"
- Full automatic checkout - no human review needed

- **Complexity:** Medium-High
- **Demo Appeal:** Very High
- **Scope:** Face recognition model, user database, privacy controls

### Phase 4: Full Automation

Complete hands-free tracking.

- Automatic checkout logging (item + person + time)
- Return detection (item appears back on shelf)
- Overdue reminders sent to the right person
- Usage analytics and trends

**Selected MVP:** Phase 1 - Capture the Moment

---

## Backlog

### Phase 1: Capture & Notify
- [ ] **Checkout zone detection** - Define camera FOV region for checkout gestures
- [ ] **Motion/gesture detection** - Detect when someone holds up an item
- [ ] **Photo capture** - High-quality image of person + item together
- [ ] **Cloud storage** - Save images with timestamps to Viam data management
- [ ] **Slack notification** - Send photo + timestamp to channel on each checkout
- [ ] **Basic dashboard** - View recent checkouts with images
- [ ] **Manual labeling UI** - Add item name and person to captured checkouts

### Phase 2: Item Recognition
- [ ] **Training data export** - Export labeled images for model training
- [ ] **Item classifier** - Train model to recognize common lab equipment
- [ ] **Auto-labeling** - Apply model to new checkouts
- [ ] **Confidence thresholds** - Flag low-confidence detections for review
- [ ] **Unknown item handling** - Queue unrecognized items for labeling
- [ ] **Model retraining pipeline** - Improve model as more data collected

### Phase 3: Face Recognition
- [ ] **User consent flow** - Opt-in for face recognition
- [ ] **Face database** - Store face embeddings for enrolled users
- [ ] **Face matching** - Identify person during checkout
- [ ] **Privacy controls** - Users can delete their data, opt out
- [ ] **Unknown person handling** - Prompt for identification or flag for review

### Event-Driven Automation (Gap Feature)
- [ ] **Checkout detected** - Capture + notification on gesture detection
- [ ] **Overdue reminder** - Item not returned after N days, notify (requires Phase 3)
- [ ] **Escalating alerts** - 3 days, 7 days, then notify manager
- [ ] **Return detected** - Item reappears on shelf camera (stretch)

### Scheduled Tasks (Gap Feature)
- [ ] **Daily summary** - Morning report of previous day's checkouts
- [ ] **Weekly utilization** - Most checked-out items, longest holds
- [ ] **Shelf audit** - Periodic shelf camera capture for reconciliation

### Customer Delivery (Gap Feature)
- [ ] **Web dashboard** - View all checkouts, search, filter
- [ ] **Mobile-friendly** - Check inventory status from phone
- [ ] **Per-team views** - Filter by team or location
- [ ] **Admin tools** - Manage items, users, locations

### Data Pipeline (Gap Feature)
- [ ] **Image capture** - Every checkout builds training dataset
- [ ] **Labeling interface** - Easy annotation of item + person
- [ ] **Model training** - Train/retrain in Viam
- [ ] **Model deployment** - Push updated models to stations
- [ ] **A/B testing** - Compare model versions

### Fleet & Scale
- [ ] **Multiple stations** - Hardware lab, supply closet, kitchen
- [ ] **Centralized view** - All stations in one dashboard
- [ ] **Station fragments** - Reusable config per checkout station
- [ ] **Cross-location search** - "Where's the RealSense?" across all locations

---

## Stretch Goals

- [ ] Return detection via shelf camera (item reappears)
- [ ] Voice assistant ("Where's the soldering iron?")
- [ ] Reservation system for high-demand items
- [ ] Integration with procurement (auto-reorder on low stock)
- [ ] Mobile app for checking inventory on the go

---

## Success Criteria

**Phase 1 (MVP) Complete When:**
- [ ] Camera detects checkout gesture reliably
- [ ] Photo captured and saved to cloud on each checkout
- [ ] Slack notification sent with image within 5 seconds
- [ ] Dashboard shows recent checkouts with images
- [ ] Works reliably for 10+ checkouts in a row

**Phase 2 Complete When:**
- [ ] Model recognizes 20+ common lab items with >90% accuracy
- [ ] Auto-labeling applied to new checkouts
- [ ] Unknown items queued for manual labeling
- [ ] Retraining pipeline works end-to-end

**Phase 3 Complete When:**
- [ ] Face recognition identifies enrolled users accurately
- [ ] Full automatic checkout (item + person + time) logged
- [ ] Overdue reminders sent to correct person
- [ ] Privacy controls implemented and documented

**Project Complete When:**
- [ ] System runs unattended for 30+ days
- [ ] Training data pipeline feeds model improvements
- [ ] Multiple checkout stations deployed
- [ ] Documentation complete

---

## Documentation Deliverables

- [ ] README with setup instructions
- [ ] Hardware assembly guide (camera mounting)
- [ ] Checkout station placement guide
- [ ] Dashboard user guide
- [ ] Adding new items guide
- [ ] Model training guide
- [ ] Privacy policy for face recognition

---

## Links

- **Jira Epic:** [TBD]
- **GitHub Repo:** [TBD]
- **Viam Organization:** [TBD]
- **Hardware BOM:** [TBD]

---

## Technical Details

### Checkout Detection

**Approach 1: Motion + Pose Detection**
```
1. Camera monitors checkout zone continuously
2. Motion detected → start analyzing frames
3. Detect "person holding object" pose
4. Capture high-res frame
5. Save + notify
```

**Approach 2: Simple Button**
```
1. Person holds up item
2. Presses physical button
3. Camera captures frame
4. Save + notify
```

**Approach 3: Dwell Time**
```
1. Camera monitors checkout zone
2. Person + object detected in zone
3. If stable for 2 seconds → capture
4. Save + notify
```

Recommendation: Start with Approach 2 (button) for reliability, evolve to Approach 1 or 3.

### Data Schema

```
checkouts:
  - id: string (uuid)
  - timestamp: datetime
  - image_url: string (cloud storage path)
  - item_name: string (nullable - manual or ML)
  - item_confidence: float (nullable - ML confidence)
  - person_name: string (nullable - manual or ML)
  - person_confidence: float (nullable - ML confidence)
  - station_id: string
  - status: enum (pending_review, labeled, auto_labeled)

items:
  - id: string
  - name: string
  - category: string
  - location: string (home station)
  - image_urls: array (reference images for training)

users:
  - id: string
  - name: string
  - email: string
  - team: string
  - face_enrolled: boolean
  - face_embedding: blob (nullable)
```

### Notification Format

**Slack message:**
```
📦 Checkout detected
📍 Hardware Lab Station
🕐 10:32 AM

[Embedded photo of person holding item]

Item: [Unknown - click to label] or [Intel RealSense D435]
Person: [Unknown - click to label] or [Shannon]
```

### ML Pipeline

**Item Recognition:**
1. Export labeled checkout images
2. Crop to item region (manual or detected)
3. Train classifier (transfer learning from ImageNet)
4. Deploy to checkout stations
5. Monitor accuracy, retrain as needed

**Face Recognition:**
1. Collect face images during enrollment (multiple angles)
2. Generate face embeddings (e.g., using face_recognition library)
3. Store embeddings in user database
4. On checkout, extract face → find nearest embedding
5. Apply confidence threshold for match

---

## Notes

**Why no tagging:**
- Zero friction for users - just hold up and go
- No inventory of tags to manage
- Works with any item immediately
- System improves over time through use

**Gap Features This Project Addresses:**
- **Event-Driven Automation** - Checkout detection, overdue alerts
- **Data Pipeline** - Images → labels → training → deployment
- **Scheduled Tasks** - Daily summaries, weekly reports
- **Customer Delivery** - Dashboard with audit trail

**Privacy Considerations:**
- Face recognition requires explicit opt-in
- Users can view and delete their data
- Option to use system without face recognition (photo audit only)
- Clear signage at checkout stations

**Why this approach is valuable:**
- Works on day one with zero ML training
- Builds its own training data through normal use
- Each phase adds value incrementally
- Solves real problem the team faces
- System will actually be used after hackathon
