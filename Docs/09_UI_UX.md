# 🎮 9. UI/UX: HUD, Screens, Menus

---

## 🖥️ Screen Hierarchy

### **Active Run (Arena Scene)**
```
Canvas (UI Root)
├─ HUD (Bottom-left + corners)
│  ├─ HealthBar (Vehicle health)
│  ├─ AmmoDisplay (Current weapon ammo)
│  ├─ WaveInfo (Wave # + Timer)
│  ├─ TimeAlive (Run duration)
│  └─ ResourceCounter (Scrap/Tech gained this run)
├─ FloatingText (damage numbers, pickup +3 Scrap)
├─ UpgradeSelectionUI (overlay, every 5 min)
├─ Pause Menu (overlay)
├─ Game Over Screen (overlay)
└─ Win Screen / Extraction (overlay)
```

### **Hub Scene**
```
Canvas (UI Root)
├─ RunSummary (if returning from Arena)
├─ MetaProgressDisplay (Total Scrap/Tech)
├─ CharacterSelect (2 Driver-Personas)
├─ VehicleSelect (Motorcycle / Quad / Jeep / Truck)
├─ BountySelect (Pick 2 of 6)
├─ ShopUI
│  ├─ ShopItem Cards (Upgrades for purchase)
│  └─ PurchaseButtons
├─ MainButtons (Start Run, Settings, Quit)
└─ Viewport of Vehicle (3D model in scene)
```

---

## 📋 HUD Layout

```
┌─────────────────────────────────────────────────┐
│                                                 │
│                   [Reticle ⊕]                   │ ← Center (crosshair)
│                                                 │
│  ❤️ 100/100      [====]                         │ ← Top-left (Health)
│  Wave 5/15       5:43                           │ ← Top-center (Wave, Time)
│                           🔫 ∞ / [==════]       │ ← Top-right (Ammo)
│  Sig: 2/2                                        │ ← Right (Signature Uses)
│                                                 │
│  Scrap: 450       Tech: 12                      │ ← Bottom-right (Resources)
│                                                 │
└─────────────────────────────────────────────────┘

Floating Text Examples:
  "+5 Scrap"  (green, fades up)
  "-20 HP"    (red, fades up)
  "CRIT!"     (yellow, big, fades)
```

---

## 🎨 Color Scheme (Wasteland Aesthetic)

| Element | Color | Hex | Purpose |
|---------|-------|-----|---------|
| **Background** | Dark Gray | #1a1a1a | Main UI bg |
| **Primary Text** | Bright White | #FFFFFF | Readable |
| **Health** | Bright Red | #FF3333 | Warning |
| **Mana/Ammo** | Cyan Blue | #00FFFF | Tech feel |
| **Resources (Scrap)** | Gold/Orange | #FFB800 | Metal |
| **Resources (Tech)** | Electric Purple | #9D4EDD | Tech |
| **Success** | Lime Green | #39FF14 | Positive |
| **Warning** | Deep Orange | #FF6B35 | Alert |
| **Accent** | Neon Pink | #FF10F0 | Highlights |

---

## 📐 HUD Components (Detailed)

### **Health Bar**
```csharp
public class HealthBar : MonoBehaviour
{
    public Image healthFill;              // Red bar
    public TextMeshProUGUI healthText;    // "100 / 100"
    public float smoothDampTime = 0.3f;
    
    void Update()
    {
        float targetFill = (float)playerHealth / playerMaxHealth;
        healthFill.fillAmount = Mathf.SmoothDamp(healthFill.fillAmount, targetFill, ref dampVel, smoothDampTime);
        healthText.text = $"{playerHealth} / {playerMaxHealth}";
    }
}
```

### **Wave Info**
```csharp
public class WaveInfoDisplay : MonoBehaviour
{
    public TextMeshProUGUI waveText;     // "Wave 5 / 15"
    public TextMeshProUGUI timerText;    // "5:43"
    
    void Update()
    {
        waveText.text = $"Wave {currentWave} / {totalWaves}";
        timerText.text = TimeToString(timeRemaining);
    }
}
```

### **Ammo Display**
```csharp
public class AmmoDisplay : MonoBehaviour
{
    public TextMeshProUGUI ammoText;     // "45 / 100" or "∞"
    public Image ammoBar;                // Visual bar
    
    void Update()
    {
        if (currentWeapon.ammoCapacity == 0)
            ammoText.text = "∞";
        else
            ammoText.text = $"{currentAmmo} / {currentWeapon.ammoCapacity}";
    }
}
```

### **Upgrade Selection UI**

```csharp
public class UpgradeSelectionUI : MonoBehaviour
{
    public UpgradeCard[] cards = new UpgradeCard[3];  // 3 choices
    
    public void ShowUpgrades(List<UpgradeData> choices)
    {
        gameObject.SetActive(true);
        Time.timeScale = 0;  // Pause game
        
        for (int i = 0; i < 3; i++)
        {
            cards[i].SetUpgrade(choices[i]);
            cards[i].OnSelected += SelectUpgrade;
        }
    }
    
    void SelectUpgrade(UpgradeData upgrade)
    {
        upgradeManager.ApplyUpgrade(upgrade);
        Time.timeScale = 1;
        gameObject.SetActive(false);
    }
}

public class UpgradeCard : MonoBehaviour
{
    public Image iconImage;
    public TextMeshProUGUI titleText;
    public TextMeshProUGUI descriptionText;
    public Button selectButton;
    public Image backgroundImage;
    
    public event System.Action<UpgradeData> OnSelected;
    
    public void SetUpgrade(UpgradeData upgrade)
    {
        iconImage.sprite = upgrade.cardIcon;
        titleText.text = upgrade.upgradeName;
        descriptionText.text = upgrade.description;
        backgroundImage.color = upgrade.cardColor;
        
        selectButton.onClick.AddListener(() => OnSelected?.Invoke(upgrade));
    }
}
```

