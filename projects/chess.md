# Project: Chess

## Overview

**One-line description:** Robot that plays chess against humans, physically moving pieces on a real board

**Project Lead:** TBD
**Team Members:** TBD
**Status:** Existing (has code, has backlog)

## Description

Chess is a robotic chess opponent that uses computer vision to detect piece presence and color, a chess engine (Stockfish) for move calculation, and a robot arm to physically move pieces on a real chessboard. Players sit across from the robot and play a normal game of chess.

The system detects **piece presence** (is there a piece?) and **piece color** (white or black) using point cloud height and RGB analysis. It does not currently identify piece types (king vs queen, etc.) — instead, it tracks game state programmatically and uses legal move constraints to infer opponent moves. This elegant approach means the robot can play against humans without needing piece type recognition.

This project demonstrates vision-based detection, precise manipulation, game engine integration, and creates an extremely engaging interactive demo.

## Viam Capabilities Demonstrated

### Core Capabilities
- [x] **Hardware Integration** — Camera, arm, gripper with consistent APIs
- [x] **Motion Planning** — Motion service, frame system, inverse kinematics
- [x] **Vision / ML Inference** — Classical CV (Hough transform, point cloud); ML is backlog
- [ ] **Data Capture & Sync** — Not primary focus (game state saved locally)
- [x] **Remote Operation** — Can play against robot remotely via video feed
- [x] **Module Development** — Chess service, piece-finder vision service via Registry
- [x] **Fragments** — Hardware configuration as reusable fragment

### Scale & Fleet Capabilities
- [ ] **Fleet Management** — Not applicable (single board)
- [x] **OTA Updates** — Module and configuration updates via Registry
- [ ] **Provisioning** — Not applicable (single board)

### Operational Capabilities
- [ ] **Scheduled Tasks** — Not applicable
- [ ] **Monitoring & Alerting** — Not applicable
- [ ] **Data Pipeline (ML Training)** — Backlog: capture → label → train → deploy for piece recognition

### Customer-Facing Capabilities
- [ ] **Customer Delivery** — Not applicable
- [ ] **Web/Mobile Apps** — Backlog: mode selection, chess clock (Option D)

## Hardware Requirements

| Component | Description | Specific Model |
|-----------|-------------|----------------|
| Arm | 7-DOF robot arm for piece movement | xArm 7 |
| Gripper | Chess piece handling | xArm Gripper |
| Camera | Board state detection (depth + RGB) | Intel RealSense D435 |
| Board | Standard chess board | Standard board |
| Pieces | Standard chess pieces | Standard pieces |
| Compute | Main controller | System76 Meerkat |
| Chess Engine | Move calculation | Stockfish (installed at /usr/games/stockfish) |
| Control (optional) | Physical button interface | Streamdeck (via viam-streamdeck module) |

**Remote-Friendly:** Yes - can play against robot remotely via video feed

---

## Existing Capabilities

The following is already implemented in viam chess:

### Board Detection
- Hough transform line detection for board edges
- Corner detection and refinement
- Perspective transform to square output image
- Point cloud filtering and coordinate transformation
- **Current limitation (v0):** Hard-coded camera position; board must be in expected field of view

### Piece Detection
- **Presence detection:** Point cloud height > 25mm indicates piece present
- **Color detection:** RGB values from point cloud classify white vs black
- **Does NOT identify piece type** — relies on game state tracking

### Game Logic
- Stockfish engine integration via UCI protocol
- Adjustable skill level (0-20)
- Castling support (kingside and queenside)
- Capture handling with graveyard positions
- Human vs robot play (infers moves from legal move constraints)
- State persistence to `~/data/chess.json` (FEN format)

### DoCommand API
- `go N` — Play N moves (alternating sides)
- `move <uci>` — Execute specific move (e.g., "e2e4")
- `reset` — Reset board to starting position
- `wipe` — Clear game state
- `center` — Move arm to center position
- `skill N` — Set Stockfish skill level

### CLI Tool
- `chesscli` for testing: move, go, reset, center commands

