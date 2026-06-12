# 🐝 SwarmOps – Multi-Agent AI Collaboration System

> **Lass mehrere KI-Agenten parallel und konfliktfrei an deinem Projekt arbeiten.**

SwarmOps ist ein dateibasiertes Koordinationssystem für KI-Entwicklungsagenten. 
Ein Planner erstellt Tasks, mehrere Worker arbeiten sie gleichzeitig ab – 
ohne sich in die Quere zu kommen.

---

## ⚡ Schnellstart (3 Schritte)

### 1. SwarmOps in dein Projekt kopieren

```bash
cp -r .swarmops/ /pfad/zu/deinem/projekt/.swarmops/
```

### 2. MOTD ausfüllen

Öffne `.swarmops/MOTD.md` und fülle die Projekt-Informationen aus 
(Name, Tech-Stack, Architektur, Coding-Standards).

### 3. Agents starten

**Planner starten** (1x) – gibt ihm die Aufgabe:
```
Lies .swarmops/SKILL.md, du bist PLANNER-1. Lies MOTD & CONFIG, dann plane die folgende Aufgabe: [DEINE AUFGABE HIER]
```

**Worker starten** (1–N mal, je in eigenem Chat-Fenster):
```
Lies .swarmops/SKILL.md, du bist WORKER. Lies MOTD & CONFIG, dann arbeite Tasks aus dem Backlog ab.
```

Das war's. Die Worker finden automatisch Tasks, claimen sie, und arbeiten sie ab. 🎉

---

## 📖 Wie es funktioniert

```
┌──────────┐     erstellt Tasks      ┌──────────────┐
│  MENSCH  │ ───────────────────────→ │   PLANNER    │
│          │     gibt Ziel vor        │   Agent      │
└──────────┘                          └──────┬───────┘
                                             │
                                    ┌────────▼────────┐
                                    │    backlog/      │
                                    │  TASK-001.md     │
                                    │  TASK-002.md     │
                                    │  TASK-003.md     │
                                    └────────┬────────┘
                                             │
                              ┌──────────────┼──────────────┐
                              │              │              │
                        ┌─────▼─────┐  ┌─────▼─────┐  ┌─────▼─────┐
                        │ WORKER-1  │  │ WORKER-2  │  │ WORKER-3  │
                        │ claimed   │  │ claimed   │  │ claimed   │
                        │ TASK-001  │  │ TASK-002  │  │ TASK-003  │
                        └─────┬─────┘  └─────┬─────┘  └─────┬─────┘
                              │              │              │
                        ┌─────▼─────────────▼──────────────▼─────┐
                        │              done/                      │
                        │  TASK-001.md  TASK-002.md  TASK-003.md  │
                        └─────────────────────────────────────────┘
```

### Kernprinzipien:

1. **1 Task = 1 Datei** – Jeder Task ist eine eigenständige Markdown-Datei
2. **Claim durch Verschieben** – Ein Worker verschiebt die Datei von `backlog/` nach `in-progress/`
3. **Natürlicher Mutex** – Wenn die Datei nicht mehr da ist, hat ein anderer Agent sie bereits geclaimed
4. **Atomare Tasks** – Jeder Task wird komplett von einem Agent erledigt
5. **Loop-Arbeitsweise** – Worker suchen automatisch den nächsten Task

---

## 📂 Dateistruktur

```
.swarmops/
├── SKILL.md              # Hauptinstruktion (das Regelwerk)
├── MOTD.md               # Projekt-Kontext für alle Agents
├── CONFIG.md             # System-Konfiguration
├── prompts/
│   ├── planner.md        # Fertige Prompts für den Planner
│   ├── worker.md         # Fertige Prompts für Worker
│   └── setup.md          # Mini-Prompts & URL-Loader
└── tasks/
    ├── backlog/          # 📋 Offene Tasks
    ├── in-progress/      # 🔨 Aktuell in Bearbeitung
    ├── review/           # 🔍 Fertig, wartet auf Review
    └── done/             # ✅ Abgeschlossen
```

---

## 🔧 Konfiguration

Bearbeite `.swarmops/CONFIG.md` um das System anzupassen:

| Setting               | Default  | Beschreibung                          |
|----------------------|----------|---------------------------------------|
| `max_concurrent_workers` | 5    | Max. gleichzeitige Worker             |
| `require_review`     | false    | Review-Pflicht vor `done`             |
| `task_size_limit`    | L        | Max. Task-Größe                       |

---

## 📊 Status prüfen

```bash
echo "=== BACKLOG ===" && ls .swarmops/tasks/backlog/ 2>/dev/null || echo "(leer)"
echo "=== IN PROGRESS ===" && ls .swarmops/tasks/in-progress/ 2>/dev/null || echo "(leer)"
echo "=== REVIEW ===" && ls .swarmops/tasks/review/ 2>/dev/null || echo "(leer)"
echo "=== DONE ===" && ls .swarmops/tasks/done/ 2>/dev/null || echo "(leer)"
```

---

## 🤖 Kompatibilität

SwarmOps funktioniert mit jedem KI-Agenten, der:
- Dateien lesen und schreiben kann
- Terminal-Befehle ausführen kann (für `mv`)
- Markdown versteht

**Getestet mit:**
- GitHub Copilot (Agent Mode)
- Cursor
- Gemini Code Assist
- Claude (mit Dateizugriff)
- ChatGPT (mit Code Interpreter)
- Windsurf
- Aider

---

## 📄 Lizenz

MIT – Nutze es wie du willst.
