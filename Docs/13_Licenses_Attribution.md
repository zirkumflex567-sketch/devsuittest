# 📜 13. Licenses & Attribution Ledger

**Prinzip:** Lückenlose Attribution für alle verwendeten Assets. Compliance mit CC0, CC-BY, MIT, Apache 2.0, Unity EULA.

---

## ✅ Asset Attribution (Vollständig)

### **3D MODELS**

| Asset | Source | License | Author | Link | Commercial | Modifications | Required Attribution |
|-------|--------|---------|--------|------|------------|---------------|-----------------------|
| Quaternius Hovercraft | Quaternius | CC0 | Quaternius | quaternius.com | ✅ | ✅ | Optional |
| Quaternius Animals Pack | Quaternius | CC0 | Quaternius | quaternius.com | ✅ | ✅ | Optional |
| Quaternius Scrapyard Props | Quaternius | CC0 | Quaternius | quaternius.com | ✅ | ✅ | Optional |
| Sci-Fi Buggy | Sketchfab (jclaesart) | CC-BY-4.0 | jclaesart | sketchfab.com/... | ✅ | ✅ | **REQUIRED** |
| Kenney.nl UI Pack | Kenney.nl | CC0 | Kenney | kenney.nl | ✅ | ✅ | Optional |
| OpenGameArt Animals | OpenGameArt.org | CC0 | Various | opengameart.org | ✅ | ✅ | Optional |

---

### **AUDIO**

| Asset | Source | License | Author | Link | Commercial | Attribution |
|-------|--------|---------|--------|------|------------|------------|
| Zapsplat SFX Collection | Zapsplat | Free Commercial | Zapsplat | zapsplat.com | ✅ | Optional |
| Freesound Weapon Sounds | Freesound.org | CC0 + CC-BY | Various | freesound.org | ✅ (CC0 ja, CC-BY attribution) | Depends |
| Freesound.org (spezifisch) | Freesound | CC-BY-3.0 | [Attribution per Sound] | freesound.org | ✅ | **REQUIRED in-game** |
| Generic UI Beep | Freesound | CC0 | [Author] | freesound.org | ✅ | Optional |

---

### **FONTS**

| Asset | Source | License | Author | Link | Commercial |
|-------|--------|---------|--------|------|------------|
| Roboto | Google Fonts | Apache 2.0 | Christian Robertson | fonts.google.com | ✅ |
| Inter | Rasmus Andersson | OFL 1.1 | Rasmus Andersson | rsms.me/inter | ✅ |

---

### **CODE & FRAMEWORKS**

| Asset | Source | License | Author | Link | Commercial |
|-------|--------|---------|--------|------|------------|
| Zenject | GitHub | MIT | ModestTree, Kremer et al. | github.com/modesttree/Zenject | ✅ |
| UniTask | GitHub | MIT | Cysharp | github.com/Cysharp/UniTask | ✅ |
| Input System | Unity | Unity EULA | Unity Technologies | package.unity | ✅ |
| Localization | Unity | Unity EULA | Unity Technologies | package.unity | ✅ |
| Cinemachine | Unity | Unity EULA | Unity Technologies | package.unity | ✅ |

---

## 📝 In-Game Credits Screen

**Anzeige im Spielmenü (Settings > Credits):**

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
GAME CREDITS & ATTRIBUTION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

ART ASSETS
─────────
• Quaternius (CC0)
  - Hovercraft Vehicle
  - Animals Pack
  - Scrapyard Props
  - UI Pack

• Kenney.nl (CC0)
  - Game Icons
  - UI Elements

• Sketchfab Artists (CC-BY)
  - [Attribution per asset]

AUDIO
─────
• Zapsplat (Free Commercial)
  - Sound Effects Collection

• Freesound.org (CC-BY/CC0)
  - Community Audio Library
  - [See individual sound credits]

FONTS
─────
• Google Fonts
  - Roboto (Apache 2.0)
  - Inter (OFL)

CODE
─────
• Zenject (MIT) – Dependency Injection
• UniTask (MIT) – Async Framework
• Unity Technologies
  - Input System, Localization, Cinemachine

SPECIAL THANKS
───────────────
• Unity Community
• OpenGameArt.org Contributors
• All Free Asset Creators

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## 🚫 Licenses zu VERMEIDEN (ND = No Derivatives)

