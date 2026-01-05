# 🎨 12. MVP Asset Stack: Free-First Strategy

**Prinzip:** Maximale Qualität mit Free/CC0-Assets, später austauschbar ohne Rework.

---

## 📋 Asset-Matrix: Kategorie × Quelle × Lizenz

### **VEHICLES (Player Vehicle)**

| Name | Source | Link | License | Commercial | Modifiable | Constraint | Status | Notes |
|------|--------|------|---------|------------|------------|-----------|--------|-------|
| **Stylized Hovercraft** | Quaternius | quaternius.com/index.html | CC0 | ✅ | ✅ | Keine | ✅ BEST | Low-poly, perfekt für WMA |
| **Sci-Fi Buggy** | Sketchfab (jclaesart) | sketchfab.com/3d-models/... | CC-BY-4.0 | ✅ | ✅ | Attribution | ✅ ALT | Etwas detailliert, aber kitbash-bar |
| **Lowpoly Vehicle** | Turbosquid Free | turbosquid.com/Search/... | Free Commercial | ✅ | ✅ | Keine | ⚠️ OK | Quality gut |
| **Free Car Model** | CGTrader Free | cgtrader.com/free-3d-models | Free Commercial | ✅ | ✅ | Keine | ⚠️ OK | Variable Qualität |

**Empfehlung für WMA:** **Quaternius Hovercraft** (CC0) oder **Sci-Fi Buggy** (CC-BY + Attribution).

---

### **MONSTERS (Horde Enemies)**

| Name | Source | License | Commercial | Modifiable | Notes | Integration |
|------|--------|---------|------------|------------|-------|-------------|
| **Stylized Animals Pack** | Quaternius | CC0 | ✅ | ✅ | 20+ low-poly animals (Boar, Hyena, Raven, Feline) | ⭐ BEST |
| **Low-Poly Creatures** | OpenGameArt.org | CC0/CC-BY | ✅ | ✅ | Mixed quality, some perfect | ✅ Good |
| **Fantasy Character Pack** | Kenney.nl | CC0 | ✅ | ✅ | Monsters, humanoids | ✅ Good |
| **Rigged Animal Models** | Sketchfab (Mixed) | CC-BY (most) | ✅ | ⚠️ Rigging-dependent | Need rigging work | ⚠️ Medium |
| **Free Monster Assets** | Unity Asset Store (Free) | EULA | ✅ | ✅ | Quality varies | ⚠️ Variable |

**Strategy:**
1. **Primary:** Quaternius Animals (CC0, kitbash to humanoid form)
2. **Secondary:** OpenGameArt.org Community (CC0 alternatives)
3. **Fallback:** Sketchfab (pre-rigged, wenn nötig Attribution)

**Kitbash Approach:**
- Wildschwein-Humanoid: Boar body + human arms + robe/armor
- Hyäne: Hyena base + upright stance modifier + clothes
- Geier: Bird wings + reptilian body + humanoid torso

---

### **ENVIRONMENT (Arena & Props)**

| Name | Source | License | Commercial | Notes | Status |
|------|--------|---------|------------|-------|--------|
| **Stylized Scrapyard Props** | Quaternius | CC0 | ✅ | Rusted vehicles, tires, containers | ⭐ BEST |
| **Low-Poly Nature Assets** | Kenney.nl | CC0 | ✅ | Rocks, dunes, grass | ✅ Good |
| **Free Industrial Kit** | Sketchfab | CC-BY/CC0 | ✅ | Machinery, cables | ✅ Good |
| **Poly Haven** | Poly Haven | CC0 | ✅ | Textures + models | ✅ Excellent |
| **Free Terrain Assets** | Unity Asset Store Free | EULA | ✅ | Terrain, foliage | ✅ Good |

**Für WMA Arena:**
- Terrain: Dunes, rocks, sand (Kenney or Poly Haven)
- Props: Rusted vehicles, scrap metal (Quaternius Scrapyard Pack)
- Decals: Hazard stripes, rust, oil stains (Textures from Poly Haven or custom)

---

### **VFX (Particles, Effects)**

| Name | Source | License | Commercial | Notes | Status |
|------|--------|---------|------------|-------|--------|
| **Stylized VFX Pack** | Quaternius | CC0 | ✅ | Explosions, impacts, etc. | ✅ Good |
| **Free Particle FX** | OpenGameArt.org | CC0 | ✅ | Various effects | ✅ Good |
| **URP VFX Samples** | Unity GitHub | Unity EULA | ✅ | Official URP examples | ✅ Reference |
| **VFX Graph Examples** | Unity Learn | Free | ✅ | Tutorials, templates | ✅ Learning |

