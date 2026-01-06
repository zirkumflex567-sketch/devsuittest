# 💾 10. Save System & Meta Progression

---

## 🎮 Save Data Hierarchy

```
SaveGame (Root)
├─ Metadata
│  ├─ SaveVersion: "1.0"
│  ├─ LastSaveTime: DateTime
│  └─ TotalPlaySessions: int
├─ MetaProgress (Persistent across runs)
│  ├─ Resources
│  │  ├─ TotalScrap: int
│  │  └─ TotalTech: int
│  ├─ Unlocks
│  │  ├─ UnlockedWeapons: List<string>
│  │  ├─ UnlockedUpgrades: List<string>
│  │  └─ UnlockedCosmetics: List<string>
│  │  ├─ UnlockedCharacters: List<string>
│  │  └─ UnlockedVehicles: List<string>
│  └─ Stats
│     ├─ RunsCompleted: int
│     ├─ BestTime: float
│     └─ TotalEnemiesKilled: long
└─ LastRunData (Session summary)
   ├─ SelectedCharacterId: string
   ├─ SelectedVehicleId: string
   ├─ SelectedBountyIds: List<string>
   ├─ RunDuration: float
   ├─ EnemiesKilled: int
   ├─ ResourcesEarned
   │  ├─ Scrap: int
   │  └─ Tech: int
   ├─ UpgradesUsed: List<string>
   ├─ FinalWave: int
   └─ WasExtracted: bool
```

---

## 📄 JSON Save File Format

**File:** `{persistentDataPath}/savegame.json`

```json
{
  "version": "1.0",
  "metadata": {
    "lastSaveTime": "2025-01-05T12:34:56Z",
    "totalPlaySessions": 42,
    "gameVersion": "0.1.0-wma"
  },
  "metaProgress": {
    "totalScrap": 1250,
    "totalTech": 150,
    "runsCompleted": 15,
    "bestTimeSeconds": 1410,
    "totalEnemiesKilled": 5342,
    "unlockedWeapons": [
      "plasma_rifle",
      "shotgun"
    ],
    "unlockedUpgrades": [
      "damage_boost_1",
      "speed_boost_1",
      "armor_plating_1"
    ],
    "unlockedCosmetics": [
      "vehicle_skin_neon_blue",
      "decal_hazard_stripe"
    ],
    "unlockedCharacters": [
      "rixa_chromlilie",
      "marek_schrottanker"
    ],
    "unlockedVehicles": [
      "motorcycle",
      "jeep"
    ]
  },
  "lastRun": {
    "date": "2025-01-05T12:30:00Z",
    "durationSeconds": 1205,
    "wave": 12,
    "enemiesKilled": 342,
    "scrapEarned": 125,
    "techEarned": 8,
    "upgradesUsed": [
      "rapid_fire",
      "armor_plating"
    ],
    "selectedCharacterId": "rixa_chromlilie",
    "selectedVehicleId": "motorcycle",
    "selectedBountyIds": [
      "bounty_headhunter",
      "bounty_toxic_rain"
    ],
    "wasExtracted": false,
    "playerCount": 1
  }
}
```

---

## 🔧 C# Save System Implementation

