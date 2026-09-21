# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Stack

Einzelne `index.html`, Vanilla JS/CSS, kein Build, kein Backend, kein Framework.
Ausdrücklich so gewollt (Nutzer-Entscheidung): bleibt Single-File.

## Users

Lars und seine Mitspieler:innen beim Brettspiel „Panda Royale" (ein Würfelspiel mit
mehreren Würfelfarben und rundenbasierter Wertung). Jede Person nutzt die App auf dem
eigenen Handy, unabhängig von den anderen – trägt während der Partie die eigenen
gewürfelten Werte pro Runde ein und behält den eigenen Punktestand im Blick.

## Product Purpose

Persönlicher Punkterechner für Panda Royale: pro Runde (1–10) die gewürfelten Werte je
Farbe eintragen, die App rechnet die farbspezifische Formel aus (Gelb, Lila ×2, Blau
ggf. ×2 mit Glitzerwürfel, Rot als (Weiß−Schwarz)×Anzahl, Grün, Klar, Mitleid), zeigt
Rundensumme, Rundenverlauf/Tabelle und Gesamtsumme. Erfolg heißt: schnelles, korrektes
Eintragen ohne Kopfrechnen, klarer Blick auf den eigenen Punktestand.

## Positioning

Ersetzt den Taschenrechner/Kopfrechnen am Spieltisch für eine Wertung mit mehreren
unterschiedlichen Formeln pro Farbe – jede Person hat ihre eigene Instanz, es gibt
bewusst keinen Abgleich zwischen Geräten.

## Operating Context

Gespielt am Tisch, gesellig, das physische Spiel (Würfel, ggf. Spielplan) bleibt im
Einsatz. Die App liest keine Spielzüge vor, sie ist reiner Rechner + Rundenprotokoll +
Kurzreferenz der Wertungsformeln (aktueller Hilfe-Screen). Läuft offline (PWA-Manifest,
Wake-Lock gegen Bildschirm-Timeout, Vollbild-Umschalter) – wichtig, da Spieleabende
nicht von Internet abhängen dürfen.

## Capabilities and Constraints

- **Zwei Eingabemodi, Modus gilt für die ganze Partie:** Im **Auto-Modus** trägt man
  die gewürfelten Einzelwerte ein und die App rechnet die farbspezifischen Formeln aus
  (Gelb, Lila ×2, Blau ggf. ×2 mit Glitzerwürfel, Rot als (Weiß−Schwarz)×Anzahl,
  Grün, Klar, Mitleid). Im **Manuell-Modus** trägt man die fertigen Farbwerte über
  **Dropdowns** ein (gleiches Bedienschema wie Auto; bei Rot sind negative Werte
  wählbar). Unabhängig vom Modus rechnet die App **immer automatisch**: Rundensumme,
  Rundenverlauf/Tabelle und Gesamtsumme.
- Der Modus wird einmalig **zu Spielbeginn** gewählt (vor der ersten Eintragung).
  Ab der ersten Eintragung ist er für die Partie fixiert; ein erneuter Tipp auf die
  Modus-Leiste gibt einen Hinweis-Toast. „Neues Spiel" setzt die Wahl wieder frei.
- Wechsel Auto→Manuell vor der ersten Eintragung übernimmt die berechneten Farbwerte
  als Startwert ins manuelle Blatt (nur wenn dieses noch leer ist) – Summen laufen
  ohne Bruch weiter.
- Bestehende Funktionalität (10 Runden, Rundentabelle, Hilfe-Screen,
  Hell-/Dunkelmodus, Wake-Lock, Vollbildmodus, localStorage-Persistenz) bleibt
  unverändert und ist nicht zu vereinfachen oder wegzulassen.
- Keine Mehrspieler-Verwaltung, kein Sync zwischen Geräten – jede Instanz ist bereits
  strukturell Ein-Personen-Rechner, das bleibt so.
- Single-File-HTML bleibt Pflicht (ausdrücklicher Nutzerwunsch), kein Build-Schritt,
  kein Backend.
- Die Wertungsformeln je Farbe (im Code und im Hilfe-Screen) sind Spielregel-Fakten und
  dürfen inhaltlich nicht verändert werden, nur ggf. visuell neu dargestellt.

## Evidence on Hand

- Bestehender, funktionierender Code: `index.html` in diesem Repo (Formeln, Texte,
  Struktur) – das ist die einzige verfügbare Quelle für Spielregel-Fakten.
- Kein Foto-/Scan-Material vom physischen Spiel vorhanden (im Unterschied zu
  [[02 Projekte/Among Cultists Begleiter]]). Eine 1:1-Grafikvorlage gibt es nicht;
  visuelle Gestaltung ist freier, muss aber die im Code sichtbaren Fakten (Panda-Motiv,
  Würfelfarben Gelb/Lila/Blau/Rot/Grün/Klar, Mitleidswürfel, Panda-Token) respektieren
  und nichts zusätzlich behaupten.

## Product Principles

1. Die Formeln je Farbe sind Spielregel-Fakten, nicht Verhandlungsmasse – im
   Auto-Modus unverändert, der Manuell-Modus umgeht sie bewusst (Wer rechnen will,
   darf; wer nicht, trägt fertige Werte ein).
2. Rundensumme, Tabelle und Gesamtwert rechnet in BEIDEN Modi die App – nie
   Kopfrechnen bei den Summen.
3. Ein Handy pro Spieler, kein Abgleich – jede Instanz bleibt für sich vollständig
   nutzbar.
4. Single-File bleibt Single-File.
