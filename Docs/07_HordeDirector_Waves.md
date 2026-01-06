# 7️⃣ Horde Director: Waves & Difficulty Curve

---

## 🌊 Wave Progression System

**Goal:** Smooth difficulty ramp, player has time to adjust but never gets bored.
**Endless:** Schwierigkeit skaliert nach Wave 15 weiter (kein Hard-Cap).

### **Wave Structure**

```csharp
[System.Serializable]
public class Wave
{
    public int waveNumber;
    public float durationSeconds = 120f;        // Wave lasts 2 min
    public float spawnBudget = 50f;             // Total "cost" of enemies
    public List<EnemySpawnRule> spawnRules;     // What to spawn
    public float difficulty = 1.0f;             // Stat multiplier
    public float restPhaseDuration = 30f;       // Before next wave
}
```

### **WMA-MVP Wave Progression (15 waves)**

| Wave | Duration | Enemy Composition | Difficulty | Note |
|------|----------|-------------------|-----------|------|
| 1 | 60s | 60% Grunt, 40% Runner | 1.0x | Tutorial friendly |
| 2 | 60s | 50% Grunt, 30% Runner, 20% Swooper | 1.0x | Introduce flying |
| 3 | 90s | 40% Grunt, 40% Runner, 20% Swooper | 1.1x | Speed up |
| 4 | 90s | 30% Grunt, 30% Runner, 30% Swooper | 1.15x | Even split |
| 5 | 120s | 20% Grunt, 40% Runner, 30% Swooper, 10% Brute | 1.2x | First heavy unit |
| 6 | 120s | Mixed (no Grunt), 25% Brute, 20% Pack | 1.25x | Escalation |
| 7 | 120s | 20% Brute, 20% Pack, 20% Lurker, 20% Swooper | 1.3x | Ranged intro |
| 8 | 150s | Balanced mid-game mix | 1.35x | Challenging |
| 9 | 150s | 30% Brute, 30% Lurker, 20% Pack | 1.4x | Pressure |
| 10 | 150s | Elite Spawns 5%, all previous types | 1.45x | Elite intro |
| 11 | 180s | 25% Titan telegraph, mixed heavy | 1.5x | Boss-like pressure |
| 12 | 180s | Plague Spreader intro, 20% spawn rate | 1.55x | New mechanic |
| 13 | 180s | 30% Apex Predator, mixed elite | 1.6x | High skill |
| 14 | 180s | All types, high elite rate 10% | 1.65x | Intense |
| 15+ | 180s | Infinite loop, scaling | +0.1x per 10 min | Endless |

---

## 👑 Endboss (WMA)

- **Spawn:** Nach der Extraction-Phase (kurz nach 15 Min) oder als Trigger vor Win
- **Telegraph:** Klare Vorwarnung pro Fähigkeit (Audio + VFX)
- **Dodge-Fokus:** Fähigkeiten sind ausweichbar (Dash/Steering)
- **Ziel:** Skill-Test, nicht Bullet-Sponging

---

## 👹 End Boss Variants (END_BOSS_PROMPT)

**Boss Variant Theme:** Fire
Boss Name: Ash-Titan
Visual Skin Description: Glowing cracks, ember plates, smoke vents (stylized, no realistic fire)
Arena Presence: Large, stomping, slow turns
Phase Mechanics: Phase 1 ground slams, Phase 2 flame arcs, Phase 3 burn aura
Signature Attacks: Ember ring pulse, forward flame sweep, ground fissure
Weakness: Stun windows after slam

**Boss Variant Theme:** Poison
Boss Name: Mire-King
Visual Skin Description: Toxic sacs, green haze, bone mask, dripping tubes
Arena Presence: Medium speed, wide strafes
Phase Mechanics: Phase 1 spit volleys, Phase 2 poison pools, Phase 3 summon adds
Signature Attacks: Triple spit fan, poison puddle trail, toxic burst
Weakness: Back sacs pop for extra damage

**Boss Variant Theme:** Chrome
Boss Name: Chrome Jugger
Visual Skin Description: Mirror plates, chrome cables, neon seams
Arena Presence: Fast dashes, sharp pivots
Phase Mechanics: Phase 1 dash strikes, Phase 2 reflect shield, Phase 3 shock pulses
Signature Attacks: Dash line slash, reflect bubble, radial shock
Weakness: Shield drops after 2 hits from behind

---

## 🎲 Spawn Rules (Data-Driven)

```csharp
[System.Serializable]
public class EnemySpawnRule
{
    public EnemyData enemyType;
    public int targetCount = 10;              // Spawn up to N of this type
    public float spawnRate = 1f;              // Enemies per second
    public float spawnIntervalVariance = 0.2f; // Random variation
    public bool groupSpawn = false;           // Spawn in clusters?
    public int groupSize = 3;
    public float difficulty = 1.0f;           // Wave-local multiplier
}
```

**Spawn-Positions:** Gegner können überall innerhalb der Arena-Volume spawnen (nicht nur am Rand).

---

## 📈 Difficulty Scaling

### **Per-Wave Multipliers**

```csharp
public class DifficultyScaler
{
    public static void ApplyWaveDifficulty(Enemy enemy, Wave wave)
    {
        enemy.stats.health = Mathf.RoundToInt(enemy.data.healthBase * wave.difficulty);
        enemy.stats.damage = Mathf.RoundToInt(enemy.data.damage * wave.difficulty);
        enemy.stats.speed = enemy.data.movementSpeed * Mathf.Sqrt(wave.difficulty);
    }
}
```

**Why Sqrt for speed?** Movement scales less aggressively than damage.

