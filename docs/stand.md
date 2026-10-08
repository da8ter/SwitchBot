# Stand

Der größte Teil des Codes stammt aus Beiträgen von IPSAttain (Autor in `library.json`) und ist älter als die heutigen Hausregeln. Hier steht, wo der Bestand abweicht, damit Änderungen nicht unbemerkt den alten Stil fortschreiben.

## Abweichungen vom Hausstandard (Stand des Codes)

- Alle drei Module erben von `IPSModule`, nicht `IPSModuleStrict`; Overrides sind untypisiert.
- Das Gerätemodul legt zehn eigene Variablenprofile `SwitchBot.*` an (u. a. `UpDown`, `toggle`, `blindTilt`, `fanSpeed`, `purifierMode`) und nutzt Systemprofile (`~Lock`, `~Battery.100`, `~ShutterPosition.100` …). Nur `lockControl` hat eine Darstellung. Die Geräte-README behauptet, es gebe keine eigenen Profile — das stimmt nicht.
- Der Splitter trägt seinen Webhook über eine eigene `RegisterHook`-Methode in die Eigenschaften des WebHook Control ein. Der Module Store verlangt das native `RegisterHook` (siehe Plattformwissen `hooks-und-grenzen.md`).
- Der Splitter baut die Webhook-Adresse mit `utf8_encode` (in PHP 8.2 veraltet).
- `SwitchBot Device/module.php` hat mehr als 500 Zeilen.
- Alle drei Module teilen das Präfix `SWB`.
- `library.json`: `date` ist 0, `url` zeigt auf den Hersteller statt aufs Repo.

## Offen

- Widerspruch zum Auslöser der falschen `LOCKED`-Meldung beim Lock Ultra ([smart-lock-ultra](entscheidungen/smart-lock-ultra.md)).

Stand: geprüft gegen den Code am 08.10.2026
