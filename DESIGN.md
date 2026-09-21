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

Objektfarben (Gehäuse, Flap-Fläche, Kategorie-Signallichter, Bedienelemente-Slots)
ändern sich nicht mit Hell/Dunkel – nur die Halle drumherum. **Text, der AUF
Gehäusen sitzt (Tabelle, Hilfe-Karten, Tab-Leiste, Labels), ist ebenfalls an das
Gehäuse gebunden** (`--case-ink` / `--case-ink2`) und wechselt nicht mit dem Theme –
sonst entsteht im Hellmodus dunkle Schrift auf dunklem Gehäuse:

```css
--wall:       #101114;  /* Bahnhofshalle, dunkel (Standard) */
--wall-light: #e3ded2;  /* Halle am Tag (Hell-Modus): heller Stein, weiches Licht */
--case:       #1c1d22;  /* Gehäuse jeder Flap-Einheit */
--case-edge:  #35373f;
--flap:       #f1ecdf;  /* Klapp-Fläche */
--ink:        #17140f;  /* Ziffern auf der Klapp-Fläche */
--accent:     #e8a838;  /* Bahnhofs-Anzeigelicht: primäre Aktionen, aktiver Tab */
--case-ink:   #e9e6df;  /* helle Tinte AUF Gehäusen (theme-unabhängig) */
--case-ink2:  #8b8a86;  /* Sekundär-Tinte AUF Gehäusen (theme-unabhängig) */
--slot:       #101114;  /* Bedienelemente als dunkle Slots (Pill, Selects, hbtn) */
--slot-border:#2c2d33;
--slot-ink:   #e9e6df;  --slot-ink2: #8b8a86;
```

Regeln:
- `--text`/`--text2` nur für Inhalte auf der Halle (`--wall`), alles auf
  `--case` nutzt `--case-ink`/`--case-ink2`.
- Bedienelemente (Runden-Pill, Selects, Icon-Buttons, Mini-Toggle) sind
  **dunkle Slots** – sie gehören zur Maschine, nicht zur Halle, und sind im
  Dunkelmodus identisch mit `--wall`.
- Der Hellmodus ist eine eigene Tag-Umgebung (`#e3ded2` warmer Stein, eigene
  Ränder `#d2cbb9`, weichere Schatten), keine reine Umfärbung der Dunkel-Halle.
  Dunkelmodus bleibt unangetastet.

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
- **Gesamt-Klappe** (`.total-flap`, `#hdr-total`) – Mini-Flap-Einheit im Header rechts
  neben Kopf-Brand; zeigt die laufende Gesamtpunktzahl und flippt bei jeder
  Wertungsänderung mit. Die Rundenanzeige (`.round-pill`) steht links, der Markenname
  in der Mitte.
- **Kategorie-Würfel** (`dieSVG()`, `.dr-die` in Eingabe, `.hc-die` in Hilfe) –
  Mini-Würfel-SVGs statt Farb-Punkte, jede Farbe mit eindeutigem Gesicht: Gelb 3,
  Lila 2, Blau 4, Rot 5, Grün 6, Klar 1 Augen, Mitleid ein Herz. Pips in
  `DIE_PIPS`, Zuordnung in `DIE_FACE` (dieselben Gesichter in Eingabe und Hilfe).
- **Setup-Dialog** (`.setup-overlay`, `.setup-card`, `.setup-opt`) – einmalige
  Moduswahl zu Spielbeginn: beim ersten Laden und nach „Neues Spiel". Abgedunkelte
  Halle mit Karten-Dialog, zwei wählbare Optionen (Auto / Manuell) mit Würfel-SVG,
  Kurzerklärung des Unterschieds und dem Hinweis, dass die Wahl für die ganze
  Partie gilt. Die Wahl speichert sich als `setupDone:true` im Spielstand – kein
  Popup bei Wiederkommenden mit laufender Partie (Migration setzt `setupDone`
  anhand vorhandener Daten).
- **Manuelle Werteingabe** (`.mi`) – **Dropdown** pro Farbe im Manuell-Modus, gleiche
  Slot-Optik und Pfeil-Grafik wie die Auto-Selects; Wertebereich −600…600, bei Rot
  auch negativ (negatives Werte-`<option>`). Negativ-Werte im Select rot eingefärbt
  (`.mi-neg`), Ergebnis-Flap bekommt wie gehabt `.neg`. Keine Umschalt-Leiste mehr
  in der Eingabe – der Modus ist Partie-Eigenschaft und wird nur im Setup-Dialog
  gewählt.
- **Gehäuse-Container** (`.die-list`, `.app-header`, `.tab-bar`, `.done-card`, `.hc`,
  `.help-rule`) – `--case`/`--case-edge`, dunkel unabhängig vom Theme.

## Motion

Eine Klapp-Animation (`flapflip`) beim Live-Update einer Flap-Zahl – `rotateX`-basiert,
simuliert eine physische Klappe. Respektiert `prefers-reduced-motion`.

## Fullscreen-Kompaktmodus

Im Vollbild passt die komplette Eingabe ohne Scrollen auf einen Screen. Die
Kompaktregeln (30 Stück) hängen an der **Body-Klasse `fs-compact`**, die `render()`
setzt: nur wenn Vollbild aktiv **und** Eingabe-Tab **und** Phase ≠ done. Bewusst per
JS-Klasse statt `:has()`-Selektor (wird nicht überall unterstützt) – Hilfe und
Tabelle bleiben im Vollbild normal scrollbar. Die 7 Würfelreihen teilen sich die
Resthöhe per Flex (`flex:1`, Rot-Zeile `flex:1.6`).

## Constraints

- Bleibt eine einzige `index.html`, Vanilla JS/CSS, kein Build, kein Backend
  (ausdrücklicher Nutzerwunsch).
- Bestehende Funktionalität/Formeln nicht verändert – nur Darstellung.
- Kein Foto-Referenzmaterial vorhanden; Welt frei gewählt (Split-Flap-Bahnhofsanzeige),
  aus drei vorgelegten Kandidaten vom Nutzer bestätigt.
