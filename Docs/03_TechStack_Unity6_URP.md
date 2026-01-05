# 3️⃣ Tech Stack: Unity 6, URP, Free Frameworks

**Engine Version:** Unity 6 LTS (2022.3.x or 2023.2+)  
**Render Pipeline:** URP (Universal Render Pipeline)  
**Target Platform (MVP):** Windows PC (1440p / 60 FPS)  
**Later:** Android/iOS (30 FPS)

---

## 🛠 Essential Packages

### **Core (Free, via Package Manager)**

| Package | Version | Purpose | Status |
|---------|---------|---------|--------|
| **URP** | 14.0+ | Rendering Pipeline | ✅ Built-in |
| **Input System** | 1.6+ | Keyboard/Gamepad Input | ✅ Install via PM |
| **Localization** | 1.4+ | DE/EN Text Management | ✅ Install via PM |
| **Cinemachine** | 3.0+ | Camera Control (optional) | ⚠️ Optional |
| **TextMesh Pro** | Latest | UI Text Rendering | ✅ Built-in |
| **Physics 2D/3D** | Built-in | Collision, Rigidbody | ✅ Built-in |

### **Free Open-Source (via GitHub / NuGet)**

| Package | Link | Purpose | License |
|---------|------|---------|---------|
| **Zenject** | github.com/modesttree/Zenject | Dependency Injection | MIT |
| **UniTask** | github.com/Cysharp/UniTask | Async/Await Tasks | MIT |
| **VContainer** | github.com/hadashiA/VContainer | Alternative DI (leaner) | MIT |

**Empfehlung:** Zenject für klare Architektur, aber VContainer ist auch OK (leichter).

### **Optional (Nice-to-Have, kostenlos)**

| Package | Purpose | License |
|---------|---------|---------|
| **Odin Inspector** | (Paid, aber Serialization helpers) | — |
| **DOTween** | Animation/Tweening | Kostenlos (mit Limitations) |
| **NaughtyAttributes** | Editor Helpers | MIT |
| **Newtonsoft.Json** | JSON Parsing (falls needed) | MIT |

---

## 🎨 Rendering Setup (URP)

### **Project Settings → URP Asset**

```
Create → Rendering → URP Asset

Settings:
- Rendering Path: Forward (default, good for mobile)
- Anti-aliasing: FXAA (Fast, low perf cost)
- Color Space: Linear (better look, slightly higher perf)
- Post-Processing: ON (Tone Mapping, Color Grading)
```

### **Shader Settings**

```
Project Settings → Quality → (for each quality level)

- Texture Quality: Medium (later reduce for mobile)
- Shadow Distance: 50m (reduce for mobile)
- LOD Bias: 1.0
- Use Dynamic Batching: ON
- Use GPU Instancing: ON (for materials)
```

### **Material Standard: URP Lit**

Alle 3D Assets nutzen **Shader: Universal Render Pipeline/Lit**

```
Base Map: Diffuse Texture
Normal Map: (if available)
Metallic: 0.0 (für stylized, meist matte)
Smoothness: 0.5 (medium rough)
Surface Type: Opaque (default)

Optional für special FX:
- Emission: für Neon, Glow
- Alpha Clipping: für Decals, Transparencies
```

### **Optional: Toon/Cell Shader (Free)**

Falls du "Toon"-Look möchtest:
- **VHS Shader** (GitHub, free, URP-compatible)
- Oder selbst einfache Toon-Shader via Shader Graph (URP)
- Alternative: Unity Shader Graph + Custom Shader

**Status für WMA-MVP:** Optional. Keep it simple, URP Lit reicht.

---

## 📦 Projektstruktur (Assembly Definitions)

Erstelle folgende Ordner-Struktur (mit `.asmdef` files):

```
Assets/
├── Scripts/
│   ├── Core/                         → Core.asmdef
│   │   ├── Bootstrap/
│   │   ├── SceneManager/
│   │   └── SaveSystem/
│   ├── Systems/                      → Systems.asmdef (depends on Core)
│   │   ├── Vehicle/
│   │   ├── Combat/
│   │   ├── HordeDirector/
│   │   ├── Loot/
│   │   └── Meta/
│   ├── Entities/                     → Entities.asmdef (depends on Core)
│   │   ├── Enemy/
│   │   └── Player/
│   ├── UI/                           → UI.asmdef (depends on Core, Systems)
│   │   ├── HUD/
│   │   ├── Menus/
│   │   └── Screens/
│   └── Utilities/                    → Utilities.asmdef
│       ├── Pooling/
│       ├── Physics/
│       └── Extensions/
├── Data/
│   ├── ScriptableObjects/
│   │   ├── Enemies/
│   │   ├── Weapons/
│   │   ├── Waves/
│   │   ├── Upgrades/
│   │   └── StatusEffects/
│   └── Config/
│       └── GameConfig.asset
├── Scenes/
│   ├── Bootstrap.unity
│   ├── MainMenu.unity
│   ├── Arena.unity
│   ├── Hub.unity
│   └── _Loading.unity
├── Prefabs/
│   ├── Player/
│   ├── Enemies/
│   ├── Weapons/
│   ├── Loot/
│   ├── VFX/
│   └── UI/
├── Materials/
│   ├── Standard/
│   ├── VFX/
│   └── Decals/
├── Textures/
│   ├── Diffuse/
│   ├── Normal/
│   ├── Masks/
│   └── Decals/
├── Models/
│   ├── Vehicle/
│   ├── Enemies/
│   ├── Props/
│   └── Arena/
├── Audio/
│   ├── SFX/
│   ├── Music/
│   └── VO/ (later)
├── VFX/
│   └── (Visual Effect Prefabs & Sub-Emitters)
├── Animations/
│   ├── Player/
│   └── Enemies/
├── Shaders/
│   └── (Custom shaders, if needed)
└── Fonts/
    └── (UI Fonts, TMP)
```