---

## Known Gaps

| Gap | Impact | Prerequisite For |
|-----|--------|------------------|
| **Piece type identification** | Cannot distinguish king from queen, etc. | Arbitrary position setup, better error recovery, robust reset |
| **Placement verification** | Cannot confirm piece is in correct position | Reliability improvements |
| **Graveyard capacity** | Only 24 positions; need 32+ | Long games with many captures |
| **En passant** | Not implemented | Rules-complete chess |
| **Promotion** | Not implemented | Rules-complete chess |
| **Board finding** | Hard-coded positions (v0) | Tolerant setup, dynamic detection |
| **App features** | No mode selection or chess clock | Player experience |

---

## MVP Options

These options build on the existing implementation:

### Option A: Polish Existing Gameplay (Reliability)
Make what exists work better and more reliably.
- **Scope:**
  - Placement verification — confirm piece is actually in correct position
  - Error recovery for failed grabs
  - Graveyard expansion (24 → 32+ positions)
  - Graveyard management improvements
  - Board finding v1 — tolerate position within 100mm, slight angle changes
  - Reset improvements
- **Complexity:** Medium
- **Demo Appeal:** High (fewer failures, longer games work)
- **Why:** Current system works but is fragile; this makes it demo-ready

### Option B: Complete Game Rules (Missing Features)
Implement the chess rules that are currently missing.
- **Scope:**
  - En passant — AI vs AI and Human vs AI
  - Promotion — AI vs AI and Human vs AI
- **Complexity:** Medium
- **Demo Appeal:** Medium (correctness matters to chess players)
- **Why:** Cannot claim "plays chess" without these rules; long games will encounter them

### Option C: Piece Type Recognition (ML)
Enable the system to identify which piece is which, not just presence + color.
- **Scope:**
  - Train ML model to classify piece types (king, queen, rook, bishop, knight, pawn)
  - Data pipeline: capture → label → train → deploy
  - Board finding v2 — full dynamic detection with orientation (A1/H8)
- **Complexity:** High
- **Demo Appeal:** High (enables new capabilities)
- **Why:** Prerequisite for arbitrary position setup, better error recovery, more robust reset
- **Unlocks:**
  - Set up game from any position (not just standard start)
  - Detect if wrong piece placed
  - Recovery when board state gets out of sync

### Option D: App & Player Experience
Add user-facing features for a polished experience.
- **Scope:**
  - Mode selection (AI vs AI, Human plays White, Human plays Black)
  - Chess clock
  - Teaching mode — replay famous games with commentary (stretch)
- **Complexity:** Medium
- **Demo Appeal:** Very High (visitor-friendly)
- **Why:** Makes the demo accessible and engaging for non-technical audiences

**Suggested order:** A → B → D → C (reliability first, then rules, then UX, then advanced ML)

**Selected MVP:** _______________

---

## Backlog

### Board Finding

| Version | Description | Status |
|---------|-------------|--------|
| v0 | Hard-coded positions — board must be in exact expected location | Current |
| v1 | Find board within ~100mm of expected, tolerate slight angle changes | Backlog |
| v2 | Full dynamic — find board anywhere, identify edges, determine A1/H8 orientation, compute all square locations | Backlog |

- [ ] **v0 → v1:** Tolerant board finding within 100mm, slight angle changes
- [ ] **v1 → v2:** Full dynamic detection — find board anywhere, identify corners, determine orientation
- [ ] **Camera centering:** Position camera so board is perfectly centered, H8 in bottom-left (x: ~1/3, y: max)

### Piece Detection & Placement
- [ ] **Placement verification:** Confirm piece is actually in correct position after placement
- [ ] **Piece type identification:** ML model to identify which piece is which (not just presence + color)
- [ ] **Data capture pipeline:** Capture board images during games for training data
- [ ] **Auto-labeling:** Label images with known game state (automatic ground truth)
- [ ] **Model training:** Train piece type classifier using captured data
- [ ] **Model deployment:** Push improved model via Registry

