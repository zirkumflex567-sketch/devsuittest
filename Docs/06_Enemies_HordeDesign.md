# 6️⃣ Horde Design: Enemy Roster & AI Behaviors

**Spawn-Regel (global):** Alle Gegner können grundsätzlich **überall in der Arena** spawnen (keine festen Kanten-Spawns).

---

## 🧟 Complete Enemy Roster (WMA-MVP + Expansion)

### **TIER 1: Early-Game (Waves 1–5)**

#### **1. Boar Grunt** (Humanoid Wildschwein)
- **Visual:** Stämmiger Boar-Humanoid, ~1.8m, grau/braun
- **Behavior:** Melee Chaser
- **Speed:** 5 m/s
- **Health:** 20 HP
- **Attack:** Melee ramming, 5 damage, 1.5s cooldown
- **Loot:** 1 Scrap, 5% Tech drop
- **AI:** Simple chase → melee attack range → ram
- **Special:** Knockback on hit (pushes player back slightly)

**Asset Source:** Free (tbd., later Sketchfab low-poly)

---

#### **2. Hyena Runner** (Dünner, Schnell)
- **Visual:** Hyänen-Humanoid, ~1.5m, grün/gelb mottled
- **Behavior:** Agile Melee Chaser
- **Speed:** 8 m/s (schnell)
- **Health:** 10 HP (fragil)
- **Attack:** Slashing claws, 3 damage, 0.8s cooldown
- **Loot:** 1 Scrap
- **AI:** Chase faster than Boar, uses circle-strafe patterns
- **Special:** Dies in 3–4 hits, but hard to hit due to speed

---

#### **3. Raven Swooper** (Fliegender Geier-Humanoid)
- **Visual:** Geier/Rabe-Humanoid, Wings, ~1.6m
- **Behavior:** Aerial Peck + Circle
- **Speed:** 6 m/s flight
- **Health:** 15 HP
- **Attack:** Peck (melee), 4 damage, 1.2s cooldown
- **Loot:** 1 Scrap + 1 Tech (10% rare drop)
- **AI:** Circles around player, dives for attack
- **Special:** Can fly over obstacles, harder to predict

---

### **TIER 2: Mid-Game (Waves 6–15)**

#### **4. Boar Brute** (Größer, Dicker)
- **Visual:** Riesiger Boar, ~2.2m, dickere Rüstung
- **Behavior:** Charge + Melee
- **Speed:** 4 m/s (langsam)
- **Health:** 40 HP
- **Attack:** Charge (3 sec wind-up) + AOE slam (8 damage, 20m range), melee (6 damage, 2s cooldown)
- **Loot:** 2 Scrap + 1 Tech (25% chance)
- **AI:** Long wind-up before charge, telegraphy clear
- **Special:** Knockback strong, damages via area effect

---

#### **5. Hyena Pack** (Gruppe von 2–3)
- **Visual:** 2–3 kleine Hyänen, linked visually
- **Behavior:** Coordinated rushes
- **Health:** 25 HP total (split across individuals)
- **Attack:** Combined melee swarm, 6 damage, 0.6s cooldown (fast, coordinated)
- **Loot:** 2 Scrap + 1 Tech
- **AI:** One leads (path), others follow; surround player
- **Special:** If one dies, others scatter briefly then regroup

---

#### **6. Venom Lurker** (Reptil-Humanoid)
- **Visual:** Schlangenartig/Reptiloid, grün/purple, ~1.7m
- **Behavior:** Hide + Spit Ranged
- **Speed:** 3 m/s (langsam)
- **Health:** 30 HP
- **Attack:** Spit projectile (toxic), 7 damage, 2s cooldown
- **Loot:** 2 Scrap + 2 Tech (35% chance)
- **AI:** Stays at range, hides behind objects if possible
- **Special:** Ranged attack telegraphed by color change

---

### **TIER 3: Late-Game (Waves 16+)**

