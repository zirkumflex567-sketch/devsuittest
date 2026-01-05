# 🎯 15. Milestones & Checklists (WMA-MVP)

**Zeitrahmen:** 4–8 Wochen (15–22 Personentage à 4 Std/Tag)

---

## 📅 Milestone Overview

```
M1: Setup & Prototyp          [Days 1–2]   → Basic Vehicle + Camera
M2: Horde & Combat            [Days 3–5]   → Spawner + 3 Enemies + 2 Weapons
M3: Loot & Upgrades           [Days 6–7]   → Pickup + UI + Application
M4: Hub & Save                [Days 8–9]   → Meta System + Persistence
M5: Polish & Audio            [Days 10–11] → SFX + Music + UI Polish
M6: Local Coop (optional)     [Days 12–13] → 2P Splitscreen / Shared Cam
M7: QA & Release              [Days 14+]   → Bug fixes, final checks
```

---

## ✅ MILESTONE 1: Setup & Prototyp (2 Days)

### **Objective:** Project structure ready, basic vehicle controllable, camera working

### **Deliverables**
- [ ] Unity 6 project created, URP configured
- [ ] Project structure (Assembly Definitions, folders)
- [ ] Zenject DI container setup
- [ ] Scene structure: Bootstrap, MainMenu, Hub, Arena
- [ ] Input System configured (WASD + Mouse)
- [ ] Vehicle Model imported (Quaternius Hovercraft)
- [ ] Vehicle Controller script (basic movement)
- [ ] Camera Controller (third-person follow)
- [ ] Reticle UI (simple crosshair)

### **Subtasks**
- [ ] M1.1: Create Unity 6 project, install packages
- [ ] M1.2: Create Zenject installers + Bootstrap scene
- [ ] M1.3: Import Vehicle model, create prefab
- [ ] M1.4: Implement VehicleController (WASD movement)
- [ ] M1.5: Implement CameraController + Cinemachine
- [ ] M1.6: Create reticle prefab, position on screen
- [ ] M1.7: Test vehicle movement in empty scene

### **Cursor Prompt (M1)**
```
[See Docs/16_Cursor_Codex_Runbooks.md → M1_Setup Prompt]
```

### **QA Checklist**
- [ ] Vehicle moves smoothly with WASD
- [ ] Camera follows vehicle smoothly, doesn't jitter
- [ ] Reticle centered on screen
- [ ] No editor errors/warnings
- [ ] Project builds without errors

### **Estimated Time:** 1.5 Days
### **Blocker:** None
### **Next:** M2

---

## ✅ MILESTONE 2: Horde & Combat (3 Days)

### **Objective:** Enemies spawn in waves, player can shoot, combat feels responsive

### **Deliverables**
- [ ] Horde Director system (wave spawning)
- [ ] 3 Enemy Types imported (Boar Grunt, Hyena Runner, Raven Swooper)
- [ ] Enemy AI (simple Chase → Attack FSM)
- [ ] Enemy Prefabs with LOD + Colliders
- [ ] 2 Weapon Types (Primary + Secondary)
- [ ] Projectile pooling system
- [ ] Weapon firing mechanics (damage, recoil)
- [ ] Hit detection (raycast / projectile collision)
- [ ] Enemy death + loot drop trigger
- [ ] Horde spawning UI (wave count, timer)

### **Subtasks**
- [ ] M2.1: Implement HordeDirector class + WaveManager
- [ ] M2.2: Create enemy spawn points (8 around arena)
- [ ] M2.3: Import 3 monster models, create materials
- [ ] M2.4: Implement EnemyAI (State Machine)
- [ ] M2.5: Implement EnemyDamageReceiver interface
- [ ] M2.6: Create weapon data + WeaponController
- [ ] M2.7: Implement Projectile pooling + firing
- [ ] M2.8: Setup hit detection (raycast / collider)
- [ ] M2.9: Create HUD canvas, show wave info
- [ ] M2.10: Test wave progression + enemy behaviors

