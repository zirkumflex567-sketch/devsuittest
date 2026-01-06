# 1️⃣ Vision: WMA (Working Minimal Alpha)

**Zielgruppe:** Indie Game Producer + Co-op Enthusiasts  
**Genre:** Horde-Arena (Survivors-like) + Vehicle Physics  
**Kern-Loop:** Drive + Shoot + Dodge + Loot + Upgrade → Repeat

---

## 🎮 Core Game Loop (Session)

```
1. [PRE-RUN] Charakter wählen + Fahrzeug wählen (4 Klassen, WMA: Motorrad/Jeep) + **2 aus 6 zufälligen Kopfgeldern**
2. [START] Fahrzeug aufgewärmt, 1 Arena, Gegner = 0
3. [MINUTE 0–30+] Horde spawnt in Wellen (Spawns überall in der Arena möglich)
   - Gegner rücken vor (Chase, Ranged, Melee variants)
   - Player steuert Fahrzeug + Charakter-Build (Drive + Primary Fire (Auto) + Secondary (Manual))
   - Gegner droppen Loot (Scrap, Tech, Health, Upgrades)
   - Horde skaliert: Wave Intensity ↑ über Zeit
4. [OPTIONAL] Alle 5 Min: Upgrade-Choice (Pick 3 aus 8) → Stats/Weapons/Mods verbessern
5. [MINUTE X (später 15 min)] Extraction Point spawnt
6. [END-BOSS] Endboss erscheint, hat ausweichbare Fähigkeiten (Telegraph + Dodge)
7. [WIN] Spieler erreicht Extraction Point → Loot in Run-Save gespeichert
   [LOSE] Fahrzeug HP → 0 → Game Over, Loot lost (nur Upgrades mitgenommen)
8. [HUB] Run-Summary, Scrap/Tech verdient, Unlocks prüfen
9. [NEXT RUN] Hub-Upgrades kaufen/aktivieren → neuer Run starten
```

---

## 🎯 Core Pillars (Must-Haves im WMA)

### **Pillar 1: Vehicle Combat**
- **Nicht:** Vehicle-vs-Vehicle
- **Ja:** Player-Vehicle vs. Horde-Monsters
- **Control:** Keyboard (WASD) + Mouse (Aim) → Gamepad later
- **Waffen:** Auto-Fire (Primary) + Manual Special (Secondary) mit Cooldown/Ammo
- **Mounts:** Alle Waffen sind fahrzeugmontiert (keine Handwaffen)
- **Feel:** Responsive, clear recoil feedback, audible/visual
- **Vehicle-Flavor:** Motorrad schnell, Quad agil, Jeep balanced (Coop), Truck schwer (alle balanciert)

### **Pillar 2: Charaktere & Skillbäume**
- **Ja:** 2 Driver-Personas mit klaren Eigenschaften
- **Je Charakter:** Skillbaum mit 3 Zweigen + Spezialfähigkeit (max. 2x pro Run)
- **Wahl:** Vor dem Run (Charakter + Vehicle)

### **Pillar 3: Horde-Skalierung**
- **Nicht:** Einzelne Boss-Kämpfe (später)
- **Ja:** 30–100 Gegner gleichzeitig (LOD/Pooling managed)
- **Skalierung:** 
  - Wave 1–10: Leichte Gegner, mittlere Spawn-Rate
  - Wave 10+: Mix aus Heavy/Ranged, Elites seltener
  - Alle 2–3 Minuten: kurze Ruhephase
- **Skalierung:** Hit-Points, Movement, Loot-Drop basierend auf Welle
- **Endlos:** Schwierigkeit kann unbegrenzt weiter steigen (Endless)

### **Pillar 4: Loot & Upgrade Loop**
- **Nicht:** Komplexes RPG-System
- **Ja:** Roguelike-lite: Jeder Run neue Upgrade-Choices
- **Ressourcen (2-Tier):**
  - Scrap (common drop) → Meta-Progression (persistent Hub)
  - Tech (rare drop) → Spezial-Upgrades
- **Run-Upgrades:** Nur diese Session, speichern bis Hub
- **Wahl-Mechanik:** Mid-run (alle 5 Min) oder nach Wellen

### **Pillar 5: Local Coop (WMA)**
- **2 Player:** Same Machine, Split-Screen ODER Shared View (TBD nach Prototyp)
- **Nicht:** Online, Matchmaking
- **Kurz-Term:** Eine Kamera, beide Spieler am Bildschirm
- **Skalierung:** Horde skaliert basierend auf Spielerzahl (2P → +30% Gegner)

### **Pillar 6: Low-Poly Stylized Feel**
- **Art:** Einheitlich, kartoonartig, keine Überdetaillierung
- **Readability:** Auch auf HD-Displays lesbar
- **Mobile-Ready:** Shader, Texturen, LODs designed für später Android/iOS

---

## 🧟 Monster Roster (Archetypen)

### **Tier 1: Early-Game (Wave 1–5)**

