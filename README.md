# 🎮 Horde Arena WMA-MVP: Complete Production Package

**A Working Minimal Alpha game in 4–8 weeks.**  
**Free assets. Open-source code. Full documentation.**

---

## 📚 START HERE

### **For Complete Overview (30 min read):**
→ [`EXECUTIVE_SUMMARY.md`](./EXECUTIVE_SUMMARY.md) ← **YOU ARE HERE**

### **For Detailed Planning (2+ hours):**
→ [`Docs/00_README.md`](./Docs/00_README.md) – Index + Reading Path

### **For Immediate Building:**
→ [`Docs/15_Milestones_Checklists.md`](./Docs/15_Milestones_Checklists.md) – All tasks

→ [`Docs/16_Cursor_Codex_Runbooks.md`](./Docs/16_Cursor_Codex_Runbooks.md) – Copy-paste prompts

---

## 📁 What's Inside

```
aber jetzt/
├─ EXECUTIVE_SUMMARY.md          ← You are here. Start with this.
├─ README.md                     ← Navigation (this file)
├─ Docs/                         ← 17 detailed planning documents
│  ├─ 00_README.md               ← Doc index + reading order
│  ├─ 01_Vision_WMA.md           ← Game loop, pillars, design
│  ├─ 02_MVP_Scope.md            ← Must/Should/Could scope
│  ├─ 03_TechStack_Unity6_URP.md ← Packages, project setup
│  ├─ 04_Architecture_Modular.md ← Systems, patterns, code examples
│  ├─ 05_DataModel_ScriptableObjects.md
│  ├─ 06_Enemies_HordeDesign.md  ← Enemy roster, stats, behaviors
│  ├─ 07_HordeDirector_Waves.md  ← Spawning, difficulty curve
│  ├─ 08_Weapons_StatusEffects.md ← Weapons, combat, upgrades
│  ├─ 09_UI_UX.md                ← HUD, menus, screens
│  ├─ 10_Save_Meta.md            ← Persistence, progression
│  ├─ 11_Localization_DE_EN.md   ← German + English translations
│  ├─ 12_AssetStack_FreeFirst.md ← Free assets + links + licenses
│  ├─ 13_Licenses_Attribution.md ← Attribution ledger
│  ├─ 14_KI_ReplacementPlan.md   ← AI asset generation prompts
│  ├─ 15_Milestones_Checklists.md ← 52 tasks, 7 milestones
│  ├─ 16_Cursor_Codex_Runbooks.md ← Implementation prompts
│  ├─ 17_DevSuite_Spezifikation.md ← Tracking web-app
│  └─ _data/
│     ├─ assets.json             ← Asset registry (270 lines)
│     └─ milestones.json         ← Milestone definitions (167 lines)
└─ HordeArena/                   ← Your Unity project (create this)
```

---

## 🚀 Quick Start (5 Minutes)

1. **Read:** [`EXECUTIVE_SUMMARY.md`](./EXECUTIVE_SUMMARY.md) (this is your briefing)
2. **Watch:** Vision in [`01_Vision_WMA.md`](./Docs/01_Vision_WMA.md)
3. **Scope:** Check [`02_MVP_Scope.md`](./Docs/02_MVP_Scope.md) (is this realistic?)
4. **Setup:** Follow [`03_TechStack_Unity6_URP.md`](./Docs/03_TechStack_Unity6_URP.md)
5. **Code:** Start M1 with [`16_Cursor_Codex_Runbooks.md`](./Docs/16_Cursor_Codex_Runbooks.md)

---

## 📖 Reading Paths (Choose Your Level)

### **Path 1: Quick Briefing (30 min)**
- EXECUTIVE_SUMMARY.md ← You are here
- Docs/01_Vision_WMA.md
- Docs/02_MVP_Scope.md

### **Path 2: Full Context (2–3 hours)**
- All of Path 1
- Docs/03_TechStack_Unity6_URP.md
- Docs/04_Architecture_Modular.md
- Docs/12_AssetStack_FreeFirst.md

### **Path 3: Complete Mastery (6+ hours)**
- All of Path 2 +
- Every .md file from 05–17 in order
- Every code example in detail

