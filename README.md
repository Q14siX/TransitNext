# TransitNext – Haltepositionen und nächste Abfahrt

Eigenständige App für **AWTRIX NG / ULANZI TC002**. Keine Installation von Home Assistant, kein MQTT-Broker und kein zusätzlicher Server. Die ULANZI fragt die Fahrplandaten eigenständig bei **Transitous/MOTIS** ab.

## Einrichtung und Installation

1. `TransitNext-Einrichtung.html` im Browser öffnen.
2. **Ort suchen**, Ort auswählen, anschließend **Haltepunkt auswählen**. Bei gleichnamigen Haltepunkten werden nach der Haltestellensuche mögliche Richtungen aus den tatsächlichen Abfahrtsdaten nachgeladen.
3. **Haltestelle hinzufügen** und gegebenenfalls weitere Haltepunkte ergänzen. Die Liste kann mit **Ändern**, **Entfernen** und den Pfeiltasten bearbeitet und sortiert werden.
4. IP-Adresse bzw. Hostname deiner AWTRIX-Uhr eingeben und **Apps auf AWTRIX installieren / aktualisieren** auswählen.
5. Alternativ mit **Installationsdateien (.ax) herunterladen** die fertig eingerichteten Skripte exportieren und in der AWTRIX-Weboberfläche unter **Scripts → Import → Save** einzeln installieren.

**Bestehende Installation:** Immer zuerst **Haltestellen von Uhr laden**, bevor Änderungen gespeichert werden. Bereits eingerichtete Einträge werden übernommen. Der Assistent bewahrt die Reihenfolge und den Aktivierungsstatus fremder AWTRIX-Apps; gelöschte TransitNext-Skripte werden erst nach expliziter Bestätigung entfernt.

## Unterschied zwischen Haltepunkt und Richtung

Ein **Haltepunkt** ist die konkrete Stelle, an der Busse oder Bahnen halten. Eine einzelne Position kann **mehrere Linien mit unterschiedlichen Fahrtzielen** bedienen. Umgekehrt können sich auf verschiedenen Straßenseiten gleichnamige Haltepunkte befinden, deren Fahrzeuge in unterschiedliche Richtungen abfahren.

Die Konfigurationsseite unterscheidet deshalb **tatsächliche Haltepositionskennungen und deren Koordinaten bzw. offizielle Steig-/Gleisangaben**, nicht bloß Fahrtziele. Sehr nahe (maximal 8 m), gleichnamige Positionen ohne widersprechende Steigangaben können gruppiert werden, damit mehrere Datenquellen denselben tatsächlichen Haltepunkt nicht unnötig mehrfach anzeigen. Weiter auseinanderliegende oder durch Steigkennungen unterscheidbare Positionen bleiben eigenständige Auswahlmöglichkeiten.

Bei mehreren gleichnamigen Haltepunkten wird hinter dem Namen eine **Orientierungsangabe** eingeblendet, beispielsweise:

- `Kaufbeuren, Lachenbühl (Haltepunkt 1 · Richtung Oberbeuren / Obergünzburg)`
- `Kaufbeuren, Lachenbühl (Haltepunkt 2 · Richtung Kaufbeuren Plärrer)`

Die Ziele in Klammern sind **aus aktuell verfügbaren Fahrten ermittelte Beispiele**, keine dauerhaft festen Richtungen und keine Filter für die Fahrplanabfrage. Die Ziffern `Haltepunkt 1/2` sind interne Unterscheidungen im Assistenten und **keine amtlichen Steignummern**. Ist eine offizielle Gleis-/Steignummer vorhanden, wird diese stattdessen angezeigt. Wenn keine Richtung abgerufen werden kann, bleibt der Haltepunkt auswählbar und wird entsprechend gekennzeichnet.

