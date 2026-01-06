# 🤖 14. KI Replacement Plan: Prompts & QA

**Ziel:** Später (Post-WMA), Free-Assets durch KI-generierte Custom-Assets ersetzen, ohne Rework.

---

## 📐 Naming Conventions (KI-Ready)

**Alle Assets folgen diesem Schema, damit KI-Replacement einfach ist:**

```
Assets/Models/Enemies/BoarGrunt/
├── BoarGrunt_LOD0.fbx              # High detail
├── BoarGrunt_LOD1.fbx              # Medium detail
├── BoarGrunt_LOD2.fbx              # Low detail
├── Materials/
│   ├── BoarGrunt_Base_Mat.mat       # Primary material
│   └── BoarGrunt_Variant_Brute.mat  # Variant for Brute type
├── Textures/
│   ├── BoarGrunt_Diffuse.png
│   ├── BoarGrunt_Normal.png
│   └── BoarGrunt_Metallic_Roughness.png
└── BoarGrunt_Prefab.prefab          # Final prefab

Assets/UI/Icons/Weapons/
├── PlasmaRifle_Icon_256.png
├── Shotgun_Icon_256.png
└── (all icons 256x256, matching style)

Assets/UI/Icons/StatusEffects/
├── Freeze_Icon.png
├── Burn_Icon.png
└── (high contrast, readable at 48x48)
```

**Principle:** Flat folder structure, naming includes type + variant + detail level.

---

## 🎨 KI Prompt Templates (Midjourney / Flux)

### **Template 1: Monster/Enemy Character**

```
Subject: [EnemyType] Humanoid Monster
Specification:

You are creating a 3D character model for a indie game.

Character Name: [BoarGrunt / HyenaRunner / RavenSwooper]
Archetype: [Melee Brute / Agile Chaser / Ranged Attacker / Flyer]
Theme: Post-apocalyptic mutated animal humanoid
Style: Low-poly stylized (100-500 triangles), mobile-friendly
Color Palette: [Specify: Earthy Greens/Browns / Toxic Purples / Metallic Silvers]

Physical Description:
- Base animal: [Boar / Hyena / Raven]
- Humanization: [Arms+Legs humanoid, bipedal stance]
- Height: ~1.7-2.2 meters
- Distinguishing Features: [Spikes / Feathers / Scales / Armor Plating]
- Silhouette: [Bulky / Lean / Stocky]

Personality/Feel: [Aggressive / Frantic / Predatory]

Style Reference: Low-poly stylized like Quaternius, readable high-contrast

Output: 
- Frontal view, turntable, T-pose
- Wireframe (to show poly budget)
- High-contrast silhouette
```

**Example für Boar Brute:**
```
Character: Boar Brute (Elite variant of BoarGrunt)
- 1.5x size of Grunt
- Heavier armor plating (visible spikes on shoulders/back)
- Darker color: Forest Green + Black Iron
- Bulky, tank-like silhouette
- T-pose, 400 triangles max
- Visible spikes telegraph its charge attack
```

---

### **Template 2: Vehicle Player Character**

```
Vehicle Name: [HoverCraft / Combat Buggy]
Theme: Post-apocalyptic wasteland
Style: Low-poly stylized, 300-600 triangles
Color Scheme: [Neon accents on rust/brown base]
Features:
- Hover/repulsor technology (visible effects)
- Mounted weapon hardpoints on [roof/sides]
- Sleek but industrial feel
- Third-person camera optimal view: rear-left angle

Output:
- Frontal, side, top-down view
- Wireframe
- Highlight weapon mount points (HP_FirePoint labels)
```

---

### **Template 3: UI Icons (Grid)**

```
Icon Style: Wasteland-tech, high-contrast, readable at 48x48
Format: 256x256 PNG, transparent background

Icons needed:
- [WeaponType] (x6): Plasma Repeater Turret, Scrap Shotgun Front Cannon, Arc Thrower Side Emitter, Junk Grenade Roof Launcher, Venom Sprayer Front Nozzle, Rail Beam Roof Cannon
- [StatusEffect] (x4): Freeze (blue), Burn (orange), Poison (green), Stun (yellow)
- [Resource] (x3): Scrap (metal), Tech (circuit), Health (cross)

Style: 
- Flat or minimal 3D
- Bold outlines
- Color-coded by category
- Consistent line weight
- No gradients (for mobile)

Example: Freeze icon = Blue snowflake on dark bg, 4px outline
```

---

### **Template 4: Decal / Surface Detail**

```
Decal Type: [Hazard Stripe / Graffiti / Rust / Dirt / Numbers]
Canvas: Flat texture, 512x512 or 1024x1024
Style: Post-apocalyptic industrial

Hazard Stripe Example:
- Yellow + Black diagonal stripes, 45 degree angle
- Pattern: 20px stripe width, repeating
- Transparency: ~70% alpha for overlay
- Use case: Warning markings on vehicles, arena props

Rust Example:
- Orange-brown splotches, irregular
- Transparency: 60-80% (overlay texture)
- Scale: Tileable at 2m x 2m
- Use case: Weathering on metal props

Output: PSD (for editing) + PNG (for game)
```

---

## 🎯 QA Checklist (KI-Asset Verification)

**Nach KI-Generierung IMMER durchprüfen:**

### **Geometry & Silhouette**
- [ ] Silhouette clear at 30m+ distance
- [ ] Symmetry correct (if intended)
- [ ] No degenerate triangles / T-junctions
- [ ] Normals facing correct direction
- [ ] Wireframe density reasonable (100-500 tris for enemy, 300-800 for vehicle)
- [ ] No Z-fighting or overlaps

