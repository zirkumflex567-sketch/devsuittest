# 🎯 16. Cursor + Codex Runbooks (Pro Milestone)

**Verwendung:** Öffne Cursor, kopiere Prompt komplett, füge ihn in Codex Chat ein (mit Projekt-Context).

**Pro-Tipp:** Speichere komplette Prompts als `.md` im Projekt `/Docs/_prompts/` für später.

---

## 🚀 MILESTONE 1: Setup & Prototyp

### **M1.1 Prompt: Project Setup & DI Container**

```
You are an expert Unity developer. I'm building a Horde Arena game 
in Unity 6 with URP and need your help setting up the core infrastructure.

TASK:
1. Create the project structure (Assembly Definitions, folders)
2. Setup Zenject Dependency Injection
3. Create Bootstrap scene that loads the DI container
4. Create scene definitions (Bootstrap, MainMenu, Hub, Arena)

CONSTRAINTS:
- Use Zenject for all service registration
- Assembly Definitions: Core, Systems, Entities, UI, Utilities
- Use async scene loading where appropriate
- No external assets yet, just architecture

DELIVERABLES:
- Project structure (folder layout with .asmdef files)
- Bootstrap.cs script (Zenject container setup)
- Installer scripts (CoreInstaller, SystemsInstaller)
- Scene structure outlined
- Namespace conventions established

Output as C# code, fully commented. Include using statements.
```

---

### **M1.2 Prompt: Vehicle Controller & Input**

```
I need to create a responsive vehicle controller for my top-down horde game.

SPECIFICATIONS:
- Input: WASD for movement (cardinal directions)
- Movement: Physics-based (Rigidbody.velocity)
- Max Speed: 20 m/s
- Acceleration: 100 m/s²
- Camera target: Vehicle position
- Coop-ready: Can handle multiple instances with different input handlers

ARCHITECTURE:
- Use Input System (UnityEngine.InputSystem)
- Separate concerns: VehicleController (logic) vs VehicleMovement (physics)
- Use interfaces for injected dependencies
- Event system for stat changes

DELIVERABLES:
- VehicleController.cs (input handling + logic)
- VehicleMovement.cs (physics implementation)
- IVehicleMovement.cs (interface)
- VehicleStats.cs (health, armor, etc.)
- Installation in Zenject

Output C# code. Add both keyboard and gamepad input.
```

---

### **M1.3 Prompt: Camera Controller (Third-Person)**

```
Create a third-person camera system for my vehicle-based horde game.

REQUIREMENTS:
- Follow vehicle from behind + above (offset: 8m back, 3m up)
- Smooth follow (lerp-based, no jitter)
- Support for Cinemachine (optional but preferred)
- Aiming reticle on screen (center)
- Coop-ready: Each player has separate camera

DELIVERABLES:
- CameraController.cs (or use Cinemachine VirtualCamera)
- ReticleController.cs (UI crosshair, fixed center)
- InstallBindings in Zenject for camera services
- Test scene setup

Output as C# code. Include camera offset tuning parameters.
Make it compatible with Cinemachine if available.
```

---

## 🌊 MILESTONE 2: Horde & Combat

### **M2.1 Prompt: Horde Director & Wave System**

```
Create the core Horde Director system that spawns enemies in waves.

SPECIFICATIONS:
- Wave-based progression (15 waves for MVP)
- Each wave has: duration, enemy spawn rules, difficulty multiplier
- Spawn budget system (allocate enemy "cost" per wave)
- Wave transitions: Combat → Rest Phase → Next Wave
- Difficulty scaling: +0.1x per 10 minutes after wave 15

ARCHITECTURE:
- HordeDirector.cs (master system)
- WaveManager.cs (current wave logic)
- WaveData.cs (ScriptableObject wave definitions)
- EnemySpawnRule.cs (data structure for spawn rules)
- DifficultyScaler.cs (apply multipliers to enemy stats)

DELIVERABLES:
- Data structure for waves (SO-compatible)
- Spawn logic (budget-based spawning)
- Difficulty scaling
- Wave timer + state machine
- Integration points documented

Output as C# code. Make it data-driven (no hardcoded wave rules).
Include event callbacks (OnWaveStart, OnWaveComplete, OnDifficultyChange).
```

---

### **M2.2 Prompt: Enemy AI State Machine**

