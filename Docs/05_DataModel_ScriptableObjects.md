# 5️⃣ Data Model: ScriptableObject Templates & Serialization

**Pattern:** Data-driven design via ScriptableObjects (SO). All game parameters tunable without code changes.

---

## 📊 Enemy Data Model

**File:** `Data/ScriptableObjects/Enemies/[EnemyType].asset`

```csharp
[CreateAssetMenu(menuName = "Game/Enemy/EnemyData")]
public class EnemyData : ScriptableObject
{
    [Header("Identity")]
    public string enemyName = "Boar Grunt";
    public EnemyType type = EnemyType.BoarGrunt;
    public GameObject meshPrefab;
    
    [Header("Stats")]
    public int healthBase = 20;
    public float healthVariance = 0.1f;  // ±10%
    public float movementSpeed = 5f;
    public float detectionRange = 30f;
    public float attackRange = 2f;
    
    [Header("Attack")]
    public float attackCooldown = 1.5f;
    public int meleeDamage = 5;
    public float projectileSpeed = 10f;
    public GameObject projectilePrefab;  // if ranged
    
    [Header("Behavior")]
    public EnemyBehavior behavior = EnemyBehavior.MeleeChaser;
    public bool useRangedAttack = false;
    public bool flees = false;
    public float fleeDistance = 15f;
    
    [Header("Loot")]
    public List<LootEntry> lootTable = new();
    
    [Header("UI")]
    public Sprite iconSprite;
    public Color displayColor = Color.white;
}

[System.Serializable]
public class LootEntry
{
    public LootType type;
    public int minAmount = 1;
    public int maxAmount = 3;
    public float dropChance = 0.8f;  // 0–1
}

public enum EnemyType
{
    BoarGrunt, BoarBrute, BoarTitan,
    HyenaRunner, HyenaPack,
    RavenSwooper,
    VenomLurker,
    PlagueSpreader,
    ApexPredator,
    Goldgoblin,  // special
}

public enum EnemyBehavior
{
    MeleeChaser,
    RangedAttacker,
    Flyer,
    GroupLeader,
}
```

---

## 🔫 Weapon Data Model

**File:** `Data/ScriptableObjects/Weapons/[WeaponName].asset`

```csharp
[CreateAssetMenu(menuName = "Game/Weapon/WeaponData")]
public class WeaponData : ScriptableObject
{
    [Header("Identity")]
    public string weaponName = "Plasma Rifle";
    public Sprite iconSprite;
    
    [Header("Fire")]
    public float fireRate = 10f;  // shots per second
    public float damage = 20f;
    public bool isProjectile = true;
    public float ammoCapacity = 100f;
    public float ammoRegenRate = 5f;  // per second
    
    [Header("Projectile (if applicable)")]
    public float projectileSpeed = 50f;
    public float projectileLifetime = 5f;
    public GameObject projectilePrefab;
    public int projectileCount = 1;  // for shotguns
    public float projectileSpread = 0.1f;  // radians
    
    [Header("Effects")]
    public float recoil = 2f;
    public float knockback = 0f;
    public VFXData muzzleFlashVFX;
    public SFXData fireSound;
    
    [Header("Upgradeable")]
    public float damageMultiplier = 1f;
    public float fireRateMultiplier = 1f;
}
```

---

## ⚡ Status Effect Model

**File:** `Data/ScriptableObjects/StatusEffects/[EffectName].asset`

```csharp
[CreateAssetMenu(menuName = "Game/StatusEffect/StatusEffectData")]
public class StatusEffectData : ScriptableObject
{
    public string effectName = "Freeze";
    public EffectType type = EffectType.Freeze;
    public float duration = 5f;
    public float stackIntensity = 1.2f;  // multiplier for stacked instances
    
    [Header("Visuals")]
    public Color tintColor = Color.cyan;
    public VFXData effectVFX;
    public ParticleSystem particleTemplate;
    
    [Header("Behavior")]
    public float speedReduction = 0.5f;  // 0 = no movement
    public int damageReduction = 0;
    public bool preventAttack = false;
    public bool breakOnDamage = false;
    
    [Header("Application")]
    public SFXData applySound;
    public bool visibleIndicator = true;
}

public enum EffectType
{
    Freeze, Burn, Poison, Stun, Slow, Bleed, Amplify,
}
```

---

## 🎁 Upgrade Data Model

**File:** `Data/ScriptableObjects/Upgrades/[UpgradeName].asset`

```csharp
[CreateAssetMenu(menuName = "Game/Upgrade/UpgradeData")]
public class UpgradeData : ScriptableObject
{
    [Header("Identity")]
    public string upgradeName = "Rapid Fire";
    public string description = "Increases fire rate by 20%";
    public Sprite cardIcon;
    public Color cardColor = Color.white;
    
    [Header("Effect")]
    public UpgradeType upgradeType = UpgradeType.FireRate;
    public float value = 0.2f;  // typically a multiplier or flat bonus
    public bool isMultiplier = true;  // if false, add flat value
    
    [Header("Stacking")]
    public bool canStack = true;
    public float stackDiminishing = 1f;  // 0.8 = 80% of previous benefit
    
    [Header("Visual")]
    public VFXData cardRevealVFX;
}

public enum UpgradeType
{
    Damage, FireRate, ProjectileSpeed, AmmoCapacity, AmmoRegenRate,
    Movement, Armor, Health, HealthRegen,
    StatusEffectChance, CritChance,
    LootMagnetRadius, ResourceMultiplier,
}
```