| Archetype | Visual | Behavior | Speed | HP | Damage | Loot |
|-----------|--------|----------|-------|----|---------|----|
| **Boar Grunt** | Wildschwein-humanoid, stämmig | Chase + Melee | Mittel | 20 | 5 | Scrap |
| **Hyena Runner** | Hyänen-humanoid, dürr | Chase (schnell) | Schnell | 10 | 3 | Scrap |
| **Raven Swooper** | Geier-humanoid, fliegend | Circle + Peck | Schnell | 15 | 4 | Scrap |

### **Tier 2: Mid-Game (Wave 5–15)**

| Archetype | Visual | Behavior | Speed | HP | Damage | Loot |
|-----------|--------|----------|-------|----|---------|----|
| **Boar Brute** | Wildschwein, größer | Charge + Melee | Langsam | 40 | 8 | Scrap x2 |
| **Hyena Pack** | 2–3 Hyänen linked | Coordinated Chase | Schnell | 25 (gesamt) | 6 | Scrap + Tech |
| **Venom Lurker** | Reptil-humanoid | Hide + Ranged Spit | Langsam | 30 | 7 | Scrap + Tech |

### **Tier 3: Late-Game (Wave 15+)**

| Archetype | Visual | Behavior | Speed | HP | Damage | Loot |
|-----------|--------|----------|-------|----|---------|----|
| **Boar Titan** | Elite Wildschwein | Charge Slam + AOE | Langsam | 80 | 12 | Tech x2 + Rare |
| **Plague Spreader** | Insekten-humanoid | Projectile Swarm | Mittel | 50 | 10 | Tech + Rare |
| **Apex Predator** | Großkatze-humanoid | Agile Slash + Dodge | Schnell | 60 | 11 | Tech + Rare |

### **Special: Goldgoblin** (seltener Gold-Spawn)
- **Visual:** Klein, glänzend, mit Münzen-Rucksack
- **Behavior:** Flieht immer von Player
- **HP:** 5 (sehr fragil)
- **Loot:** 3–5x normales Tech + Bonus Scrap
- **Spawn-Rate:** 1:300 Monster (sehr selten)

---

## 🎲 Resource Tiers

### **Scrap (Common)**
- **Drops:** ~70% aller Gegner
- **Menge:** 1–5 pro Drop, abhängig von Monster-Tier
- **Verwendung:** Meta-Hub (persistent zwischen Runs)
  - Weapon Unlocks
  - Vehicle Upgrades (durability, cargo)
  - Cosmetics

### **Tech (Rare)**
- **Drops:** ~20% aller Gegner, Elites/Gold bevorzugt
- **Menge:** 1–3 pro Drop
- **Verwendung:** Meta-Hub (persistent)
  - Special Ability Unlocks
  - Rare Cosmetics
  - Hub-Facility Upgrades

### **Run-Upgrades (Session-only)**
- **Drops:** Nach jeder Welle oder bei Milestone (5 Min)
- **Auswahl-Mechanic:** 3 aus 8 zufälligen Karten
- **Kategorien:**
  - Weapon Stats (Damage +10%, Fire Rate +15%, etc.)
  - Movement (Speed +5%, Dodge Range +20%)
  - Defense (Armor +10%, Heal +50HP)
  - Special Effects (Freezing Rounds, Explosive Blasts, Lifesteal)
- **Stacking:** Mehrfaches Upgrading derselben Eigenschaft möglich (Balancing später)

---

## 🎯 Kopfgeld-System (Pre-Run)

- **Vor dem Run:** 6 zufällige Kopfgelder aus einem Pool
- **Auswahl:** 2 aktivierbar (Stacking erlaubt)
- **Schwierigkeit:** Leicht / Mittel / Hart / Brutal
- **Belohnungen:** Scrap/Tech-Bonus, Run-Mods, seltene Upgrade-Chance
- **Beispiele:**
  - **"Kopfjäger"**: +25% Elite-Spawn, +15% Scrap
  - **"Giftregen"**: Mehr Ranged Gegner, +20% Tech
  - **"Gnadenlos"**: Gegner +15% HP, +1 Upgrade-Karte am Start

---

## 🏛️ Hub / Meta-Progression (Rudimentär im WMA)

### **Shop (Level 1–2 Einfachheit)**
```
Scrap Ausgaben:
- [Weapon] Upgrade Slot 1: 50 Scrap → +damage on next run
- [Defense] Upgrade Slot 2: 50 Scrap → +armor on next run
- [Cosmetic] Boar Paint: 25 Scrap → Vehicle Skin unlock

Tech Ausgaben (rarer):
- [Special] Cloaking Module: 20 Tech → Special Ability unlock
- [Cosmetic] Neon Decal: 10 Tech → Decal unlock
```

### **Workshop (Level 1–2)**
- Visuelle Representation: "Equipment auf Vehicle auslegen, anschauen"
- Nicht-Interaktiv im WMA (nur Display)
- Später: Crafting, Mod-Slots

