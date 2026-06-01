# LPH 6 — Informationsliste

## Quelle der Felder — Projektanalyse

| Feldgruppe | Herkunft aus Projektanalyse |
|---|---|
| `Ausschreibungsstand.xlsx` | Konsistent in (Projekt-Nr.), (Projekt-Nr.), (Projekt-Nr.), (Projekt-Nr.), (Projekt-Nr.), (Projekt-Nr.) — Standardformat je `13 Doku/Doku LPH 6/` |
| CPV-Codes | Referenzprojekt (Quartier) — `6_LP6_VDV/CPV-Codes.pdf` |
| Gewerkstruktur | Referenz-Projekt B (Sporthalle) — `06 Gewerk/` mit Nummerierung 04, 05, 07, 22, 29 |
| Kostenanschlag DIN 276 | HOAI § 34 + Standardarchitektur-Praxis |

## Pflicht-Quellen im Projektordner

| Quelle | Suchpfad | Zweck |
|---|---|---|
| LPH 5 Report | `**/LPH5_Report*.html` | Brücke |
| Ausschreibungsstand | `**/13 Doku*/**/Ausschreibungsstand.xlsx`, `**/13 Dokumentationen/**/Ausschreibungsstand.xlsx` | 6.11 |
| LV-Dateien | `**/06 Gewerk*/**/*.X83`, `**/*.X81`, `**/*LV*.pdf`, `**/*Leistungsverzeichnis*.docx` | 6.3 |
| Massenermittlung | `**/*Massen*.xlsx`, `**/*Aufmass*.pdf` | 6.4 |
| Kostenanschlag | `**/*Kostenanschlag*.pdf`, `**/*KAS*.xlsx` | 6.5 |
| CPV-Codes | `**/*CPV*.pdf` | 6.6 |
| Bieterlisten | `**/*Bieter*.xlsx`, `**/*Bieterliste*.pdf` | 6.10 |
| Bauzeitenplan | `**/*Bauzeit*.pdf`, `**/*Terminplan*.pdf` | 6.8 |
| BVB/ZVB Vorlagen | `**/*BVB*.docx`, `**/*ZVB*.docx`, `**/*Vertragsbedingungen*.pdf` | 6.9 |

## Platzhalter-Referenz → Herkunft

| Platzhalter | Datenquelle | Typ |
|---|---|---|
| Basis-Platzhalter | LPH 5 Report | Text |
| `{{6_1_STAMMDATEN_TEXT}}` | LPH 5 Report | Fließtext |
| `{{6_1_STAMMDATEN_TABELLE}}` | Beteiligtenliste | HTML `<table class="proj-table">` |
| `{{6_1_STRATEGIE_TEXT}}` | AG-Entscheidung / Protokoll | Fließtext |
| `{{6_2_GEWERKE_TEXT}}` | Gewerkeliste | Einleitungstext |
| `{{6_2_GEWERKE_TABELLE}}` | Ausschreibungsstand.xlsx | HTML `<table>`: Gewerk-Nr., Bezeichnung, KGR, LV-Stand, Fachplaner |
| `{{6_3_LV_TEXT}}` | LV-Dateien | Fließtext |
| `{{6_3_LV_TABELLE}}` | LV-Inhalte | HTML `<table>`: Gewerk, Positionen, Alternativen, Eventual, Format |
| `{{6_4_MASSEN_TEXT}}` | Massenermittlung | Fließtext |
| `{{6_4_MASSEN_TABELLE}}` | Massenermittlung.xlsx | HTML `<table>`: Bauteil/Raum, Menge, Einheit, Quelle |
| `{{6_5_KOSTEN_TEXT}}` | Kostenanschlag | Fließtext max. 5 Sätze |
| `{{6_5_KOSTEN_TABELLE}}` | Kostenanschlag DIN 276 | HTML `<table>` KGR 100–700 mit Summenzeile `.sum-row` |
| `{{6_5_KOSTEN_VERGLEICH}}` | Kostenberechnung LPH 3 vs. KAS | HTML `<table>`: KGR, LPH 3, LPH 6, Δ, Δ% |
| `{{6_6_CPV_TEXT}}` | CPV-Codes.pdf | Fließtext (nur bei öff. Vergabe) |
| `{{6_6_CPV_TABELLE}}` | CPV-Codes.pdf | HTML `<table>`: Gewerk, CPV-Code, Bezeichnung |
| `{{6_7_VERFAHREN_TEXT}}` | Vergabeentscheidung | Fließtext |
| `{{6_7_VERFAHREN_TABELLE}}` | Vergabeübersicht | HTML `<table>`: Gewerk, Verfahrensart, Rechtsgrundlage |
| `{{6_8_TERMIN_TEXT}}` | Bauzeitenplan | Fließtext |
| `{{6_8_TERMIN_TABELLE}}` | Ausschreibungsterminplan | HTML `<table>`: Gewerk, Versand LV, Fragen, Submission, Vergabe |
| `{{6_9_BVB_TEXT}}` | BVB/ZVB-Dokumente | Fließtext: Zusammenfassung Gewährl., Zahlung, Strafe, Sicherheiten |
| `{{6_10_BIETER_TEXT}}` | Bieterlisten | Fließtext |
| `{{6_10_BIETER_TABELLE}}` | Bieterliste je Gewerk | HTML `<table>`: Gewerk, Bieter 1–n, Kontakte, Status |
| `{{6_11_AUSSCHR_TEXT}}` | Ausschreibungsstand.xlsx | Fließtext: Stand in Zahlen |
| `{{6_11_AUSSCHR_TABELLE}}` | Ausschreibungsstand.xlsx | HTML `<table>`: Gewerk, Status, LV-Volumen, Verfahren, Submission, Vergabesumme |
| `{{6_12_OFFEN_TEXT}}` / `{{6_12_OFFEN_TABELLE}}` | Protokolle | Fließtext + HTML Tabelle |
| `{{ABSCHLUSS_TEXT}}`, `{{DATEILISTE}}` | Standard | Text / `<li>` |

## Stil-Vorgaben

- Fachbegriffe: HOAI § 34, VOB/A + VOB/B + VOB/C, DIN 276, StLB-Bau, GAEB, CPV
- Preise mit „netto/brutto" und MwSt-Hinweis
- Mengen mit VOB/C-Aufmaßregeln nachvollziehbar