---

## 🌊 Wave & Difficulty Model

**File:** `Data/ScriptableObjects/Waves/[WaveName].asset`

```csharp
[CreateAssetMenu(menuName = "Game/Wave/WaveData")]
public class WaveData : ScriptableObject
{
    [Header("Wave Identity")]
    public int waveNumber = 1;
    public string waveName = "Early Pressure";
    
    [Header("Spawning")]
    public float durationSeconds = 60f;
    public List<EnemySpawnGroup> enemySpawnGroups = new();
    public float spawnRateMultiplier = 1f;
    
    [Header("Difficulty")]
    public float enemyHealthMultiplier = 1f;
    public float enemyDamageMultiplier = 1f;
    public float enemySpeedMultiplier = 1f;
    
    [Header("Special")]
    public bool includeElites = false;
    public float eliteSpawnChance = 0.05f;  // 5%
    public bool includeGoldgoblin = false;
    public float goldgoblinChance = 0.02f;  // 2%
    
    [Header("Rewards")]
    public float lootDropMultiplier = 1f;
    public float techDropChance = 0.15f;  // 15% instead of 20%
}

[System.Serializable]
public class EnemySpawnGroup
{
    public EnemyData enemyType;
    public int countToSpawn = 10;
    public float spawnInterval = 1f;  // seconds between spawns
}
```

---

## 🎮 Game Config (Master)

**File:** `Data/Config/GameConfig.asset`

```csharp
[CreateAssetMenu(menuName = "Game/Config/GameConfig")]
public class GameConfig : ScriptableObject
{
    [Header("Player (Vehicle)")]
    public float playerBaseSpeed = 20f;
    public int playerBaseHealth = 100;
    public float playerBaseArmor = 0f;
    
    [Header("Combat")]
    public float projectilePoolSize = 100;
    public float enemyDetectionRange = 40f;
    
    [Header("Horde")]
    public List<WaveData> waveProgression = new();
    public float waveInterval = 120f;  // seconds between waves
    public float timeBetweenUpgradeOffers = 300f;  // 5 minutes
    
    [Header("Loot")]
    public float lootMagnetRadius = 5f;
    public float lootMagnetSpeed = 8f;
    public float scrapDropRate = 0.7f;
    public float techDropRate = 0.15f;
    
    [Header("Extraction")]
    public float extractionSpawnTime = 900f;  // 15 minutes
    public float extractionRadius = 10f;
    
    [Header("Coop")]
    public float coopEnemyCountMultiplier = 1.3f;  // 30% more enemies with 2 players
    
    [Header("UI")]
    public float damageFloatingTextDuration = 1f;
    public float killNotificationDuration = 2f;
    
    [Header("Audio")]
    public float masterVolume = 0.8f;
    public float sfxVolume = 1f;
    public float musicVolume = 0.6f;
}
```

---

## 🎯 Run State Model (Runtime)

**Not a ScriptableObject, but serializable:**

```csharp
[System.Serializable]
public class RunState
{
    [Header("Time & Progress")]
    public float elapsedTime;
    public int currentWaveNumber;
    public List<int> activeUpgradesIds = new();
    
    [Header("Resources")]
    public int scrapCollected;
    public int techCollected;
    
    [Header("Stats")]
    public int totalEnemiesKilled;
    public int totalDamageDealt;
    public int totalDamageTaken;
    
    [Header("Run Modifiers")]
    public bool extractionSpawned;
    public int playerCount = 1;  // 1 or 2
}
```

---

## 💾 Save File Structure (JSON)

```json
{
  "version": "1.0",
  "metadata": {
    "lastSaveTime": "2025-01-05T12:34:56Z",
    "totalPlaysessions": 42
  },
  "metaProgress": {
    "totalScrap": 1250,
    "totalTech": 150,
    "runsCompleted": 15,
    "bestTimeMinutes": 23.5,
    "unlockedUpgrades": ["rapid_fire", "armor_plating", "health_regen"],
    "unlockedWeapons": ["plasma_rifle", "shotgun"],
    "cosmetics": {
      "vehicleSkin": "neon_blue",
      "decals": ["hazard_stripe", "rust"]
    }
  },
  "lastRun": {
    "date": "2025-01-05T12:30:00Z",
    "duration": 1205,
    "enemiesKilled": 342,
    "scrapEarned": 125,
    "techEarned": 8,
    "upgradesUsed": ["rapid_fire", "armor_plating"],
    "finalWave": 12,
    "extracted": true
  }
}
```

---

**Nächster Schritt:** 06_Enemies_HordeDesign.md (Roster, Stats, Behaviors)
