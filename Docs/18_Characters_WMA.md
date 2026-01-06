# 18. Charaktere (WMA) — Prompt-Suite Format

Diese Datei folgt dem Format aus `Docs/_prompts/wma_prompt_suite_game.md`.

---

## PLAYABLE CHARACTER — Rixa "Chromlilie" Voss

**Name**
Rixa "Chromlilie" Voss

**Short Lore (3–5 sentences, stylized, dark humor)**
Rixa mixt CHROM wie andere Cocktails. Ihre Tattoos sind Erinnerungen an Rennen, Explosionen und Partys, die niemand offiziell bestätigt. Sie lacht, wenn es gefährlich wird, und wird gefährlich, wenn sie lacht. Wer ihr vertraut, bekommt Buffs. Wer ihr nicht vertraut, bekommt Bisse vom Bully.

**Base Stats (HP, Armor, Move Speed, Crit, Pickup Radius)**
- HP: 90
- Armor: 5
- Move Speed: +10%
- Crit: +5%
- Pickup Radius: +10%

**Passive Trait (core identity, always active)**
**Chromrausch:** Jeder Buff (eigener oder im Umkreis) gibt +3% Schaden fuer 6s, stapelbar bis 5.

**Passive Skill Points (3–5 filler passives that scale over time)**
- Buff-Dauer +5%
- Status-Chance +3%
- AoE-Radius +5%
- Pickup-Radius +5%
- Crit-Damage +5%

**Active Ability (limited-use or cooldown-based)**
**Bully XL — "Hundangriff"** (2 Einsaetze pro Run)
- Ruft einen American Bully XL.
- 3 schnelle Bisse auf naechste Ziele.
- Jeder Biss: 120 Schaden + 1.0s Stun.

**Skill Tree (3 branches, each with 3 skills + 1 capstone)**

Branch A — **Chrom-Alchemie (Buff + Burst)**
1. **Chrom-Gabe**: Buffs geben +12% Schaden (6s).
2. **Ueberlack**: Buffs erzeugen 20% Schadensbonus als AoE-Explosion.
3. **Chrom-Overclock**: Buff-Stapel geben +15% Crit-Damage.
4. **Capstone: Glanzkoller**: Jeder 5. Buff loest Schock-AoE aus (0.8s Stun).

Branch B — **Secco & Chaos (Tempo + Control)**
1. **Secco-Toast**: Kurzbuff im 6m Radius -> +8% Feuerrate (6s).
2. **Kater-Ketten**: Jeder 3. Kill verwirrt Ziele 2s (falsches Targeting).
3. **Hangover-Herz**: Verwirrte Ziele nehmen +15% Schaden.
4. **Capstone: Party-Rausch**: Alle 12s kurzer Massen-Charm (0.6s).

Branch C — **Herzbrecherin (Charm + Sustain)**
1. **Kuschelblick**: 10% Chance, Gegner 2s zu charmen (weicht zurueck).
2. **Giftige Liebe**: Charmed Targets hinterlassen DOT-Spur (leichter Schaden).
3. **Eifersucht**: Charm endet mit 1s Taunt auf naechstes Ziel.
4. **Capstone: Fataler Kuss**: Charmed Targets explodieren bei Tod (kleines AoE).

**AoE & Coop Synergies (with other characters and enemy states)**
- Kombiniert mit Mareks Magnetsturm: Charm + Slow = perfekte AoE-Fenster.
- Funktioniert stark gegen debuffte Ziele (Slow, Confuse) -> Burst-Ketten.
- Buff-heavy Playstyle erhoeht AoE-Explosionsfrequenz.

**Weapon Pairing Guidance (non-meta)**
- Rixa bevorzugt schnelle oder statuslastige Mounts (Plasma Repeater Turret, Arc Thrower Side Emitter).
- Scrap Shotgun Front Cannon oder Junk Grenade Roof Launcher sind moeglich, aber nicht zwingend optimal fuer ihre Buff-Stacks.

**Run-Upgrades (UPGRADE_PROMPT Format)**
1. **Upgrade Name:** Chrom-Bonbon
   **Effect:** Buff-Dauer laenger
   **Numeric Values:** +20% Buff-Dauer
   **Synergies:** Chromrausch, Glanzkoller
2. **Upgrade Name:** Lipstick Crit
   **Effect:** Crit-Chance erhoeht
   **Numeric Values:** +6% Crit Chance
   **Synergies:** Chrom-Overclock
3. **Upgrade Name:** Secco-Pulse
   **Effect:** Feuerrate-Buff staerker
   **Numeric Values:** +6% Feuerrate waehrend Secco-Toast
   **Synergies:** Party-Rausch
4. **Upgrade Name:** Herzmagnet
   **Effect:** Charm-Chance erhoeht
   **Numeric Values:** +6% Charm Chance
   **Synergies:** Fataler Kuss
5. **Upgrade Name:** Chromsplitter
   **Effect:** AoE-Schaden hoeher
   **Numeric Values:** +15% AoE Damage
   **Synergies:** Ueberlack
6. **Upgrade Name:** Hundeleine
   **Effect:** Bully XL laesst nach jedem Biss eine Blutspur
   **Numeric Values:** DOT 20 Schaden ueber 3s
   **Synergies:** Giftige Liebe

---

## PLAYABLE CHARACTER — Marek "Schrottanker" Graul

