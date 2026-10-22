# Datenschutzerklärung

Gilt für die Browser-Erweiterung **Hangar-Exporter** (Chrome, Edge, Firefox), ab Version 0.5.0. Herausgeber ist der Inhaber dieses Repositorys; Kontakt über das GitHub-Konto des Repositorys. Der Herausgeber betreibt keinen Server, der Daten der Nutzer empfängt.

## 1. Was die Erweiterung tut

Die Erweiterung liest auf Knopfdruck die Hangar-Seiten deines eigenen Kontos bei RSI (`robertsspaceindustries.com`), mit deiner bestehenden Anmeldung im Browser, und gibt das Ergebnis dorthin, wo du es im Fenster hinschickst. Sie liest nur und ändert bei RSI nichts. Es passiert nichts von selbst: Erst wenn du **Hangar lesen** drückst, wird gelesen, gespeichert oder gesendet, und immer an genau **ein** Ziel.

Beim Basetool kommt dazu, was du selbst auslöst: **Anmelden** und **Trennen** (sie sprechen mit der Anmeldeadresse des Basetool; nach der Anmeldung meldet die Erweiterung an die Daten-Adresse noch die gewählte Bezeichnung, ohne dass dein Hangar gelesen wird) und nach **Hangar lesen** eine Vorschau. Für die Vorschau fragt die Erweiterung das Basetool nach deinen vorhandenen Schiffen und nennt ihm die Namen der Schiffstypen, damit es sie zuordnen kann. Geschrieben wird erst, wenn du **Jetzt senden** drückst.

## 2. Wohin Daten gehen (nur auf deine Wahl)

| Ziel | Was geht dorthin | Wohin |
|---|---|---|
| Datei | Hangar-Daten als CSV oder JSON: je Pledge Name, Pledge-Nummer, Kaufdatum, Preis (USD) und Inhalt. Gutscheincodes sind geschwärzt, Spitznamen fehlen; nur wenn du es im Fenster für eine Datei einschaltest, stehen sie darin | Download-Ordner deines Rechners |
| VerseKit | Schiffsliste: je Schiff Name, Hersteller, Versicherung, Paket, Pledge-Nummer, Kaufdatum und Kaufpreis (USD); nie Spitznamen, Gutscheincodes oder Ausstattung | nur `127.0.0.1` (dein Rechner) |
| Basetool | Schiffe deines Hangars: Name des Schiffstyps (zum Zuordnen), Versicherung, je Schiff eine daraus gebildete Kennung (Prüfsumme, nie die rohe Pledge-Nummer) und der Name des Schiffs im Basetool (ohne den Haken nur der Name, den das Basetool schon hat; mit dem Haken **Spitznamen mitsenden** auch dein Spitzname). Bei der Anmeldung dazu die von dir gewählte Bezeichnung dieser Installation; in jeder Anfrage an die Daten-Adresse auch Name und Version der Erweiterung samt der öffentlichen Adresse des Projekts (`Hangar-Exporter/<Version> (+https://github.com/Drachennarr/Hangar-Exporter-Releases)`) | `ingest.profit-base.online` (Daten) und `profit-base.online` (Anmeldung), erst nach deiner Anmeldung im Basetool |