```csharp
[System.Serializable]
public class SaveGame
{
    public SaveMetadata metadata;
    public MetaProgress metaProgress;
    public RunData lastRun;
}

[System.Serializable]
public class SaveMetadata
{
    public string version = "1.0";
    public long lastSaveTime;
    public int totalPlaySessions;
    public string gameVersion;
}

[System.Serializable]
public class MetaProgress
{
    public int totalScrap;
    public int totalTech;
    public int runsCompleted;
    public float bestTimeSeconds;
    public long totalEnemiesKilled;
    
    public List<string> unlockedWeapons = new();
    public List<string> unlockedUpgrades = new();
    public List<string> unlockedCosmetics = new();
    public List<string> unlockedCharacters = new();
    public List<string> unlockedVehicles = new();
}

[System.Serializable]
public class RunData
{
    public long dateUnixMs;
    public float durationSeconds;
    public int wave;
    public int enemiesKilled;
    public int scrapEarned;
    public int techEarned;
    public List<string> upgradesUsed = new();
    public string selectedCharacterId;
    public string selectedVehicleId;
    public List<string> selectedBountyIds = new();
    public bool wasExtracted;
    public int playerCount;
}

public class SaveSystem : MonoBehaviour, IDisposable
{
    private string savePath;
    
    void Awake()
    {
        savePath = Path.Combine(Application.persistentDataPath, "savegame.json");
    }
    
    public void SaveGame(SaveGame data)
    {
        try
        {
            data.metadata.lastSaveTime = System.DateTimeOffset.Now.ToUnixTimeMilliseconds();
            data.metadata.totalPlaySessions++;
            
            string json = JsonConvert.SerializeObject(data, Formatting.Indented);
            File.WriteAllText(savePath, json);
            
            Debug.Log($"Game saved to {savePath}");
        }
        catch (System.Exception e)
        {
            Debug.LogError($"Save failed: {e.Message}");
        }
    }
    
    public SaveGame LoadGame()
    {
        try
        {
            if (!File.Exists(savePath))
                return CreateDefaultSave();
            
            string json = File.ReadAllText(savePath);
            SaveGame data = JsonConvert.DeserializeObject<SaveGame>(json);
            
            Debug.Log($"Game loaded from {savePath}");
            return data;
        }
        catch (System.Exception e)
        {
            Debug.LogError($"Load failed: {e.Message}. Creating new save.");
            return CreateDefaultSave();
        }
    }
    
    private SaveGame CreateDefaultSave()
    {
        return new SaveGame
        {
            metadata = new SaveMetadata
            {
                version = "1.0",
                gameVersion = "0.1.0-wma",
                totalPlaySessions = 0
            },
            metaProgress = new MetaProgress
            {
                totalScrap = 0,
                totalTech = 0,
                unlockedWeapons = new() { "plasma_rifle" },  // default
                unlockedUpgrades = new(),
                unlockedCharacters = new() { "rixa_chromlilie", "marek_schrottanker" },
                unlockedVehicles = new() { "motorcycle", "jeep" },
            },
            lastRun = new RunData()
        };
    }
    
    public void Dispose()
    {
        // Optional: cleanup
    }
}
```

---

## 🛍️ Unlock System

### **Weapon Unlocks**

```csharp
public class WeaponUnlockManager
{
    public bool TryUnlockWeapon(string weaponId, int scrapCost, int techCost)
    {
        if (metaProgress.totalScrap < scrapCost || metaProgress.totalTech < techCost)
            return false;
        
        if (metaProgress.unlockedWeapons.Contains(weaponId))
            return false;  // Already unlocked
        
        metaProgress.unlockedWeapons.Add(weaponId);
        metaProgress.totalScrap -= scrapCost;
        metaProgress.totalTech -= techCost;
        
        saveSystem.SaveGame(currentSaveGame);
        return true;
    }
    
    public bool IsWeaponUnlocked(string weaponId)
    {
        return metaProgress.unlockedWeapons.Contains(weaponId);
    }
}
```

### **Upgrade Unlocks**

```csharp
[System.Serializable]
public class UpgradeUnlock
{
    public string upgradeId;
    public int scrapCost = 50;
    public int techCost = 0;
    public string description;
    public UpgradeType type;
    public float value = 0.1f;  // 10% boost
}

public class UpgradeUnlockManager
{
    public bool TryPermanentlyUnlockUpgrade(string upgradeId)
    {
        UpgradeUnlock unlock = upgradeDatabase.GetUnlock(upgradeId);
        
        if (metaProgress.totalScrap < unlock.scrapCost)
            return false;
        
        if (metaProgress.unlockedUpgrades.Contains(upgradeId))
            return false;  // Already unlocked
        
        metaProgress.unlockedUpgrades.Add(upgradeId);
        metaProgress.totalScrap -= unlock.scrapCost;
        metaProgress.totalTech -= unlock.techCost;
        
        saveSystem.SaveGame(currentSaveGame);
        return true;
    }
}
```

