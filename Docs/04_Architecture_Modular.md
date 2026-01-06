# 4️⃣ Modular Architecture & Systems Design

**Principle:** Everything is a System. Systems communicate via Events or Interfaces.

---

## 🏗️ System Overview

```
┌─────────────────────────────────────────────────┐
│              GameManager (Root)                 │
├─────────────────────────────────────────────────┤
│
├─ Bootstrap System (Scene Loading, DI Container)
│
├─ Vehicle System
│  ├─ VehicleController (Input → Movement)
│  ├─ VehicleStats (Health, Armor, Speed)
│  └─ VehicleDamageReceiver
│
├─ Character System
│  ├─ CharacterSelect (Pre-Run)
│  ├─ CharacterStats (Traits, Passives)
│  └─ SkillTreeRuntime (3-Branch Tree)
│
├─ Combat System
│  ├─ WeaponController (Primary + Secondary)
│  ├─ Projectile Manager (Pooling)
│  ├─ HitscanHandler (Raycast + Damage)
│  └─ CombatEvents (OnShot, OnHit, OnKill)
│
├─ Horde Director (Spawning, Waves, Difficulty)
│  ├─ WaveManager (Current Wave Logic)
│  ├─ SpawnerController (Enemy Spawn Volumes)
│  └─ DifficultyScaler (Wave-based tuning)
│
├─ Enemy System
│  ├─ EnemyFactory (Instantiation from SO)
│  ├─ EnemyPool (Object Reuse)
│  ├─ EnemyAI (State Machine per enemy)
│  └─ EnemyDamageReceiver
│
├─ Loot System
│  ├─ LootDropper (Spawn drops on enemy death)
│  ├─ LootPickup (Magnet radius, collection)
│  └─ ResourceAccumulator (Scrap/Tech count)
│
├─ Upgrade System
│  ├─ RunUpgradeManager (Current session upgrades)
│  ├─ UpgradeSelectionUI
│  └─ UpgradeApplier (Apply stats to player)
│
├─ Bounty System
│  ├─ BountyDeck (6 random bounties)
│  ├─ BountySelectionUI (Pick 2)
│  └─ BountyModifierApplier (Difficulty + Rewards)
│
├─ Meta / Save System
│  ├─ MetaProgressManager (Persistent resources)
│  ├─ SaveGame Handler
│  └─ RunSummaryData
│
├─ Camera System
│  ├─ CameraController (Follow, Offset)
│  └─ ReticleController (Aim visualization)
│
├─ UI System
│  ├─ HUDController (Health, Ammo, Wave, Timer)
│  ├─ MenuController (Pause, Game Over)
│  └─ ScreenManager (Scene transitions)
│
└─ Audio System
   ├─ SFXPlayer (with pooling)
   ├─ MusicManager (looping)
   └─ VolumeController
```

---

## 🔌 Communication Patterns

### **Pattern 1: Events (Observer)**

```csharp
public interface ICombatEvents
{
    event System.Action<int> OnEnemyKilled;     // damage dealt
    event System.Action<int> OnDamageTaken;     // damage received
    event System.Action<WeaponData> OnWeaponSwap;
}

// Usage:
combatEvents.OnEnemyKilled += (dmg) => {
    audioSystem.PlaySFX("kill");
    lootSystem.TrySpawnDrop(position, enemyType);
};
```

### **Pattern 2: Interfaces (Dependency)**

```csharp
public class VehicleController : MonoBehaviour
{
    private IInputHandler input;
    private IVehicleMovement movement;
    private ICombatEvents combat;

    [Inject]
    public void Construct(IInputHandler input, IVehicleMovement movement, ICombatEvents combat)
    {
        this.input = input;
        this.movement = movement;
        this.combat = combat;
    }
}
```

### **Pattern 3: ScriptableObject Config**

```csharp
[CreateAssetMenu(menuName = "Game/Config")]
public class GameConfig : ScriptableObject
{
    public float playerSpeedMultiplier = 1.0f;
    public int maxHealthBase = 100;
    public List<WeaponData> availableWeapons;
    // ... all tunable parameters
}

// Access:
public class CombatSystem : MonoBehaviour
{
    [SerializeField] private GameConfig config;
    
    void Start()
    {
        maxDamage = config.maxHealthBase;
    }
}
```

---

## 🎯 Key Systems (Detailed)

### **1. Vehicle System**

**Components:**
- `VehicleController`: Input (WASD) → Movement velocity
- `VehicleMovement`: Physics-based or kinematic movement
- `VehicleStats`: Health, Armor, Speed multiplier
- `VehicleDamageReceiver`: Implements IDamageReceiver interface

