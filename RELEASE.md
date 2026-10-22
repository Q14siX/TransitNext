# TransitNext – Erstveröffentlichung / Initial Release

**Version:** `20261022.161148`  
**Datum / Date:** 22 October 2026  
**Plattform / Platform:** AWTRIX NG · ULANZI TC002 · 52 × 16 Pixel  
**Entwickler / Author:** [Q14siX](https://github.com/Q14siX)  
**Repository:** [github.com/Q14siX/TransitNext](https://github.com/Q14siX/TransitNext)

## Deutsch

### TransitNext – Die nächste Abfahrt im Blick

TransitNext macht aus deiner AWTRIX-NG-Uhr eine eigenständige Abfahrtsanzeige für Busse, Bahnen und weitere öffentliche Verkehrsmittel. Über den webbasierten Einrichtungsassistenten werden die gewünschten Haltepunkte ausgewählt. Anschließend fragt das Gerät die nächsten Abfahrten selbstständig über die **Transitous/MOTIS-API** ab. **Home Assistant, MQTT-Broker, zusätzlicher Server oder persönlicher API-Schlüssel sind nicht erforderlich.**

### Funktionen der Erstveröffentlichung

- **Immer nur die nächste Abfahrt** pro konfiguriertem Haltepunkt.
- **Mehrere Haltepunkte** zentral hinzufügen, bearbeiten, entfernen und sortieren; Anzeige nacheinander über die AWTRIX-App-Rotation.
- **Physische Haltepositionen unterscheiden:** Gleichnamige Haltestellen können unterschiedliche Einstiegspositionen besitzen. Verschiedene Fahrtziele einer Position werden nicht als eigenständige Haltepunkte behandelt.
- **Richtungsinformationen bei der Auswahl** aus aktuellen Abfahrten, nur als Orientierung, nicht als fester Richtungsfilter.
- **Farbige Liniennummer**, Minuten-Countdown oder Abfahrtsuhrzeit sowie **scrollender Streckentext**, beispielsweise `Märzenbachweg > Aitrang, Gemeindeamt`.
- **Einstellbarer Suchzeitraum** von 1 bis 72 Stunden und **Abrufintervall** von 1 bis 30 Minuten.
- Einstellbare Farben und optionale Verspätungsanzeige, soweit entsprechende Quelldaten verfügbar sind.
- Webbasierte Orts- und Haltestellensuche mit manueller Abfahrtsprüfung.
- **Direkte Installation auf AWTRIX NG**, Export individuell erzeugter `.ax`-Dateien und nachträgliches Einlesen bestehender TransitNext-Konfigurationen.

### Installation

1. [Repository öffnen](https://github.com/Q14siX/TransitNext) und mit **Code → Download ZIP** herunterladen.
2. ZIP entpacken und `TransitNext-Einrichtung.html` lokal im Browser öffnen.
3. Ort und Haltepunkt(e) wählen und die Reihenfolge festlegen.
4. Suchzeitraum, Aktualisierungsintervall und Zeitdarstellung einstellen.
5. Geräteadresse eingeben und **Apps auf AWTRIX installieren / aktualisieren** wählen.

Alternativ können die **vorkonfigurierten** `.ax`-Skripte exportiert und in der AWTRIX-NG-Weboberfläche über **Scripts → Import → Save** importiert werden.

Die im Repository enthaltene `TransitNext.template.ax` ist eine **Skriptvorlage mit Platzhaltern** und darf nicht unverändert als fertige Anwendung installiert werden.

### Datenquelle und Hinweise

TransitNext verwendet **[Transitous](https://transitous.org/)** und die **[MOTIS-API](https://transitous.org/api/)**, insbesondere `/api/v6/stoptimes`. Die Fahrplandaten stammen aus verschiedenen regionalen Verkehrsunternehmen und weiteren Datenlieferanten.

**Datenquellen und Nutzungsbedingungen:** [Transitous – Sources](https://transitous.org/sources/) · [OpenStreetMap](https://www.openstreetmap.org/copyright) · [Transitous API](https://transitous.org/api/)

Abdeckung, Haltepositionsdaten, Echtzeitprognosen und Verspätungen hängen von den jeweiligen Zulieferern ab. Transitous ist ein Community-Dienst ohne garantierte Verfügbarkeit. Für zeitkritische Fahrten offizielle Verkehrsauskünfte prüfen.

**Teststatus:** Konfiguration, Skripterzeugung, Haltepositionsprüfung, Mehrfachverwaltung und Installationsabläufe wurden mit simulierten API- und AWTRIX-Gerätedaten geprüft. Ein vollständiger Live-Test auf physischer ULANZI-TC002-Hardware ist nicht bestätigt.

**Lizenz:** [MIT](./LICENSE) für den Anwendungscode. Verkehrsdaten und sonstige Inhalte Dritter unterliegen ihren eigenen Lizenzbedingungen.

---

## English

### TransitNext – Your next departure at a glance

TransitNext transforms AWTRIX NG into a standalone departure board for buses, trains, and other public transport services. Select physical boarding positions with the browser-based setup tool. The device then retrieves departure information directly from the **Transitous/MOTIS API**. **No Home Assistant, MQTT broker, additional server, or personal API key required.**

### Initial release features

- **Only the next departure** for each configured boarding position.
- **Multiple stops** managed in one interface and displayed sequentially via native AWTRIX app rotation.
- **Physical boarding position selection:** Stops with identical names but separate boarding positions can be distinguished; different destinations from one pole do not become separate stop entries.
- **Direction hints** based on current departures assist selection but do not restrict which routes are displayed.
- **Colored route number**, departure countdown or clock time, and **scrolling stop-to-destination text**, e.g. `Märzenbachweg > Aitrang, Gemeindeamt`.
- **Adjustable look-ahead window** (1–72 hours) and **refresh interval** (1–30 minutes).
- Custom colors and optional delays where available from upstream data.
- Browser-based city/stop selection and manual departure checks.
- **Direct device installation**, export of configured `.ax` scripts, and read-back of existing TransitNext installations for editing.

### Installation

1. Visit [Q14siX/TransitNext](https://github.com/Q14siX/TransitNext) and select **Code → Download ZIP**.
2. Extract the archive and open `TransitNext-Einrichtung.html` locally in a browser.
3. Select your city and physical stop(s), and set the order.
4. Configure the search horizon, refresh interval, and departure time display.
5. Enter your device IP address/hostname and select **Apps auf AWTRIX installieren / aktualisieren** (Install/update apps on AWTRIX).

Alternatively, export **configured** `.ax` files and import them in the AWTRIX NG web interface via **Scripts → Import → Save**.

The repository's `TransitNext.template.ax` contains configuration placeholders and is **not intended to be installed unchanged**.

### Data source and limitations

TransitNext uses **[Transitous](https://transitous.org/)** and the **[MOTIS API](https://transitous.org/api/)**, including `/api/v6/stoptimes`. Data is aggregated from regional public transport operators and other timetable providers.

**Upstream sources and terms:** [Transitous – Sources](https://transitous.org/sources/) · [OpenStreetMap](https://www.openstreetmap.org/copyright) · [Transitous API policy](https://transitous.org/api/)

Coverage, stop geometry, realtime information, and delays vary by upstream provider. Transitous is a community-operated best-effort service without uptime guarantees. Confirm important journeys using official operator information.

**Testing:** Configuration, code generation, stop validation, multi-stop management, and installation workflows were tested with simulated service and device responses. Full live testing on physical ULANZI TC002 hardware has not been confirmed.

**License:** [MIT](./LICENSE) for the application code. Upstream transit data and other third-party materials retain their own licensing terms.