```
Create a simple but effective enemy AI using a state machine.

STATES:
- Idle: Waiting for player detection
- Chase: Moving toward player
- MeleeAttack: In close range, attacking
- RangedAttack: At range, firing projectiles
- Retreat: Fleeing (special enemies only)
- Dead: Returning to pool

REQUIREMENTS:
- Detection range: configurable per enemy type
- Attack cooldowns per state
- Crowd avoidance (simple Physics.OverlapSphere check)
- Works with any movement system
- Coop-aware: finds nearest player

DELIVERABLES:
- EnemyAI.cs (state machine core)
- EnemyState.cs (enum)
- StatePatterns (Chase, Attack, etc.)
- Crowd avoidance logic
- Configurable parameters

Output as C# code. Use enum-based state machine.
Include transition conditions clearly. Make it extensible for new states.
```

---

### **M2.3 Prompt: Combat System & Projectiles**

```
Implement a weapons + projectile system with pooling.

WEAPON TYPES:
- Primary: Auto-fire (fire rate: 10 shots/sec)
- Secondary: Manual, cooldown (fire rate: 2 shots/sec)

PROJECTILE SYSTEM:
- Pool-based (create N projectiles at start, reuse)
- Hitscan (raycast) support for instant-hit weapons
- Collision detection (sphere cast for projectiles)
- Damage application via IDamageReceiver interface
- Knockback on hit

ARCHITECTURE:
- WeaponController.cs (input + firing logic)
- WeaponData.cs (ScriptableObject for weapon configuration)
- Projectile.cs (pooled projectile behavior)
- ProjectilePool.cs (object pooling manager)
- HitscanHandler.cs (raycast weapon logic)
- ICombatEvents.cs (event interface for kills, hits)

DELIVERABLES:
- Weapon fire mechanics
- Projectile pooling system
- Hit detection (raycast + sphere)
- Damage application
- Recoil feedback (camera/aiming)

Output as C# code. Make weapons configurable via ScriptableObjects.
Include visual effects hooks (muzzle flash position, impact VFX).
```

---

### **M2.4 Prompt: Enemy Damage Receiver & Death**

```
Create a system for enemies to take damage and die.

REQUIREMENTS:
- IDamageReceiver interface (standardized)
- Health pool with variance (±10% per enemy type)
- Damage reduction (armor system, minimal for MVP)
- Death callback (triggers loot drop, removal from active list)
- Pooling-aware: SetActive(false) instead of Destroy

ARCHITECTURE:
- IDamageReceiver.cs (interface)
- EnemyDamageReceiver.cs (implementation)
- Health.cs (shared health component)
- Death event system
- Integration with LootSystem

DELIVERABLES:
- Damage application system
- Health tracking
- Death triggers
- Event callbacks for loot drops
- Pooling-safe cleanup

Output as C# code. Use interfaces for maximum modularity.
Make it compatible with player vehicles too.
```

---

### **M2.5 Prompt: HUD & Wave Display**

```
Create a HUD system that shows:
- Current health
- Ammo/charge level (if weapon has it)
- Wave number + timer
- Current time survived
- Score (optional: enemy count)

REQUIREMENTS:
- TextMeshPro text elements
- Health bar (visual + numeric)
- Wave info updating in real-time
- Clean layout, high contrast
- Mobile-friendly readability

DELIVERABLES:
- HUDController.cs (main HUD manager)
- UI prefab (Canvas + elements)
- Data binding (health ↔ UI bar)
- Event subscriptions (HordeDirector.OnWaveChange, etc.)

Output as C# code and describe UI hierarchy.
Make HUD elements configurable (sizes, colors, positions).
```

---

## 🎁 MILESTONE 3: Loot & Upgrades

### **M3.1 Prompt: Loot Drop & Pickup System**

```
Create a loot system with auto-pickup and magnet radius.

LOOT TYPES:
- Scrap (common): Persistent meta-resource
- Tech (rare): Persistent meta-resource
- RunUpgrade (immediate): Stat mods for current run
- HealthPack (consumable): Heal player

PICKUP MECHANICS:
- Drops on enemy death at kill location
- Magnet radius: 5m, auto-move to player
- Collection animation (float to player over 0.5s)
- On-screen feedback (popup text with amount)

ARCHITECTURE:
- LootDrop.cs (individual loot item)
- LootDropper.cs (spawner, called on enemy death)
- LootPickup.cs (magnet & collection logic)
- LootType.cs (enum)
- ILootReceiver.cs (interface for collection)

DELIVERABLES:
- Loot spawn system
- Magnet radius pickup
- Resource accumulation
- Event triggers (ResourceGained, LootCollected)
- Visual prefab (glow, floating animation)

Output as C# code. Use object pooling for loot items.
Include random variance (Scrap: 1-5 per drop).
```