**Behavior:**
```csharp
public class VehicleController : MonoBehaviour
{
    [SerializeField] private float maxSpeed = 20f;
    [SerializeField] private float acceleration = 100f;
    private Vector3 velocity;
    private IInputHandler input;

    void Update()
    {
        Vector3 moveInput = input.GetMovement(); // (x, 0, z)
        velocity += moveInput * acceleration * Time.deltaTime;
        velocity = Vector3.ClampMagnitude(velocity, maxSpeed);
        
        transform.Translate(velocity * Time.deltaTime);
    }
}
```

**Coop:** 2x VehicleController instances, separate inputs per player.

---

### **2. Character System**

**Components:**
- `CharacterSelect`: Pre-Run Auswahl (2 Characters)
- `CharacterStats`: Passives, Startwerte, Modifiers
- `SkillTreeRuntime`: 3-Zweig-Tree, Run-Upgrades als Nodes
- `CharacterAbility`: Spezialfähigkeit (max. 2x pro Run)

**Behavior:**
```csharp
[CreateAssetMenu(menuName = "Game/Character/CharacterData")]
public class CharacterData : ScriptableObject
{
    public string characterId;
    public string displayName;
    public int baseHealth;
    public float moveSpeedMultiplier = 1f;
    public int baseArmor;
    public float critChanceBonus;
    public string passiveId;
    public AbilityData signatureAbility;
    public SkillTreeData skillTree;
}
```

---

### **3. Combat System**

**Components:**
- `WeaponController`: Manages Primary + Secondary
- `Projectile`: Pooled, moves forward, detects hits
- `HitscanHandler`: Raycast-based weapon (instant-hit)

**Weapon Data (ScriptableObject):**
```csharp
[CreateAssetMenu]
public class WeaponData : ScriptableObject
{
    public string weaponName;
    public float damage = 10f;
    public float fireRate = 0.1f;          // shots per second
    public float ammo = 100f;               // if applicable
    public float recoil = 5f;
    public bool isProjectile = true;
    public Prefab projectilePrefab;        // if projectile
}
```

**Fire Logic:**
```csharp
public class WeaponController : MonoBehaviour
{
    private float lastFireTime = 0f;
    private WeaponData currentWeapon;
    
    public void Fire(Vector3 direction)
    {
        if (Time.time - lastFireTime < 1f / currentWeapon.fireRate)
            return;
        
        lastFireTime = Time.time;
        
        if (currentWeapon.isProjectile)
            SpawnProjectile(direction);
        else
            HitscanFire(direction);
    }
}
```

---

### **4. Horde Director & Spawning**

**Components:**
- `HordeDirector`: Master spawner, wave logic
- `WaveManager`: Current wave state + difficulty
- `SpawnerVolume`: Spawnable area (random positions anywhere)

**Wave Definition (ScriptableObject):**
```csharp
[System.Serializable]
public class WaveData
{
    public int waveNumber;
    public List<EnemySpawnGroup> enemyGroups;   // List of {enemyType, count}
    public float difficulty = 1.0f;              // health/damage multiplier
    public float spawnRate = 5f;                 // enemies per second
}
```

**Spawning Logic:**
```csharp
public class HordeDirector : MonoBehaviour
{
    private float spawnBudget = 0f;  // Accumulating budget
    private Queue<EnemyType> toSpawn;

    void Update()
    {
        spawnBudget += currentWave.spawnRate * Time.deltaTime;
        
        while (spawnBudget >= 1f && toSpawn.Count > 0)
        {
            SpawnEnemy(toSpawn.Dequeue());
            spawnBudget -= 1f;
            currentEnemyCount++;
        }
        
        // Check wave complete
        if (currentEnemyCount == 0 && toSpawn.Count == 0)
            AdvanceWave();
    }
}
```

---

### **5. Enemy AI (Simple State Machine)**

**States:** Chase, Attack (Melee), RangedAttack, Retreat, Idle

```csharp
public enum EnemyState { Idle, Chase, MeleeAttack, RangedAttack, Retreat, Dead }

public class EnemyAI : MonoBehaviour
{
    private EnemyState state = EnemyState.Idle;
    private Transform playerTarget;
    private float detectionRange = 30f;

    void Update()
    {
        switch (state)
        {
            case EnemyState.Idle:
                if (IsPlayerInRange())
                    state = EnemyState.Chase;
                break;
                
            case EnemyState.Chase:
                MoveTowardPlayer();
                if (IsInAttackRange())
                    state = GetAttackState();
                break;
                
            case EnemyState.MeleeAttack:
                if (!IsInAttackRange())
                    state = EnemyState.Chase;
                else
                    AttackMelee();
                break;
                
            // ... etc
        }
    }
}
```

**Crowd Avoidance (Simple):**
- Use `Physics.OverlapSphere()` to check nearby enemies
- If too close, move away slightly (Random.insideUnitSphere)

---

### **6. Loot System**

