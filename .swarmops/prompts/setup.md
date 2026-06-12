# 🚀 SwarmOps – Quick-Start Prompts

> **Kopiere einfach einen der Prompts unten und starte damit einen KI-Agenten.**
> Die SKILL.md wird automatisch von GitHub geladen.

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

## 🛠 Erstmalige Projekt-Einrichtung

Wenn du SwarmOps zum ersten Mal in ein neues Projekt integrierst:

### Variante A: Repo klonen
```bash
git clone git@github.com:LucazPlays/SwarmOps.git /tmp/swarmops-temp
cp -r /tmp/swarmops-temp/.swarmops/ /pfad/zu/deinem/projekt/.swarmops/
rm -rf /tmp/swarmops-temp
```

### Variante B: Nur .swarmops/ kopieren (wenn schon geklont)
```bash
cp -r .swarmops/ /pfad/zu/deinem/projekt/.swarmops/
```

### Variante C: Per KI-Agent einrichten lassen
```
Klone das SwarmOps-System von https://github.com/LucazPlays/SwarmOps in dieses Projekt. Kopiere den .swarmops/ Ordner hierher. Fülle dann die MOTD.md aus mit:
- Projektname: [NAME]
- Tech-Stack: [STACK]  
- Beschreibung: [BESCHREIBUNG]
```

---

## 🚀 Kompletter Workflow (Beispiel)

### Schritt 1: Planner starten
```
Lies .swarmops/SKILL.md, du bist PLANNER-1. Lies MOTD & CONFIG, dann plane: 
Baue eine REST-API mit Express.js für User-Management mit Login, Registration und Profil-Bearbeitung.
```
→ Planner erstellt z.B. 6 Tasks in `backlog/`

### Schritt 2: Worker starten (3x parallel)
Öffne 3 Chat-Fenster und paste jeweils:
```
Lies .swarmops/SKILL.md, du bist WORKER. Lies MOTD & CONFIG, starte den Arbeits-Loop.
```
→ Worker-1 claimed TASK-001, Worker-2 claimed TASK-002, Worker-3 claimed TASK-003

### Schritt 3: Beobachten
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