### **Progress Tracking**
- Runs: Anzahl gesamt, Best Score (Time Survived)
- Unlocks: Weapon/Ability Progress
- Achievements (optional später): "Kill 1000 Enemies", "Survive 30 Min", etc.

---

## 📍 Single Arena (WMA MVP)

### **Environment: Wasteland/Scrapyard**
- **Theme:** Postapokalyptisch, industriell, sandiges Ödland
- **Size:** ~100m x 100m (tunable, später)
- **Features:**
  - Terrain variations (dunes, rocks, debris piles)
  - Statische Props (wrecked vehicles, rusted machinery, tires, containers)
  - Spawn Points: Dynamisch überall in der Arena (keine festen Kanten-Spawns)
  - Extraction Point: Spawnt nach X Min als glow/beacon (Mitte oder Rand-Position)
  - Safe Zone: Optinal — evtl. Center ist ruhiger (später)

### **Lighting & Mood**
- **Time-of-Day:** Static Sunset oder Neon-Industriel
- **Color Grading:** Desaturated Greens/Oranges, High Contrast (Lesbarkeit)
- **Fog:** Leicht (visibility ~80m), um Horde-Performance zu helfen

---

## 🎥 Camera & Input

### **Camera**
- **Mode:** Third-Person hinter Fahrzeug
- **Distance:** ~8–12m (tunable)
- **Height:** ~2–3m über Vehicle-Center
- **Follow:** Smooth follow with slight lag (Cinemachine Virtual Camera)
- **Coop-Mode:** TBD
  - Option A: Split-Screen (jeder Player eigene Hälfte)
  - Option B: Shared Camera (wide FOV, beide sichtbar)

### **Input**
- **Primary:** Keyboard (WASD) + Mouse (Aim + Fire)
- **Secondary:** Gamepad (XBOX layout, later)
- **Actions:**
  - **Move:** W/A/S/D (or Analog Stick)
  - **Aim:** Mouse Position (or Analog Stick Right)
  - **Primary Fire:** Left Click / LT
  - **Secondary Fire:** Right Click / RT
  - **Interact (future):** E / X

---

## 📊 WMA Scope (Must/Should/Could)

### **Must-Haves (WMA-MVP)**
- ✅ 1 Spieler oder 2-Player Coop (splitscreen oder shared)
- ✅ 2 Charaktere (Driver-Personas) + Skillbäume (3 Zweige)
- ✅ Fahrzeug-Select: 4 Klassen (Motorrad, Quad, Jeep, Truck)
- ✅ WMA: Motorrad (Solo) + Jeep (Coop)
- ✅ Vehicle Controller + Third-Person Camera
- ✅ 6–8 Monster-Types (Low-Poly Variants)
- ✅ 2–3 Waffen-Types (Auto, Special)
- ✅ Horde Spawner + Wave System (Skalierung)
- ✅ Loot Pickup + Upgrade UI
- ✅ Pre-Run: 2 aus 6 Kopfgeldern wählen
- ✅ Endboss mit ausweichbaren Fähigkeiten (3 Varianten)
- ✅ Save/Meta (Scrap/Tech persistent)
- ✅ UI: HUD (Health, Ammo, Score), Pause Screen, Game Over, Hub
- ✅ Localization: DE + EN
- ✅ SFX + Musik (du selbst)

### **Should-Haves (WMA+ / Post-MVP)**
- 🟡 10+ Monster-Types
- 🟡 5+ Waffen-Types
- 🟡 Elite-Monster (unique telegraphed attacks)
- 🟡 Status Effects (Freeze, Burn, Poison) visual/mechanical
- 🟡 Achievements/Leaderboard (Local)
- 🟡 Better Hub UI (Cosmetic preview, crafting teaser)
- 🟡 Gamepad Support (vollständig)

### **Could-Haves (Late oder nie)**
- 🔵 3+ Arenen/Biomes
- 🔵 Online Coop (später, großer Scope)
- 🔵 Battle Pass / Seasonal Content
- 🔵 Boss Encounters
- 🔵 Story Mode / Campaign

---

## ⚡ Key Design Goals

1. **Fun Loop:** Drive, Shoot, Pick Up, Repeat (schnell & satisfying)
2. **Readable:** Auch bei 100 Gegnern → klare Silhouetten, HUD contrast
3. **Progressive:** Difficulty ramps smooth, kein sudden spikes
4. **Replayable:** Jeden Run anders durch Upgrade-Randomness
5. **Coop-Friendly:** Beide Player sehen Action, gleiche Priorität

---

## 🚨 Constraints

- **Single Arena:** Keine Biome-Wechsel im MVP
- **Singleplayer→Coop:** Code muss von Anfang an Coop-aware sein
- **Free Assets:** Konsistenz durch Kitbashing + Decals, nicht perfekt
- **No Complex AI:** State Machine reicht, keine Fancy Pathfinding (später)
- **Performance:** Target 60 FPS PC (1440p), Later Mobile 30 FPS

---

**Nächster Schritt:** 02_MVP_Scope.md (detaillierte Must/Should/Could + Out-of-Scope)
