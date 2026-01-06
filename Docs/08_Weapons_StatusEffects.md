# 🔫 8. Weapons & Status Effects System

---

## 🎯 Vehicle-Mounted Weapon Roster (6 Concepts)

**WMA Rule:** All weapons are vehicle-mounted, improvised, and scrap-built. No handheld weapons.

### **Plasma Repeater Turret**
**Weapon Overview**
- Name: Plasma Repeater Turret
- Mount Position: Roof
- Weapon Class: Primary
- Core Fantasy: A patched turret that never stops spitting hot plasma.

**Base Stats**
- Fire Rate: 9 shots/sec
- Damage: 18 per hit
- Effective Range: Long (80m)
- Area of Effect: None
- Ammo / Overheat Logic: Infinite, builds heat after 4s (0.5s cooldown pause)

**Special Mechanic**
- While vehicle is moving above 60% speed, every 6th hit on same target deals +40% damage.

**Synergies**
- Upgrades: Fire Rate, Crit Chance
- Weapon Synergy: Arc Thrower Side Emitter (clear pack, turret focuses elite)
- Enemy Interaction: Good vs elites due to stacking bonus.

**Mods (3)**
- Capacitor Loop: +10% fire rate, -8% damage.
- Punch-Through Coils: Shots pierce 1 target, -10% crit chance.
- Welded Radiator: Heat buildup -20%, -5% move speed (added weight).

**Lore Snippet**
It started as a rooftop AC unit. Now it hums like a shrine and cooks anything in line. Drivers call it the \"roof kiln\" and trust it more than brakes.

---

### **Scrap Shotgun Front Cannon**
**Weapon Overview**
- Name: Scrap Shotgun Front Cannon
- Mount Position: Front
- Weapon Class: Secondary
- Core Fantasy: A nose-mounted blast of bolted junk for point-blank clears.

**Base Stats**
- Fire Rate: 1.6 shots/sec (0.6s cooldown)
- Damage: 7 pellets x 22 = 154 max
- Effective Range: Short (18m)
- Area of Effect: Small cone
- Ammo / Overheat Logic: Limited (24 shells, regen 4/sec out of combat)

**Special Mechanic**
- Recoil pushes the vehicle back slightly (readable bump) and briefly slows steering.

**Synergies**
- Upgrades: AoE Size, Status Chance (Freeze/Burn)
- Weapon Synergy: Junk Grenade Roof Launcher (blast then finish survivors)
- Enemy Interaction: Strong vs packs and unarmored swarms.

**Mods (3)**
- Wide Choke: +20% cone size, -15% pellet damage.
- Slug Swap: 1 slug at 90 damage, +30% range, loses stagger.
- Scrapload: +2 pellets, +10% recoil (riskier at speed).

**Lore Snippet**
It fires whatever fits the pipe. Bolts, teeth, coins, and once a wedding ring. Nobody asks whose ring it was.

---

### **Arc Thrower Side Emitter**
**Weapon Overview**
- Name: Arc Thrower Side Emitter
- Mount Position: Side
- Weapon Class: Primary
- Core Fantasy: Side-mounted coils that chain shocks through tight packs.

**Base Stats**
- Fire Rate: 3 shots/sec
- Damage: 26 initial, 16 chained
- Effective Range: Medium (35m)
- Area of Effect: Chain 2 additional targets
- Ammo / Overheat Logic: Regen battery (40 charges, regen 6/sec)

**Special Mechanic**
- Chains prefer targets on the vehicle's moving side (turning into crowds increases chains).

**Synergies**
- Upgrades: Status Chance (Shock/Slow), AoE Size
- Weapon Synergy: Plasma Repeater Turret (strip packs, focus single)
- Enemy Interaction: Excellent vs grouped enemies, weaker vs lone targets.

**Mods (3)**
- Forked Arc: +1 chain target, -10% damage.
- Grounded Coils: Chain range +25%, -15% fire rate.
- Static Bite: +10% crit chance, -20% battery regen.

**Lore Snippet**
The side coils were welded on after a generator accident. Now the sparks are on purpose, and nobody rides beside it unless they like their teeth chattering.

---

### **Junk Grenade Roof Launcher**
**Weapon Overview**
- Name: Junk Grenade Roof Launcher
- Mount Position: Roof
- Weapon Class: Secondary
- Core Fantasy: A roof rack that lobs rattling scrap grenades into crowds.

**Base Stats**
- Fire Rate: 0.9 shots/sec (1.1s cooldown)
- Damage: 110 impact, 60 splash
- Effective Range: Medium (30m)
- Area of Effect: 4m radius
- Ammo / Overheat Logic: Limited (12 grenades, regen 1/sec)

**Special Mechanic**
- Grenades bounce once; timing depends on vehicle speed (faster = longer arc).

**Synergies**
- Upgrades: AoE Size, Status Chance (Burn)
- Weapon Synergy: Scrap Shotgun Front Cannon (crowd soften, close finish)
- Enemy Interaction: Strong vs crowds, soft vs fast dodgers.

**Mods (3)**
- Sticky Glue: Grenades stick to first target, -20% splash radius.
- Scatter Can: +2 mini grenades, -30% damage each.
- Hot Reload: +25% regen rate, -10% impact damage.

**Lore Snippet**
It is a roof rack with a bad attitude. The grenades are old cans packed with nails and regret. The fact that it still fires is a miracle.

---

### **Venom Sprayer Front Nozzle**
**Weapon Overview**
- Name: Venom Sprayer Front Nozzle
- Mount Position: Front
- Weapon Class: Primary
- Core Fantasy: A pressure sprayer that melts armor with poison mist.

