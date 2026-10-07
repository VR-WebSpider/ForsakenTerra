# Forsaken Terra: Isolation

A multiplayer wilderness survival RPG framework built in **Unreal Engine 5 (C++)** by **Vivekanand Rajbhar (WebSpider Studios)**.

This project was built to establish an open-world survival game loop: managing character vitals (hunger, thirst, stamina), drag-and-drop replicated inventory, equippable firearms, dynamic day/night cycles, and hostile sensor-driven zombie AI.

---

## ⚡ Technical Highlights

### 1. Survival Vitals & Metabolism Model
* **Decay Calculations:** Hunger and Thirst decay over time via delta time accumulation, with decay multipliers driven by character velocity (walking, sprinting, resting).
* **Affliction Penalties:** Reaching zero hunger or thirst begins damaging core health over tick intervals. Sprinting is locked when stamina depletes.
* **Consumable Interaction:** Food items restore hunger, clean water restores thirst, and bandages/medkits trigger health restoration over a time window.

### 2. Replicated Grid Inventory
* **Weight & Slot Constraints:** Inventory capacity enforces both maximum slot limits and maximum encumbrance weight. Exceeding carry limits gradually slows maximum walking speed.
* **Equippable Gear:** Dedicated equipment sockets for primary rifles, secondary sidearms, and utility tools (flashlights, melee).
* **Drop & Loot Containers:** World item actors (`SPickupActor`) spawn dropped physics meshes with networked interact prompt delegates (`SUsableActor`).

### 3. Dynamic Day/Night Cycle & Lighting
* Celestial actor driving continuous directional light rotation, atmospheric Rayleigh scattering, and night sky skylight captures.
* Day-night cycle rate can be dynamically configured in seconds per full 24-hour in-game rotation.

### 4. Hostile Creature AI & Perception
* **PawnSensing Component:** Zombie AI detects player footsteps within an audio range radius and spots characters in a 90-degree visual cone.
* **Behavior Tree Logic:** Switches between ambient roaming waypoints, investigating sudden sound events, and direct sprint pursuits when visual contact is confirmed.

---

## 📁 Project Structure

```
Source/SurvivalGame/
├── Private/
│   ├── AI/                  # Zombie character, AI controller, and patrol tasks
│   ├── Components/          # Character movement and carry object components
│   ├── Items/               # Consumables, flashlights, weapons, and pickups
│   ├── Player/              # SCharacter, SPlayerController, and spectator pawns
│   ├── UI/                  # HUD and inventory UMG bindings
│   └── World/               # GameMode, GameState, and TimeOfDay manager
└── Public/                  # Header declarations and shared structs
```

---

## 🛠️ How to Build & Run

### Requirements
* Unreal Engine 5.8 (or 5.7 / 4.27)
* Visual Studio 2022 (with *Game Development with C++* workload)
* Windows 10/11 64-bit

### Steps
1. Clone the repository:
   ```bash
   git clone https://github.com/VR-WebSpider/ForsakenTerra.git
   ```
2. Right-click `SurvivalGame.uproject` → **Generate Visual Studio project files**.
3. Open `SurvivalGame.sln` in Visual Studio 2022.
4. Set build configuration to **Development Editor** | **Win64**.
5. Build and launch (F5).
6. Open `/Game/Maps/CoopLandscape_Map` to test multiplayer survival mechanics, item harvesting, and zombie AI loops.

---

## 📜 Credits & License

* Developed and extended by **Vivekanand Rajbhar (WebSpider Studios)**.
* Built upon foundational survival game architecture created by **Tom Looman**.
* Licensed under the [MIT License](LICENSE).
