# 🎮 Horde Arena MVP — Komplette Produktion & Tech Stack

**Projekt:** Indie Horde-Arena Spiel (Brotato/Vampire Survivors in 3D)  
**Engine:** Unity 6 + URP (Universal Render Pipeline)  
**Zielplattform:** PC (Local Coop 2P), später Android/iOS  
**Scope:** Working Minimal Alpha (WMA) → Playable in 4–8 Wochen  
**Lizenz:** Dokumentation CC0. Assets siehe Docs/13_Licenses_Attribution.md

---

## 📚 Dokumente — Lese-Reihenfolge

Für **schnellen Überblick:**
1. Diesen README
2. → **01_Vision_WMA.md** (Game Loop, Pillars)
3. → **02_MVP_Scope.md** (Must/Should/Could)
4. → **03_TechStack_Unity6_URP.md** (Setup)

Für **tiefe Planung:**
5. **04_Architecture_Modular.md** (Systems, Patterns)
6. **05_DataModel_ScriptableObjects.md** (Datenstruktur)
7. **06_Enemies_HordeDesign.md** (Monster Roster)
8. **07_HordeDirector_Waves.md** (Schwierigkeit, Spawning)
9. **08_Weapons_StatusEffects.md** (Combat Loop)
10. **09_UI_UX.md** (HUD, Screens, Localization)
11. **10_Save_Meta.md** (Progression, Run Data)
12. **18_Characters_WMA.md** (Charaktere, Skillbäume, Prompts)
13. **19_Comparison_Tables.md** (Database-Tabellen)

Für **Asset & Production:**
14. **12_AssetStack_FreeFirst.md** (Mit Tabellen + Links)
15. **13_Licenses_Attribution.md** (Ledger für alle Assets)
16. **14_KI_ReplacementPlan.md** (KI-Prompts, QA-Checklists)

Für **Execution:**
17. **15_Milestones_Checklists.md** (Alle Tasks)
18. **16_Cursor_Codex_Runbooks.md** (Pro Milestone: Prompts & Steps)

---

## 🎯 Kern-Annahmen (Transparent)

✅ **Gameplay**
- Single-Player + **Local Coop (2P, Split-Screen oder Shared View)** im MVP
- Character-Select (2 Driver-Personas) + Vehicle-Select
- Fahrzeuge: **Motorrad, Quad, Jeep, Truck** (balanciert)
- WMA-Restriktion: **Motorrad (Solo)** und **Jeep (Coop)**
- Vor dem Run: **2 von 6 zufälligen Kopfgeldern wählen** (Schwierigkeit + Belohnung)
- Third-Person Fahrzeug-Perspektive mit Reticle/Aiming
- Auto-Fire Primär-Waffe + manuelle Special-Waffe
- 1 Arena + Horde-Spawner (Wellen-Skalierung)
- Extraction Mechanic nach X Minuten
- Loot-Drops, Upgrades (roguelike-lite)
- Endboss mit ausweichbaren Fähigkeiten (3 Varianten)

✅ **Art Direction**
- Low-Poly / Stylized / Mobile-freundlich
- URP-basiert, optional Toon-Shader (free)
- Monster-Theme: **Humanoide Mutationen** (Wildschweine, Hyänen, Geier etc.)
- Charaktere im **Borderlands/Cel-Shaded** Look (siehe Docs/18)

✅ **Audio**
- Musik: Du selbst
- SFX: Free-Pools (Freesound.org, Zapsplat) oder KI-generiert
- VO: Optional später (KI-TTS Deutsch bevorzugt)

✅ **Localization**
- DE + EN im MVP (UI Text, einfache Dialoge, Lore)
- String Tables (Unity Localization Package)
- Glossar in Docs/11_Localization_DE_EN.md

✅ **Tech Stack**
- **Free Frameworks:** Zenject (DI), UniTask, Input System, Localization
- **Optional:** Cinemachine (Kamera), Odin Inspector (Dev-friendly, aber nicht required)

---

## 📊 Machbarkeit (WMA-MVP, 4–8 Wochen)

| Bereich | Free Assets | Aufwand | Risiko | Status |
|---------|-------------|---------|--------|--------|
| **3D Art: Vehicle** | ⚠️ Teilweise | Med | Med (Style-Match) | ⚠️ |
| **3D Art: Monsters** | ✅ Ja | High | Med (Varianten) | ⚠️ |
| **3D Art: Arena** | ✅ Ja | Med | Low | ✅ |
| **VFX** | ✅ Ja | Med | Low | ✅ |
| **UI/HUD/Icons** | ✅ Ja | Low | Low | ✅ |
| **Audio SFX** | ✅ Ja | Low | Low | ✅ |
| **Code: Vehicle Controller** | ✅ Ja (free asset) | Low | Low | ✅ |
| **Code: Horde Director** | ⚠️ Minimal | Med | Low | ⚠️ |
| **Code: Enemy AI** | ⚠️ Minimal | Med | Low | ⚠️ |
| **Localization (DE/EN)** | ✅ Ja | Low | Low | ✅ |
| **Save/Progression** | ⚠️ Minimal | Low | Low | ✅ |