**Name**
Marek "Schrottanker" Graul

**Short Lore (3–5 sentences, stylized, dark humor)**
Marek redet wenig und schweissig. Seine Antwort auf Chaos ist Gewicht: Stahlplatten, Magnetspulen und Drohnen aus Schrott. Er baut Festungen aus Wracks und nennt es "Balance". Gegner nennt er nicht Feinde, sondern "Rohmaterial".

**Base Stats (HP, Armor, Move Speed, Crit, Pickup Radius)**
- HP: 120
- Armor: 15
- Move Speed: -8%
- Crit: -2%
- Pickup Radius: +20%

**Passive Trait (core identity, always active)**
**Schrottkern:** Jeder 5. Pickup gibt 5% Schild (max 25%).

**Passive Skill Points (3–5 filler passives that scale over time)**
- Schild-Kapazitaet +5%
- Magnet-Radius +5%
- Drohnen-Schaden +5%
- Armor +2
- HP-Regen +0.2%/s

**Active Ability (limited-use or cooldown-based)**
**Magnetsturm — "Kaefig"** (2 Einsaetze pro Run)
- 4s Magnetfeld im 10m Radius.
- Gegner: -40% Speed.
- Projektile: 20% Ablenkung.

**Skill Tree (3 branches, each with 3 skills + 1 capstone)**

Branch A — **Magnetik (Control + Loot)**
1. **Polwechsel**: Alle 15s Impuls -> zieht Gegner 1m an (Interrupt).
2. **Metallregen**: Magnetfeld gibt +10% Loot.
3. **Eddy-Kaefig**: Verlangsamte Gegner nehmen +20% Schaden.
4. **Capstone: Schwerkraftknoten**: Magnetfeld haelt Elites 1s fest.

Branch B — **Drohnenwerk (Summon + Burst)**
1. **Schrotthummeln**: 2 Drohnen feuern auf naechstes Ziel.
2. **Akkustand**: Drohnen-Treffer laden 1% Spezialfaehigkeit.
3. **Saegezahn**: Drohnen verursachen Bleed (leichtes DOT).
4. **Capstone: Schwarmbefehl**: Drohnen buendeln Feuer (Burst auf markiertes Ziel).

Branch C — **Bollwerk (Defense + Taunt)**
1. **Plattenpanzer**: +10 Armor, -5% Rueckstoss.
2. **Rammbarriere**: Kontakt loest 1s Taunt aus.
3. **Reparatur-Fuge**: Alle 20s +2% HP Repair.
4. **Capstone: Eiserne Klammer**: Bei HP < 30% -> -25% Damage (6s).

**AoE & Coop Synergies (with other characters and enemy states)**
- Magnetsturm + Rixas Charm: Gruppen bleiben gebuendelt fuer AoE-Bursts.
- Drohnen markieren Ziele, damit Burst-Upgrades sicherer sitzen.
- Kontrolliert Control-heavy Gegner mit Interrupts.

**Weapon Pairing Guidance (non-meta)**
- Marek bevorzugt kontrolllastige Mounts (Junk Grenade Roof Launcher, Venom Sprayer Front Nozzle).
- Rail Beam Roof Cannon ist moeglich, aber eher fuer Elite-Picks als Default.

**Run-Upgrades (UPGRADE_PROMPT Format)**
1. **Upgrade Name:** Magnet-Linse
   **Effect:** Magnetfeld staerker
   **Numeric Values:** -10% zusaetzliche Enemy Speed
   **Synergies:** Eddy-Kaefig
2. **Upgrade Name:** Schrottkrone
   **Effect:** Schild-Kapazitaet erhoeht
   **Numeric Values:** +10% Max Shield
   **Synergies:** Schrottkern
3. **Upgrade Name:** Schraubenschwarm
   **Effect:** Drohnen feuern schneller
   **Numeric Values:** +15% Drohnen-Firerate
   **Synergies:** Schwarmbefehl
4. **Upgrade Name:** Stahlfaust
   **Effect:** Taunt laenger
   **Numeric Values:** +0.5s Taunt Duration
   **Synergies:** Rammbarriere
5. **Upgrade Name:** Glaettung
   **Effect:** Rueckstoss weiter reduziert
   **Numeric Values:** -10% Recoil
   **Synergies:** Plattenpanzer
6. **Upgrade Name:** Generator-Herz
   **Effect:** Spezialfaehigkeit laedt schneller
   **Numeric Values:** +8% Ability Charge Rate
   **Synergies:** Akkustand

---

## Character Model Prompt Inputs (for [CHARACTER_MODEL_PROMPT])

**Rixa — Character Description**
Adult punk-alchemist, neon-dyed hair, heavy tattoos (incl. neck), colorful layers, bunny or teddy hoodie, chrome vials, secco bottle, chaotic accessories.

**Rixa — Silhouette Notes**
Slim athletic, oversized sleeves, strong outline, readable at distance.

**Rixa — Accessories / Props**
Chrome canisters, secco bottle, hoodie ears, charms.

**Marek — Character Description**
Rugged scavenger-engineer, heavy scrap armor, magnet gauntlets, tool belt, drone companion, welding mask on hip.

**Marek — Silhouette Notes**
Broad, stable posture, chunky armor blocks, high readability.

**Marek — Accessories / Props**
Small drone, cable coils, scrap plates, welding gear.
