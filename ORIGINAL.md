# Das Original: Netzteilplatine PS3116 des Roland TR-808

Quelle ist das Service Manual „TR-808 Service Notes“ (Roland, 15.06.1981,
3. Auflage), archive.org-Scan `Roland_TR-808_Service_Manual.pdf`
(MD5 `77ac6c77c9e0d92ea67b2021ecc97623`, 16 Seiten). Das Manual liegt nicht in
diesem Repo; wer nachprüfen will, lädt es selbst und legt es nach `vorlage/`
(dort ist es per `.gitignore` ausgeschlossen).

| Blatt | Inhalt | Verwendet für |
|---|---|---|
| 2 | Pinbelegungen (TA7179P, µA7805) | Symbol IC2, IC1 |
| 10 | Stückliste | Bauteiltypen, Platinennummern |
| 12 | Bestückungsplan POWER SUPPLY PS3116-051/-054, PCB 291-405A | Platinenumriss, Bauteilpositionen |
| 13 | Schaltbild (oben links: POWER SUPPLY) | Schaltplan |
| 15 | Design Changes | gelesen, betrifft das Netzteil nicht |

## Varianten

Die Platine ist für alle Netzspannungen dieselbe; sie unterscheidet sich nur in
Bestückung und Zubehör:

| Netz | Platine | T1 | Schalter | C1 | Sicherungen F1–F4 |
|---|---|---|---|---|---|
| 100 V | PS3116-051 | N-217N | SDG5P-001 | ECQ-UC1A473MC | SGA 0,5 A |
| 117 V | PS3116-051 | N-218C | SDG5P-001 | ECQ-UC1A473MC | SGA 0,5 A |
| 220 V | PS3116-054 | N-219D | SDG5P-502 | ECQ-U2A473MF | CEE 250 mAT |
| 240 V | PS3116-054 | N-219D | SDG5P-502 | ECQ-U2A473MF | CEE 250 mAT |

**Dieses Repo bildet die 220/240-V-Variante (PS3116-054) ab.** Für 100/117 V
ändern sich nur die Werte von C1 und F1–F4 (im Schaltplan als Text vermerkt).
Laut Manual sitzen F2 und F3 bei späten 100/117-V-Geräten anders; der Hinweis
im Plan ist an dieser Stelle schlecht lesbar, siehe „Offen“.

## Schaltung

* **Netz:** Anschluss 3 (W1) und 1 (W3) sind die Netzleitung. 3 und 4 sowie 1
  und 2 sind auf der Platine verbunden. Der Netzschalter (zweipolig, nicht auf
  der Platine) verbindet 4–5 und 2–6. C1 (47 nF, Funkentstörung) liegt zwischen
  5 und 6, F1 vom Schalter zu Anschluss 8. T1 hängt an 7, 8, 9 (Primär) und
  10–14 (Sekundär).
* **+5 V:** Wicklung gelb–gelb (10, 11) → F2 → Brücke D1 (W02) → C3 1000 µ/16,
  C4 100 n → IC1 µA7805 → +5 V. C2 100 n und C16 10 µ am Ausgang. Anschluss 19 ist
  +5 V, 15 und 18 sind die 5-V-Masse.
* **RAM-Puffer:** D3 (1S2473) vom +5 V, D4 (1S2473) von der Batterie 3 × 1,5 V
  (Anschluss 16, Minus an 15), beide Kathoden auf Anschluss 17.
* **±15 V:** Wicklung rot–schwarz–rot (12, 13 Mittelanzapfung, 14) → F3/F4 → Brücke
  D2 → C13, C12 je 1000 µ/35 → ±23 V. IC2 TA7179P (zweifach nachführender Regler)
  mit den Durchlasstransistoren Q1 2SB596 (+) und Q2 2SD880 (−), je ein
  Basisvorwiderstand 47 Ω (R7, R1) mit 100 n (C10, C9), 3,3 Ω Strombegrenzung (R2,
  R5), Teiler R3/R4 15 k, C7/C8 10 n Kompensation. Ausgang +15 V (22), 0 V (21),
  −15 V (20). C5, C14, C6, C15 Siebung, C11 470 µ/16 mit R6 220 Ω als Last.
* **Sekundärspannungen laut Plan bei 0,15 A DC:** 10 V (gelb–gelb), 23 V je
  Hälfte (rot–schwarz).

## Was der Nachbau ändert

* Das Original ist **einseitig** (Drahtbrücke J1). Dieser Nachbau ist **zweilagig**,
  die Brücke entfällt; Platinenumriss, Bohrungen, Anschlüsse und Bauteillagen
  folgen dem Bestückungsplan und sind am Scan-Kupfer nachjustiert; die Leiterbahnen
  **folgen dem Original-Kupfer nur zu 36 %** (Router mit Kostenkarte aus dem Scan, siehe
  README), der Rest ist neu verlegt.
* Die beiden Massen (5-V-Zweig: Anschlüsse 15/18; ±15-V-Zweig: 13/21) sind im Plan
  **nicht** verbunden und bleiben es auch hier. Sie treffen sich erst außerhalb
  der Platine, vermutlich auf der Hauptplatine.
* Trafo T1, Netzschalter und Batterie sind nicht auf der Platine und stehen im
  Schaltplan nur als externe Symbole.

## Offen / nicht belegt

* **Maßstab:** Der Bestückungsplan trägt kein Maßband. Der Maßstab (0,544 mm je pt)
  ist aus dem TO-220-Beinraster (2,54 mm) und dem DIP-14 abgeleitet; die
  Platine misst damit 142,9 × 119,4 mm, Toleranz grob ±3 %. Vor einer Fertigung
  am Gerät gegenmessen (Löcher des Kühlkörpers 246-101A, Abstand der
  Sicherungsclips 22,5 mm).
* **Beschriftung im Bestückungsplan weicht vom Schaltbild ab** bei R1/R7 und
  C9/C10 (die Zuordnung zu Q1/Q2 ist vertauscht). Die Netzliste folgt dem
  Schaltbild; die Bauteile sitzen im Layout nach Funktion.
* **Rastermaße der Bauteile** (Widerstände, Folienkondensatoren) sind aus dem Kupfer des Scans
  gewählt (Pads müssen auf Kupferstücken liegen, die nur ein Netz tragen), nicht aus dem Manual;
  bei vier Kupferstücken bleibt ein Netzkonflikt im Abgleich (AC15_A/AC15_RAW_A u. a., vermutlich
  zusammenhängendes Kupfer durch die Rasterqualität). Das Manual nennt keine Bauformen.
* **Gehäuse der Bauteile:** W02 als runde Brücke ø 9,8 mm (Vishay WOG), Elkos nach
  gemessenem Durchmesser; das Manual nennt keine Bauformen.
* Pinbelegung 2SB596 / 2SD880: B-C-E (MOSPEC bzw. DC Components, Datenblätter
  archive.org/Händler, nicht im Repo).
* Fußnote zu den Sicherungen („F2–F3 on later 100/117V versions … 10 ohm 1/4W
  (fusing resistor)“) ist im Scan angeschnitten und nicht eindeutig lesbar.
