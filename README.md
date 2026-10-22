# TransitNext

**Deine nächste Bus- oder Bahnabfahrt direkt auf AWTRIX NG.** / **Your next public transport departure on AWTRIX NG.**

TransitNext ist eine eigenständige Abfahrtsanzeige für **AWTRIX NG auf der ULANZI TC002 (52 × 16 Pixel)**. Du verwaltest deine Haltepunkte zentral im Browser; die Uhr ruft die Abfahrtsdaten anschließend selbst über **Transitous/MOTIS** ab. **Kein Home Assistant, kein MQTT-Broker und kein zusätzlicher Server erforderlich.**

TransitNext is a standalone public transport departure board for **AWTRIX NG / ULANZI TC002**. Configure your stops in a browser; the device fetches departures directly from **Transitous/MOTIS**. **No Home Assistant, MQTT broker, or extra server required.**

[Einrichtungsassistent / Setup tool](./TransitNext-Einrichtung.html) · [Skriptvorlage / Script template](./TransitNext.template.ax) · [Release Notes](./RELEASE.md)

> **Wichtig / Important:** GitHub führt HTML-Dateien nicht als Web-App aus. Öffne **Code → Download ZIP**, entpacke das Repository und starte \`TransitNext-Einrichtung.html\` lokal im Browser. Die Datei \`TransitNext.template.ax\` ist eine Vorlage mit Platzhaltern und **nicht** zur direkten Installation vorgesehen.
>
> GitHub does not run HTML files as web applications. Choose **Code → Download ZIP**, extract it, and open \`TransitNext-Einrichtung.html\` locally. \`TransitNext.template.ax\` is an unconfigured template, **not** a ready-to-install script.

---

## Deutsch

### Funktionen

- **Nur die nächste Abfahrt:** Pro ausgewähltem Haltepunkt zeigt die Uhr ausschließlich die nächste verfügbare Abfahrt.
- **Mehrere Haltepunkte:** Über eine Konfigurationsseite hinzufügen, ändern, entfernen und sortieren; AWTRIX NG zeigt sie nacheinander in seiner App-Rotation.
- **Bus und Bahn:** Verkehrsmittel und Regionen, für die Transitous Fahrplandaten bereitstellt – nicht nur Kaufbeuren.
- **Haltepositionen statt Fahrtziele:** Gleichnamige Haltestellen können unterschiedliche physische Einstiegspositionen haben. Mehrere Linien oder Ziele einer Position bleiben ein einziger Eintrag.
- **Richtungsangaben zur Auswahl:** Bei mehreren Positionen können Ziele aktueller Fahrten als Orientierung erscheinen. Diese Hinweise sind keine festen Richtungsfilter.
- **LED-gerechte Darstellung:** Farbiges Linienfeld, Countdown oder Abfahrtsuhrzeit, darunter scrollende Laufschrift. Der Ortsname am Beginn kann entfallen, z. B. \`Märzenbachweg > Aitrang, Gemeindeamt\`.
- **Personalisierbar:** Automatische Linienfarben, optionale Verspätungen und anpassbare Anzeigefarben.
- **Abrufsteuerung:** Aktualisierung alle **1–30 Minuten** und Suchzeitraum **1–72 Stunden**.
- **Direkte Installation:** Einrichtungsassistent installiert individuelle Berry-Skripte auf der AWTRIX NG oder exportiert konfigurierte \`.ax\`-Dateien.

### Voraussetzungen

- ULANZI TC002 oder kompatibles AWTRIX-NG-Gerät mit **52 × 16 Pixeln** und Berry-Skriptunterstützung.
- WLAN- und Internetverbindung der Uhr für die Fahrplanauskunft.
- Moderner Browser; für die Direktinstallation muss die Uhr im lokalen Netzwerk erreichbar sein.
- **Kein persönlicher API-Schlüssel** erforderlich.

### Einrichtung und Installation

1. Repository [Q14siX/TransitNext](https://github.com/Q14siX/TransitNext) über **Code → Download ZIP** herunterladen und entpacken.
2. **\`TransitNext-Einrichtung.html\`** im Browser öffnen.
3. **Ort suchen**, passenden Ort auswählen, Haltestellen filtern und die gewünschte **Halteposition** wählen.
4. **Haltestelle hinzufügen** anklicken; für weitere Haltepunkte wiederholen. Die Reihenfolge über die Pfeiltasten festlegen.
5. **Suchzeitraum**, **Abrufintervall** und **Zeitdarstellung** konfigurieren.
6. IP-Adresse oder Hostnamen der ULANZI eingeben und **Apps auf AWTRIX installieren / aktualisieren** verwenden.

Jeder Haltepunkt erhält eine eigene native AWTRIX-App. Die AWTRIX-Rotation schaltet zwischen diesen Apps um; **innerhalb jeder App erscheint nur eine Abfahrt**.

**Manuelle Installation:** Im Assistenten **Installationsdateien (.ax) herunterladen** wählen. Die generierten Dateien entpacken und in der AWTRIX-Weboberfläche über **Scripts → Import → Save** importieren. Danach bei Bedarf die Reihenfolge unter **Apps** festlegen.

### Haltestellen nachträglich verwalten

Die HTML-Konfigurationsseite erneut öffnen, Geräteadresse eingeben und **Haltestellen von Uhr laden** wählen, **bevor** Änderungen vorgenommen werden. Anschließend Haltepunkte hinzufügen, ersetzen, entfernen oder sortieren und über **Apps auf AWTRIX installieren / aktualisieren** synchronisieren.

Die Verwaltung ist auf **20 Haltepunkte** ausgelegt; die tatsächliche installierbare Anzahl hängt vom freien Gerätespeicher ab. Andere AWTRIX-Apps sollen von der Synchronisierung unberührt bleiben.

### Haltepunkt und Fahrtrichtung

Ein Haltestellenname kann mehrere gegenüberliegende Haltepositionen bezeichnen. Eine einzelne Position kann wiederum unterschiedliche Linien und Ziele bedienen. TransitNext verwendet die vom Anbieter gelieferten **Haltepositions-IDs**, Koordinaten und ggf. Steig- oder Gleisangaben. Nahe passende Einträge dürfen unter engen Bedingungen zusammengefasst werden (bis zu **8 m**, ohne widersprechende Steigdaten).

Richtungsangaben im Auswahlfeld sind **Beispiele aus aktuellen Abfahrten** und beschränken die spätere Anzeige **nicht** auf ein bestimmtes Ziel. Der Sensor bzw. das Skript zeigt die früheste passende Abfahrt der ausdrücklich ausgewählten Position. Bei unvollständigen oder fehlerhaften Geodaten kann die eindeutige physische Zuordnung eingeschränkt sein. Mit **Abfahrten prüfen** lässt sich die Auswahl vorab plausibilisieren.

### Beispielanzeige

\`\`\`text
[ 76 ]   8 min
         Märzenbachweg > Aitrang, Gemeindeamt
\`\`\`

*Schematische Darstellung.* Auf dem 52 × 16-Pixel-Display bleibt die Liniennummer fest stehen, während längere Texte horizontal scrollen. Wahlweise wird statt des Countdowns die Abfahrtsuhrzeit angezeigt. Verspätungs- und Ausfallinformationen werden verwendet, **soweit die Quelle sie liefert**.

### Datenquelle, Urheberrecht und Zuverlässigkeit

TransitNext bezieht Orts-, Haltestellen- und Abfahrtsinformationen über **[Transitous](https://transitous.org/)** und die **[MOTIS-API](https://transitous.org/api/)**, insbesondere den Endpunkt \`/api/v6/stoptimes\`. Transitous bündelt Daten regionaler Verkehrsunternehmen und weiterer Fahrplananbieter.

**Attribution / Datenquellen:** [Transitous – Sources](https://transitous.org/sources/) · [OpenStreetMap](https://www.openstreetmap.org/copyright)

Fahrplandaten, Verspätungen, Echtzeitstatus und Haltepositionsinformationen sind abhängig von den zuliefernden Betreibern. Transitous ist ein ehrenamtlich betriebener **Best-Effort-Dienst** ohne Verfügbarkeitsgarantie. Die öffentliche API ist für **quelloffene, nicht kommerzielle und ressourcenschonende Anwendungen** vorgesehen; beachte die [Nutzungsbedingungen](https://transitous.org/api/). Bei wichtigen Fahrten die offiziellen Verkehrsauskünfte prüfen.

### Lizenz und Projekt

**Entwickler:** [Q14siX](https://github.com/Q14siX) · **Lizenz des Quellcodes:** [MIT](./LICENSE). Für Verkehrsdaten und Inhalte Dritter gelten deren eigene Lizenzen.

TransitNext ist ein unabhängiges Community-Projekt, keine offizielle Anwendung von AWTRIX NG, Transitous oder Verkehrsunternehmen. Die Funktionsprüfung erfolgte mit simulierten API- und Geräteantworten; ein vollständiger Live-Test auf realer TC002-Hardware wurde nicht bestätigt.

---

## English

### Features

- **Next departure only:** Display the soonest available departure for each selected physical boarding position.
- **Multiple stops:** Add, edit, remove, and reorder stops on one configuration page. AWTRIX NG cycles between the resulting native script apps.
- **Bus, rail, and more:** Works wherever the Transitous data source offers public transport departures.
- **Position-aware selection:** Different boarding positions sharing a stop name can remain separate; several destinations served by one position remain grouped.
- **Direction hints:** Currently known destinations may help distinguish positions, but are **not permanent destination filters**.
- **LED-friendly layout:** Colored route number, departure countdown or clock time, and scrolling stop-to-destination text, e.g. \`Märzenbachweg > Aitrang, Gemeindeamt\`.
- **Customizable:** Automatic line colors, optional delay information, custom display colors, **1–30-minute** update interval, and **1–72-hour** search window.
- **Standalone operation:** Native Berry script on the clock; no Home Assistant, MQTT, separate server, or API key.

### Requirements

ULANZI TC002 or compatible **52 × 16 AWTRIX NG** display with Berry scripting support; device Wi-Fi/internet access; modern browser. Direct installation requires local network connectivity between browser and device.

### Setup and installation

1. Download [Q14siX/TransitNext](https://github.com/Q14siX/TransitNext) using **Code → Download ZIP**, extract the archive, and open **\`TransitNext-Einrichtung.html\`** locally.
2. Search for a **city**, choose it, and select the correct **physical stop/boarding position**.
3. Click **Haltestelle hinzufügen** (Add stop) for each desired position. Set the display order.
4. Configure the update interval, search window, and countdown/time display.
5. Enter the AWTRIX NG IP address or hostname and click **Apps auf AWTRIX installieren / aktualisieren** (Install/update apps).

**Manual alternative:** Use **Installationsdateien (.ax) herunterladen** (Download installation files). Import the generated \`.ax\` files via **AWTRIX NG → Scripts → Import → Save**. The included \`TransitNext.template.ax\` contains placeholders and is **not installation-ready** without configuration.

### Changing existing stops

Open the same setup page again, enter the device address, and click **Haltestellen von Uhr laden** (Load stops from device) **before making changes**. Add, replace, remove, or reorder entries, then synchronize. Up to **20** stops can be configured, subject to available device memory. Other AWTRIX apps are intended to be preserved.

### Physical boarding positions vs. directions

A named stop can include distinct boarding poles/platforms, while one pole may serve multiple destinations. TransitNext selects from provided stop IDs, geometry and platform information, with narrowly restricted matching of compatible nearby records (up to **8 metres**). Direction labels from current departures are **selection hints only**, not filters. Missing or incorrect upstream location data can prevent perfect distinction; use **Abfahrten prüfen** (Check departures) to verify a selection.

### Data source, attribution, and limitations

TransitNext retrieves stop and departure data from the **[Transitous](https://transitous.org/) [MOTIS API](https://transitous.org/api/)**, including \`/api/v6/stoptimes\`. Transitous aggregates feeds from local operators and public transit data publishers.

**Source attribution and licenses:** [Transitous – Sources](https://transitous.org/sources/) · [OpenStreetMap](https://www.openstreetmap.org/copyright)

Realtime information, delays, cancellations, and boarding-position accuracy depend on upstream data. Transitous is a volunteer-run **best-effort service**, without guaranteed availability. Its public API is intended for **open-source, non-commercial, resource-conscious applications**; see the [usage policy](https://transitous.org/api/). Confirm critical departures with the transport operator.

**Author:** [Q14siX](https://github.com/Q14siX) · **Code license:** [MIT](./LICENSE). Transit data and third-party content retain their own licensing terms.

TransitNext is an independent community project, not affiliated with AWTRIX NG, Transitous, or public transport operators. Setup and generated scripts have been tested against simulated API/device responses; complete live validation on physical ULANZI TC002 hardware has not yet been confirmed.