---

## 🔧 Input Setup (Input System)

### **Action Map: Gameplay**

```
Gameplay ActionMap:
  Movement         → <Keyboard>/{A,W,S,D} | <Gamepad>/LeftStick
  Aim             → <Mouse>/Position | <Gamepad>/RightStick
  Fire Primary    → <Mouse>/LeftButton | <Gamepad>/LT
  Fire Secondary  → <Mouse>/RightButton | <Gamepad>/RT
  Interact        → <Keyboard>/E | <Gamepad>/Y
  Pause           → <Keyboard>/Escape | <Gamepad>/Start
```

### **Action Map: UI**

```
UIActionMap:
  Navigate        → <Keyboard>/Arrow Keys | <Gamepad>/DPad
  Select          → <Keyboard>/Enter | <Gamepad>/A
  Cancel          → <Keyboard>/Escape | <Gamepad>/B
  Submit          → <Mouse>/LeftButton | <Gamepad>/A
```

**Implementation:** PlayerInput Component + Event Callbacks.

---

## 🎮 Coop Input Handling

**Approach:** 2x PlayerInput instances, 1 per Player

```csharp
// Simplified structure
PlayerInput P1 = new(actionsAsset, deviceIndex: 0);
PlayerInput P2 = new(actionsAsset, deviceIndex: 1);

// Each has own GameObject in scene, own Camera, own Input handler
P1.OnMove += VehicleController1.OnMove;
P1.OnFire += CombatSystem1.OnFire;
// (same for P2)
```

**Splitscreen:** 2x Cameras, 1 per player, normalized Viewports (left/right halves).

---

## 💾 Save System Approach (Simple)

**Format:** JSON (via Newtonsoft.Json oder built-in JsonUtility)

**Data Structure:**

```csharp
[System.Serializable]
public class SaveGame
{
    public MetaData meta;          // Persistent resources
    public RunData currentRun;      // Active run (wenn paused)
}

[System.Serializable]
public class MetaData
{
    public int totalScrap;
    public int totalTech;
    public List<UnlockedUpgrade> unlockedUpgrades;
    public int runsCompleted;
}

[System.Serializable]
public class RunData
{
    public float timeElapsed;
    public int enemiesKilled;
    public int lootCollected;
    public List<ActiveUpgrade> activeUpgrades;
    // ... more run stats
}
```

**Save Location:** `Application.persistentDataPath + "/savegame.json"`

**Read/Write:** Simple File I/O + JSON Deserialization.

---

## 📍 Scene Structure

### **Scene 1: Bootstrap**
- Load GameManager (Zenject Container)
- Load SceneManager
- Load SaveSystem
- Transition → MainMenu

### **Scene 2: MainMenu**
- UI: Play, Settings, Quit
- Display Run Summary (if returning from Arena)

### **Scene 3: Hub**
- Player Vehicle visible (third-person view)
- Shop UI, Workshop UI
- Option to start new Run

### **Scene 4: Arena** (Main gameplay)
- Terrain/Props loaded
- Spawner initialized
- Horde Director active
- Player Vehicle + Camera
- HUD + UI Canvas

### **Scene 5: Loading** (optional)
- Loading screen between scenes

---

## 🔄 Dependency Injection (Zenject Pattern)

### **Installers (Setup)**

```
Installers/
  ├── CoreInstaller          → Register Core Systems
  ├── SystemsInstaller       → Register Game Systems
  ├── EntitiesInstaller      → Register Pools, Factories
  └── UIInstaller            → Register UI Controllers
```

### **Container Pattern**

```csharp
public class GameInstaller : MonoInstaller
{
    public override void InstallBindings()
    {
        Container.Bind<IGameConfig>().To<GameConfig>().AsSingle();
        Container.Bind<IHordeDirector>().To<HordeDirector>().AsSingle();
        Container.Bind<ICombatSystem>().To<CombatSystem>().AsSingle();
        Container.Bind<ILootSystem>().To<LootSystem>().AsSingle();
        Container.Bind<ISaveSystem>().To<SaveSystem>().AsSingle();
        // ... etc
    }
}
```

**Benefits:**
- Easy testing
- Decoupled systems
- Simple to swap implementations

---

**Nächster Schritt:** 04_Architecture_Modular.md (Systems Overview, Patterns)
