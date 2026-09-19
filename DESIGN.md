# Design

<!-- impeccable:design-schema 1 -->

## World

**Bahnhofs-Klapptafel.** Jede Wertungszeile ist eine physische Split-Flap-Einheit wie
am Bahnsteig: dunkles Gehäuse, cremefarbene Klapp-Fläche mit Scharnier-Linie, fette
Mono-Ziffern. Verweigert den generischen Formular-Screen (Dropdown-Reihen auf neutralem
Grund), den die vorherige Version hatte.

Gegenprobe: Spieler sitzt abends am Tisch, würfelt, tippt die Werte ein – soll sich wie
ein Blick auf die Anzeigetafel anfühlen, nicht wie ein Web-Formular.

## Mode

**Operate.** Aufgabe: Werte eintragen, Summe ablesen. Klarheit schlägt Ausdruck; der
Flap-Look sitzt exakt auf den Zahlen, die gelesen werden müssen, nicht auf jedem Pixel.

## Palette

Objektfarben (Gehäuse, Flap-Fläche, Kategorie-Signallichter) ändern sich nicht mit
Hell/Dunkel – nur die Halle drumherum:

```css
--wall:       #101114;  /* Bahnhofshalle, dunkel (Standard) */
--wall-light: #dedad0;  /* Halle bei Hell-Modus (prefers-color-scheme: light) */
--case:       #1c1d22;  /* Gehäuse jeder Flap-Einheit */
--case-edge:  #35373f;
--flap:       #f1ecdf;  /* Klapp-Fläche */
--ink:        #17140f;  /* Ziffern auf der Klapp-Fläche */
--accent:     #e8a838;  /* Bahnhofs-Anzeigelicht: primäre Aktionen, aktiver Tab */
```

Kategorie-Signallichter (unverändert aus dem Spiel, nicht neu erfunden): Gelb `#f0bb3a`,
Lila `#a78bfa`, Blau `#60a5fa`, Rot `#f87171`, Grün `#4ade80`, Klar `#9aa3b2`,
Mitleid `#f472b6` – je ein kleiner Punkt (Signallicht) statt einer Farbfläche.

## Type

- **Oswald** 600/700, Großbuchstaben, gesperrt – Bahnhofsschild-Beschriftung (Labels,
  Titel, Buttons).
- **Space Mono** 700 – alle angezeigten Zahlen (Klapp-Ziffern, Tabellenwerte), weil es
  echte Messwerte/Daten sind, kein Stilmittel.
- **DM Sans** – unverändert für Fließtext in der Hilfe (bereits vorhanden, funktioniert).

## Components

- **Flap-Zahl** (`.dr-result`, `.rt-val`, `.wscore`) – cremefarbene Fläche, dünne
  Scharnier-Linie via `::after`, Klapp-Animation (`flapflip`, 0.34s) beim Ändern eines
  Werts, ausgelöst über `flipEl()`.
- **Signallicht** (`.dr-stripe`) – kleiner Punkt statt Farbbalken, Kategoriefarbe direkt
  inline gesetzt.
- **Gehäuse-Container** (`.die-list`, `.app-header`, `.tab-bar`, `.done-card`, `.hc`,
  `.help-rule`) – `--case`/`--case-edge`, dunkel unabhängig vom Theme.

## Motion

Eine Klapp-Animation (`flapflip`) beim Live-Update einer Flap-Zahl – `rotateX`-basiert,
simuliert eine physische Klappe. Respektiert `prefers-reduced-motion`.

## Constraints

- Bleibt eine einzige `index.html`, Vanilla JS/CSS, kein Build, kein Backend
  (ausdrücklicher Nutzerwunsch).
- Bestehende Funktionalität/Formeln nicht verändert – nur Darstellung.
- Kein Foto-Referenzmaterial vorhanden; Welt frei gewählt (Split-Flap-Bahnhofsanzeige),
  aus drei vorgelegten Kandidaten vom Nutzer bestätigt.