#### **7. Boar Titan** (Elite Größe, Kopf der Welle)
- **Visual:** Massive Boar, ~2.8m, armored
- **Behavior:** Charge Slam + AOE Shockwave
- **Speed:** 2 m/s
- **Health:** 80 HP
- **Attack:** 
  - Slam (5s wind-up): 12 damage AOE, 30m radius
  - Melee: 8 damage, 1.5s cooldown
- **Loot:** 3 Tech + 1 Rare Upgrade drop
- **AI:** Charges only after clear telegraph, slam creates shockwave knockback
- **Special:** Stun-immune (thick skull), clear attack tells
- **Damage Type:** Kinetic/Blunt

---

#### **8. Plague Spreader** (Insekten-Humanoid)
- **Visual:** Chitinous insect-mutant, ~1.9m, purple/yellow
- **Behavior:** Projectile Swarm + Movement
- **Speed:** 5 m/s
- **Health:** 50 HP
- **Attack:** 3x projectile spray (parasite, 3 damage each), 1.2s cooldown
- **Loot:** 2 Tech + Poison Status Effect upgrade (10% chance)
- **AI:** Projectiles auto-spread on ground, doesn't require direct aim
- **Special:** Multi-projectile telegraphed by silhouette change

---

#### **9. Apex Predator** (Großkatze-Humanoid)
- **Visual:** Feline/Tiger-Humanoid, muscular, 2m
- **Behavior:** Agile Slashing + Dodge
- **Speed:** 7 m/s
- **Health:** 60 HP
- **Attack:** Multi-slash combo (2x swing), 5+5 damage, 0.9s between swings
- **Loot:** 3 Tech + guaranteed Rare drop
- **AI:** Dodges incoming fire 40% of time, does quick circles before attack
- **Special:** Quick recovery between attacks, hard to predict timing

---

### **SPECIAL: Goldgoblin** (Rare Spawn, ~1:300 ratio)

- **Visual:** Small goblin, shiny, coins visible on back, ~0.8m
- **Behavior:** Flees from player always
- **Speed:** 10 m/s (fastest)
- **Health:** 5 HP (one-shot)
- **Attack:** None (no damage dealt)
- **Loot:** 5x Tech + 10 Scrap + **Guaranteed Rare Upgrade**
- **AI:** Runs away immediately on spawn, tries to reach arena edge
- **Special:** No attack, but worth 5x normal rewards
- **Spawn:** Every ~300 enemies killed, random chance

---

## 🤖 AI State Machine (Generic)

```csharp
public enum EnemyState
{
    Idle,           // Waiting for detection
    Chase,          // Moving toward player
    MeleeAttack,    // In melee range, attacking
    RangedAttack,   // At range, firing projectiles
    Retreat,        // Fleeing (for special enemies)
    Dead,           // Destroyed, returning to pool
}

public class EnemyAI : MonoBehaviour
{
    private EnemyState currentState = EnemyState.Idle;
    private Transform playerTarget;
    private float nextAttackTime;
    private float detectionRange = 35f;
    
    void Update()
    {
        // State machine
        switch (currentState)
        {
            case EnemyState.Idle:
                if (CanSeePlayer())
                    TransitionTo(EnemyState.Chase);
                break;
                
            case EnemyState.Chase:
                MoveTowardPlayer();
                
                if (IsInMeleeRange())
                    TransitionTo(EnemyState.MeleeAttack);
                else if (IsInRangedRange() && data.useRangedAttack)
                    TransitionTo(EnemyState.RangedAttack);
                break;
                
            case EnemyState.MeleeAttack:
                if (!IsInMeleeRange())
                    TransitionTo(EnemyState.Chase);
                else if (Time.time >= nextAttackTime)
                    AttackMelee();
                break;
                
            case EnemyState.RangedAttack:
                if (IsInMeleeRange())
                    TransitionTo(EnemyState.MeleeAttack);
                else if (Time.time >= nextAttackTime)
                    AttackRanged();
                break;
                
            case EnemyState.Retreat:
                MoveAwayFromPlayer();
                if (Vector3.Distance(transform.position, playerTarget.position) > 50f)
                    TransitionTo(EnemyState.Chase);
                break;
        }
        
        // Crowd avoidance
        ApplyCrowdAvoidance();
    }
    
    private bool CanSeePlayer()
    {
        return Vector3.Distance(transform.position, playerTarget.position) <= detectionRange;
    }
    
    private void ApplyCrowdAvoidance()
    {
        Collider[] nearby = Physics.OverlapSphere(transform.position, 2f);
        foreach (var col in nearby)
        {
            if (col.CompareTag("Enemy") && col.gameObject != gameObject)
            {
                Vector3 away = (transform.position - col.transform.position).normalized;
                rigidbody.velocity += away * 0.5f;  // Push away gently
            }
        }
    }
}
```