**Für WMA-MVP:**
- Muzzle Flashes: Simple orange/yellow sparks (Quaternius or custom)
- Hit Effects: Impact particles, dust clouds
- Explosions: Optional (simple radial expansion)
- Status Effects: Color overlays (Freeze = Blue tint, Burn = Orange)

---

### **UI / HUD / ICONS**

| Name | Source | License | Commercial | Notes | Status |
|------|--------|---------|------------|-------|--------|
| **Kenney UI Pack** | Kenney.nl | CC0 | ✅ | Buttons, icons, bars, 900+ assets | ⭐ BEST |
| **Game Icons Pack** | Game Icons (Delapouite) | CC-BY-3.0 | ✅ | 5000+ icons, high quality | ✅ Excellent |
| **OpenGameArt UI** | OpenGameArt.org | CC0/CC-BY | ✅ | Variable quality | ✅ Good |
| **Material Design Icons** | Material Design | Apache 2.0 | ✅ | Generic, anpassbar | ⚠️ Generic |
| **Free Font: Inter** | Rasmus Andersson | OFL | ✅ | Modern sans-serif | ✅ Excellent |
| **Free Font: Roboto** | Google Fonts | Apache 2.0 | ✅ | Versatile, readable | ✅ Good |

**Für WMA:**
- HUD: Health Bar (Kenney), Ammo Counter (custom text)
- Icons: Weapon Icons (Kenney), Enemy Icons (custom or Game Icons)
- Buttons: Pause, Resume, Quit (Kenney UI)
- Font: Roboto or Inter (Google Fonts, kostenlos)

---

### **AUDIO / SFX**

| Name | Source | License | Commercial | Notes | Status |
|------|--------|---------|------------|-------|--------|
| **Freesound.org** | CC0 / CC-BY | CC-Variants | ✅ (mit Attribution) | 300k+ sounds | ✅ BEST |
| **Zapsplat** | Zapsplat | Free Commercial | ✅ | SFX collections | ✅ BEST |
| **OpenGameArt Audio** | OpenGameArt.org | CC0 / CC-BY | ✅ | Game-specific sounds | ✅ Good |
| **Freepik SFX** | Freepik | Free Commercial | ✅ | Pack downloads | ⚠️ Variable |
| **Sonniss.com** | Sonniss | CC0 | ✅ | Game SFX, well-organized | ✅ Excellent |

**Für WMA-MVP:**
- **Weapon Fire:** Plasma shot, laser, bullet (Zapsplat oder Freesound)
- **Hit/Impact:** Metal clang, flesh hit, explosion (Freesound)
- **Enemy Death:** Creature death sounds (Freesound)
- **Loot Pickup:** Coin/chime sounds (Freesound)
- **UI Clicks:** Soft beeps (Freesound)
- **Ambient:** Wind, machinery hum (Zapsplat)

**Attribution Strategy:** String Tables mit Credit-Liste in Settings.

---

### **CODE / FRAMEWORKS (Free, Open-Source)**

| Name | Source | License | Purpose | Status |
|------|--------|---------|---------|--------|
| **Zenject** | GitHub (ExtensingContent) | MIT | Dependency Injection | ✅ Setup |
| **UniTask** | GitHub (Cysharp) | MIT | Async/await tasks | ✅ Optional |
| **VContainer** | GitHub (hadashiA) | MIT | Lightweight DI | ✅ Alternative |
| **Input System** | Unity Package Manager | Unity EULA | Input handling | ✅ Installed |
| **Localization** | Unity Package Manager | Unity EULA | DE/EN text | ✅ Installed |
| **Cinemachine** | Unity Package Manager | Unity EULA | Camera control | ⚠️ Optional |

**Standard für WMA:** Input System + Localization (built-in), Zenject für DI.

---

### **MISCELLANEOUS**

| Name | Source | License | Commercial | Notes | Status |
|------|--------|---------|------------|-------|--------|
| **Free Color Grading LUT** | Various (Poly Haven) | CC0 | ✅ | Post-processing | ✅ Optional |
| **Free SkyBox** | Poly Haven / Unity Asset Store | CC0 / Free | ✅ | Environment | ✅ Good |
| **Toon Shader (Free)** | GitHub (jwu02) | MIT | ✅ | Optional style | ⚠️ Optional |