### **QA Checklist**
- [ ] Enemies spawn every 2–3 seconds in wave
- [ ] At least 2 wave types spawn (easy, then hard)
- [ ] Weapon primary fire works (projectile visible)
- [ ] Weapon secondary fire works (different feel)
- [ ] Enemies chase player when visible
- [ ] Enemy melee attacks damage player
- [ ] Shooting enemy deals damage (visible health reduction)
- [ ] Enemy death triggers loot drop
- [ ] HUD shows current wave + wave timer
- [ ] No major performance issues (60+ FPS with 30 enemies)

### **Estimated Time:** 3 Days
### **Blocker:** M1
### **Next:** M3

---

## ✅ MILESTONE 3: Loot & Upgrades (2 Days)

### **Objective:** Loot drops, player can pick up, upgrades apply and change stats

### **Deliverables**
- [ ] Loot drop system (Scrap, Tech, Upgrades)
- [ ] Loot pickup prefab with magnet radius
- [ ] UI: Upgrade selection screen (show 3 choices)
- [ ] Upgrade application logic (stat modifications)
- [ ] HUD: Resource counter (Scrap/Tech/Health)
- [ ] Upgrade data structure (ScriptableObjects)

### **Subtasks**
- [ ] M3.1: Create LootDrop prefab + LootDropper script
- [ ] M3.2: Implement magnet radius (auto-pickup)
- [ ] M3.3: Create Upgrade data (SO templates)
- [ ] M3.4: Implement UpgradeSelectionUI (show every 5 min)
- [ ] M3.5: Implement UpgradeApplier (apply stat mods)
- [ ] M3.6: Add resource display to HUD
- [ ] M3.7: Test upgrade effects (damage ↑, speed ↑, etc.)

### **QA Checklist**
- [ ] Loot drops on enemy death (visible)
- [ ] Loot auto-magnetizes to player at 5m radius
- [ ] Loot disappears when collected
- [ ] Upgrade UI appears every 5 minutes
- [ ] Selecting upgrade applies stat changes immediately
- [ ] Resource counter updates correctly
- [ ] Multiple upgrades stack correctly
- [ ] No UI overlap / readability issues

### **Estimated Time:** 2 Days
### **Blocker:** M2
### **Next:** M4

---

## ✅ MILESTONE 4: Hub & Save System (2 Days)

### **Objective:** Persistent meta-progression, shop functional, save/load works

### **Deliverables**
- [ ] Hub scene (minimal, shows vehicle + UI)
- [ ] Shop UI (buy upgrades with Scrap/Tech)
- [ ] Save system (JSON serialization)
- [ ] Load system (restore meta progress)
- [ ] Run summary screen (end of run)
- [ ] Meta progression tracking (total Scrap/Tech)

### **Subtasks**
- [ ] M4.1: Create Hub scene layout
- [ ] M4.2: Implement SaveSystem (JSON writer/reader)
- [ ] M4.3: Create MetaProgressManager (persistent data)
- [ ] M4.4: Implement Shop UI + purchase logic
- [ ] M4.5: Create RunSummaryScreen (show stats)
- [ ] M4.6: Implement Game Over → Hub transition
- [ ] M4.7: Test save/load cycle

### **QA Checklist**
- [ ] Hub scene loads without errors
- [ ] Shop shows available upgrades
- [ ] Player can buy upgrade with Scrap
- [ ] Game Over screen shows run summary
- [ ] Closing and reopening game preserves meta progress
- [ ] Run summary data matches stats tracker
- [ ] No save file corruption

### **Estimated Time:** 2 Days
### **Blocker:** M3
### **Next:** M5

---

## ✅ MILESTONE 5: Polish & Audio (2 Days)

### **Objective:** Game feels complete, SFX + Music added, UI polished

### **Deliverables**
- [ ] SFX integrated (weapon, hit, pickup, UI)
- [ ] Background music looping
- [ ] Volume sliders (Settings screen)
- [ ] UI polish (colors, spacing, animations)
- [ ] Game Over + Win screen
- [ ] Pause menu functional
- [ ] Localization DE + EN (all UI text)

### **Subtasks**
- [ ] M5.1: Import SFX assets (Zapsplat / Freesound)
- [ ] M5.2: Implement SFXPlayer (audio pooling)
- [ ] M5.3: Wire SFX to game events (fire, hit, death, etc.)
- [ ] M5.4: Implement music looping
- [ ] M5.5: Create Settings screen (volume controls)
- [ ] M5.6: Polish HUD visuals (colors, fonts)
- [ ] M5.7: Create Game Over + Pause screens
- [ ] M5.8: Setup Localization (DE + EN)
- [ ] M5.9: Translate UI text