---

## 🎯 Behavior Specifics

### **Melee Chaser (Boar Grunt, Hyena Runner)**
- Direct path toward player
- Attack when in range
- Simple linear movement
- Knockback on hit (victim pushed back, attacker slightly pushed forward)

### **Charge/Ram (Boar Brute, Boar Titan)**
- Detect player
- Play wind-up animation (3–5 sec)
- Visual telegraph (red glow, audio cue)
- Charge in straight line
- AOE impact on arrival
- Recovery time before next charge

### **Ranged (Venom Lurker, Plague Spreader)**
- Keep distance from player
- Fire projectiles at intervals
- Move sideways if too close
- Take cover behind props if possible (optional advanced)

### **Agile/Dodging (Apex Predator)**
- Chase with frequent direction changes
- 40% dodge chance when projectile detected
- Fast attacks with short recovery
- Circle player before attacking

### **Flying (Raven Swooper)**
- Altitude varies (2–5m above ground)
- Dive attack pattern (descend, attack, ascend)
- Can navigate around obstacles

### **Fleeing (Goldgoblin)**
- Run away immediately on detection
- Don't attack, just flee
- Prioritize reaching arena edge

---

## 📊 Enemy Balance Matrix (WMA-MVP)

| Enemy | HP | Speed | Damage | Behavior | Spawn Wave | Rarity |
|-------|----|----|--------|----------|-----------|--------|
| Boar Grunt | 20 | 5 | 5 | Chase | 1+ | 40% |
| Hyena Runner | 10 | 8 | 3 | Agile Chase | 1+ | 30% |
| Raven Swooper | 15 | 6 | 4 | Aerial | 1+ | 20% |
| Boar Brute | 40 | 4 | 8 | Charge | 6+ | 40% |
| Hyena Pack | 25 | 7 | 6 | Swarm | 6+ | 25% |
| Venom Lurker | 30 | 3 | 7 | Ranged | 6+ | 20% |
| Boar Titan | 80 | 2 | 12 | Elite Charge | 16+ | 10% |
| Plague Spreader | 50 | 5 | 9 | Swarm Projectile | 12+ | 15% |
| Apex Predator | 60 | 7 | 11 | Evasive | 16+ | 12% |
| Goldgoblin | 5 | 10 | 0 | Flee | Random | <0.5% |

---

## 🧩 Prompt Suite Enemy Cards (ENEMY_DESIGN_PROMPT)

**Boar Grunt**
- Role: Chaser
- HP: 20
- Movement Speed: 5 m/s
- Damage: 5
- Special Ability: Knockback ram
- Weakness: Kiting, slow effects
- Loot Drop: 1 Scrap, 5% Tech

**Hyena Runner**
- Role: Chaser
- HP: 10
- Movement Speed: 8 m/s
- Damage: 3
- Special Ability: Zig-zag sprint
- Weakness: Stun, freeze
- Loot Drop: 1 Scrap

**Raven Swooper**
- Role: Disruptor (Flyer)
- HP: 15
- Movement Speed: 6 m/s (flight)
- Damage: 4
- Special Ability: Dive attack
- Weakness: Predictable dive windows
- Loot Drop: 1 Scrap, 10% Tech

