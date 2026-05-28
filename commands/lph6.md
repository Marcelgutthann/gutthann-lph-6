---
name: lph6
description: Erstellt einen vollstaendigen LPH 6 Bericht Vorbereitung der Vergabe (HOAI Paragraph 34, Gebaeude und Innenraeume) fuer ein beliebiges Architekturprojekt. Durchsucht alle Dateien im Projektordner, extrahiert Daten und befuellt das standardisierte HTML-Template. Baut auf der LPH 5 Dokumentation auf.
user-invocable: true
---

# LPH 6 Vorbereitung der Vergabe — Automatische Generierung

## OUTPUT-KONVENTION (verbindlich)

**WICHTIGSTE REGEL: Es wird ein EINZIGER Ordner namens `Claude/` im Projekt-Root erzeugt. ALLE Outputs landen dort drin. NIRGENDS sonst im Projekt.**

```
<Projekt-Root>/                           <- bleibt unveraendert
├── (die existierenden Projektordner)       (welche Struktur auch immer)
│
└── Claude/                               <- EINZIGER Ordner den wir anlegen
    ├── Projekt_Historie.md                 <- kumulative Wissensbasis
    ├── LPH_1/LPH1_Report_YYYY-MM-DD.html
    ├── LPH_2/LPH2_Report_YYYY-MM-DD.html
    ├── ... bis LPH_8/
    ├── Dashboard/Projekt_Dashboard_YYYY-MM-DD.html
    └── Fachplaner-Analyse/Fachplaner_Analyse_YYYY-MM-DD.md
```

**Dein konkreter Output-Pfad fuer diesen Skill:**
```
<Projekt-Root>/Claude/LPH_6/LPH6_Report_YYYY-MM-DD.html
```

**Pflichten beim Schreiben:**
1. Wenn `<Projekt-Root>/Claude/` nicht existiert: anlegen (mkdir)
2. Wenn `<Projekt-Root>/Claude/LPH_6` nicht existiert: anlegen
3. Datums-Format im Dateinamen: `YYYY-MM-DD` (z.B. 2026-05-27)
4. Bei jedem Aufruf: NEUE Datei mit aktuellem Datum (keine Ueberschreibung)

**NIEMALS schreibst du:**
- In andere Ordner des Projekts (00 Aktennotiz/, 11 Doku/, etc.) - keine Verschmutzung der Projekt-Struktur
- In den Projekt-Root direkt - nur in `Claude/` Unterstruktur
- In `~/.claude/plugins/` - das ist Read-only Plugin-Code
- In versteckte Ordner (.claude/) - nutze ausschliesslich `Claude/` (sichtbar)

---

## WISSENSBASIS NUTZEN

Falls `<Projekt-Root>/Claude/Projekt_Historie.md` existiert:
- ZUERST diese Datei lesen - sie enthaelt chronologisch alle E-Mails, Aktennotizen, Beschluesse
- Spart Zeit + Tokens (statt das ganze Projekt jedes Mal neu zu scannen)

Falls die Datei NICHT existiert:
- Empfehle dem User: "Tipp: Fuer aktuelle Daten zuerst /projekt-historie ausfuehren"
- Trotzdem das Projekt direkt scannen (Fallback)

---


## Template

Zentrale Ablage:
```
<via Plugin-Distribution geladen - Template liegt im Plugin selbst>
```

Kopiere nach `{Projekt}\13 Dokumentationen\Dokumentation LPH 6\LPH6_Report.html`.
Referenzen: `LPH6_Checkliste.md`, `LPH6_Informationsliste.md`.

## Ablauf — 6 Schritte

### Schritt 1: LPH 5 Dokumentation finden (PFLICHT)
- Suche nach `*LPH5*`, `*LPH_5*`, `*Ausfuehrung*Doku*`
- Pruefe: Werkplaene vollstaendig? Planverzeichnis final? Raumbuch?
- Extrahiere: Planverzeichnis, Bauteilkatalog, Massenermittlung