---

### **M3.2 Prompt: Upgrade Selection & Application**

```
Create a roguelike-style upgrade selection system.

FLOW:
1. Every 5 minutes, show UI with 3 random upgrades
2. Player clicks one
3. Upgrade applies immediately to current run
4. UI closes, game continues

UPGRADES:
- Categorized: Damage, Speed, Armor, StatusEffects, etc.
- Stat multipliers: 1.1x, 1.2x, etc.
- Can stack (multiple selections possible)
- Show description on card

ARCHITECTURE:
- UpgradeData.cs (ScriptableObject for each upgrade)
- UpgradeSelectionUI.cs (card picker)
- UpgradeApplier.cs (applies mods to player stats)
- RunUpgradeManager.cs (tracks active upgrades in session)

DELIVERABLES:
- Upgrade data structure
- Selection UI (3-card picker)
- Application logic (stat modifications)
- Stacking rules (diminishing returns optional)
- Event callbacks (OnUpgradeSelected, OnApplied)

Output as C# code. Make upgrade effects data-driven.
Include UI prefab structure description.
```

---

## 💾 MILESTONE 4: Hub & Save System

### **M4.1 Prompt: Save System (JSON Serialization)**

```
Create a persistent save system using JSON.

DATA TO SAVE:
- Meta Progress: Total Scrap, Total Tech, Runs Completed
- Last Run Summary: Time, Kills, Resources Earned, Upgrades Used
- Game Settings: Volume levels, Difficulty setting (future)

REQUIREMENTS:
- Use Newtonsoft.Json or built-in JsonUtility
- Save to Application.persistentDataPath
- Version support (for future migration)
- Auto-save after each run completion

ARCHITECTURE:
- SaveGame.cs (root serializable class)
- MetaData.cs (persistent player progress)
- RunData.cs (per-run summary)
- SaveSystem.cs (I/O operations)
- SaveManager.cs (Zenject service)

DELIVERABLES:
- Serializable data structures
- Save/Load methods
- File I/O (with error handling)
- Version checking
- Zenject service binding

Output as C# code. Use [System.Serializable] for JSON compatibility.
Include directory creation if needed.
Make save location easily configurable.
```

---

### **M4.2 Prompt: Hub Scene & Shop System**

```
Create a minimal Hub scene with a working shop.

HUB FEATURES:
- Display current resources (Scrap, Tech count)
- Shop UI: Buy upgrades with Scrap/Tech
- Run summary display (if returning from Arena)
- Button to start new Run (go to Arena)
- Simple visual: Vehicle displayed, UI overlays

SHOP MECHANICS:
- Show available items
- Cost display
- "Afford" check (greyed out if insufficient resources)
- Apply purchase (deduct resources, grant upgrade for next run)

ARCHITECTURE:
- HubManager.cs (scene orchestration)
- ShopUI.cs (shop display & purchase)
- ShopItem.cs (data structure)
- MetaProgressDisplay.cs (show Scrap/Tech)

DELIVERABLES:
- Hub scene setup
- Shop UI prefab
- Purchase logic
- Scene transitions (Hub → Arena)
- Resource display

Output as C# code + UI hierarchy description.
Keep it simple: minimal 3D (just vehicle model).
```

---

### **M4.3 Prompt: Run Summary Screen**

```
Create a screen that appears after game ends (win or loss).

DISPLAY:
- Time Survived
- Enemies Killed
- Resources Earned (Scrap, Tech)
- Upgrades Used (list)
- Final Wave Reached
- Win/Loss Message

BUTTONS:
- Return to Hub
- Restart Run (optional)

ARCHITECTURE:
- RunSummaryScreen.cs (UI controller)
- RunSummaryData.cs (data carrier)
- Transition logic (Arena → Summary → Hub)

DELIVERABLES:
- Summary UI prefab
- Data population logic
- Button actions
- Scene transition flow

Output as C# code + UI layout description.
```

