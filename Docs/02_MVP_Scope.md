# 2️⃣ MVP Scope: Must / Should / Could / Out-of-Scope

---

## ✅ MUST-HAVES (WMA-MVP, unverhandelbar)

### **Gameplay Core**
- [ ] 1 Arena (Scrapyard/Wasteland) mit Terrain Variations
- [ ] 2 spielbare Charaktere (Driver-Personas) mit Skillbäumen (3 Zweige)
- [ ] Vehicle-Select: 4 Klassen (Motorrad, Quad, Jeep, Truck)
- [ ] WMA-Restriktion: Motorrad (Solo) + Jeep (Coop)
- [ ] Third-Person Camera hinter Vehicle mit Aim-Reticle
- [ ] 6–8 Monster-Types (Low-Poly, Horde-ready)
- [ ] Horde Spawner mit Wave System (Skalierung über Zeit)
- [ ] 2–3 Weapon Types (Auto Primary, Manual Special min. 1x)
- [ ] Alle Waffen sind fahrzeugmontiert (keine Handwaffen)
- [ ] Loot Drops (Scrap, Tech, Run-Upgrades)
- [ ] Pre-Run: 2 aus 6 zufälligen Kopfgeldern wählen (Schwierigkeit + Belohnung)
- [ ] Extraction Mechanic (nach ~15 Min spawn Extraction Point)
- [ ] Endboss mit ausweichbaren Fähigkeiten (3 Varianten, WMA)
- [ ] Game Over / Win Condition
- [ ] **Local Coop 2-Player** (Splitscreen oder Shared Cam, TBD)

### **Meta/Hub**
- [ ] Persistent Resources: Scrap, Tech, Run-Summary
- [ ] Simple Shop (2–3 Upgrade Slots, kostengünstig)
- [ ] Save/Load (Spielstand + Meta-Upgrades)
- [ ] Run-History (sichtbar aber minimal)

### **UI/UX**
- [ ] HUD während Run: Health, Ammo, Score, Wave Count, Timer
- [ ] Pause Menu (funktional)
- [ ] Game Over Screen
- [ ] Hub/Menu Screen (minimal)
- [ ] Tooltips (Upgrade Cards, Shop Items)

### **Audio**
- [ ] SFX Pool: Waffen, Hit/Death, Loot-Pickup, UI
- [ ] Musik (1 Track oder Loop, von dir komponiert)
- [ ] Volume Slider

### **Localization**
- [ ] DE + EN UI Text (via Unity Localization)
- [ ] String Tables für alle UI-Text
- [ ] Glossary (Weapon names, Enemy names, etc.)

### **Code Quality**
- [ ] Modular Architecture (Systems, Patterns)
- [ ] Scriptable Objects für Data (Enemies, Weapons, Waves, etc.)
- [ ] Object Pooling für: Projectiles, VFX, Enemies
- [ ] Simple Save-System (JSON oder PlayerPrefs)

---

## 🟡 SHOULD-HAVES (WMA+ / Early Polish, wichtig aber nicht MVP-blocking)

### **Gameplay**
- [ ] 10+ Monster-Types (expanded roster)
- [ ] 5+ Weapon Types (variety)
- [ ] Elite-Monster (rare spawns, unique telegraph/attacks)
- [ ] Status Effects (Freeze, Burn, Poison) mit visuals
- [ ] Special Abilities (z.B. Evasion, Shield, Heal) als Run-Upgrades
- [ ] Goldgoblin (seltener, special behavior)
- [ ] Difficulty Settings (Easy/Normal/Hard)
- [ ] Tutorial / First-Time User Experience

### **Audio**
- [ ] Voice Lines (KI-TTS Deutsch, optional)
- [ ] More SFX Variety (per weapon, per enemy)
- [ ] Music Intensity Scaling (stärker bei Danger)

### **UI/UX**
- [ ] Better Hub Display (Vehicle sichtbar, Equipment preview)
- [ ] Upgrade Card Visual Polish (Icons, Animations)
- [ ] Leaderboard / Best Times (Local Storage)
- [ ] Settings: Volume, Brightness, Colorblind Mode
- [ ] Controller Support (vollständig)

### **Features**
- [ ] Achievements System (Basic: "Kill 1000", "Survive 30min")
- [ ] Stats Tracking (Kills, Damage Dealt, Upgrades Used)
- [ ] Cosmetics (Vehicle Skins, Decals, Colors)

---

## 🔵 COULD-HAVES (Nice-to-Have, später oder niemals)

- [ ] 3+ Arenen/Biomes
- [ ] Boss Encounters
- [ ] Story/Campaign Mode
- [ ] Online Coop (großer Scope, später)
- [ ] Mobile App / Dashboard
- [ ] Battle Pass / Seasonal Content
- [ ] User-Generated Content (Map Editor, etc.)
- [ ] Integrated Streaming / Clip Tools

---

## ❌ OUT-OF-SCOPE (WMA & WMA+)

