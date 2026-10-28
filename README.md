# Left 4 Bots 2 (Pace and Carry Fork)

This is a fork of [smilz0's Left 4 Bots 2](https://github.com/smilz0/Left4Bots). 

While preserving the core human-like behavior and automation of L4B2, this fork introduces **squad pacing**, **single-file snake formations**, **persistent item carrying (`carry_always`)**, and **expanded primary weapon enforcement (Rifles & SMGs)**.

---

## 🌟 New Features in This Fork

### 1. 🚶 Squad Pacing (`pace_with_me` & `pace_stop`)
* **Speed Mirroring:** Bots automatically match your exact speed. When you walk (`+speed`), the bots walk alongside you. When you stop, they stop. When you sprint, they break formation and revert to native pathing to keep up.
* **Squad Formations:** Bots arrange themselves into dynamic tactical slots around you (Front-Left, Front-Right, Flanks, Rear).
* **Natural Drift:** Bots periodically shift their spacing subtly so they look and feel like human teammates rather than rigid statues.
* **Combat Intelligence:** If a Tank spawns, a teammate is incapacitated, or an intense fight breaks out, pacing automatically pauses so bots can defend themselves and revive allies freely.

### 2. 🐍 Single-File Conga Line (`snake_in` & `snake_out`) - WIP
* **Breadcrumb Navigation:** Bots record and follow a trail of footprints left by the leader, forming a single-file line behind you.
* WIP. Bots warp to maintain formation.

### 3. 📦 Persistent Item Carrier (`carry_always`)
In vanilla L4B2, dropping a carried item during combat often cancels the order.
* **Permanent Assignment:** Assign a bot to be the permanent carrier of a specific object (Gnome, Cola, Gascan, Fireworks, Propane Tank, or Oxygen Tank).
* **Combat Drop & Auto-Recovery:** When attacked, the bot will drop the item to fight. Once the danger has passed (`carry_always_safe_time`), the bot will automatically search for the item and pick it back up without needing a new command.

### 4. 🔫 Rifle & SMG Weapon Enforcement
* Vanilla L4B2 includes settings to force bots to stay on Shotguns or Sniper Rifles (`enforce_shotgun`, `enforce_sniper_rifle`).
* This fork expands enforcement to **Assault Rifles (`enforce_rifle`)** and **SMGs (`enforce_smg`)**, preventing bots from unnecessarily swapping away from their primaries to weak sidearms.

---

## 🕹️ New Chat & Console Commands

Use these via in-game chat using `!l4b <botsource> <command> [args]` (or in console via `scripted_user_func l4b,...`):

| Command | Example | Description |
| :--- | :--- | :--- |
| `pace_with_me` | `!l4b bots pace_with_me` | Orders bots to pace with you. You can optionally specify a slot number (1–4) or another survivor's name. |
| `pace_stop` | `!l4b bots pace_stop` | Cancels pacing mode and restores normal bot AI behavior. |
| `snake_in` | `!l4b bots snake_in` | Forms a single-file line behind you (or behind a specified target). |
| `snake_out` | `!l4b bots snake_out` | Disbands the snake formation and returns bots to normal movement. |
| `carry_always` | `!l4b ellis carry_always gnome` | Assigns a bot to permanently carry an item type (`gnome`, `cola`, `gascan`, `propane_tank`, `fireworkscrate`, `oxygentank`), or the item you are looking at. |
| `checkmemory` | `!l4b ellis checkmemory` | Debug command: displays what item model the bot is currently assigned to carry. |
| `cancel carry_always` | `!l4b ellis cancel carry_always` | Clears the persistent carry memory and drops the item. |

---

## ⚙️ New Settings Configuration

The following new options can be configured in `left4bots_settings.nut` or via `!l4b settings [setting] [value]`:

### Weapon Enforcement
```nut
// [0 - 15] Bitflag: Prevent bots from switching away from Rifles to secondary.
// 15 = All secondaries blocked (pistol + magnum + melee + chainsaw), 0 = Vanilla behavior.
enforce_rifle = 15

// [0 - 15] Bitflag: Prevent bots from switching away from SMGs to secondary.
enforce_smg = 15
```

### Squad Pacing Offsets & Spacing
```nut
// Side and Back offsets for squad formation slots (relative to leader)
pace_slot1_side = 50       // Slot 1 (Front Right)
pace_slot1_back = -120

pace_slot2_side = -60      // Slot 2 (Behind Left)
pace_slot2_back = -20

pace_slot3_side = -50      // Slot 3 (Front Left)
pace_slot3_back = -100

pace_slot4_side = 50       // Slot 4 (Behind Right)
pace_slot4_back = -20

// Scale range for dynamic positioning drift (0.2 = keeps bots at least 20% separated)
pace_drift_min_scale = 0.2
pace_drift_max_scale = 1.0

// Time interval (in seconds) between selecting new drift positions
pace_drift_min_time = 3.0
pace_drift_max_time = 6.0
```

### Snake Formation & Teleport Settings
```nut
// Distance (in units) the bot will stay behind the target ahead of it
snake_formation_distance = 50

// Max distance before the bot teleports to catch up if stuck/lagged behind
snake_formation_teleport_distance = 100
```

---

## 📜 Credits
* **[smilz0](https://github.com/smilz0/Left4Bots)** - Original creator of Left 4 Bots 2.
* **[EagleRaviOrange](https://github.com/grotovu/Left4Bots)** - Fork author: Squad pacing, dynamic drift formation, breadcrumb snake formation, `carry_always` logic, and Rifle/SMG weapon enforcement.
