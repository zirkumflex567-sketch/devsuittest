# 🔫 8. Weapons & Status Effects System

---

## 🎯 WMA-MVP Weapon Roster (2–3 Types)

### **Weapon 1: Plasma Rifle** (Primary - Auto)
- **Firing Mode:** Full auto
- **Fire Rate:** 10 shots/second
- **Damage:** 20 per hit
- **Projectile Speed:** 50 m/s
- **Range:** 100m (unlimited)
- **Ammo:** Infinite (energy-based)
- **Recoil:** Slight (2 pixels screen bounce)
- **VFX:** Orange/cyan plasma bolt
- **SFX:** High-pitched laser zap
- **Unlock:** Available from start

### **Weapon 2: Shotgun** (Secondary - Manual)
- **Firing Mode:** Single shot, manual trigger
- **Fire Rate:** 2 shots/second (0.5s cooldown)
- **Damage:** 50 per pellet, 5 pellets = 250 total
- **Projectile Count:** 5 pellets (spread pattern)
- **Projectile Speed:** 40 m/s
- **Range:** 30m (pellets spread over distance)
- **Ammo:** 30 shots, regen 5/sec when not firing
- **Recoil:** Strong (screen push back)
- **VFX:** Red explosion on impact
- **SFX:** Heavy boom
- **Unlock:** Available from start

### **Weapon 3 (Optional): Sniper/Beam** (Prestige - Manual)
- **Firing Mode:** Hitscan (instant, no projectile)
- **Fire Rate:** 1 shot/second (1s cooldown)
- **Damage:** 100 per shot
- **Range:** Unlimited (raycast through scene)
- **Ammo:** 20 shots, slow regen (1/sec)
- **Recoil:** Extreme (camera shake)
- **VFX:** Blue beam + impact point
- **SFX:** Deep laser pulse
- **Unlock:** Unlock via meta progression (50 Tech)

---

## ⚡ Status Effects (Optional MVP, Important Later)

### **Effect 1: Freeze**
```csharp
public class FreezeEffect : StatusEffect
{
    public float speedReduction = 0.3f;  // 70% slow
    public float duration = 5f;
    public Color tintColor = Color.cyan;
    public ParticleSystem frozenParticles;
}

// Application:
// Enemy hit by frozen projectile → Apply Freeze
// Freezes movement completely after 2 stacks
// Visual: Blue tint + ice particles
```

### **Effect 2: Burn**
```csharp
public class BurnEffect : StatusEffect
{
    public float damagePerTick = 5f;
    public float tickInterval = 0.5f;
    public float duration = 8f;
    public Color tintColor = Color.yellow;
}

// Application: Pyro weapon upgrade
// Deals damage over time
// Visual: Orange/red tint + flame particles
```

### **Effect 3: Poison**
```csharp
public class PoisonEffect : StatusEffect
{
    public float damageMultiplier = 1.5f;  // Take more damage
    public float duration = 6f;
    public Color tintColor = Color.green;
}

// Application: Venom Lurker projectiles (base game)
// Take amplified damage while poisoned
// Visual: Green tint + cloud particles
```

---

## 🛠️ Weapon Data Structure (ScriptableObject)

```csharp
[CreateAssetMenu(menuName = "Game/Weapon/WeaponData")]
public class WeaponData : ScriptableObject
{
    [Header("Identity")]
    public string weaponName = "Plasma Rifle";
    public Sprite weaponIcon;
    public int weaponId = 0;
    
    [Header("Firing")]
    public float fireRate = 10f;            // shots per second
    public float damagePerShot = 20f;
    public FireModeType fireMode = FireModeType.FullAuto;
    
    [Header("Projectile")]
    public bool isProjectile = true;
    public float projectileSpeed = 50f;
    public int projectileCount = 1;         // for shotgun
    public float projectileSpread = 0f;     // radians
    public float projectileLifetime = 5f;
    public GameObject projectilePrefab;
    
    [Header("Hitscan (if applicable)")]
    public bool useHitscan = false;
    public float hitscanRange = 100f;
    
    [Header("Ammo")]
    public float ammoCapacity = 100f;
    public float ammoRegenRate = 5f;        // per second, 0 = no regen
    
    [Header("Effects")]
    public float recoil = 2f;               // screen shake magnitude
    public float knockback = 0f;            // to player
    public VFXData muzzleFlashVFX;
    public SFXData fireSoundEffect;
    
    [Header("Status Effects")]
    public StatusEffectData statusEffectOnHit;  // optional
    public float statusEffectChance = 0f;       // 0–1
    
    [Header("Upgradeable")]
    public float damageMultiplier = 1f;     // dynamic upgrade
    public float fireRateMultiplier = 1f;   // dynamic upgrade
    
    [Header("Unlock")]
    public int metaScrapCost = 0;           // 0 = available from start
    public int metaTechCost = 0;
}

public enum FireModeType { FullAuto, SingleShot, BurstFire, Hitscan }
```

---

## 🎯 Weapon Upgrade System

**Upgrades that affect weapons:**

```csharp
// Data-driven upgrades
public enum WeaponUpgradeType
{
    DamageBoost,        // +10% damage
    FireRateBoost,      // +15% fire rate
    ProjectileSpeed,    // +20% projectile speed
    AmmoCapacity,       // +50 ammo (flat)
    StatusEffectChance, // +10% proc chance
    ShotgunSpread,      // +5% pellet spread (more coverage)
}

// Application example:
public class UpgradeApplier
{
    public void ApplyWeaponUpgrade(WeaponData weapon, UpgradeData upgrade)
    {
        switch(upgrade.upgradeType)
        {
            case WeaponUpgradeType.DamageBoost:
                weapon.damageMultiplier *= 1.1f;
                break;
            case WeaponUpgradeType.FireRateBoost:
                weapon.fireRateMultiplier *= 1.15f;
                break;
            // ... etc
        }
    }
}
```