**DO NOT USE:**
- ❌ Creative Commons ND (Non-Derivative) Lizensen
- ❌ Proprietary Assets ohne Commercial Use Permission
- ❌ GPL-licensed content (zu restriktiv für Kommerz)
- ❌ Assets mit "Personal Use Only"

**WARUM:** Wir modifizieren Assets (Kitbashing, Recoloring, etc.). ND-Lizensen verbieten das.

---

## ✅ Safe Licenses (Commercial Use + Modification allowed)

- ✅ **CC0** (Public Domain, kein Attribution nötig, aber empfohlen)
- ✅ **CC-BY** (Attribution required, free to modify)
- ✅ **CC-BY-SA** (Attribution required, modified works must share same license)
- ✅ **MIT** (Code only, very permissive)
- ✅ **Apache 2.0** (Code only, very permissive)
- ✅ **OFL** (Fonts only, very permissive)
- ✅ **Unity EULA** (For Unity Editor Packages)

---

## 📋 License Audit Checklist (Pre-Release)

Vor Release müssen ALLE Assets durchcheckt sein:

- [ ] Alle 3D Models: Quelle + Lizenz dokumentiert
- [ ] Alle SFX: Quelle + Lizenz dokumentiert
- [ ] Alle Texturen/Sprites: Quelle + Lizenz dokumentiert
- [ ] Alle Fonts: Quelle + Lizenz dokumentiert
- [ ] Alle Code Libraries: Lizenz in package.json oder LICENSE file
- [ ] Credits Screen: vollständig, readable in-game
- [ ] LICENSE.txt: im Repo root, listet alles auf
- [ ] README.md: Erwähnt Attribution Requirements
- [ ] Keine ND-Lizenzen vorhanden
- [ ] Keine GPL-Assets vorhanden
- [ ] Keine "Personal Use Only" Assets

---

## 📄 Sample LICENSE.txt (Repo Root)

```
HORDE ARENA WMA-MVP
License & Attribution File
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

This game uses the following third-party assets under open licenses:

ART & MODELS (CC0 - No Attribution Required)
─────────────────────────────────────────────
• Quaternius (CC0)
  - Stylized Hovercraft
  - Animals Pack (Boar, Hyena, Raven, etc.)
  - Scrapyard Props (Vehicles, Machinery, etc.)
  - UI Pack (Buttons, Icons, etc.)
  Source: https://quaternius.com

ART & MODELS (CC-BY - Attribution Required)
──────────────────────────────────────────
• jclaesart - Sci-Fi Buggy (CC-BY-4.0)
  Attribution: See in-game Credits screen
  Source: https://sketchfab.com/...

AUDIO (Free Commercial)
───────────────────────
• Zapsplat (Free Commercial)
  Source: https://zapsplat.com
  
• Freesound.org (CC-BY & CC0 Mixed)
  Individual tracks attributed in-game
  Source: https://freesound.org

FONTS (Open Licenses)
─────────────────────
• Roboto Font (Apache 2.0)
  Author: Christian Robertson
  Source: https://fonts.google.com
  
• Inter Font (OFL 1.1)
  Author: Rasmus Andersson
  Source: https://rsms.me/inter

FRAMEWORKS & LIBRARIES (MIT/Apache/EULA)
──────────────────────────────────────────
• Zenject (MIT) - Dependency Injection
• UniTask (MIT) - Async Framework
• Unity Input System (Unity EULA)
• Unity Localization (Unity EULA)
• Cinemachine (Unity EULA)

For full details, see the in-game Credits screen.

Complied with Creative Commons, MIT, Apache 2.0, OFL, and Unity EULA.
```

---

## 🔄 Attribution Workflow (für Developers)

**Jedes Mal, wenn du ein neues Asset hinzufügst:**

1. **Download & Import:** Asset in appropriate folder (`Assets/Models/`, etc.)
2. **License Check:** 
   - Notiere Lizenz (CC0, CC-BY, MIT, etc.)
   - KEIN ND-Lizensen!
   - Commercial Use erlaubt?
3. **Add to Registry:** Update `Docs/_data/assets.json` oder spreadsheet
4. **Update Credits:** In-game Credits Screen + LICENSE.txt
5. **Commit:** Git commit mit Attribution info

**Template Commit Message:**
```
Added [AssetName] from [Source] ([License])
Attribution: [Author] if required
```

---

**Nächster Schritt:** 14_KI_ReplacementPlan.md (Prompts für KI-generierte Assets)
