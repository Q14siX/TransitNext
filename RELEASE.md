# TransitNext – Release

Version: `20261022.161148`

## Änderungen (DE)

- Eine Halteposition ist unabhängig von ihren Fahrtzielen: Verschiedene Ziele von einer Position erzeugen nicht mehrere Konfigurationseinträge.
- Gleichnamige, tatsächlich getrennte Haltepunkte bleiben einzeln auswählbar.
- Maximal 8 m Geometrieabstand und kompatible Steigangaben ersetzen die bisherige 110-m-Namensgruppierung.
- Bei mehrfach auftretenden Haltestellennamen werden echte aktuelle Fahrtrichtungen als Orientierung angezeigt; mehrere Ziele eines Haltepunkts werden dabei gemeinsam aufgeführt.
- Die Firmware erhält eine Liste der explizit erlaubten Haltepositions-IDs (`stop_ids`) und berücksichtigt nur Abfahrten mit passenden IDs. Die unsichere Textnamen-Zuordnung wurde entfernt.
- Bestehende TransitNext-Apps ohne `stop_ids` werden über ihre bisherige `stop_id` übernommen und können danach aktualisiert werden.
- Mehrfach-Haltestellenverwaltung, automatische Rotation, direkte AWTRIX-Installation und `.ax`-Export bleiben erhalten.

**Verifiziert:** Browser-Tests mit simulierten Abfahrten und vier Haltepositions-IDs; Prüfung unterschiedlicher Ziele derselben Position, getrennter gegenüberliegender Positionen, erlaubter Abfahrts-IDs, Installation und Einlesen von zwei Apps sowie Entfernen ohne Einfluss auf Fremd-Apps. Ein Live- oder Hardwaretest steht weiterhin aus.

## Changes (EN)

Boarding poles are identified by physical stop IDs and positions rather than trip destinations. Stops of the same name on opposite sides remain separately selectable while trips with different destinations sharing the same pole remain within one configured entry. Boarding-pole direction hints are retrieved from current departures. The native script uses exact stored allowed IDs and a narrow 8 m lookup instead of the former unsafe 110 m name-based search. Existing multi-stop management, direct installation, export and migration support remain available. Tested with mocked APIs and device behavior only.