---

## 💥 Projectile System

```csharp
public class Projectile : MonoBehaviour
{
    public Vector3 velocity;
    public float damage;
    public float lifetime;
    private float spawnTime;
    
    public void Initialize(Vector3 direction, float speed, float dmg)
    {
        velocity = direction.normalized * speed;
        damage = dmg;
        spawnTime = Time.time;
    }
    
    void Update()
    {
        // Move projectile
        transform.Translate(velocity * Time.deltaTime, Space.World);
        
        // Check lifetime
        if (Time.time - spawnTime > lifetime)
            ReturnToPool();
        
        // Check collision
        if (Physics.SphereCast(transform.position, 0.1f, velocity.normalized, 
            out RaycastHit hit, velocity.magnitude * Time.deltaTime))
        {
            IDamageReceiver dmgReceiver = hit.collider.GetComponent<IDamageReceiver>();
            if (dmgReceiver != null)
            {
                dmgReceiver.TakeDamage((int)damage);
                OnHit(hit);
                ReturnToPool();
            }
        }
    }
    
    void OnHit(RaycastHit hit)
    {
        // VFX at impact
        Instantiate(impactVFX, hit.point, Quaternion.identity);
        // SFX at impact
        audioSystem.PlaySFX("impact", hit.point);
    }
    
    void ReturnToPool()
    {
        gameObject.SetActive(false);  // pooling
    }
}
```

---

## 🏗️ Architecture Integration

### **WeaponController (in VehicleController)**
```csharp
public class WeaponController : MonoBehaviour
{
    private WeaponData[] weapons = new WeaponData[2];  // Primary + Secondary
    private float[] ammoRemaining = new float[2];
    private float[] lastFireTime = new float[2];
    
    public void Fire(int weaponSlot, Vector3 direction)
    {
        WeaponData weapon = weapons[weaponSlot];
        
        // Check fire rate
        if (Time.time - lastFireTime[weaponSlot] < 1f / (weapon.fireRate * weapon.fireRateMultiplier))
            return;
        
        // Check ammo
        if (weapon.ammoCapacity > 0 && ammoRemaining[weaponSlot] <= 0)
            return;
        
        lastFireTime[weaponSlot] = Time.time;
        
        if (weapon.useHitscan)
            FireHitscan(weapon, direction);
        else
            FireProjectile(weapon, direction);
        
        combatEvents.OnWeaponFired?.Invoke(weapon);
    }
    
    void FireProjectile(WeaponData weapon, Vector3 direction)
    {
        for (int i = 0; i < weapon.projectileCount; i++)
        {
            Vector3 spreadDir = Quaternion.AngleAxis(
                Random.Range(-weapon.projectileSpread, weapon.projectileSpread),
                Vector3.up
            ) * direction;
            
            Projectile proj = projectilePool.Get();
            proj.Initialize(spreadDir, weapon.projectileSpeed, 
                            weapon.damagePerShot * weapon.damageMultiplier);
        }
        
        ammoRemaining[weaponSlot] -= 1;
    }
}
```

---

## 📋 Status Effect Application

```csharp
public interface IStatusEffectTarget
{
    void ApplyStatusEffect(StatusEffectData effect);
    void RemoveStatusEffect(EffectType effectType);
}

public class Enemy : MonoBehaviour, IStatusEffectTarget
{
    private Dictionary<EffectType, float> activeEffects = new();
    
    public void ApplyStatusEffect(StatusEffectData effect)
    {
        if (activeEffects.ContainsKey(effect.type))
        {
            // Stack or reset
            activeEffects[effect.type] = effect.duration;
        }
        else
        {
            activeEffects[effect.type] = effect.duration;
            StartCoroutine(ApplyEffectOverTime(effect));
        }
    }
    
    IEnumerator ApplyEffectOverTime(StatusEffectData effect)
    {
        float elapsed = 0;
        while (elapsed < effect.duration)
        {
            // Apply stat changes
            if (effect.type == EffectType.Freeze)
                movementSpeed *= 0.3f;
            else if (effect.type == EffectType.Burn)
                health -= effect.damagePerTick;
            
            // Visual feedback
            GetComponent<Renderer>().material.color = effect.tintColor;
            
            yield return new WaitForSeconds(0.5f);
            elapsed += 0.5f;
        }
        
        // Remove effect
        activeEffects.Remove(effect.type);
        GetComponent<Renderer>().material.color = Color.white;
    }
}
```

---

## 🎵 SFX Data Structure

```csharp
[System.Serializable]
public class SFXData
{
    public AudioClip clip;
    public float volume = 1f;
    public float pitch = 1f;
    public bool useRandomPitch = true;
    public float pitchVariance = 0.1f;
}
```

---

## 📊 Weapon Balance Matrix (WMA-MVP)

| Weapon | Damage | Fire Rate | Range | Ammo | Difficulty |
|--------|--------|-----------|-------|------|-----------|
| **Plasma Rifle** | 20 | 10/sec | 100m | Infinite | Beginner |
| **Shotgun** | 250 (5x50) | 2/sec | 30m | 30 | Intermediate |
| **Sniper** (unlock) | 100 | 1/sec | ∞ | 20 | Advanced |

---

**Nächster Schritt:** 09_UI_UX.md (HUD, Menus, Screens)
