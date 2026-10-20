# Scope Dispatch

[English](README.md) · **Deutsch**

### Fünf Techniker. Zwanzig Aufträge. Und dann ändert sich der Plan.

Scope Dispatch ist eine lokale Anwendung zur Einsatzplanung für ein fiktives technisches Serviceteam. Sie ordnet Aufträge geeigneten Fachkräften zu, berücksichtigt Ankunftsfenster und Fahrtzeiten und zeigt Änderungen vor der Übernahme.

Ich habe das Projekt mit Codex entwickelt, um einen weiteren Bereich industrieller Software aufzugreifen: die Organisation der Menschen, die Kamerasysteme, Roboter und Fertigungsanlagen betreuen.

![Scope Dispatch mit Servicerouten, Auftragsdetails und Tagesplanung](assets/dispatch-overview.jpg)

## Eine Änderung durch den Plan verfolgen

Eine Kameraprüfung fällt aus und benötigt dringend Unterstützung. Scope Dispatch ergänzt den Auftrag, berechnet einen neuen Vorschlag und zeigt, welche Termine sich ändern würden. Ein fest zugesagter Termin behält seine Fachkraft und Ankunftszeit. Fällt jemand aus, lässt sich die Arbeit auf das verbleibende Team verteilen.

[Bildschirmaufnahme ansehen](assets/dispatch-walkthrough.mp4) · [Aufbau und Entscheidungen](docs/CASE_STUDY.de.md)

![Kurze Vorschau aus der tatsächlich bedienbaren Anwendung](assets/dispatch-preview.gif)

Karte und Zeitachse verwenden denselben berechneten Plan. Die Wege folgen einem fiktiven Straßennetz mit festen Fahrtzeiten. Live-Navigation und Verkehrsdaten sind nicht enthalten.

## Was sich bedienen lässt

- **Einen Servicetag planen.** Fünf Techniker, vier Fachgebiete, Ankunftsfenster, Einsatzdauer und eine gemeinsame Mittagspause an der Servicebasis.
- **Änderungen prüfen.** Jeder Vorschlag zeigt seine Auswirkungen, bevor er gespeichert wird. Nicht eingeplante Aufträge bleiben sichtbar.
- **Zusagen schützen.** Ein Termin lässt sich auf eine bestimmte Fachkraft und genaue Ankunftszeit festlegen.
- **Aufträge neu zuordnen.** Per Ziehen auf eine andere Technikerzeile oder über die Auswahl. Die Anwendung prüft Qualifikation und Verfügbarkeit und schlägt passende Zeiten vor.
- **Anfragen mit lokaler KI vorbereiten.** Ein Sprachmodell überträgt eine Servicenachricht in einen Entwurf. Fehlende oder nicht belegte Angaben bleiben leer. Eine Person prüft die Angaben und wählt Kunde und Standort.
- **Den bestätigten Plan nutzen.** Eine kompakte Technikeransicht, der Änderungsverlauf und ein lokaler Export greifen auf den übernommenen Stand zu.

![Ein lokales KI-Modell bereitet eine Serviceanfrage zur persönlichen Prüfung vor](assets/local-ai-intake.jpg)

## Was ich geprüft habe

Im aufgezeichneten Vergleich für den normalen Tag planen beide Verfahren alle 20 Aufträge ein. Die gesamte Fahrtzeit beträgt **640 Minuten** bei Planung nach Eingangsreihenfolge und **468 Minuten** beim berechneten Vorschlag. Im kombinierten Szenario mit Eilauftrag und Personalausfall plant die Suche **21 von 21 Aufträgen** ein; das Ausgangsverfahren schafft **19 von 21**.

Diese Werte stammen aus dem fiktiven Datensatz. Sie sind keine Einsparungen bei einem Kunden und kein Nachweis für den bestmöglichen Plan. Die Suche ist zeitlich begrenzt; ihre Ergebnisse können mit der verfügbaren Rechenzeit variieren.

**36 automatisierte Tests sind bestanden.** Bei sechs Anfragen an das lokale Modell stimmen nach der Validierung außerdem alle 24 erwarteten strukturierten Felder. Diese kleine Prüfung erlaubt keine allgemeine Aussage zur Modellgenauigkeit. Die [Prüfdokumentation](docs/VERIFICATION.md) enthält die Vergleiche, Browserprüfungen, während der Entwicklung gefundene Modellfehler und die Grenzen der Demo.

## Nur die Präsentation ist öffentlich

Dieses Repository enthält Dokumentation und Aufnahmen. **Quellcode, ausführbare Anwendung, Konfiguration, Datenbank, Modelldateien und vollständige Testartefakte bleiben privat.** Es gibt keine öffentlich gehostete Anwendung.

Für eigene Inhalte wird keine Open-Source- oder Creative-Commons-Lizenz erteilt. [Rechte](RIGHTS.md) · [Verwendete Software Dritter](THIRD_PARTY_NOTICES.md).

Eigenständiges Projekt von **LeonScope**, entwickelt mit Codex.