---

## 🔊 MILESTONE 5: Polish & Audio + Localization

### **M5.1 Prompt: Audio System (SFX + Music)**

```
Create a simple audio manager for SFX and music.

FEATURES:
- SFX pooling (reuse audio sources)
- Music looping (background track)
- Volume control (master volume slider)
- Mute functionality (Settings)

SFX CATEGORIES:
- Weapon firing
- Hit/impact sounds
- Enemy death
- Loot pickup
- UI clicks
- Ambient (wind, machinery)

ARCHITECTURE:
- SFXPlayer.cs (pooled SFX playback)
- MusicManager.cs (music looping + crossfade)
- AudioPool.cs (object pooling for sources)
- AudioController.cs (volume + settings)
- AudioSettings.cs (SO for tuning)

DELIVERABLES:
- Audio pooling system
- SFX event triggers (OnWeaponFire, OnHit, etc.)
- Music manager
- Volume sliders (UI)
- Settings persistence

Output as C# code. Make audio sources poolable.
Include spatial audio positioning (attach to positions in world).
```

---

### **M5.2 Prompt: Localization (DE + EN)**

```
Setup Unity Localization for DE + EN languages.

SCOPE:
- All UI text (buttons, HUD, menus)
- System messages (wave start, game over, etc.)
- Enemy names, weapon names, upgrade names
- Lore snippets (if any)

REQUIREMENTS:
- Use Unity Localization package
- String tables for organized access
- Easy switching between languages (Settings menu)
- Default to English, with German fallback support

ARCHITECTURE:
- String tables (one per category: UI, Enemies, Weapons, etc.)
- LanguageManager.cs (language switching)
- LocalizationInstaller.cs (Zenject setup)
- Settings UI (language selector)

DELIVERABLES:
- String table setup (DE + EN)
- LanguageManager service
- Settings UI for language selection
- All UI text localized
- Localization data export for later VO

Output instructions + C# code for manager.
Include CSV export for easy translation review.
```

---

### **M5.3 Prompt: UI Polish & Game Over Screen**

```
Polish the UI and create Game Over / Win screens.

SCREENS:
- Game Over (Loss): "You Died" + Run Summary + Restart Button
- Game Won (Extraction): "Extracted!" + Run Summary + Return to Hub
- Pause Menu: Resume, Settings, Quit

UI IMPROVEMENTS:
- Color scheme: High contrast, wasteland aesthetic
- Fonts: Roboto (from Google Fonts)
- Spacing: Clear hierarchy, readable at 1440p
- Animations: Smooth transitions, button highlights

ARCHITECTURE:
- ScreenManager.cs (shows/hides screens)
- PauseManager.cs (pause logic)
- GameOverScreen.cs (death screen)
- WinScreen.cs (extraction screen)

DELIVERABLES:
- Game Over screen prefab
- Win screen prefab
- Pause menu prefab
- Color & font standards documented
- Animation clips (fade in/out)

Output as C# code + UI hierarchy.
```

---

## ⭐ MILESTONE 6: Local Coop (Optional)

### **M6.1 Prompt: 2-Player Setup & Input Handling**

```
Extend the game for 2-player local coop.

SETUP:
- Duplicate Vehicle + Camera for Player 2
- Split-screen cameras (left/right halves)
- Separate input handlers (P1: Keyboard+Mouse, P2: Gamepad)
- Shared run state (resources, waves, etc.)

COOP MECHANICS:
- Horde scales (+30% enemies with 2P)
- Shared loot pool
- Shared upgrades (apply to both vehicles)
- Win condition: Either player extraction success

ARCHITECTURE:
- PlayerInput wrapper (per-player input handler)
- PlayerManager.cs (tracks active players)
- CoopScaler.cs (scales horde for player count)
- CameraManager.cs (splitscreen viewports)

DELIVERABLES:
- 2x Player setup
- Input configuration
- Splitscreen cameras
- Horde scaling
- Shared state synchronization

Output as C# code. Include gamepad button mapping.
```

---

**Nächster Schritt:** 16_Cursor_Codex_Runbooks (Part 2) - M7 & weitere Prompts

*Hinweis: Diese Prompts sind Starter-Templates. In echter Verwendung mit Cursor + Codex detaillierter machen (Projekt-Context hinzufügen, Fehler zeigen, Feedback geben).*
