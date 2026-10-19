# TPM Board — Anlagen

Ein Lernprojekt von Dejan Vujic, erstellt mit Unterstützung von OpenAI Codex. Acht beispielhafte Anlagen mit Roboterbeladung, digitale TPM-Checks, Auffälligkeitsmeldungen und Prüfverlauf.

## Start

`index.html` im Browser öffnen oder einen lokalen statischen Webserver verwenden. Keine Installation oder externen Bibliotheken erforderlich.

## Funktionen

- Acht Anlagen auswählen
- TPM-Prüfung mit Kürzel, Bemerkung und nächstem Prüftermin dokumentieren
- Je Punkt: In Ordnung, Auffällig oder Nicht geprüft
- Auffällige Checks erzeugen automatisch eine offene Meldung
- Zusätzliche Meldungen mit Priorität erfassen und erledigen
- Prüfverlauf und Übersicht über fällige Prüfungen
- Speicherung im localStorage des jeweiligen Browsers
- Demo-Daten nach Bestätigung zurücksetzen

## Statuslogik

Offene Meldungen haben Vorrang. Danach folgen überfällige Prüftermine, fehlende aktuelle Prüfungen und unvollständige Prüfungen. Nur ein heutiger Check mit ausschließlich „In Ordnung“ erhält den grünen Prüfstatus. Eine erledigte Meldung ändert das historische Prüfprotokoll nicht. „Heute dokumentiert“ zählt auch unvollständige Protokolle, nicht nur erfolgreiche Checks. Die Termine sind Prüftermine, keine automatisch berechneten Wartungsintervalle.

Alle Zellen beginnen ungeprüft mit dem heutigen Prüftermin. Zeitangaben verwenden die lokale Browserzeit. Keine Live-Maschinendaten, Benutzerkonten, Serverdatenbank oder OEE-Berechnung.

## Dateien

- index.html: Seitenstruktur
- style.css: responsive Gestaltung
- app.js: Zustandsverwaltung, Eingaben, Darstellung und Speicherung

## GitHub Pages

Dateien direkt in ein Repository `tpm-board` hochladen. Settings → Pages → Deploy from a branch → main → / (root). Die tatsächliche Live-Adresse zeigt GitHub nach der Veröffentlichung an.

## Grenzen und Weiterentwicklung

Demonstration, kein betriebliches Freigabe- oder Sicherheitssystem. Beispiel-Prüfpunkte müssen gegen betriebliche Wartungspläne und Herstellerunterlagen geprüft werden. localStorage ist keine revisionssichere Dokumentation; Daten können durch Löschen der Browserdaten verloren gehen und werden nicht zwischen Geräten synchronisiert. Keine personenbezogenen oder betrieblich vertraulichen Daten für die öffentliche Demo verwenden.

Mögliche nächste Schritte: konkrete Beladung und Prüfpunkte anpassen, Wartungsintervalle, Filter, Export, Python-Backend und Datenbank.


## Wochenübersicht (3-Schichtbetrieb)

Matrix mit acht Anlagen, sieben Tagen und drei Schichten (168 Felder pro Woche). Früh 06–14 Uhr, Spät 14–22 Uhr, Nacht 22–06 Uhr am Folgetag. Nachtschichten werden dem Starttag zugeordnet. Wochen beginnen montags; Zeitbasis ist die lokale Browserzeit.

Jedes Feld ist anklickbar: Offen, Geplant, Geprüft, Auffällig oder Nicht vorgesehen. Notizen und Status werden im selben lokalen Browser-Datensatz gespeichert. Vorherige und nächste Wochen sind erreichbar. Die Statusanzeige enthält Symbole sowie ausgeschriebene zugängliche Beschriftungen und Tooltips.

Wichtig: Die Wochenmatrix ist ein separat gepflegter manueller TPM-Plan. Detaillierte Prüfprotokolle und Meldungen aktualisieren diese Schichtfelder nicht automatisch; der Wochenplan steuert auch nicht die Kennzahlen der Anlagenkarten. Damit bleiben Planung, manuelle Rückmeldung und tatsächliche Dokumentation getrennt erkennbar. Eine spätere Zuordnung von Prüfprotokollen zu Schichten ist eine mögliche Erweiterung. Keine Produktions- oder Maschinen-Livestatusanzeige.

## Kontakt zur Instandhaltung

Eine E-Mail-Adresse wird im Board hinterlegt und lokal gespeichert. Jede offene Meldung hat einen Kontaktbutton, der per mailto einen E-Mail-Entwurf mit Anlage, Priorität, Zeitpunkt, Meldungs-ID und Beschreibung vorbereitet. Der Benutzer prüft und versendet ihn in seinem Mailprogramm selbst. Voraussetzung ist ein konfiguriertes Mailprogramm oder Webmail-Protokollhandler. Es gibt keinen automatischen Versand, keinen Versandnachweis und keine automatische Statusänderung der Meldung. Das Zurücksetzen der Demo entfernt auch die Kontaktadresse.