---

## 🔄 Integration Roadmap (Pro Asset-Typ)

### **VEHICLES: Quick Integration**
```
✅ Download Quaternius Hovercraft
✅ Import FBX in Assets/Models/Vehicle/
✅ Create Material (URP Lit) + assign
✅ Add Collider (BoxCollider für simplicity)
✅ Create Prefab
⏱️ Time: ~30 min
```

### **MONSTERS: Kitbash + Variant Creation**
```
✅ Download Quaternius Animals Pack
✅ Extract boar.fbx, hyena.fbx, etc.
✅ For each: Create humanoid stance (blender 5 min / skip)
✅ Import in Assets/Models/Enemies/
✅ Create Materials per type (Color variants)
✅ Add Colliders (simplified)
✅ Create Prefabs with LOD0/LOD1
✅ Duplicate + recolor für Varianten (Brute = größer, Titan = 1.5x size)
⏱️ Time: ~2–3 hours (inkl. Variant Recoloring)
```

### **ENVIRONMENT: Modular Kitbash**
```
✅ Download Kenney + Quaternius Props
✅ Organize in Assets/Models/Arena/Props/
✅ Create 10–15 unique placements (randomized)
✅ Decal Layer für Rust, Hazard Stripes
✅ LOD für performance (Props LOD2 at 50m)
⏱️ Time: ~2 hours
```

### **UI: Drop-in Templates**
```
✅ Use Kenney UI Pack sprites directly
✅ Create Canvas + HUD prefab
✅ TextMeshPro für text (Font: Roboto)
✅ Buttons prefab (with Kenney sprite bg)
⏱️ Time: ~1 hour
```

### **AUDIO: Collection & Attribution**
```
✅ Download SFX packs (Zapsplat, Freesound)
✅ Organize in Assets/Audio/SFX/
✅ Create audio clusters (Weapons, Enemies, UI)
✅ Attribution text in Credits
⏱️ Time: ~1.5 hours
```

---

## ⚠️ Common Issues & Workarounds

### **Issue 1: Style Inconsistency**
**Problem:** Free assets have different poly counts, texture densities, art styles.  
**Workaround:**
- Standardize shader (URP Lit)
- Unify normal maps (all generated or all hand-painted)
- Decals hide seams (rust, graffiti, numbers)
- LOD aggressively (far away = super simple)

### **Issue 2: Rigging Problems**
**Problem:** Pre-rigged humanoids may have bad bones.  
**Workaround:**
- Use Quaternius (no rigging needed, low-poly)
- Or commission quick rig fix (cheap, 1–2 hours)
- Or use kinematic movement (no animation, just IK legs)

### **Issue 3: Scale Mismatches**
**Problem:** Assets from different sources have wildly different scales.  
**Workaround:**
- Standard: 1 Unity unit = 1 meter
- Audit all imports: scale on import if needed
- Document scale in Asset Registry

### **Issue 4: License Attribution**
**Problem:** Tracking all licenses, avoiding ND (non-derivative) licenses.  
**Workaround:**
- Spreadsheet (see Docs/13_Licenses_Attribution.md)
- Automated credit screen in game
- Include LICENSE.txt in release

---

## 🎯 Download Checklist (WMA-MVP, Phase 1)

Vor Codex-Implementierung:

- [ ] **Quaternius Hovercraft** → Assets/Models/Vehicle/
- [ ] **Quaternius Animals Pack** → Assets/Models/Enemies/
- [ ] **Quaternius Scrapyard Props** → Assets/Models/Arena/Props/
- [ ] **Kenney.nl UI Pack** → Assets/Sprites/UI/
- [ ] **Kenney.nl Game Icons** → Assets/Sprites/Icons/
- [ ] **Freesound SFX Collections** → Assets/Audio/SFX/
- [ ] **Zapsplat Weapon Sounds** → Assets/Audio/SFX/Weapons/
- [ ] **Roboto Font** → Assets/Fonts/ (von Google Fonts)
- [ ] **Poly Haven Textures** (optional, für Decals) → Assets/Textures/Decals/

**Total Download Time:** ~2–3 Stunden (abhängig von Bandwidth).

---

**Nächster Schritt:** 13_Licenses_Attribution.md (vollständiges Ledger)