**Auf der Uhr** werden ausschließlich die ausdrücklich für den gewählten Haltepunkt gespeicherten Kennungen berücksichtigt. Die früher verwendete unsichere Namensprüfung und der 110-m-Umkreis wurden entfernt. So gelangen Fahrten einer gegenüberliegenden, nicht ausgewählten Position nicht allein wegen des gleichen Haltestellennamens in die Anzeige.

**Datengrenze:** Wenn Transitous für physisch unterschiedliche Positionen identische oder fehlerhafte Koordinaten bzw. Kennungen meldet und keine zusätzlichen Steigdaten liefert, lässt sich der Unterschied nicht mit Sicherheit rekonstruieren. Derzeit wurde nur mit simulierten Haltepositions- und Abfahrtsdaten geprüft. Vor einer produktiven Nutzung mit unbekannten Haltestellen die ermittelten Richtungen und Abfahrten über **Abfahrten prüfen** plausibilisieren.

## Anzeige

- Pro konfiguriertem Haltepunkt **genau eine native Skript-App**, der Reihe nach in der AWTRIX-Rotation.
- Innerhalb einer App **immer nur die zeitlich nächste gültige Abfahrt** dieser Position, unabhängig von Linie oder Fahrtziel.
- Links: farbiges Linienfeld, rechts oben: Minuten oder Abfahrtsuhrzeit, rechts unten: Laufschrift mit **verkürztem Starthaltestellennamen**, z. B. `Lachenbühl > Aitrang, Gemeindeamt`.
- Suchzeitraum (1–72 Stunden), Aktualisierungsintervall (1–30 Minuten), Linienfarben und Anzeigeoptionen bleiben erhalten.
- Die Abfahrtsdaten werden unter Berücksichtigung der zulässigen Haltepositions-IDs gefiltert. Fahrtausfälle werden ausgeschlossen, soweit sie in den Daten gekennzeichnet sind.

## Technische Grenzen

- Die Nutzung erfordert eine mit dem Internet verbundene AWTRIX-NG-Uhr und aktuelle Abfahrtsdaten der Quelle Transitous/MOTIS.
- Pro Haltepunkt werden die zugehörigen konkreten IDs gespeichert (`stop_id` als primäre ID, `stop_ids` als explizite Liste). Für bestehende Installationen ohne `stop_ids` gilt die primäre ID.
- Die native Abfrage nutzt `/api/v6/stoptimes` mit `radius=8` und `exactRadius=true`. Die tatsächlichen Ereignisse werden zusätzlich anhand ihrer IDs validiert.
- Die Konfigurationsseite zeigt Richtungen nur für gleichnamige, mehrfach vorhandene Haltepunkte, um nicht für sämtliche Haltestellen eines Orts zahlreiche API-Aufrufe auszulösen.
- Maximal 20 Haltestellen in der Konfigurationsseite; die tatsächlich installierbare Anzahl hängt vom verfügbaren Speicher der ULANZI ab.
- Ein Live-Test auf echter ULANZI-TC002-Hardware und gegen die tatsächlichen Daten des Kaufbeurer Verkehrs steht aus.

---

# English

TransitNext is a standalone AWTRIX NG / ULANZI TC002 app showing the next departure for each configured boarding position. No Home Assistant or MQTT required. The browser-based configuration supports searching a town, selecting individual boarding poles/platforms, adding multiple positions, changing their order, editing or removing them, reading an existing device configuration, and installing native Berry scripts directly onto the clock (or exporting `.ax` files).

A **boarding position is not a destination**. Multiple routes with different destinations may depart from one physical pole. Opposite sides of a road may use the same public stop name but must remain separately selectable. This release uses exact stop IDs, coordinates and supplied platform markers, grouping only nearby matching positions within 8 metres; route headsigns are used as informative examples for disambiguation, not as stop identifiers or route filters. The device filters departures by explicit selected IDs, not just by matching name.

Position numbers are UI-only identifiers, not official platform numbers. When platform geometry or metadata is missing or wrong, reliable physical disambiguation cannot be guaranteed. Tests used mocked data and a simulated AWTRIX device; no live hardware verification has been performed.