**Zum Basetool** werden keine Kaufpreise, Kaufdaten oder Pledge-Nummern im Klartext, keine Gutscheincodes, Seriennummern, Zugangsdaten oder Sitzungs-Token von RSI übertragen. Bei Änderungen kommt, soweit das Basetool sie selbst geliefert hat, die Ortsangabe des Schiffs wieder mit zurück. **An keinem Ziel** werden Seriennummern, Zugangsdaten oder Sitzungs-Token von RSI ausgegeben. Beim Basetool werden die Daten vom Betreiber des Basetool nach dessen eigenen Bedingungen verarbeitet; dafür gilt dessen Datenschutzerklärung (siehe das [Projekt auf GitHub](https://github.com/krt-profit/basetool)).

## 3. Was nicht passiert

Keine Analyse, keine Statistik, keine Werbung, keine Weitergabe an Dritte, keine Fremdbibliotheken, kein nachgeladener Code. Die Erweiterung verbindet sich nur mit `robertsspaceindustries.com` (Hangar-Seiten deines Kontos, auf Wunsch die Buy-back-Seiten und die öffentliche Schiffsliste), mit `127.0.0.1` und, wenn du das Basetool als Ziel nutzt, mit den beiden oben genannten Basetool-Adressen. Sie nutzt weder die Web-Sitzung noch Cookies des Basetool.

**Updates in Firefox:** Das Firefox-Paket trägt im Manifest eine feste Update-Adresse in diesem Repository (`updates.json`). Diese Adresse fragt **Firefox** ab, nicht die Erweiterung. Aus deinem Hangar geht dabei nichts an GitHub; GitHub sieht beim Abruf nur die Internetadresse (IP) deines Rechners. Chrome und Edge bekommen keine Update-Adresse von dieser Erweiterung.

## 4. Was lokal im Browser gespeichert wird

- Kopplungscodes (Port und Zugangswert) für VerseKit, im Speicher der Erweiterung (`storage.local`).
- Die zuletzt gewählte Option des Ziel-Menüs im Fenster (nur der Name des Eintrags, zum Beispiel `csv`), im Speicher der Erweiterung (`storage.local`), damit sie beim nächsten Öffnen vorausgewählt ist. Das Fenster auf der Seite greift dafür nie selbst auf den Speicher zu; es bittet das Hintergrundprogramm der Erweiterung darum.
- Für das Basetool zusätzlich der gemessene Zeitversatz deiner Uhr gegenüber dem Server (je Server eine Zahl und der Zeitpunkt der Messung, höchstens zwölf Stunden gültig), im Speicher der Erweiterung (`storage.local`), damit die Nachweise der Anmeldung auch nach einem Neustart des Hintergrundprogramms zur Serverzeit passen.
- Für das Basetool: ein Zugriffsschlüssel (Refresh-Token) und die von dir gewählte Bezeichnung der Installation im Speicher der Erweiterung (`storage.local`), der nicht exportierbare Schlüssel für den Nachweis der Anmeldung (DPoP) in der Datenbank der Erweiterung (IndexedDB) sowie der zuletzt abgeglichene Stand deiner Schiffe im Basetool (Namen, Orte, Versicherungen, Kennungen), damit nur Änderungen gesendet werden (`storage.local`). Hat das Basetool eine Sendung wegen eines aufgebrauchten Kontingents abgelehnt, wird gemerkt, bis wann nichts weiter gesendet wird (nach der Antwort des Basetool, sonst bis zum Ende des Tages beziehungsweise eine Stunde; `storage.local`). In Chrome und Edge sperrt die Erweiterung diesen Speicher auch für ihre eigenen Skripte auf den RSI-Seiten; nur das Hintergrundprogramm der Erweiterung liest ihn.
- Während einer Anmeldung liegt der Geräte-Code nur im Arbeitsspeicher des Browsers (`storage.session`) und verschwindet spätestens, wenn der Browser geschlossen wird.
- Nichts davon wird in `storage.sync` abgelegt, also nicht über dein Browser-Konto auf andere Geräte synchronisiert. Zugangswerte erscheinen nicht in Protokollen, Meldungen oder Exportdateien; die Erweiterung schreibt keine Protokolle. Ausnahme: Hält das Basetool eine Sendung wegen vieler Entfernungen an, zeigt das Fenster einmal die Adresse zum Bestätigen im Browser an (nicht gespeichert, nach 30 Minuten wieder entfernt). Die Vorschau zeigt auch Namen deiner Schiffe, die das Basetool schon kennt (nur im Fenster, nichts davon wird gespeichert oder weitergegeben).

Für Firefox nennt das Paket dem Browser, welche Daten die Erweiterung im Zusammenhang mit dem Basetool übermitteln kann: Nichts ist Pflicht, optional sind die Anmeldung beim Basetool und der Inhalt deines Hangars (Schiffe), und zwar nur, wenn du das Basetool als Ziel nutzt.

## 5. Löschen und Trennen

- **Trennen** im Fenster (je Ziel): Beim Basetool wird der Zugriffsschlüssel (Refresh-Token) beim Basetool widerrufen und danach lokal gelöscht, ebenso der Schlüssel, die Bezeichnung, der gemerkte Stand, eine gemerkte Wartezeit, der gemerkte Zeitversatz der Uhr und eine begonnene Anmeldung. Lässt sich der Widerruf nicht bestätigen (zum Beispiel ohne Netz), wird trotzdem lokal gelöscht und das Fenster sagt es; die Verbindung kann dann im Basetool unter den verbundenen Anwendungen getrennt werden. Bei VerseKit wird der Kopplungscode gelöscht.
- **Deinstallieren** der Erweiterung entfernt ihre gespeicherten Daten, soweit der Browser das zulässt.
- Daten, die beim Basetool liegen, verwaltest du beim Basetool.

## 6. Änderungen

Änderungen dieser Erklärung stehen in diesem Repository (Verlauf der Datei `PRIVACY.md`). Sie gelten ab der Version, mit der sie veröffentlicht werden.