### Game Rules
- [ ] **En passant (AI vs AI):** Implement en passant capture
- [ ] **En passant (Human vs AI):** Detect and handle en passant from human player
- [ ] **Promotion (AI vs AI):** Implement pawn promotion (queen default or selection)
- [ ] **Promotion (Human vs AI):** Detect and handle promotion from human player

### Physical Execution
- [ ] **Graveyard expansion:** Increase capacity from 24 to 32+ positions
- [ ] **Graveyard management:** Improve organization and piece placement
- [ ] **Error recovery:** Detect and recover from failed grabs
- [ ] **Reset improvements:** More robust board reset logic
- [ ] **Difficulty levels:** Adjustable AI difficulty via Stockfish skill (already supported, needs UI)

### App & UX
- [ ] **Mode selection:** AI vs AI, Human plays White, Human plays Black
- [ ] **Chess clock:** Timed games with visual clock display
- [ ] **Teaching mode:** Replay famous games move-by-move with commentary
- [ ] **Voice commentary:** Robot announces moves
- [ ] **Remote play:** Play against robot from anywhere via app

### Data & Analytics
- [ ] **Game recording:** Capture and replay games with data service
- [ ] **Player statistics:** Track wins/losses/draws per player
- [ ] **Tournament mode:** Track multiple games, maintain leaderboard

### Event-Driven Automation
- [ ] **Game end detection:** Detect checkmate/stalemate, auto-save game and offer reset
- [ ] **Timeout handling:** If no move detected for X minutes, prompt player
- [ ] **Illegal position alert:** Alert if detected position is impossible

---

## Stretch Goals

- [ ] Play other games (checkers, Go with different board)
- [ ] Personality modes (aggressive, defensive, teaching)
- [ ] Celebrity voice packs for commentary
- [ ] AR overlay showing possible moves
- [ ] Integration with chess.com or Lichess for ratings
- [ ] Robot vs robot (two arms)
- [ ] Multi-board fleet with centralized tournaments

---

## Links

- **Existing Code:** ~/viam/viam-chess
- **GitHub Repo:** https://github.com/erh/viam-chess
- **Module ID:** erh:viam-chess
- **Hardware Doc:** https://docs.google.com/document/d/1T_ZlkjAxhhUZB5_EhZ64C6UP2SrXKVqBU8UHFkGirrw/
- **Setup Photos:** https://photos.app.goo.gl/GDuryUgFtMPufmRD7
- **Jira Epic:** [TBD]
- **Viam Organization:** [TBD]

---

## Technical Details

### How Human vs Robot Works

The system can play against humans **without piece type recognition** because:

1. It knows the current game state (which piece is on which square)
2. It knows all legal moves for the human's color
3. When the human moves, vision detects:
   - Square X (had a piece) → now empty
   - Square Y (was empty or had opponent piece) → now has a piece of human's color
4. **Only one legal move** matches that visual delta

Example: If it's Black's turn and the system sees e7 went from "black piece" to "empty" and e5 went from "empty" to "black piece", the system knows a black pawn was on e7 (from game state), and the only legal move producing this result is `e7e5`.

### Board Finding Versions

**v0 (Current):** Hard-coded camera position. Board must be in expected location.

**v1 (Backlog):** Find board within ~100mm of expected position. Tolerate slight angle changes. Uses existing Hough transform infrastructure.

**v2 (Backlog):** Full dynamic detection:
1. Find the board (anywhere in camera view)
2. Find edges
3. Identify A1/H8 corners (orientation)
4. Compute all 64 square locations
5. May require piece type recognition to determine orientation

### Stockfish Integration

- Communicates via UCI protocol over stdin/stdout
- Skill level 0-20 (maps to Stockfish's skill setting)
- Engine runs as subprocess
- FEN position sent before each move request

---

## Notes

**Design Insight:**
Piece type recognition is unnecessary for gameplay because legal move constraints + game state tracking uniquely identify any move. This is a lesson in practical robotics — sometimes you don't need the "obvious" capability.