---

## 🎯 Pre-Run Auswahl (Charakter + Vehicle + Bounties)

**Flow (Hub):**
1. Charakter wählen (Portrait + Passive + Skillzweige)
2. Vehicle wählen (4 Klassen: Motorrad, Quad, Jeep, Truck)
   - WMA: Motorrad (Solo), Jeep (Coop)
3. 6 zufällige Kopfgelder anzeigen → 2 auswählen
4. Start Run

**Bounty Card UI:**
- Titel, Schwierigkeit (Easy/Medium/Hard/Brutal)
- Modifiers (z.B. +Elite, +Ranged, -Heal)
- Rewards (Scrap/Tech/Upgrade-Bonus)

## 🎯 Game Over Screen

```
┌──────────────────────────────────┐
│                                  │
│         YOU DIED                 │
│                                  │
│  ═════════════════════════════   │
│                                  │
│  Time Survived:  5:43            │
│  Enemies Killed: 342             │
│  Scrap Earned:   125             │
│  Tech Earned:    8               │
│  Final Wave:     8 / 15          │
│                                  │
│  [RETURN TO HUB]  [RESTART]      │
│                                  │
└──────────────────────────────────┘
```

---

## ✅ Extraction / Win Screen

```
┌──────────────────────────────────┐
│                                  │
│       EXTRACTION SUCCESSFUL      │
│                                  │
│  ═════════════════════════════   │
│                                  │
│  Time Survived:  15:23           │
│  Enemies Killed: 1247            │
│  Scrap Earned:   847             │
│  Tech Earned:    45              │
│  Final Wave:     15 / 15         │
│                                  │
│  ⭐ BONUS: +50 Scrap (5 min+)    │
│                                  │
│  [RETURN TO HUB]  [RESTART]      │
│                                  │
└──────────────────────────────────┘
```

---

## ⏸️ Pause Menu

```
┌──────────────────────────────────┐
│        GAME PAUSED               │
│                                  │
│  [RESUME]                        │
│  [SETTINGS]                      │
│  [RETURN TO HUB]                 │
│  [QUIT TO DESKTOP]               │
│                                  │
└──────────────────────────────────┘
```

### **Settings Screen** (in Pause Menu)

```
┌──────────────────────────────────┐
│        SETTINGS                  │
│                                  │
│  Master Volume:   [======] 80%  │
│  SFX Volume:      [========] 100% │
│  Music Volume:    [====] 60%     │
│                                  │
│  Language:  [DE ▼]               │
│  Colorblind Mode: [OFF]          │
│                                  │
│  [BACK]                          │
│                                  │
└──────────────────────────────────┘
```

---

## 🏪 Hub/Shop UI

```
┌────────────────────────────────────────────┐
│                                            │
│  Total Scrap: 1250    Total Tech: 150     │
│                                            │
│  ═══════════════════════════════════════   │
│                                            │
│  ┌─────────────┐ ┌─────────────┐          │
│  │ +DAMAGE     │ │ +SPEED      │          │
│  │ 10% boost   │ │ 5% boost    │          │
│  │ Cost: 50    │ │ Cost: 75    │          │
│  │ [BUY]       │ │ [BUY]       │          │
│  └─────────────┘ └─────────────┘          │
│                                            │
│  ┌─────────────┐                          │
│  │ +ARMOR      │                          │
│  │ 10% boost   │                          │
│  │ Cost: 100   │                          │
│  │ [BUY]       │                          │
│  └─────────────┘                          │
│                                            │
│  ═══════════════════════════════════════   │
│                    [START RUN]             │
│                                            │
└────────────────────────────────────────────┘
```

---

## 🎮 Font & Text Standards

- **Title Font:** Roboto Bold, 36pt
- **Body Font:** Roboto Regular, 20pt
- **Small Font:** Roboto Regular, 14pt
- **Monospace (Numbers):** Roboto Mono, 18pt (for ammo, HP)

**Contrast Minimum:** WCAG AA (4.5:1 ratio) for all text.

---

## 🌍 Localization (DE/EN)

**All UI strings in String Tables:**

```
UI_MainMenu_PlayButton = "PLAY" / "SPIELEN"
UI_MainMenu_QuitButton = "QUIT" / "BEENDEN"
UI_HUD_Wave = "Wave {0}" / "Welle {0}"
UI_HUD_Health = "Health" / "Gesundheit"
UI_GameOver_YouDied = "YOU DIED" / "DU BIST TOT"
... (hundreds more)
```

---

**Nächster Schritt:** 10_Save_Meta.md (Save System & Progression Details)
