# 💻 DevSuite: Lokale Web-App Spezifikation

**Zweck:** Ein interaktives Dashboard für alle Dokumente, Milestones, Prompts + Fortschritts-Tracking.

**Tech Stack:** Vite + Vue 3 (oder Astro) + TailwindCSS + LocalStorage

**Offline-First:** Läuft komplett lokal, kein Internet nötig nach dem Build.

---

## 🎯 Feature Set

### **1. Markdown Viewer**
- Liest alle `.md` Dateien aus `/Docs/`
- Rendert sie mit GitHub Flavored Markdown
- Inhaltsverzeichnis (sidebar links)
- Breadcrumb navigation
- Search (Cmd+K) über alle Docs

### **2. Interactive Task Tracker**
- Ladet Checklists aus `.md` Dateien
- Zeigt Checkboxen an ([ ] → clickable)
- Speichert State in LocalStorage
- Zeigt Fortschritt % per Milestone
- Notizen-Feld pro Task (optional)

### **3. Prompt Library Browser**
- Kategorisiert (M1, M2, M3, etc.)
- Filter nach Status (Ready, WIP, Testing)
- Variable Substitution UI (z.B. [ENEMY_TYPE] → input field)
- Copy-to-Clipboard Button (full prompt)
- History (recently used prompts)

### **4. Asset Registry**
- Ladet `_data/assets.json`
- Filter nach: Lizenz, Kategorie, Kompatibilität, Status
- Link-Buttons zu Quellen
- Lokal tracking: "Heruntergeladen?" / "Importiert?"

### **5. Dashboard**
- Overview: WMA-MVP Fortschritt (%)
- Quick Stats: Aufgaben erledigt, aktive Milestones
- Next Steps (aus Docs/15...)
- Recent Activity (gerade bearbeitete Tasks)

### **6. Settings & Export**
- Dark/Light Mode
- Font Size
- Export Progress als JSON (Backup)
- Import Progress aus JSON
- Reset all data

---

## 📊 Datenstruktur (JSON Schemas)

### **tasks.json** (Auto-generated aus .md Checklists)

```json
{
  "milestones": [
    {
      "id": "m1",
      "name": "Milestone 1: Setup & Prototyp",
      "status": "in-progress",
      "progress": 0.6,
      "tasks": [
        {
          "id": "m1_1",
          "description": "Create Unity 6 project, install packages",
          "completed": true,
          "notes": "Unity 6.0.1, URP configured",
          "dueDate": "2025-01-06"
        },
        {
          "id": "m1_2",
          "description": "Create Zenject installers + Bootstrap scene",
          "completed": false,
          "notes": "",
          "dueDate": "2025-01-06"
        }
      ]
    }
  ]
}
```

### **prompts.json** (Prompt Library)

```json
{
  "prompts": [
    {
      "id": "m1_setup",
      "category": "m1-setup",
      "title": "Project Setup & DI Container",
      "description": "Create project structure and Zenject DI setup",
      "content": "[Full prompt text here...]",
      "variables": [],
      "tags": ["setup", "architecture", "zenject"],
      "status": "ready",
      "lastUsed": "2025-01-05T12:00:00Z"
    },
    {
      "id": "m1_vehicle",
      "category": "m1-setup",
      "title": "Vehicle Controller & Input",
      "description": "Create responsive WASD vehicle movement",
      "content": "[Full prompt text here...]",
      "variables": ["ASSET_SOURCE", "MAX_SPEED", "ACCELERATION"],
      "tags": ["vehicle", "input", "movement"],
      "status": "ready",
      "lastUsed": null
    }
  ]
}
```

### **assets.json** (Asset Registry)

```json
{
  "assets": [
    {
      "id": "quaternius_hovercraft",
      "name": "Quaternius Hovercraft",
      "category": "vehicles",
      "source": "Quaternius",
      "url": "https://quaternius.com",
      "license": "CC0",
      "commercial": true,
      "modifiable": true,
      "constraints": "none",
      "status": "pending",
      "notes": "Preferred for WMA MVP",
      "downloaded": false,
      "imported": false,
      "importPath": "Assets/Models/Vehicle/"
    }
  ]
}
```

### **milestones.json** (Milestone Definitions)

```json
{
  "milestones": [
    {
      "id": "m1",
      "name": "Setup & Prototyp",
      "duration": 2,
      "startDate": "2025-01-06",
      "blocker": null,
      "deliverables": [
        "Unity 6 project with URP",
        "Zenject DI container",
        "Vehicle controller + camera"
      ]
    }
  ]
}
```

---

## 🏗️ UI Layout

```
┌─────────────────────────────────────────────────────┐
│  🎮 Horde Arena DevSuite                   [⚙️]    │
├──────────────┬──────────────────────────────────────┤
│              │                                      │
│ SIDEBAR      │ MAIN CONTENT                         │
│ ─────────    │ ─────────────────────────────────    │
│ 📚 Docs      │ Dashboard / Task Tracker / Prompts   │
│  ├─ 00_README                                       │
│  ├─ 01_Vision │ Quick Stats:                       │
│  ├─ ...       │ • M1: 60% complete                 │
│  │            │ • M2: 0% (blocked)                 │
│ 🎯 Milestones │ • Total: 15% done                  │
│  ├─ M1       │                                     │
│  ├─ M2       │ [Active Tasks Table]                │
│  └─ ...      │ ID | Description | Status | ...    │
│              │                                     │
│ 📋 Tasks     │                                     │
│ 🔐 Prompts   │ [Prompt: Codex M1 Setup]           │
│ 🎨 Assets    │                                     │
│ ⚙️ Settings  │ [Copy] [Bookmark] [History]         │
│              │                                     │
└──────────────┴──────────────────────────────────────┘
```