### **QA Checklist**
- [ ] All weapon sounds play on fire
- [ ] Hit feedback SFX plays on impact
- [ ] Pickup/loot SFX plays on collection
- [ ] Music plays continuously, loops smoothly
- [ ] Volume sliders adjust master volume
- [ ] UI text readable, good contrast
- [ ] Game Over screen shows correctly
- [ ] Pause menu pauses gameplay
- [ ] DE + EN text correctly displayed

### **Estimated Time:** 2 Days
### **Blocker:** M4
### **Next:** M6 (optional) or M7

---

## ⭐ MILESTONE 6: Local Coop (Optional, 1–2 Days)

### **Objective:** 2 players can play simultaneously on same PC

### **Deliverables**
- [ ] 2x Vehicle Controller instances
- [ ] 2x Camera setup (splitscreen left/right or shared)
- [ ] 2x Input handlers (separate gamepad/keyboard per player)
- [ ] Horde scaling (+30% enemies with 2P)
- [ ] Shared run state (combined resources, upgrades)

### **Subtasks**
- [ ] M6.1: Duplicate Vehicle + Camera, create player 2 setup
- [ ] M6.2: Configure splitscreen viewports (left/right halves)
- [ ] M6.3: Setup 2x PlayerInput (controller mapping)
- [ ] M6.4: Modify HordeDirector for 2P scaling
- [ ] M6.5: Sync resource/upgrade state between players
- [ ] M6.6: Test 2P gameplay

### **QA Checklist**
- [ ] Player 1 can control vehicle with WASD + Mouse
- [ ] Player 2 can control with Gamepad (or alt keyboard)
- [ ] Both cameras visible in splitscreen
- [ ] No camera clipping / overlap
- [ ] Horde has 30% more enemies with 2P
- [ ] Loot shared correctly (both players benefit)

### **Estimated Time:** 1–2 Days
### **Blocker:** M5
### **Next:** M7

---

## ✅ MILESTONE 7: QA & Release (1+ Days)

### **Objective:** No critical bugs, game is playable from start to finish

### **Deliverables**
- [ ] Bug list (low priority: known issues)
- [ ] Performance optimized (60 FPS target)
- [ ] Credits screen complete
- [ ] Build tested on target machine
- [ ] Release build created

### **Subtasks**
- [ ] M7.1: Run through full game flow (start → extraction → win)
- [ ] M7.2: Test all major features (weapons, upgrades, save, coop)
- [ ] M7.3: Performance profiling (identify bottlenecks)
- [ ] M7.4: Create in-game credits/attribution screen
- [ ] M7.5: Build executable + test
- [ ] M7.6: Create release checklist

### **QA Checklist**
- [ ] No crashes
- [ ] All UI readable
- [ ] Gameplay loop works (start → play → upgrade → extraction → win)
- [ ] Audio plays correctly
- [ ] Localization works
- [ ] Save/load works
- [ ] Performance: 60+ FPS (1440p)
- [ ] Credits displayed correctly

### **Estimated Time:** 1–2 Days
### **Blocker:** M6 (if included) or M5

---

## 📊 Timeline Summary

| Milestone | Days | Start | End | Blocker | Deliverable |
|-----------|------|-------|-----|---------|------------|
| **M1** | 2 | Day 1 | Day 2 | — | Vehicle + Camera |
| **M2** | 3 | Day 3 | Day 5 | M1 | Horde + Combat |
| **M3** | 2 | Day 6 | Day 7 | M2 | Loot + Upgrades |
| **M4** | 2 | Day 8 | Day 9 | M3 | Hub + Save |
| **M5** | 2 | Day 10 | Day 11 | M4 | Polish + Audio |
| **M6** | 2 | Day 12 | Day 13 | M5 | Local Coop |
| **M7** | 1+ | Day 14+ | — | M6 | QA + Release |
| **TOTAL** | 14–16 | — | — | — | **Playable WMA-MVP** |

---

**Nächster Schritt:** 16_Cursor_Codex_Runbooks.md (Detaillierte Cursor Prompts für jedes Milestone)