### **Per-Minute Escalation (Beyond Wave 15)**

```csharp
public float GetDifficultyAtTime(float elapsedMinutes)
{
    if (currentWave < 15)
        return waves[currentWave].difficulty;
    
    // After wave 15: +0.1x every 10 minutes
    float minutesAfterWave15 = elapsedMinutes - 15f * 2f;
    return 1.65f + (minutesAfterWave15 / 10f) * 0.1f;
}
```

---

## 🧟 Elite Spawn Rules

### **Elite Chance Calculation**

```csharp
public bool TrySpawnElite(int wave)
{
    if (wave < 10) return false;  // No elites before wave 10
    
    float baseChance = 0.05f;     // 5%
    float escalation = (wave - 10f) * 0.01f;  // +1% per wave
    float finalChance = Mathf.Min(baseChance + escalation, 0.25f); // Cap at 25%
    
    return Random.value < finalChance;
}
```

### **Elite Visual Indicator**
- Larger model
- Glowing aura (particle effect)
- Audio cue on spawn
- Name tag: "[ELITE] Boar Brute"

---

## 🪙 Goldgoblin Spawn Rules

```csharp
public bool TrySpawnGoldgoblin(int totalEnemiesKilled)
{
    // ~1 Goldgoblin per 300 enemies
    float chance = 1f / 300f;  // ~0.33%
    
    // Boost chance if player is doing well (hasn't died, high score)
    if (playerStats.timeAlive > 600f)  // 10+ min
        chance *= 1.2f;
    
    return Random.value < chance;
}

// Spawn location: Random position inside arena
public Vector3 GetGoldgoblinSpawnPos()
{
    Vector2 circle = Random.insideUnitCircle * arenaRadius;
    return arenaCenter + new Vector3(circle.x, 0f, circle.y);
}
```

---

## ⏰ Wave Timing & Rest Phases

```csharp
public enum HordeState
{
    Idle,           // Waiting for wave to start
    WaveActive,     // Enemies spawning
    WaveComplete,   // All enemies dead, waiting for rest
    RestPhase,      // Player downtime, UI shows timer
    BossPrep,       // Before special waves
}

public class WaveManager : MonoBehaviour
{
    private float waveStartTime;
    private float waveEndTime;
    private float restStartTime;
    private float restDuration = 30f;
    
    void Update()
    {
        switch (state)
        {
            case HordeState.WaveActive:
                if (Time.time >= waveEndTime && AllEnemiesDead())
                {
                    state = HordeState.WaveComplete;
                    restStartTime = Time.time;
                }
                break;
                
            case HordeState.WaveComplete:
                if (Time.time >= restStartTime + restDuration)
                    AdvanceWave();
                break;
        }
    }
}
```

---

## 🎁 Upgrade Offer Timing

**Every 5 minutes or after wave complete (whichever first), show upgrade screen:**

```csharp
public void CheckForUpgradeOffer()
{
    bool timeElapsed = Time.time - lastUpgradeTime >= 300f;  // 5 min
    bool waveJustComplete = state == HordeState.WaveComplete;
    
    if (timeElapsed || waveJustComplete)
    {
        ShowUpgradeSelectionUI(3);  // Pick 3 from random pool
        lastUpgradeTime = Time.time;
    }
}
```

---

## 📍 Extraction Point Mechanics

```csharp
public class ExtractionManager : MonoBehaviour
{
    private float extractionSpawnTime = 900f;  // 15 minutes
    private bool extractionSpawned = false;
    private Vector3 extractionPoint;
    
    void Update()
    {
        if (!extractionSpawned && Time.time >= extractionSpawnTime)
        {
            SpawnExtractionPoint();
            extractionSpawned = true;
        }
    }
    
    private void SpawnExtractionPoint()
    {
        // Spawn at random edge or center
        extractionPoint = arenaCenter + Random.insideUnitSphere * 40f;
        
        // Visual beacon (glowing circle, particle effect)
        GameObject beacon = Instantiate(extractionBeaconPrefab, extractionPoint, Quaternion.identity);
        beacon.GetComponent<AudioSource>().PlayOneShot(extractionSpawnSFX);
    }
    
    public bool CheckIfPlayerInExtractionZone(Vector3 playerPos)
    {
        return Vector3.Distance(playerPos, extractionPoint) < 5f;
    }
}
```

---

## 🎯 Difficulty Curves (Visual Reference)

```
Difficulty Over Time (WMA-MVP)

Difficulty
    |
  1.7 |                    /.../  (escalating beyond wave 15)
  1.6 |                  /
  1.5 |                /      
  1.4 |              /
  1.3 |            /
  1.2 |          /
  1.1 |        /
  1.0 |______/________________
      0     5     10    15    20+ Minutes
      (Waves 1–15+)
```

**Characteristics:**
- Smooth ramp, no sudden spikes
- Wave 5–6 noticeably harder (new heavy units)
- Wave 10 noticeable (elites introduced)
- After 15 min: soft difficulty cap, but endless scaling possible

---

## 🔄 Coop Scaling

```csharp
public float GetCoopDifficultyMultiplier(int playerCount)
{
    if (playerCount == 1) return 1.0f;
    if (playerCount == 2) return 1.3f;  // 30% more enemies
    if (playerCount == 3) return 1.6f;  // (future)
    if (playerCount == 4) return 2.0f;  // (future)
    
    return 1.0f + (playerCount - 1) * 0.3f;  // Generic formula
}
```

---

**Nächster Schritt:** 08_Weapons_StatusEffects.md (Combat Loop Details)