**Boar Brute**
- Role: Tank
- HP: 40
- Movement Speed: 4 m/s
- Damage: 8
- Special Ability: Wind-up charge slam
- Weakness: Telegraph window
- Loot Drop: 2 Scrap, 25% Tech

**Hyena Pack**
- Role: Chaser (Group)
- HP: 25 (total)
- Movement Speed: 7 m/s
- Damage: 6
- Special Ability: Pack surround
- Weakness: AoE damage
- Loot Drop: 2 Scrap, 1 Tech

**Venom Lurker**
- Role: Ranged
- HP: 30
- Movement Speed: 3 m/s
- Damage: 7
- Special Ability: Toxic spit projectile
- Weakness: Close-range pressure
- Loot Drop: 2 Scrap, 2 Tech

**Plague Spreader**
- Role: Ranged
- HP: 50
- Movement Speed: 5 m/s
- Damage: 9
- Special Ability: Swarm spray
- Weakness: Interrupts, stun
- Loot Drop: 2 Tech, 10% Poison upgrade

**Apex Predator**
- Role: Elite Chaser
- HP: 60
- Movement Speed: 7 m/s
- Damage: 11
- Special Ability: Dodge + double slash
- Weakness: Predictable dodge timing
- Loot Drop: 3 Tech, guaranteed Rare

**Goldgoblin**
- Role: Flee
- HP: 5
- Movement Speed: 10 m/s
- Damage: 0
- Special Ability: Escape sprint
- Weakness: Any hit
- Loot Drop: 5x Tech, 10 Scrap, guaranteed Rare

---

## ⚙️ Reactive Enemies (ENEMY_DESIGN_REACTIVE_PROMPT)

**Boar Brute**
- Visual Identity: Heavy plate shoulders, spiked collar, thick tusks
- Role: Tank
- Special Mechanic: If charmed, breaks charm with a roar and gains +15% speed for 3s
- Armor / Weak Points: Heavy front armor, weak rear
- Death Effect: Short shockwave knockback

**Venom Lurker**
- Visual Identity: Toxic sacs, thin tail, green glow
- Role: Ranged
- Special Mechanic: Buff-heavy players trigger extra spit volley (cooldown 8s)
- Armor / Weak Points: Exposed back sacs
- Death Effect: Toxic puddle (2s)

**Hyena Pack**
- Visual Identity: Linked chain collar, small scavenger masks
- Role: Chaser
- Special Mechanic: Magnet/Drone control forces pack to spread for 2s
- Armor / Weak Points: None, fragile units
- Death Effect: Scatter burst (brief fear)

---

## 🛡️ Elite Variants (ELITE_ENEMY_PROMPT)

**Elite Boar Brute**
- Visual Description: Reinforced shoulder plates, hanging chains, glowing tusk tips
- Armor Logic: Front armor reduces damage by 30%
- Unique Ability: Double-charge with short pause

**Elite Venom Lurker**
- Visual Description: Toxic tank on back, green tube veins, mask visor
- Armor Logic: Back tank is weak spot (takes +50% damage)
- Unique Ability: Poison cloud on hit (1.5s)

**Elite Apex Predator**
- Visual Description: Carbon blades on arms, bright eye glow, spine plates
- Armor Logic: Light armor on head, weak tail core
- Unique Ability: Dash-through slash, leaves bleeding trail

---

## 🏆 Elite & Special Mechanics

### **Elite Variant (any enemy, 2–5% spawn rate)**
- **Visual:** Larger, different color, particle aura
- **Stat Boost:** 1.5x HP, 1.3x Damage, 1.2x Speed
- **Loot:** 3x normal drops
- **Behavior:** More aggressive, tighter pattern

### **Goldgoblin (special 1:300 spawn)**
- Reward-focused, no combat threat
- Unique visual (shiny, coins)
- 5x loot drop
- Guaranteed rare upgrade on kill

---

**Nächster Schritt:** 07_HordeDirector_Waves.md (Spawn Rules, Difficulty Curve)
