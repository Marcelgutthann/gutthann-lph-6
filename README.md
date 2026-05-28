# LPH 6 - Vorbereitung der Vergabe - Plugin fuer Claude Code

> Automatische Erstellung von LPH 6 Berichten nach HOAI Paragraph 33 (Gebaeude und Innenraeume) - generisch fuer Architektur- und Planungsbueros.

## Was dieses Plugin macht

Wenn du in einem Projektordner `/lph6` eintippst, durchsucht Claude alle Projekt-Dateien (PDFs, DOCX, XLSX, MSG) und erstellt daraus einen kompletten LPH 6 Bericht als HTML.

## Installation

```
/plugin marketplace add github:Marcelgutthann/gutthann-claude-marketplace
/plugin install lph-6
```

Nach der Installation: Claude Code einmal neu starten.

## Nutzung

1. Im Projektordner Claude Code oeffnen
2. `CLAUDE.md` anlegen mit Projektdaten (Projektnummer, AG, Ort)
3. Pflicht-Dateien ablegen (siehe `templates/LPH6_Informationsliste.md` falls vorhanden)
4. `/lph6` eintippen
5. Claude erzeugt `LPH6_Report.html` im Projektordner

## Templates

| Datei | Zweck |
|---|---|
| `templates/LPH6_Template.html` | HTML-Template (druckfest, mit Platzhaltern) |
| `templates/LPH6_Checkliste.md` | Pflicht-Checkliste fuer LPH 6 |
| `templates/LPH6_Informationsliste.md` | Such-Patterns + Datenquellen-Heuristik |

## Eingebaute Lessons-Learned (verbindlich)

- **Druckfest**: Print-CSS mit `print-color-adjust:exact` fuer ALLE dunklen Elemente
- **Quellen-Belege**: QUELLEN-Block unter jeder Checkliste mit Datei + Datum + Herkunft
- **Goal-Cards druckbar**: schwarzer Text auf hellem BG mit Akzentstreifen
- **Kurze Bindestriche** in Ueberschriften
- **Bauherr vs. Projektsteuerer** klar getrennt
- **Pre-Flight Checklist** vor jedem fertig