---

## 📊 Meta Progression Tracking

```csharp
public class MetaProgressTracker : MonoBehaviour
{
    private SaveGame currentSave;
    
    public void AddScrap(int amount)
    {
        currentSave.metaProgress.totalScrap += amount;
        OnMetaProgressChanged?.Invoke();
    }
    
    public void AddTech(int amount)
    {
        currentSave.metaProgress.totalTech += amount;
        OnMetaProgressChanged?.Invoke();
    }
    
    public void RecordRunCompletion(RunData run)
    {
        currentSave.metaProgress.runsCompleted++;
        
        if (run.durationSeconds > currentSave.metaProgress.bestTimeSeconds)
            currentSave.metaProgress.bestTimeSeconds = run.durationSeconds;
        
        currentSave.metaProgress.totalEnemiesKilled += run.enemiesKilled;
        currentSave.lastRun = run;
        
        SaveGame();
    }
    
    public void SaveGame()
    {
        saveSystem.SaveGame(currentSave);
    }
    
    public event System.Action OnMetaProgressChanged;
}
```

---

## 🎁 Cosmetics System

```csharp
[System.Serializable]
public class CosmeticItem
{
    public string cosmeticId;
    public CosmeticType type;  // VehicleSkin, Decal, Trail, etc.
    public int scrapCost;
    public int techCost;
    public string displayName;
    public Sprite preview;
}

public enum CosmeticType
{
    VehicleSkin,
    Decal,
    EngineTrail,
    WeaponShader,
    HUDTheme,
}

public class CosmeticManager : MonoBehaviour
{
    public bool UnlockCosmetic(string cosmeticId)
    {
        CosmeticItem item = cosmeticDatabase.Get(cosmeticId);
        
        if (metaProgress.totalScrap < item.scrapCost)
            return false;
        
        metaProgress.unlockedCosmetics.Add(cosmeticId);
        metaProgress.totalScrap -= item.scrapCost;
        metaProgress.totalTech -= item.techCost;
        
        return true;
    }
    
    public void ApplyCosmeticToVehicle(string cosmeticId)
    {
        if (!metaProgress.unlockedCosmetics.Contains(cosmeticId))
            return;  // Not unlocked
        
        CosmeticItem cosmetic = cosmeticDatabase.Get(cosmeticId);
        
        // Apply to vehicle visuals
        vehicleRenderer.ApplySkin(cosmetic);
    }
}
```

---

## 🔄 Run Summary Flow

```csharp
public class RunSummaryManager : MonoBehaviour
{
    public void OnRunEnd(bool extracted, RunData runData)
    {
        // Calculate bonuses
        if (extracted)
            runData.scrapEarned += 50;  // Extraction bonus
        
        if (runData.durationSeconds > 600)  // 10 min+
            runData.scrapEarned += 25;  // Endurance bonus
        
        // Loot loss on death: only bank resources if extracted
        if (extracted)
        {
            metaTracker.AddScrap(runData.scrapEarned);
            metaTracker.AddTech(runData.techEarned);
        }
        metaTracker.RecordRunCompletion(runData);
        
        // Show summary
        uiManager.ShowRunSummary(runData);
        
        // Transition to Hub
        SceneManager.LoadScene("Hub");
    }
}
```

---

## 🌍 Localization String Tables

**Key pattern:** `UI_[SCREEN]_[ELEMENT]`

```
UI_MainMenu_PlayButton
UI_MainMenu_SettingsButton
UI_MainMenu_QuitButton
UI_HUD_Wave
UI_HUD_Health
UI_HUD_Ammo
UI_GameOver_YouDied
UI_GameOver_Extracted
UI_Shop_BuyButton
UI_Shop_Afforded
UI_Shop_NotAfforded
... (hundreds more)
```

---

**Nächster Schritt:** 11_Localization_DE_EN.md (Full Glossary & String Tables)