---

## 🔧 Implementation Roadmap

### **Phase 1: Static Markdown Viewer** (Day 1)
- [ ] Vite + Vue 3 setup
- [ ] Markdown parser (marked.js)
- [ ] Sidebar navigation (docs list)
- [ ] Basic styling

### **Phase 2: Task Tracker** (Day 2)
- [ ] Parse `.md` checklists
- [ ] LocalStorage for task state
- [ ] Checkbox UI + update logic
- [ ] Progress bar

### **Phase 3: Prompt Library** (Day 2.5)
- [ ] Load `prompts.json`
- [ ] Filter/search UI
- [ ] Variable substitution
- [ ] Copy-to-clipboard

### **Phase 4: Asset Registry** (Day 3)
- [ ] Load `assets.json`
- [ ] Filter UI (license, category, status)
- [ ] Download link buttons
- [ ] Local tracking

### **Phase 5: Dashboard & Export** (Day 3.5)
- [ ] Dashboard overview
- [ ] Export/Import progress (JSON)
- [ ] Settings (theme, font size)
- [ ] Dark mode support

---

## 📝 Tech Stack Decision

| Option | Pros | Cons | Verdict |
|--------|------|------|---------|
| **Vite + Vue 3** | Fast, reactive, TailwindCSS easy | Learning curve | ✅ Recommended |
| **Astro** | Simple, static-friendly, lightweight | Less reactive for tasks | ⚠️ Okay |
| **Next.js** | Full-featured, static export | Overkill, npm bloat | ❌ Too much |
| **Vanilla JS** | No dependencies, lightweight | Tedious to maintain | ❌ Too minimal |

**Choice:** **Vite + Vue 3 + TailwindCSS**

---

## 🚀 Vite Project Template

```bash
# Initial setup:
npm create vite@latest devsuite -- --template vue
cd devsuite
npm install

# Install dependencies:
npm install -D tailwindcss postcss autoprefixer marked highlight.js

# Dev server:
npm run dev

# Build:
npm run build
```

**Folder structure:**
```
devsuite/
├── src/
│   ├── components/
│   │   ├── DocViewer.vue
│   │   ├── TaskTracker.vue
│   │   ├── PromptBrowser.vue
│   │   ├── AssetRegistry.vue
│   │   └── Dashboard.vue
│   ├── stores/
│   │   ├── taskStore.js (pinia)
│   │   ├── promptStore.js
│   │   └── settingsStore.js
│   ├── data/
│   │   ├── tasks.json
│   │   ├── prompts.json
│   │   └── assets.json
│   ├── App.vue
│   └── main.js
├── public/
│   └── docs/ (symlink or copy of Docs/)
└── vite.config.js
```

---

## 💾 LocalStorage Keys

```javascript
// Task progress
localStorage.setItem('tasks:m1_1', true);  // Completed status
localStorage.setItem('tasks:m1_1:notes', 'Some notes');

// Prompt history
localStorage.setItem('prompts:recent', JSON.stringify([
  { id: 'm1_setup', timestamp: '2025-01-05T12:00:00Z' },
  ...
]));

// Settings
localStorage.setItem('settings:theme', 'dark');
localStorage.setItem('settings:fontSize', '16px');

// Asset status
localStorage.setItem('assets:quaternius_hovercraft:downloaded', true);
localStorage.setItem('assets:quaternius_hovercraft:imported', true);

// Export/Import
localStorage.setItem('progress:export', JSON.stringify({
  tasks: {...},
  timestamp: '2025-01-05T12:30:00Z'
}));
```

---

## 📖 Usage Guide

1. **Start DevSuite:** `npm run dev` (lädt auf localhost:5173)
2. **Read Docs:** Sidebar → klick auf Doc Name → Markdown rendered
3. **Track Tasks:** Milestone klicken → Checklist anzeigen → Checkbox klicken zum aktualisieren
4. **Copy Prompts:** Prompts Tab → Filter/Search → Copy Button → in Cursor einfügen
5. **Manage Assets:** Assets Tab → Filter → Download-Link → nach Import als "imported" markieren
6. **Export Progress:** Settings → Export JSON → Backup speichern

---

## 🎨 Styling (TailwindCSS)

```css
/* Dark mode base */
@tailwind base;
@tailwind components;
@tailwind utilities;

.prose {
  @apply dark:prose-invert;
}

.task-item {
  @apply flex items-center gap-2 p-2 rounded hover:bg-gray-100 dark:hover:bg-gray-800;
}

.task-complete {
  @apply line-through text-gray-500;
}
```

---

**Nächster Schritt:** Datenfiles (`.json`) erstellen und in `_data/` speichern
