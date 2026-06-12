# 🚀 SwarmOps – Quick-Start Prompts

> **Kopiere einfach einen der Prompts unten und starte damit einen KI-Agenten.**
> Die SKILL.md wird automatisch von GitHub geladen.

---

## ⚡ Installer-Prompt (Einmal-Setup)

> **Diesen EINEN Prompt in einen beliebigen KI-Agenten pasten – er installiert SwarmOps komplett im aktuellen Projekt.**

```
Du bist ein Setup-Agent. Deine einzige Aufgabe: Installiere das SwarmOps Multi-Agent-System in diesem Projekt.

Schritt 1 – Dateien herunterladen:
Lade folgende Dateien von GitHub herunter und speichere sie exakt unter den angegebenen Pfaden relativ zum Projekt-Root:

- https://raw.githubusercontent.com/LucazPlays/SwarmOps/main/.swarmops/SKILL.md → .swarmops/SKILL.md
- https://raw.githubusercontent.com/LucazPlays/SwarmOps/main/.swarmops/MOTD.md → .swarmops/MOTD.md
- https://raw.githubusercontent.com/LucazPlays/SwarmOps/main/.swarmops/CONFIG.md → .swarmops/CONFIG.md
- https://raw.githubusercontent.com/LucazPlays/SwarmOps/main/.swarmops/prompts/planner.md → .swarmops/prompts/planner.md
- https://raw.githubusercontent.com/LucazPlays/SwarmOps/main/.swarmops/prompts/worker.md → .swarmops/prompts/worker.md
- https://raw.githubusercontent.com/LucazPlays/SwarmOps/main/.swarmops/prompts/setup.md → .swarmops/prompts/setup.md

Schritt 2 – Verzeichnisse erstellen:
Erstelle diese Verzeichnisse (falls sie nicht existieren):
- .swarmops/tasks/backlog/
- .swarmops/tasks/in-progress/
- .swarmops/tasks/review/
- .swarmops/tasks/done/

Schritt 3 – MOTD ausfüllen:
Analysiere das aktuelle Projekt (Dateien, package.json, README, etc.) und fülle die MOTD.md automatisch aus:
- Projektname (aus package.json, Verzeichnisname, oder README)
- Tech-Stack (erkenne Sprachen, Frameworks, Tools)
- Architektur-Überblick (Ordnerstruktur)
- Coding-Standards (aus Linter-Configs, .editorconfig, etc.)

Schritt 4 – Bestätigung:
Gib eine Zusammenfassung aus, was installiert wurde, und zeige die Prompts für Planner und Worker an.
```

---

## 📌 Die URLs

| Datei      | Raw-URL                                                                                     |
|-----------|--------------------------------------------------------------------------------------------|
| SKILL.md  | `https://raw.githubusercontent.com/LucazPlays/SwarmOps/main/.swarmops/SKILL.md`            |
| MOTD.md   | `https://raw.githubusercontent.com/LucazPlays/SwarmOps/main/.swarmops/MOTD.md`             |
| CONFIG.md | `https://raw.githubusercontent.com/LucazPlays/SwarmOps/main/.swarmops/CONFIG.md`           |
| Planner   | `https://raw.githubusercontent.com/LucazPlays/SwarmOps/main/.swarmops/prompts/planner.md`  |
| Worker    | `https://raw.githubusercontent.com/LucazPlays/SwarmOps/main/.swarmops/prompts/worker.md`   |

---

## 🧠 Planner starten

### Mit URL (Remote-Projekt):
```
Lade die Datei von https://raw.githubusercontent.com/LucazPlays/SwarmOps/main/.swarmops/SKILL.md und befolge die Anweisungen darin. Du bist PLANNER-1. Lies danach MOTD.md und CONFIG.md im selben Verzeichnis. Dann plane die folgende Aufgabe: [DEINE AUFGABE HIER]
```

### Lokal (wenn .swarmops/ bereits im Projekt liegt):
```
Lies .swarmops/SKILL.md, du bist PLANNER-1. Lies MOTD & CONFIG, dann plane die folgende Aufgabe: [DEINE AUFGABE HIER]
```

### Einzeiler:
```
Lies .swarmops/SKILL.md, du bist PLANNER-1. Lies MOTD & CONFIG, dann plane: [AUFGABE]
```

---

## 👷 Worker starten

### Mit URL (Remote-Projekt):
```
Lade die Datei von https://raw.githubusercontent.com/LucazPlays/SwarmOps/main/.swarmops/SKILL.md und befolge die Anweisungen darin. Du bist ein WORKER Agent. Lies danach MOTD.md und CONFIG.md im selben Verzeichnis. Dann starte deinen Arbeits-Loop: Scanne das Backlog, claime einen Task, arbeite ihn komplett ab, und suche den nächsten.
```

### Lokal (wenn .swarmops/ bereits im Projekt liegt):
```
Lies .swarmops/SKILL.md, du bist WORKER. Lies MOTD & CONFIG, dann arbeite Tasks aus dem Backlog ab.
```

### Einzeiler:
```
Lies .swarmops/SKILL.md, du bist WORKER. Lies MOTD & CONFIG, starte den Arbeits-Loop.
```

---

## 🚀 Kompletter Workflow (Beispiel)

### Schritt 1: SwarmOps installieren
Paste den **Installer-Prompt** oben in einen KI-Agenten. Er richtet alles automatisch ein.

### Schritt 2: Planner starten
```
Lies .swarmops/SKILL.md, du bist PLANNER-1. Lies MOTD & CONFIG, dann plane: 
Baue eine REST-API mit Express.js für User-Management mit Login, Registration und Profil-Bearbeitung.
```
→ Planner erstellt z.B. 6 Tasks in `backlog/`

### Schritt 3: Worker starten (3x parallel)
Öffne 3 Chat-Fenster und paste jeweils:
```
Lies .swarmops/SKILL.md, du bist WORKER. Lies MOTD & CONFIG, starte den Arbeits-Loop.
```
→ Worker-1 claimed TASK-001, Worker-2 claimed TASK-002, Worker-3 claimed TASK-003

### Schritt 4: Beobachten
```bash
echo "=== BACKLOG ===" && ls .swarmops/tasks/backlog/ 2>/dev/null || echo "(leer)"
echo "=== IN PROGRESS ===" && ls .swarmops/tasks/in-progress/ 2>/dev/null || echo "(leer)"  
echo "=== DONE ===" && ls .swarmops/tasks/done/ 2>/dev/null || echo "(leer)"
```

---

## 🔗 Links

- **Repository**: [github.com/LucazPlays/SwarmOps](https://github.com/LucazPlays/SwarmOps)
- **SKILL.md (Raw)**: [Raw Link](https://raw.githubusercontent.com/LucazPlays/SwarmOps/main/.swarmops/SKILL.md)
- **Planner-Prompt**: [Raw Link](https://raw.githubusercontent.com/LucazPlays/SwarmOps/main/.swarmops/prompts/planner.md)
- **Worker-Prompt**: [Raw Link](https://raw.githubusercontent.com/LucazPlays/SwarmOps/main/.swarmops/prompts/worker.md)
