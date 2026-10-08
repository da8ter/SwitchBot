# SwitchBot Smart Lock Ultra: Status und Steuerung getrennt

Eingeführt im April 2026 (Commit `12cb323`), Darstellung im Juni 2026 nachgezogen (`a054c2e`).

## Entscheidungen

- **Zwei Variablen beim Ultra.** `lockState` (Boolean) zeigt nur den Zustand und ist beim Smart Lock Ultra nicht schaltbar; bedient wird über `lockControl` (Integer, Aufzählung). Bei Lock und Smart Lock Pro bleibt `lockState` schaltbar wie bisher.
- **Zuordnung nach beobachtetem Verhalten, nicht nach Fremddoku.** `lockControl` 0 = „Tür öffnen“ → Cloud-Befehl `unlock` (zieht die Falle), 1 = „Abschließen“ → `lock`, 2 = „Aufschließen“ → `deadbolt` (Riegel zurück, die Falle hält die Tür). Beobachtet an einem Lock Ultra mit Night-Latch; die Home-Assistant-Doku beschreibt `deadbolt` dagegen als „Open Door“ (nicht am Code prüfbar).
- **Nur `locked` heißt abgeschlossen.** Ein Webhook mit `lockState` setzt die Variable nur bei `locked` auf wahr (wie die HA-Integration `switchbot_cloud`); `latchboltlocked` zählt seitdem als nicht abgeschlossen. `jammed` erzeugt eine Log-Warnung.
- **`lockControl` folgt keinem Webhook.** Die Variable behält den zuletzt gesendeten Befehl, weil die Cloud danach einen falschen `LOCKED`-Status meldet. Den Live-Zustand zeigt `lockState`.
- **Darstellung bei der Registrierung.** Die Aufzählung wird als drittes Argument an `RegisterVariableInteger` übergeben, nicht nachträglich per `IPS_SetVariableCustomPresentation`.

## Offen

- Code-Kommentar und Geräte-README nennen verschiedene Auslöser für die falsche `LOCKED`-Meldung (Kommentar: nach `deadbolt`, README: nach `unlock`). Welcher stimmt, ist nicht am Code prüfbar.

Stand: geprüft gegen den Code am 08.10.2026
