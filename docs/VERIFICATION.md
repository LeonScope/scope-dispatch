# Verification / Prüfdokumentation

Recorded locally on **20 October 2026**. Python 3.11.6, OR-Tools 9.14.6206, Ollama 0.40.6 and Qwen3 4B were used. The application, data and full test exports remain private.

## Planning comparison

The baseline inserts jobs in input order at the earliest feasible arrival, checking skills, timing, travel and the fixed break. The search uses the same job set and constraints, with priority penalties for missed work and a one-second search budget.

| Scenario | Available technicians | Jobs | Baseline: assigned | Search: assigned | Baseline travel | Search travel |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| Normal day | 5 | 20 | 20 | 20 | 640 min | 468 min |
| Urgent camera job | 5 | 21 | 21 | 21 | 687 min | 514 min |
| Urgent job + one absence | 4 | 21 | 19 | 21 | 643 min | 524 min |

The baseline missed the urgent job in the combined scenario; the search included it. Travel includes the routes back to base. The cases use synthetic data and fixed travel times on a fictional road graph.

These are observed runs, not a guaranteed improvement, a global-optimum certificate or production performance data. The search is time bounded and can produce different valid results when processing availability changes. Adding fixed appointments also changes the problem; screenshots of those checks need not match the table above.

## Automated tests

**36 tests passed.** The suite checks:

- Exact job coverage, no duplicate visits, qualified assignments and absence handling.
- Arrival windows, travel between successive appointments, duration, lunch at the base and return before shift end.
- The urgent job, impossible arrival windows and missing skills.
- Preserving a locked appointment's person and exact time.
- Accepting eligible manual assignments and rejecting ineligible ones; applying the same requested person in the baseline comparison.
- Rejecting tampered arrival times, forged metrics and missing breaks.
- Every displayed road path uses real edges in the demo graph.
- A proposal does not change stored state; acceptance persists once and rejects stale revisions.
- Rejecting absence when it conflicts with a locked appointment and preventing duplicate emergency jobs.
- Intake field validation, unsupported model numbers, ungrounded skill suggestions, missing models and incomplete responses.
- Local HTTP state loading, origin/host checks, invalid JSON and denial of source/database paths.

The solver output has its own acceptance validator. The test suite also asserts timing and skill invariants directly, rather than only calling that validator.

## Local AI check

Six manually specified regression examples were sent to the running local model: four service requests, one without duration or times, and one without enough detail to identify a skill.

After validation, **all 24 expected fields matched**: skill, duration, earliest arrival and latest arrival for each example. The title and quoted passage are not included in that field score. These are development examples, not a held-out benchmark.

Two defects were found during development:

1. The model omitted the first boundary of an explicit arrival window. More precise field descriptions corrected the tested example.
2. It inferred robotics from a vague request for manufacturing support. A conservative domain-term check now clears such unsupported suggestions.

The application checks numeric support and verbatim evidence. Skill suggestions need a related term in the input. These checks do **not** prove that the model has correctly understood negation, conflicting statements, unusual wording or every possible service problem. A person must review the draft.

## Browser checks and recordings

The working application was operated in the local browser. Checks covered proposal acceptance and discard, an urgent job with an existing fixed appointment, a subsequent absence, an invalid skill assignment, an actual drag onto another technician's row, local AI intake through a completed planning proposal, the technician view, history and JSON export.

The downloaded export was validated against the scheduling rules. Saved state survived application restarts. A 390 px viewport was checked for responsive layout; the wide timeline remains horizontally scrollable within its own panel. The browser reported no captured console warnings or errors during the final check.

The MP4 is an approximately 22-second capture of actual browser interaction at normal speed. The GIF is a lower-frame-rate preview of that same recording. Screenshots are taken from the application. They are not proposed interface mockups.

## Scope limits

- Fictional people, customers, jobs and roads.
- One day, one skill per job, fixed shifts and a fixed break at base.
- No live traffic, GPS, street navigation or real dispatch integration.
- No execution clock or automatic protection of already completed work.
- A local single-operator application, not a deployed multi-user service.
- The technician screen is a view of confirmed data, without mobile offline synchronization.
- No general AI accuracy, business ROI or global optimality claim.

---

## Deutsch

Am **20. Oktober 2026** wurden lokal **36 automatisierte Tests** bestanden. Die Tabelle oben vergleicht die Planung nach Eingangsreihenfolge mit der zeitlich begrenzten Suche auf jeweils denselben Aufträgen und Bedingungen.

Im normalen Szenario planen beide Verfahren alle 20 Einsätze ein; die Fahrtzeit beträgt 640 beziehungsweise 468 Minuten. Mit Eilauftrag und Personalausfall schafft die Suche 21 von 21 Aufträgen, das Ausgangsverfahren 19 von 21. Die Werte stammen aus einer fiktiven Region mit festen Fahrtzeiten. Sie belegen weder reale Kundeneinsparungen noch einen global optimalen Plan.

Sechs Anfragen an das lokale KI-Modell ergaben nach der Validierung 24 passende strukturierte Felder. Bezeichnung und Belegzitat gehören nicht zu dieser Wertung. Die Beispiele wurden während der Entwicklung festgelegt und sind kein unabhängiger Genauigkeitstest. Gefundene Fehler bei Zeitfenstern und unbelegten Fachgebieten führten zu präziseren Feldbeschreibungen und zusätzlichen Prüfungen. Eine persönliche Kontrolle bleibt erforderlich.

Im Browser wurden die Übernahme und das Verwerfen von Vorschlägen, Eilauftrag, feste Zusage, Personalausfall, ungültige Zuordnung, tatsächliches Ziehen auf eine Technikerzeile, KI-Erfassung, Technikeransicht, Verlauf und Export geprüft. Der heruntergeladene Plan wurde nochmals gegen die Planungsregeln validiert. Die gespeicherten Daten blieben nach Neustarts erhalten.

Die etwa 22 Sekunden lange Aufnahme zeigt die echte Anwendung in normaler Geschwindigkeit. Die GIF-Vorschau verwendet dieselbe Aufnahme mit geringerer Bildrate. Der Quellcode, die Datenbank, lokale Modelle und vollständigen Testartefakte werden nicht veröffentlicht.
