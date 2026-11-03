# Hangar-Exporter

Browser-Erweiterung für Chrome, Edge und Firefox. Sie liest deinen eigenen Hangar von der RSI-Seite (Star Citizen) und speichert ihn als Datei oder schickt ihn auf deinen Wunsch an [VerseKit](https://github.com/Xharig/VerseKit) auf demselben Rechner oder an das [Basetool](https://github.com/krt-profit/basetool).

> Inoffizielles Fan-Werkzeug. Nicht mit Cloud Imperium Games oder Roberts Space Industries verbunden. Star Citizen ist eine Marke von Cloud Imperium Games.

In diesem Repository liegen die fertigen Pakete, die Prüfsummen und die Texte zu Datenschutz und Sicherheit. Die Pakete enthalten die Quelldateien der Erweiterung unverändert und unminifiziert (lesbares JavaScript); beim Paketbau wird nur die Manifest-Datei je Browser angepasst.

## Was sie tut

- Auf der Hangar-Seite bei RSI erscheint ein Knopf **Hangar exportieren**. Gelesen, gespeichert oder gesendet wird erst, wenn du im Fenster **Hangar lesen** drückst, und immer an genau **ein** Ziel.
- Ziele: **VerseKit** (nur auf deinem Rechner), **Basetool** (mit Anmeldung und Vorschau vor dem Senden), **CSV-Datei**, **JSON-Datei (Übergabedatei)**, beide Dateien oder eine **Schiffsliste**.
- **Das Basetool bekommt nur Schiffe** (Typ, Versicherung, eine daraus gebildete Kennung), nie Kaufpreise, Kaufdaten oder Pledge-Nummern im Klartext. Die **Dateien** und die **Schiffsliste für VerseKit** enthalten dagegen Angaben aus deinem Hangar wie Pledge-Nummer, Kaufdatum und Preis; Gutscheincodes sind geschwärzt, Spitznamen fehlen (außer du schaltest sie für eine Datei ein). Zugangsdaten, Seriennummern und Sitzungs-Token gehen nie hinaus. Was genau wohin geht, steht in der [Datenschutzerklärung](PRIVACY.md).
- Keine Analyse, keine Werbung, keine Fremdbibliotheken, kein nachgeladener Code.

## Download und Installation

Die neueste Fassung findest du unter **[Releases](https://github.com/Drachennarr/Hangar-Exporter-Releases/releases/latest)**. Dort liegen für jede Version:

| Datei | Wofür |
|---|---|
| `Hangar-Exporter-chrome-v<Version>.zip` | Chrome und Edge |
| `<Kennung>-<Version>.xpi` | Firefox (von Mozilla signiert) |
| `SHA256SUMS.txt` | Prüfsummen der Dateien |

**Firefox:** Die `.xpi`-Datei herunterladen und in das Firefox-Fenster ziehen (oder `about:addons` öffnen, auf das Zahnrad klicken und **Add-on aus Datei installieren** wählen). Firefox aktualisiert die Erweiterung danach selbst. Wenn das Senden an VerseKit oder das Basetool nicht klappt, prüfe unter `about:addons` > **Hangar-Exporter** > **Berechtigungen**, ob der Zugriff auf `127.0.0.1` und `ingest.profit-base.online` erlaubt ist.

**Chrome und Edge:** Das Zip in einen eigenen Ordner entpacken (Rechtsklick > **Alle extrahieren**). Dann:

- **Chrome:** `chrome://extensions` öffnen, oben rechts den **Entwicklermodus** einschalten, **Entpackte Erweiterung laden** wählen und den Ordner angeben.
- **Edge:** `edge://extensions` öffnen, links unten in der Seitenleiste den **Entwicklermodus** einschalten (bei schmalem Fenster erst oben links das Menü ☰ aufklappen), dann oben **Entpackte Dateien laden** wählen und den Ordner angeben.

Anzugeben ist der Ordner, in dem die `manifest.json` liegt. Der Ordner muss an seinem Platz bleiben: Wer ihn löscht oder verschiebt, deaktiviert die Erweiterung. Der Browser warnt bei jedem Start vor Erweiterungen im Entwicklermodus. Auf verwalteten Rechnern (Firma, Schule) kann der Entwicklermodus gesperrt sein. Die Erweiterung hat eine feste Kennung (`hgmnaolojobpmeieccpholmjacbjkpbm`), auch beim Laden als entpackter Ordner. Für eine neue Version den alten Eintrag entfernen und die neue Fassung laden, oder den vorhandenen Eintrag mit dem Neu-laden-Knopf (Edge: **Erneut laden**) aktualisieren, nachdem du den Ordner ersetzt hast; Chrome und Edge aktualisieren sie nicht von selbst.

**Prüfsumme prüfen** (PowerShell, im Ordner der heruntergeladenen Datei; `<Dateiname>` ersetzen):

```powershell
Get-FileHash .\<Dateiname> -Algorithm SHA256
```

Der Wert muss mit der Zeile in `SHA256SUMS.txt` übereinstimmen. Groß- und Kleinschreibung spielt keine Rolle.

## Datenschutz und Sicherheit

- [Datenschutzerklärung](PRIVACY.md): was gelesen, gesendet und gespeichert wird und wie du es löschst.
- [Sicherheitshinweise](SECURITY.md): wie du eine Schwachstelle meldest und welche Grundsätze das Projekt einhält.

## Lizenz

Copyright (C) 2026 Drachennarr. GNU General Public License, nur Version 3 (GPL-3.0-only, siehe [LICENSE](LICENSE)). Lizenztext (`LICENSE`) und Urheberhinweis (`COPYRIGHT.txt`) liegen auch in jedem Paket.
