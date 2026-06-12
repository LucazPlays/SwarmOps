---
name: swarmops
description: >
  Multi-Agent Koordinationssystem für parallele KI-Entwicklung.
  Ermöglicht es einem Planner-Agent Tasks zu erstellen und mehreren Worker-Agents
  diese gleichzeitig konfliktfrei abzuarbeiten.
---

# SwarmOps – Multi-Agent Collaboration Skill

> **Ein dateibasiertes Koordinationssystem, mit dem mehrere KI-Agenten parallel an einem Projekt arbeiten können, ohne sich in die Quere zu kommen.**

---

## 🧭 Überblick

SwarmOps organisiert KI-Zusammenarbeit über **drei Rollen**:

| Rolle       | Aufgabe                                     | Anzahl  |
|-------------|---------------------------------------------|---------|
| **Planner** | Analysiert Anforderungen, erstellt Tasks     | 1       |
| **Worker**  | Claimed und bearbeitet einzelne Tasks        | 1–N     |
| **Human**   | Gibt Ziel vor, reviewed Ergebnisse           | 1       |

---

## 📁 Dateistruktur

```
.swarmops/
├── SKILL.md                 ← Du liest gerade diese Datei
├── MOTD.md                  ← Projekt-Kontext (Ziele, Stack, Regeln)
├── CONFIG.md                ← System-Konfiguration
├── prompts/
│   ├── planner.md           ← Prompt für den Planner-Agent
│   ├── worker.md            ← Prompt für jeden Worker-Agent
│   └── setup.md             ← Mini-Prompt zum Initialisieren
└── tasks/
    ├── backlog/             ← Offene Tasks (vom Planner erstellt)
    ├── in-progress/         ← Aktuell in Bearbeitung (von Worker geclaimed)
    ├── review/              ← Fertig, wartet auf Review
    └── done/                ← Abgeschlossen & verifiziert
```

---

## 📋 Task-Datei Format

Jeder Task ist eine eigenständige Markdown-Datei. Der Dateiname folgt dem Schema:
`TASK-XXX_kurztitel.md` (z.B. `TASK-001_auth-login.md`)

```markdown
# TASK-XXX: Kurzer, beschreibender Titel

| Feld         | Wert                              |
|-------------|-----------------------------------|
| Priority    | 🔴 HIGH / 🟡 MEDIUM / 🟢 LOW     |
| Size        | S / M / L / XL                    |
| Created     | YYYY-MM-DDTHH:MM:SS+TZ           |
| Claimed-By  | – (Agent-ID beim Claim eintragen) |
| Claimed-At  | – (Timestamp beim Claim eintragen)|
| Depends-On  | TASK-YYY oder "none"              |

## Beschreibung

Detaillierte Beschreibung der Aufgabe. Was genau soll implementiert,
geändert oder gefixt werden? Kontext und Hintergründe.

## Akzeptanzkriterien

- [ ] Kriterium 1: Konkret und prüfbar
- [ ] Kriterium 2: Konkret und prüfbar
- [ ] Kriterium 3: Konkret und prüfbar

## Betroffene Dateien

- `pfad/zur/datei1.ext` – Was dort zu ändern ist
- `pfad/zur/datei2.ext` – Was dort zu ändern ist

## Kontext & Hinweise

Zusätzliche Informationen, Links, Code-Beispiele oder Referenzen,
die dem Worker helfen, den Task effizient zu bearbeiten.

## Progress Log

<!-- Worker fügt hier chronologische Einträge hinzu -->
<!-- Format: [YYYY-MM-DD HH:MM] AGENT-ID: Nachricht -->
```

### Regeln für Task-Dateien

1. **Dateiname = Identität**: `TASK-XXX_kurztitel.md` – die Nummer ist einzigartig
2. **Nummerierung**: Fortlaufend, 3-stellig, mit führenden Nullen (001, 002, ...)
3. **Jeder Task ist atomar**: Ein Task = eine in sich geschlossene Arbeitseinheit
4. **Keine halben Sachen**: Ein Task wird entweder komplett erledigt oder gar nicht
5. **Progress Log ist Pflicht**: Jeder Arbeitsschritt wird dokumentiert

---

## 🔄 Claim-Protokoll (Race-Condition-Schutz)

Das Claim-Protokoll stellt sicher, dass nie zwei Agents am selben Task arbeiten.

### Schritt-für-Schritt:

```
┌─────────────────────────────────────────────────────┐
│  1. SCAN    → Lese tasks/backlog/ Verzeichnis       │
│  2. SELECT  → Wähle Task (Priorität + Dependencies) │
│  3. CLAIM   → Verschiebe Datei nach in-progress/    │
│  4. TAG     → Schreibe Claimed-By & Claimed-At      │
│  5. WORK    → Arbeite den Task komplett ab           │
│  6. VERIFY  → Prüfe alle Akzeptanzkriterien         │
│  7. MOVE    → Verschiebe nach done/ oder review/    │
│  8. LOOP    → Zurück zu Schritt 1                   │
└─────────────────────────────────────────────────────┘
```

### Konflikt-Erkennung:

- **Datei nicht mehr in `backlog/`?** → Bereits geclaimed. Nächsten Task wählen.
- **`mv`-Befehl schlägt fehl?** → Datei wurde gleichzeitig verschoben. Nächsten Task wählen.
- **Niemals** eine Datei in `in-progress/` überschreiben oder claimen.

### Prioritäts-Reihenfolge:

1. 🔴 HIGH-Priority Tasks zuerst
2. 🟡 MEDIUM-Priority Tasks danach
3. 🟢 LOW-Priority Tasks zuletzt
4. Bei gleicher Priorität: niedrigere Task-Nummer zuerst
5. **NIEMALS** einen Task claimen, dessen `Depends-On` noch nicht in `done/` liegt

---

## 📝 Progress-Log Format

Jeder Worker dokumentiert seinen Fortschritt im Progress-Log des Tasks:

```markdown
## Progress Log

[2026-06-12 21:30] WORKER-1: Task geclaimed, starte Analyse
[2026-06-12 21:35] WORKER-1: Datei src/auth.ts erstellt, Grundgerüst steht
[2026-06-12 21:42] WORKER-1: Login-Logik implementiert, Tests geschrieben
[2026-06-12 21:45] WORKER-1: Alle Akzeptanzkriterien erfüllt ✅ → move to done
```

### Regeln:

- **Timestamp** in `[YYYY-MM-DD HH:MM]` Format
- **Agent-ID** direkt nach dem Timestamp
- **Statusmeldungen** bei: Start, Meilensteine, Probleme, Abschluss
- **Akzeptanzkriterien** einzeln abhaken: `- [x] Kriterium erfüllt`

---

## 🚫 Regeln für alle Agents

### DO:
- ✅ Immer die MOTD.md lesen bevor du startest
- ✅ Immer nur EINEN Task gleichzeitig bearbeiten
- ✅ Task KOMPLETT fertigstellen bevor du den nächsten nimmst
- ✅ Progress Log führen
- ✅ Akzeptanzkriterien als Checkliste nutzen
- ✅ Dependencies prüfen bevor du einen Task claimst

### DON'T:
- ❌ Niemals Dateien anderer Agents in `in-progress/` anfassen
- ❌ Niemals einen Task halb fertig nach `done/` verschieben
- ❌ Niemals Tasks in `backlog/` editieren (nur der Planner darf das)
- ❌ Niemals zwei Tasks gleichzeitig claimen
- ❌ Niemals an Dateien arbeiten, die einem anderen Task zugeordnet sind

---

## 🛠 Befehle (für Agents)

### Backlog scannen
```bash
ls -la .swarmops/tasks/backlog/
```

### Task claimen
```bash
mv .swarmops/tasks/backlog/TASK-XXX_titel.md .swarmops/tasks/in-progress/
```

### Task abschließen
```bash
mv .swarmops/tasks/in-progress/TASK-XXX_titel.md .swarmops/tasks/done/
```

### Task zum Review geben
```bash
mv .swarmops/tasks/in-progress/TASK-XXX_titel.md .swarmops/tasks/review/
```

### Gesamtstatus prüfen
```bash
echo "=== BACKLOG ===" && ls .swarmops/tasks/backlog/ 2>/dev/null || echo "(leer)"
echo "=== IN PROGRESS ===" && ls .swarmops/tasks/in-progress/ 2>/dev/null || echo "(leer)"
echo "=== REVIEW ===" && ls .swarmops/tasks/review/ 2>/dev/null || echo "(leer)"
echo "=== DONE ===" && ls .swarmops/tasks/done/ 2>/dev/null || echo "(leer)"
```

---

## 🚀 Quick-Start

1. **Setup**: Kopiere `.swarmops/` in dein Projekt-Root
2. **MOTD anpassen**: Editiere `MOTD.md` mit Projekt-Kontext
3. **Planner starten**: Nutze den Prompt aus `prompts/planner.md`
4. **Worker starten**: Nutze den Prompt aus `prompts/worker.md` (pro Agent 1x)
5. **Beobachten**: Status prüfen mit dem Gesamtstatus-Befehl oben