| Feature | Reason |
|---------|--------|
| **Online Multiplayer** | Großer Scope, später als separate Milestone |
| **Vehicle Vs Vehicle** | Fokus auf PvE Horde, nicht PvP |
| **Multiple Arenas (>1)** | MVP: 1 Arena. Later: Biome-System |
| **Complex Quest/Story** | Minimal narrative, focused on gameplay loop |
| **Crafting System** | Only simple shop, not complex recipes |
| **Base Building / Colonies** | Out of scope for survivors-like |
| **Mobile Release (MVP)** | PC-First, Mobile porting later |
| **VR Support** | Out of scope |
| **Ray Tracing / High-End Graphics** | Low-Poly stylized, no AAA visuals |
| **Voice Chat in Coop** | Local Coop only, no networking |

---

## 🎯 Measurement (Definition of Done)

Wann ist WMA-MVP **DONE**?

### **Playable Criteria**
- ✅ Game startet, erster Run ist spielbar
- ✅ Mindestens 2 Waffen-Types schießen
- ✅ Mindestens 6 Monster-Types spawnen & greifen an
- ✅ Loot droppt, Upgrades funktionieren
- ✅ Extraction Point spawnt, kann "gewonnen" werden
- ✅ Run-Daten speichern/laden funktioniert
- ✅ Hub-Shop: Upgrades können mit Ressourcen gekauft werden
- ✅ 2-Player Coop: beide Spieler können gleichzeitig spielen (Min. ein splitscreen Prototype)

### **Quality Criteria**
- ✅ Keine kritischen Bugs (Crashes, Sequence Breaks)
- ✅ FPS stabil (30+ auf target machine)
- ✅ UI lesbar auf 1440p (schriftgröße, contrast)
- ✅ Audio Works (SFX, Musik abspielbar)
- ✅ Localization: DE Text korrekt, EN fallback OK

### **Time Criteria**
- ✅ Playtime bis "Win": 10–20 Minuten
- ✅ Run Variety: Upgrades fühlen sich unterschiedlich an
- ✅ Kein Softlock / Unendliche Loops

---

## 📅 Milestone Timeline (Rough)

| Milestone | Duration | Blockers | Output |
|-----------|----------|----------|--------|
| **M1: Setup & Prototyp** | 2 days | None | Projekt, Basic Vehicle + Camera |
| **M2: Horde & Combat** | 3 days | M1 | Spawner, 3 Monster-Types, 2 Waffen |
| **M3: Loot & Upgrades** | 2 days | M2 | Pickup, UI, Upgrade Logic |
| **M4: Hub & Save** | 2 days | M3 | Meta System, Shop, Persistence |
| **M5: Polish & QA** | 2–3 days | M4 | Bug fixes, SFX/Music, Localization |
| **M6: Local Coop (optional extra)** | 1–2 days | M5 | Splitscreen oder shared cam |
| **Total** | 12–15 days | — | **Playable WMA-MVP** |

---

## 🔄 Iteration Plan (Nach WMA-MVP)

### **Phase: WMA+1 (Post-MVP, ~1 Woche)**
- Monster-Roster auf 10+ erweitern
- 5+ Waffen-Types
- Elite-Monster + special spawning rules
- Status Effects (visual)
- Better Hub UI

### **Phase: WMA+2 (Full Feature Pass, ~2 Wochen)**
- Achievements
- Cosmetics System
- Difficulty Settings
- Better SFX/Music Variance
- Gamepad Full Support

### **Phase: Full Release Candidate (TBD)**
- Mobile Port (Performance, Input)
- More Arenas
- Story/Lore Integration
- Online Coop (separate game mode?)

---

## 📊 Scope-Lock Matrix

| Aspect | WMA-MVP | WMA+ | Later |
|--------|---------|------|-------|
| **Monsters** | 6–8 types | 10+ types | Bosses, Faction Variants |
| **Weapons** | 2–3 types | 5+ types | Exotic, Legendary |
| **Arenas** | 1 (Scrapyard) | 1 (same) | 3+ Biomes |
| **AI Complexity** | Simple FSM | Same + tells | Tactics, Formations |
| **Upgrades** | Passive only | Passive + Active | Mod System |
| **Coop** | Local 2P | Local 2P | Online eventually |
| **Platforms** | PC Desktop | PC + Gamepad | Mobile, Console? |
| **Visuals** | Low-Poly URP | Same polish | AAA-ish art |

---

## 🚨 Risk Mitigations

| Risk | Impact | Mitigation |
|------|--------|-----------|
| Free Assets nicht stylistically consistent | High | Kitbashing + Decals, Asset Audit |
| Horde Performance (1000+ enemies) | High | LOD, Pooling, Frustum Culling, Simple AI |
| Coop Camera/Input handling complex | Medium | Prototype M1, TDD approach |
| Localization Bugs (String IDs) | Low | String Table Audit, Test in both languages |
| Extraction Point UX unclear | Low | Clear Visual Beacon, Tutorial Tooltip |

---

**Nächster Schritt:** 03_TechStack_Unity6_URP.md (Packages, Render Settings, Projekt-Setup)