### **Rigging & Animation Ready**
- [ ] Bones/Armature present if needed
- [ ] Root bone at center
- [ ] Shoulder/hip/knee joints accessible
- [ ] Weights reasonable (no "flying" vertices)
- [ ] Can import into engine without errors

### **Materials & Textures**
- [ ] Diffuse map: correct colors, readable
- [ ] Normal map: plausible (bumpy, not flat)
- [ ] Metallic: 0-1 range, sensible values
- [ ] Roughness: not too shiny (0.5 default for stylized)
- [ ] Emission: if used, for highlights only
- [ ] Texel density: consistent across model

### **Compatibility**
- [ ] Exports to FBX 2019 or later
- [ ] Imports clean into Unity URP (no shader errors)
- [ ] Colliders addable (not blocking tight geometry)
- [ ] LOD variants can be generated (simple decimation)
- [ ] No dependencies on external software

### **Style Consistency**
- [ ] Matches art direction (low-poly, stylized)
- [ ] Color palette aligns (no random colors)
- [ ] Silhouette readable on all resolutions
- [ ] Contrast sufficient (no muddy colors)
- [ ] Proportions correct (compare to reference)

### **Performance**
- [ ] Triangle count within budget
- [ ] Texture resolution suitable (512x512 typical, 256x256 minimum)
- [ ] Material complexity low (URP Lit, no custom shaders)
- [ ] No overdraw issues
- [ ] Culling bounds correct

### **Integration**
- [ ] Named correctly (BoarGrunt_LOD0.fbx, etc.)
- [ ] In correct folder (Assets/Models/Enemies/BoarGrunt/)
- [ ] Metadata complete (textures, materials in same folder)
- [ ] Prefab created and tested
- [ ] Collider geometry appropriate
- [ ] Hardpoints (HP_*) added if needed

---

## 🔄 Workflow: Replace Asset (Schritt-für-Schritt)

**Szenario:** Quaternius Boar Grunt zu KI-generiertem Modell upgraden (Post-MVP)

### **Phase 1: Brief & Generation**
1. **Write Prompt:** [siehe Template 1 oben]
2. **Generate:** Midjourney / Flux x3 variations
3. **Select:** Best match zur desired Silhouette
4. **Export:** As FBX (oder STL → Blender cleanup → FBX)

### **Phase 2: QA & Cleanup**
5. **Import Test:** FBX in new scene
6. **Check Geometry:** Wireframe, normals, degenerate tris
7. **Fix Issues:** Blender if needed (normal fix, cleanup)
8. **LOD Generation:** Automated (Unity LOD → Auto-Decimate)
9. **Texture Bake:** If needed (Substance Painter or Marmoset)

### **Phase 3: Material & Integration**
10. **Create Material:** URP Lit, assign textures
11. **Test in Scene:** Place next to old asset, compare
12. **Create Prefab:** Update existing prefab, test in-game
13. **Collider Check:** BoxCollider still works, or use capsule

### **Phase 4: Verification & Commit**
14. **Run QA Checklist** [siehe oben]
15. **Test in Horde:** Spawn 10x new model, check performance
16. **Update Attribution:** If using AI service, note in credits
17. **Commit:** `Upgrade: BoarGrunt model to KI-generated version`

---

## 📋 Asset Replacement Priority (Post-MVP)

| Asset | Current Source | KI Replacement Priority | Reason | Estimated Effort |
|-------|-----------------|------------------------|---------|----|
| **Vehicle** | Quaternius | Medium | Works, but custom look nice | 4–8 hours |
| **BoarGrunt** | Quaternius | Low | Works fine, keep | Skip |
| **BoarBrute** | Variant | High | Differentiation needed | 2 hours |
| **Hyena Runner** | Quaternius | Low | Functional | Skip |
| **Raven Swooper** | Quaternius | Medium | Wings can be better | 3 hours |
| **Goldgoblin** | Custom needed | High | Unique design | 3 hours |
| **UI Icons** | Kenney | Medium | Consistency pass | 2 hours |
| **Weapon VFX** | Particles | Low | Serviceable | Skip |

---

## 🚀 KI Services (Optionen)

| Service | Model | Cost | Quality | Integration |
|---------|-------|------|---------|-------------|
| **Midjourney** | GPT-4V | $20/month | High | Manual export |
| **Flux.1** | Custom | Free (Replicate API) | Medium-High | API or CLI |
| **Blender AI** | Upscayl + addons | Free | Variable | Integrated |
| **Stable Diffusion** | Open-source | Free | Medium | Local setup |

**Empfehlung für Indie:** Midjourney (high quality) oder Flux (kostenlos auf Replicate API).

---

## 📝 Attribution für KI-Assets

**Wenn du KI-generierte Assets verwendest:**

```
Credits:
- [AssetName] generated with [Service] (Midjourney / Flux / etc.)
- Prompt: [Simplified version of prompt]
- Post-processing: [Any manual edits]
- License: CC0 (selbst erstellt) oder [Custom]
```

**Beispiel:**
```
Boar Brute 3D Model v2
- Generated with Midjourney (March 2025)
- Post-processed in Blender (normals, cleanup)
- License: CC0 (Custom Creation)
```

---

**Nächster Schritt:** 15_Milestones_Checklists.md (Alle Milestones + Tasks)
