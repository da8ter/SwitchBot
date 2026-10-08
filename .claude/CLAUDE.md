# SwitchBot

Symcon-Bibliothek für SwitchBot-Geräte über die SwitchBot Cloud API v1.1 (Token + Secret aus der App), mit Cloud-Webhook für Statusmeldungen. Öffentliches Repo `da8ter/SwitchBot`, Branch `main`. Der Großteil des Codes stammt aus Beiträgen von IPSAttain (Autor in `library.json`); eigene Änderungen bisher vor allem am Smart Lock Ultra.

Projektwissen: **`.claude/docs/README.md`**, Abweichungen vom Hausstandard und Offenes in `.claude/docs/stand.md`. Betriebsdaten dieses Rechners: `CLAUDE.local.md` (nicht eingecheckt).

## Aufbau

- **`SwitchBot Splitter/`** (Splitter, `SWB`): Cloud-Zugang (Signatur aus Token/Secret), Webhook `/hook/switchbot/<Instanz>` und dessen Anmeldung bei SwitchBot.
- **`SwitchBot Konfigurator/`** (Konfigurator, `SWB`): Geräteliste, legt Geräte-Instanzen an.
- **`SwitchBot Device/`** (Gerät, `SWB`): ein `module.php` mit `switch` je Gerätetyp (Bot, Curtain, Lock/Pro/Ultra, Plug, Lichter, Blind Tilt, Air Purifier, Hubs, AI Art Frame, IR-Geräte); Formular-Teile in `libs/form*.json`.
- **`actions/updateDevice.json`**: Aktion „Daten aktualisieren“ (`SWB_DeviceStatus`).
- Alle Module `IPSModule` (nicht Strict), teils mit Variablenprofilen — siehe `.claude/docs/stand.md`.

## Prüfen

Kein Prüfstand. `php -l <Datei>` auf jede geänderte Datei; Verhalten am echten Gerät nur auf Zuruf.

## Regeln

- **Commits:** ein Thema je Commit, deutsche Botschaft, **ohne** Co-Authored-By-Zeile; Prüfungen vorher. Ändert ein Commit eine Entscheidung aus `docs/`, die Datei im selben Commit nachziehen.
- **Nie** `git checkout`/`git restore` auf Dateien: Arbeitskopien können nicht committete Arbeit enthalten.
- **Push und Release nur auf Zuruf.** Release: `version`, `build` und `date` (Unix-Zeitstempel) in `library.json` hochsetzen.
- **Öffentliches Repo:** keine IP-Adressen, Ports, Instanz-IDs, Geräte-IDs, Token/Secrets, Konten, Pfade unter `/Users/` — auch nicht in Kommentaren, READMEs und Bildschirmfotos.
- **Neuer Code** folgt den Hausregeln (Darstellungen statt Profile, Übersetzung über `locale.json`); den Altbestand nur auf Zuruf umbauen, das Repo wird mit IPSAttain geteilt.
- **Symcon-Plattformwissen** (gemessen, für alle Module): https://github.com/da8ter/SymDo-Family-Organizer/tree/SymDo-Beta/.claude/docs/plattform, lokal `../List/.claude/docs/plattform/`.