**Loot Drop:**
```csharp
public class EnemyDamageReceiver : MonoBehaviour, IDamageReceiver
{
    public void TakeDamage(int damage)
    {
        health -= damage;
        if (health <= 0)
        {
            lootDropper.DropLoot(transform.position, enemyType);
            // ... death animation, effects
            gameObject.SetActive(false);  // pooling
        }
    }
}
```

**Loot Types:**
```csharp
public enum LootType { Scrap, Tech, HealthPack, RunUpgrade }

[System.Serializable]
public class LootDrop
{
    public LootType type;
    public int amount;
}
```

**Pickup (Magnet Radius):**
```csharp
public class LootPickup : MonoBehaviour
{
    void Update()
    {
        if (Vector3.Distance(transform.position, player.position) < magnetRadius)
        {
            // Float to player + collect
            transform.position = Vector3.Lerp(transform.position, player.position, 5f * Time.deltaTime);
        }
    }
}
```

---

### **7. Upgrade System (Run-local)**

**Upgrade Data:**
```csharp
[CreateAssetMenu]
public class UpgradeData : ScriptableObject
{
    public string upgradeName;
    public string description;
    public UpgradeType type;  // Damage, Speed, Armor, etc.
    public float value;        // magnitude of upgrade
}
```

**Selection UI:**
```csharp
public class UpgradeSelectionUI : MonoBehaviour
{
    // Shows 3 random upgrades every 5 minutes
    // Player clicks one → UpgradeApplier.Apply(upgrade)
    
    public void SelectUpgrade(UpgradeData upgrade)
    {
        upgradeManager.ApplyUpgrade(upgrade);
        this.gameObject.SetActive(false);
    }
}
```

**Application:**
```csharp
public class UpgradeApplier : MonoBehaviour
{
    public void Apply(UpgradeData upgrade)
    {
        if (upgrade.type == UpgradeType.Damage)
            weaponController.DamageMultiplier *= (1f + upgrade.value);
        else if (upgrade.type == UpgradeType.Speed)
            vehicleController.MaxSpeed *= (1f + upgrade.value);
        // ... etc
    }
}
```

---

### **8. Bounty System**

**Bounty Deck + Selection:**
```csharp
[CreateAssetMenu(menuName = "Game/Bounty/BountyData")]
public class BountyData : ScriptableObject
{
    public string bountyId;
    public string title;
    public BountyDifficulty difficulty;
    public string description;
    public List<RunModifier> modifiers;
    public List<BountyReward> rewards;
}

public enum BountyDifficulty { Easy, Medium, Hard, Brutal }
```

**Runtime Apply:**
```csharp
public class BountyModifierApplier : MonoBehaviour
{
    public void ApplyBounties(List<BountyData> selected)
    {
        foreach (var bounty in selected)
            ApplyModifiers(bounty.modifiers);
    }
}
```

---

### **9. Save/Meta System**

**On Run End:**
```csharp
public class RunSummaryManager : MonoBehaviour
{
    public void SaveRunAndReturnToHub()
    {
        RunData runData = new RunData
        {
            timeElapsed = hordeDirector.TimeElapsed,
            enemiesKilled = combatSystem.TotalKills,
            scrapEarned = lootSystem.ScrapCollected,
            techEarned = lootSystem.TechCollected,
        };
        
        saveSystem.SaveRun(runData);
        sceneManager.LoadScene("Hub");
    }
}
```

**On Hub Entry:**
```csharp
public class HubManager : MonoBehaviour
{
    void Start()
    {
        var lastRun = saveSystem.GetLastRun();
        uiController.ShowRunSummary(lastRun);
        
        metaProgress.AddScrap(lastRun.scrapEarned);
        metaProgress.AddTech(lastRun.techEarned);
        
        saveSystem.SaveMetaProgress(metaProgress);
    }
}
```

---

## 📐 Prefab Standard

**All Prefabs follow this structure:**

```
MyPrefab (Root)
├─ [Transform] Position, Rotation, Scale
├─ [Collider] For physics
├─ [Rigidbody] If physics-based
├─ Visuals (Child)
│  ├─ Mesh
│  ├─ Material
│  └─ Tint/Emissive (if needed)
├─ HP_* (Hardpoints, empty GameObjects)
│  ├─ HP_FirePoint
│  ├─ HP_CameraTarget
│  └─ HP_LootSpawn
├─ VFX_* (VFX Sub-Prefabs)
│  └─ VFX_ImpactSpark (Particle System, initially inactive)
└─ [Scripts]
   ├─ Main Controller
   └─ Event Handler
```

**Naming Conventions:**
- `HP_*` = Hardpoint (attach projectiles, cameras, effects)
- `VFX_*` = Visual Effect nodes
- `SFX_*` = Audio trigger points
- `LOD0, LOD1, LOD2` = Level-of-Detail meshes

---

**Nächster Schritt:** 05_DataModel_ScriptableObjects.md (Data Structure + SO Templates)