**Base Stats**
- Fire Rate: 12 ticks/sec
- Damage: 6 per tick + 12 DPS poison
- Effective Range: Short (12m)
- Area of Effect: Narrow cone
- Ammo / Overheat Logic: Fuel tank (100 units, regen 8/sec)

**Special Mechanic**
- Poison stacks up to 3; ramming during spray adds +1 stack (readable splatter).

**Synergies**
- Upgrades: Status Chance, Damage Over Time
- Weapon Synergy: Rail Beam Roof Cannon (mark target, beam finish)
- Enemy Interaction: Strong vs tanks/elites, weaker vs flyers.

**Mods (3)**
- Wide Nozzle: +25% cone, -10% poison DPS.
- Corrosive Mix: +1 max poison stack, -15% base damage.
- Pressure Burst: First 2s +20% damage, then -10% (timing risk).

**Lore Snippet**
It used to water crops. Now it waters graves. The smell lingers, so nobody parks too close.

---

### **Rail Beam Roof Cannon**
**Weapon Overview**
- Name: Rail Beam Roof Cannon
- Mount Position: Roof
- Weapon Class: Special
- Core Fantasy: A welded rail cannon that cuts a straight line through chaos.

**Base Stats**
- Fire Rate: 0.6 shots/sec (1.6s cooldown)
- Damage: 220 per beam
- Effective Range: Long (90m)
- Area of Effect: Piercing line (1.5m width, 3 targets)
- Ammo / Overheat Logic: Limited (8 shots, regen 0.5/sec)

**Special Mechanic**
- 0.4s charge wind-up; steering during charge widens aim drift.

**Synergies**
- Upgrades: Crit Damage, Fire Rate (cooldown), AoE Line Width
- Weapon Synergy: Venom Sprayer Front Nozzle (marking targets for beam)
- Enemy Interaction: Great vs elites and lined-up packs.

**Mods (3)**
- Rapid Capacitor: -20% cooldown, -15% damage.
- Overcharge Prism: +35% damage, +0.2s charge time.
- Wide Beam: +0.5m width, -1 pierce count.

**Lore Snippet**
It started as a crane rail and a dare. The recoil bends axles, but the beam makes problems disappear in a single, clean line. Clean is rare out here.

---

## 🧪 Run-Buff Übersicht (WMA, grob)

**Offense**
- Damage +X%
- Fire Rate +X%
- Crit Chance +X% / Crit Damage +X%
- Projectile Count +1 (Scrap Shotgun style)
- Status Chance +X% (Freeze/Burn/Poison)

**Defense**
- Max HP +X
- Armor +X
- HP Regen +X/s
- Temporary Shield (on pickup / on kill)

**Mobility**
- Move Speed +X%
- Turn Rate +X%
- Dash Cooldown -X% (falls Dash vorhanden)

**Utility**
- Loot Magnet Radius +X
- Scrap/Tech Gain +X%
- Pickup Vacuum Speed +X%

**Signature / Skill**
- Signature Cooldown -X%
- Signature Uses +1 (selten, capped)
- Skill Tree Node Bonus (branch-spezifisch)

---

## 🧩 Beispiel-Upgrades (UPGRADE_PROMPT)

**Upgrade Name:** Rapid Fire
**Effect:** Feuerrate erhoehen
**Numeric Values:** +15% Fire Rate
**Synergies:** Secco-Toast, Scrap Shotgun Front Cannon

**Upgrade Name:** Armor Plating
**Effect:** Ruestung erhoehen
**Numeric Values:** +10 Armor
**Synergies:** Marek Bollwerk

**Upgrade Name:** Magnet Core
**Effect:** Pickup Radius groesser
**Numeric Values:** +20% Pickup Radius
**Synergies:** Schrottkern, Loot-Magnet

**Upgrade Name:** Critical Bloom
**Effect:** Crit Chance erhoehen
**Numeric Values:** +6% Crit Chance
**Synergies:** Chrom-Overclock

**Upgrade Name:** Frost Bite
**Effect:** Freeze Chance erhoehen
**Numeric Values:** +12% Freeze Chance
**Synergies:** Kiting, Boss-Dodge windows

**Upgrade Name:** Shock Burst
**Effect:** AoE auf Kill
**Numeric Values:** 20% Weapon Damage im 3m Radius
**Synergies:** Glanzkoller, AoE Builds

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
    public string weaponName = "Plasma Repeater Turret";
    public Sprite weaponIcon;
    public int weaponId = 0;
    public WeaponMount mount = WeaponMount.Roof;
    
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
public enum WeaponMount { Front, Roof, Side, Rear }
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
    ShotgunSpread,      // +5% pellet spread (Scrap Shotgun coverage)
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

## 📊 Weapon Balance Matrix (WMA)

| Weapon | Damage | Fire Rate / CD | Range | Ammo | Role |
|--------|--------|----------------|-------|------|------|
| **Plasma Repeater Turret** | 18 | 9/sec | 80m | Infinite (heat) | Sustained |
| **Scrap Shotgun Front Cannon** | 154 max | 1.6/sec | 18m | 24 (regen) | Burst |
| **Arc Thrower Side Emitter** | 26 + chain | 3/sec | 35m | 40 (regen) | Chain |
| **Junk Grenade Roof Launcher** | 110 + 60 | 0.9/sec | 30m | 12 (regen) | AoE |
| **Venom Sprayer Front Nozzle** | 6 + DOT | 12 ticks/sec | 12m | 100 (regen) | DOT |
| **Rail Beam Roof Cannon** | 220 | 0.6/sec | 90m | 8 (regen) | Pierce |

---

**Nächster Schritt:** 09_UI_UX.md (HUD, Menus, Screens)
