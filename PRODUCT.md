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

- Keine neuen Features in diesem Durchgang – nur visuelle Überarbeitung. Bestehende
  Funktionalität (10 Runden, 7 Wertungskategorien mit ihren exakten Formeln,
  Rundentabelle, Hilfe-Screen, Hell-/Dunkelmodus, Wake-Lock, Vollbildmodus,
  localStorage-Persistenz) bleibt unverändert und ist nicht zu vereinfachen oder
  wegzulassen.
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

1. Keine Feature-Änderung – dieser Durchgang ist Optik, nicht Funktion.
2. Formeln und Regeltexte sind Fakten aus dem bestehenden Code, nicht Verhandlungsmasse.
3. Ein Handy pro Spieler, kein Abgleich – jede Instanz bleibt für sich vollständig
   nutzbar.
4. Single-File bleibt Single-File.