**Größte Risiken:**
1. **Monster-Style-Konsistenz** → Lösung: Asset Kitbashing + Decals (nicht perfekt OK)
2. **Horde-Performance** (1000+ Enemies) → Lösung: LOD + Pooling + simple AI state machine
3. **Vehicle-Style-Match** → Lösung: Kitbash oder KI-Generierung für schnellen Replacement

**Geschätzte Aufwand (Personentage):**
- Design & Planning: 2–3 Tage (DONE nach dieser Doku)
- Tech Setup (URP, Zenject, Scenes): 1–2 Tage
- Vehicle Controller + Camera: 1 Tag
- Enemy AI + Horde Director: 3–5 Tage
- Weapon/Combat System: 2–3 Tage
- UI/HUD/Screens: 2 Tage
- Save/Meta: 1 Tag
- Localization: 1 Tag
- Testing/Polish: 2–3 Tage
- **TOTAL: 15–22 Personentage (~4–5 Wochen @ 4 Std/Tag)**

---

## 🛠 Datenstruktur (Maschinenlesbar)

| Datei | Typ | Zweck |
|-------|-----|--------|
| `_data/assets.csv` / `.json` | Matrix | Asset-Registry mit Lizenz, Link, Kompatibilität |
| `_data/milestones.json` | Struktur | Alle Milestones + Task-IDs + Abhängigkeiten |
| `_data/prompts_library.json` | Struktur | KI-Prompts für Asset-Generierung + QA |
| `_data/enemies.json` | Data | Enemy Roster (Archetypen, Stats, Loot) |
| `_data/weapons.json` | Data | Weapon Configs |
| `_data/status_effects.json` | Data | Status Effects + Upgrades |
| `_data/waves.json` | Data | Wellen-Definitionen + Difficulty Curve |

---

## 🎨 DevSuite (Lokale Web-App)

**Technologie:** Vite + Vue 3 (oder Astro)  
**Features:**
- Markdown Viewer (alle Docs)
- Interactive Task Tracker (Checkboxes + Notizen)
- Prompt Library (mit Variable Substitution + Copy-to-Clipboard)
- Asset-Browser (mit Filter nach Lizenz, Status, Kompatibilität)
- Progress Export/Import (JSON)

**Siehe:** Docs/16_DevSuite_Spezifikation.md (separate Datei, nicht in diesem README)

---

## 🚀 Schnellstart (Producer-Checkliste)

Vor dem Coding:

- [ ] **Datei 01_Vision_WMA.md** vollständig durchlesen
- [ ] **Datei 02_MVP_Scope.md** reviewen (Must/Should/Could abgleichen)
- [ ] **Datei 03_TechStack_Unity6_URP.md** → Packages installieren + Render Settings
- [ ] **Datei 04_Architecture_Modular.md** → Projektstruktur anlegen
- [ ] **Datei 12_AssetStack_FreeFirst.md** → Assets manuell downloadable oder per Package Manager importieren
- [ ] **Datei 15_Milestones_Checklists.md** → in GitHub Issues / Linear / Jira importieren
- [ ] **Datei 16_Cursor_Codex_Runbooks.md** → 1. Milestone Prompts kopieren

---

## 📞 Support & Links

**Free-Asset-Quellen:**
- Sketchfab (Filter: Commercial Use, CC0/CC-BY) → sketchfab.com
- OpenGameArt.org → opengameart.org
- Freesound.org (Audio) → freesound.org
- Zapsplat (Audio, SFX) → zapsplat.com
- Quaternius (Low-Poly) → quaternius.com

**Unity Resources:**
- URP Shader Examples: github.com/Unity-Technologies/Graphics
- Zenject Docs: zenject-documentation.readthedocs.io
- UniTask Docs: github.com/Cysharp/UniTask

**KI-Asset-Generierung (später):**
- Siehe Docs/14_KI_ReplacementPlan.md (mit Prompts + QA)

---

## 📝 Lizenz & Attribution

Diese Dokumentation selbst: **CC0** (Public Domain).  
Alle Assets: Siehe **Docs/13_Licenses_Attribution.md** (vollständiger Attribution Ledger).

---

**Nächster Schritt:** Öffne **Docs/01_Vision_WMA.md** und beginne mit der Lektüre.

---

*Last Updated: 2025-01-05*  
*Next Review: Nach MVP-Milestone*
