# 🐝 SwarmOps – Schnellstart

> **Kopiere EINEN der Prompts unten und paste ihn in einen beliebigen KI-Agenten. Fertig.**

---

## 🔧 1. Installation (einmalig)

Diesen Prompt in einen KI-Agenten pasten – er installiert SwarmOps komplett im aktuellen Projekt:

```
Installiere das SwarmOps Multi-Agent-System in diesem Projekt. Gehe dabei exakt diese Schritte durch:

1. HERUNTERLADEN – Lade jede dieser Dateien von GitHub herunter und speichere sie exakt unter dem angegebenen Pfad (relativ zum Projekt-Root). Erstelle alle nötigen Verzeichnisse automatisch:

   https://raw.githubusercontent.com/LucazPlays/SwarmOps/main/.swarmops/SKILL.md         → .swarmops/SKILL.md
   https://raw.githubusercontent.com/LucazPlays/SwarmOps/main/.swarmops/MOTD.md          → .swarmops/MOTD.md
   https://raw.githubusercontent.com/LucazPlays/SwarmOps/main/.swarmops/CONFIG.md        → .swarmops/CONFIG.md
   https://raw.githubusercontent.com/LucazPlays/SwarmOps/main/.swarmops/prompts/planner.md → .swarmops/prompts/planner.md
   https://raw.githubusercontent.com/LucazPlays/SwarmOps/main/.swarmops/prompts/worker.md  → .swarmops/prompts/worker.md
   https://raw.githubusercontent.com/LucazPlays/SwarmOps/main/.swarmops/prompts/setup.md   → .swarmops/prompts/setup.md

2. VERZEICHNISSE ANLEGEN – Erstelle diese vier Ordner:
   .swarmops/tasks/backlog/
   .swarmops/tasks/in-progress/
   .swarmops/tasks/review/
   .swarmops/tasks/done/

3. MOTD AUSFÜLLEN – Analysiere das aktuelle Projekt vollständig (lies package.json, README, Ordnerstruktur, Linter-Configs, .editorconfig, Dockerfiles, etc.) und fülle .swarmops/MOTD.md automatisch aus:
   - Projektname
   - Beschreibung
   - Tech-Stack (Sprache, Framework, DB, Styling, Testing)
   - Architektur-Überblick (Ordnerstruktur)
   - Coding-Standards (aus vorhandenen Configs ableiten)
   - Aktuelle Ziele (aus README oder offenen Issues ableiten)

4. BESTÄTIGUNG – Gib am Ende aus:
   - ✅ Welche Dateien installiert wurden
   - 📋 Den Inhalt der ausgefüllten MOTD.md
   - 🧠 Den Planner-Prompt zum Kopieren
   - 👷 Den Worker-Prompt zum Kopieren
```

---

## 🧠 2. Planner starten

Nach der Installation – diesen Prompt in einen KI-Agenten pasten:

```
Lies .swarmops/SKILL.md, du bist PLANNER-1. Lies MOTD & CONFIG, dann plane die folgende Aufgabe: [DEINE AUFGABE HIER BESCHREIBEN]
```

---

## 👷 3. Worker starten

Pro Worker-Agent einmal diesen Prompt pasten (beliebig viele parallel):

```
Lies .swarmops/SKILL.md, du bist WORKER. Lies MOTD & CONFIG, starte den Arbeits-Loop.
```

---

## Das war's. 🎉

```
Installation:  1 Prompt → Agent richtet alles ein
Planner:       1 Prompt → Agent erstellt Tasks
Worker:        1 Prompt → Agent arbeitet Tasks ab (x-mal parallel starten)
```

Mehr Infos: [github.com/LucazPlays/SwarmOps](https://github.com/LucazPlays/SwarmOps)