### **Path 4: Daily Workflow**
- Docs/15_Milestones_Checklists.md (today's tasks)
- Docs/16_Cursor_Codex_Runbooks.md (today's prompts)
- Reference other docs as needed

---

## 🎮 Game Overview

| Aspect | Details |
|--------|---------|
| **Genre** | Horde Arena (Survivors-like / Brotato) |
| **Engine** | Unity 6 + URP (Universal Render Pipeline) |
| **Players** | 1–2 (Local Coop, same PC) |
| **Perspective** | Third-Person Vehicle Camera |
| **Gameplay Loop** | Drive + Shoot + Dodge + Loot + Upgrade |
| **Session Length** | 10–30 minutes |
| **Target Platforms** | PC (MVP), later Android/iOS |
| **Art Style** | Low-Poly, Stylized, Mobile-Friendly |
| **Audio** | Music (you), SFX (free libraries) |
| **Localization** | German + English |
| **Cost** | $0 (all free assets + frameworks) |

---

## 💼 Project Management

### **Timeline**
- **Week 1:** M1 (Setup) + M2 (Horde & Combat)
- **Week 2:** M3 (Loot) + M4 (Hub & Save)
- **Week 3:** M5 (Audio) + M6 (Local Coop)
- **Week 4+:** M7 (QA) + Polish → **RELEASE** 🚀

### **Milestones**
1. [M1] Setup & Prototyp (2 days)
2. [M2] Horde & Combat (3 days)
3. [M3] Loot & Upgrades (2 days)
4. [M4] Hub & Save System (2 days)
5. [M5] Polish & Audio (2 days)
6. [M6] Local Coop (2 days, optional)
7. [M7] QA & Release (1+ days)

**52 total tasks across all milestones.**  
See: [`Docs/15_Milestones_Checklists.md`](./Docs/15_Milestones_Checklists.md)

---

## 🛠️ Tech Stack

**Free Frameworks:**
- ✅ Zenject (DI, MIT license)
- ✅ UniTask (async, MIT license)
- ✅ Input System (built-in)
- ✅ Localization (built-in)
- ✅ Cinemachine (built-in, optional)

**Free Assets:**
- ✅ Quaternius (models, CC0)
- ✅ Kenney (UI, icons, CC0)
- ✅ Freesound (audio, CC0+CC-BY)
- ✅ Zapsplat (SFX, free commercial)
- ✅ Google Fonts (fonts, open source)

**Zero Cost. Zero GPL. Zero ND Licenses.**

See: [`Docs/12_AssetStack_FreeFirst.md`](./Docs/12_AssetStack_FreeFirst.md)

---

## 📊 Documentation Stats

| Category | Count | Lines |
|----------|-------|-------|
| Markdown Docs | 17 files | ~5,000 |
| JSON Data Files | 2 files | ~400 |
| Code Examples | 100+ snippets | ~2,000 |
| Checklists | 52 tasks | ~300 |
| Prompts | 40+ | ~600 |
| **TOTAL** | **~60 files** | **~8,300 lines** |

Everything you need. No fluff. No assumptions.

---

## 🎯 Key Documents (By Use Case)

**"What game am I building?"**  
→ [`Docs/01_Vision_WMA.md`](./Docs/01_Vision_WMA.md)

**"What's in MVP, what's later?"**  
→ [`Docs/02_MVP_Scope.md`](./Docs/02_MVP_Scope.md)

**"How do I set up the project?"**  
→ [`Docs/03_TechStack_Unity6_URP.md`](./Docs/03_TechStack_Unity6_URP.md)

**"How should I architect this?"**  
→ [`Docs/04_Architecture_Modular.md`](./Docs/04_Architecture_Modular.md)

**"What are the enemies?"**  
→ [`Docs/06_Enemies_HordeDesign.md`](./Docs/06_Enemies_HordeDesign.md)

**"How do waves work?"**  
→ [`Docs/07_HordeDirector_Waves.md`](./Docs/07_HordeDirector_Waves.md)

**"What weapons are there?"**  
→ [`Docs/08_Weapons_StatusEffects.md`](./Docs/08_Weapons_StatusEffects.md)

**"What's my UI layout?"**  
→ [`Docs/09_UI_UX.md`](./Docs/09_UI_UX.md)

**"How do I save the game?"**  
→ [`Docs/10_Save_Meta.md`](./Docs/10_Save_Meta.md)

**"Translations?"**  
→ [`Docs/11_Localization_DE_EN.md`](./Docs/11_Localization_DE_EN.md)

**"What free assets should I use?"**  
→ [`Docs/12_AssetStack_FreeFirst.md`](./Docs/12_AssetStack_FreeFirst.md)

**"License compliance?"**  
→ [`Docs/13_Licenses_Attribution.md`](./Docs/13_Licenses_Attribution.md)

**"How do I replace assets with AI later?"**  
→ [`Docs/14_KI_ReplacementPlan.md`](./Docs/14_KI_ReplacementPlan.md)

**"What's my task list?"**  
→ [`Docs/15_Milestones_Checklists.md`](./Docs/15_Milestones_Checklists.md)

**"How do I code each milestone?"**  
→ [`Docs/16_Cursor_Codex_Runbooks.md`](./Docs/16_Cursor_Codex_Runbooks.md)

**"How do I build a project dashboard?"**  
→ [`Docs/17_DevSuite_Spezifikation.md`](./Docs/17_DevSuite_Spezifikation.md)

---

## ✅ Confidence Checklist

Before you start, make sure you understand:

- [ ] The game is a **horde arena**, not a story game
- [ ] **2-player local coop** is part of MVP
- [ ] **Free assets only** (CC0, CC-BY, MIT)
- [ ] **4–8 weeks** to playable (realistic)
- [ ] **Architecture first**, then visuals
- [ ] **No hardcoding**—everything data-driven
- [ ] **Daily builds**—keep it playable
- [ ] **Scope lock**—Must/Should/Could is final

---

## 🎓 How to Use Cursor + Codex

1. **Setup:** Add `Docs/` folder to Cursor project context
2. **Per Milestone:** Copy prompt from `Docs/16_Cursor_Codex_Runbooks.md`
3. **Paste:** Into Codex chat with full project context
4. **Iterate:** Follow Codex responses, fix code, commit
5. **Repeat:** Next milestone

Each milestone takes 1–3 days. Codex writes 80% of the code.

---

## 🚨 Critical Warnings

- ❌ **Do NOT use GPL assets** (you're making a commercial game)
- ❌ **Do NOT use ND (Non-Derivative) licenses** (you're modifying assets)
- ❌ **Do NOT hardcode game data** (use ScriptableObjects)
- ❌ **Do NOT skip architecture** (technical debt kills projects)
- ❌ **Do NOT lose playability** (build daily, test constantly)

All these are addressed in the docs.

---

## 💡 Pro Tips

- **Cursor MCP:** Add this to `.cursor/config.json`:
  ```json
  "include": ["Docs/**", "HordeArena/Assets/**"]
  ```
  Gives Codex full context.

- **DevSuite First:** Build the web dashboard in Week 1.  
  Saves hours on milestone tracking.

- **Asset Audit:** Run license check weekly.  
  Docs/13 has the checklist.

- **Playtesting:** Build daily. Play daily.  
  Find bugs early.

- **Save Prompts:** Every successful Codex session, save the prompt.  
  Reuse for future projects.

---

## 📞 Support Resources

**Official Docs:**
- [Unity 6 Docs](https://docs.unity3d.com/)
- [URP Docs](https://docs.unity3d.com/Packages/com.unity.render-pipelines.universal)
- [Zenject GitHub](https://github.com/modesttree/Zenject)
- [UniTask GitHub](https://github.com/Cysharp/UniTask)

**Community:**
- [r/gamedev](https://reddit.com/r/gamedev) – Feedback
- [Game Dev Stack Exchange](https://gamedev.stackexchange.com) – Q&A
- [Godot/Unity Discord](https://discord.gg/gamedev) – Real-time help

**Free Asset Packs:**
- [Quaternius.com](https://quaternius.com) – Models
- [Kenney.nl](https://kenney.nl) – Everything
- [Freesound.org](https://freesound.org) – Audio
- [Poly Haven](https://polyhaven.com) – Textures

---

## 🎉 What Success Looks Like

**Week 3:**
- ✅ Game is playable (broken, but playable)
- ✅ You can drive, shoot, enemies spawn
- ✅ Loot drops, upgrades work
- ✅ Game saves/loads
- ✅ Audio plays

**Week 4+:**
- ✅ All bugs fixed
- ✅ UI polished
- ✅ Coop works
- ✅ Ready to release on itch.io

---

## 📝 License & Attribution

**This Documentation:** CC0 (Public Domain)  
**Code Examples:** CC0  
**All Referenced Assets:** See Docs/13_Licenses_Attribution.md

---

## 🚀 Next Step

**Read EXECUTIVE_SUMMARY.md (this file) top-to-bottom (5 min)**

Then:

→ **[Docs/00_README.md](./Docs/00_README.md)** for orientation

→ **[Docs/01_Vision_WMA.md](./Docs/01_Vision_WMA.md)** for game design

→ **Start building!**

---

**Good luck. You've got this.** 🎮

*Last Updated: 2025-01-05*  
*Next Review: After M2*

---

[← Back to EXECUTIVE_SUMMARY](./EXECUTIVE_SUMMARY.md) | [Docs Index →](./Docs/00_README.md)