### Schritt 2: Projektordner durchsuchen
- **Ausschreibungsstand**: `**/Ausschreibungsstand.xlsx` (PFLICHTQUELLE - in allen Projekten standardisiert)
- **LVs**: `**/*LV*.pdf`, `**/*Leistungsverzeichnis*`, `**/*.X83`, `**/*.X81` (GAEB)
- **Gewerkeliste**: `**/*Gewerk*/**`
- **Massenermittlung**: `**/*Massen*.xlsx`, `**/*Aufmass*.pdf`
- **Kostenanschlag**: `**/*Kostenanschlag*.pdf`, `**/*KAS*`
- **CPV-Codes**: `**/*CPV*.pdf` (bei oeff. Vergabe)
- **Bieterlisten**: `**/*Bieter*.xlsx`
- **BVB/ZVB**: `**/*BVB*.docx`, `**/*ZVB*.docx`, `**/*Vertragsbedingungen*`

### Schritt 3: Daten extrahieren
Siehe `LPH6_Informationsliste.md`:
- **Ausschreibungsstrategie**: Einzel- vs. Generalvergabe, Lose, oeffentlich/privat
- **Gewerkeliste**: Nr. (01-15), Bezeichnung, KGR, LV-Stand, Fachplaner
- **LV-Struktur**: Positionen pro Gewerk, Alternativen, Eventualien, GAEB-Format
- **Massenermittlung**: Bauteil/Raum, Menge, Einheit, Quelle
- **Kostenanschlag DIN 276**: KGR 100-700, vs. Kostenberechnung LPH 3/4
- **CPV-Codes** (bei oeff. Vergabe)
- **Vergabeverfahren** je Gewerk (VOB/A § 3)
- **Terminplan Ausschreibung**: Versand LV, Bieterfragen, Submission, Vergabe
- **BVB/ZVB**: Gewaehrleistung, Zahlung, Vertragsstrafe, Sicherheiten
- **Bieterlisten** je Gewerk (mind. 3 bei beschraenkter Vergabe)
- **Ausschreibungsstand.xlsx**: Status je Gewerk

### Schritt 4: Template kopieren und befuellen
1. Kopiere `LPH6_Template.html` ins Projekt
2. Ersetze ALLE `{{PLATZHALTER}}`
3. HTML-Tabellen fuer alle `*_TABELLE`-Felder
4. Summenzeile Kosten mit CSS-Klasse `.sum-row` markieren
5. Sidebar `{{DATEILISTE}}`

### Schritt 5: Preisvergleich LPH 3 -> LPH 6
- KB LPH 3 (ggf. aktualisiert LPH 4/5) vs. Kostenanschlag LPH 6
- Je KGR Δ und Δ% berechnen
- Auffaelligkeiten markieren (Δ > 10%)
- Risikopuffer 5-10% bei KGR 300/400

### Schritt 6: Qualitaetspruefung
- PowerShell `Select-String` auf `{{`
- Preise netto/brutto mit MwSt
- Mengen VOB/C-konform
- Stil sachlich, technisch, passiv
- EU-Schwelle gepruft (aktuell 5,538 Mio. EUR fuer Bauleistungen)

## Design-Regeln
- Schwarz `#1a1a1a`, A4 quer, contenteditable, randlos
- Kostentabellen mit `.sum-row` fuer Summen

## Platzhalter-Referenz
Siehe `LPH6_Informationsliste.md`. Hauptfelder:
Basis-Platzhalter + 6.1 bis 6.12 + Abschluss
(`{{6_1_STAMMDATEN_TEXT}}`, `{{6_1_STRATEGIE_TEXT}}`, `{{6_2_GEWERKE_*}}`, `{{6_3_LV_*}}`, `{{6_4_MASSEN_*}}`, `{{6_5_KOSTEN_TEXT}}`, `{{6_5_KOSTEN_TABELLE}}`, `{{6_5_KOSTEN_VERGLEICH}}`, `{{6_6_CPV_*}}`, `{{6_7_VERFAHREN_*}}`, `{{6_8_TERMIN_*}}`, `{{6_9_BVB_TEXT}}`, `{{6_10_BIETER_*}}`, `{{6_11_AUSSCHR_*}}`, `{{6_12_OFFEN_*}}`, `{{ABSCHLUSS_TEXT}}`, `{{DATEILISTE}}`).
