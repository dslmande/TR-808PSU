# Stückliste TR-808PSU Rev0.3

Aus dem Schaltplan erzeugt (`psu/TR-808PSU_Rev0.3_bom.csv`). **Keine Preise, keine Lieferanten:** nichts davon ist geprüft.
Bauteile des Netzteils nach Service Manual (PS3116, 220/240 V); Spalte „Bemerkung“ nennt das Originalteil, wo das Manual eines nennt.

| Bezeichner | Menge | Wert | Funktion | Bauform (KiCad) | Bemerkung |
|---|---|---|---|---|---|
| C1 | 1 | 0.047u/X2 | Funkentstörkondensator X2, 220/240 V | `C_Rect_L26.5mm_W8.5mm_P22.50mm_MKS4` | Original ECQ-U2A473MF (Panasonic), 47 nF, 275 V~ |
| C2 | 1 | 0.1u | Entkopplung +5 V | `C_Rect_L13.0mm_W4.0mm_P10.00mm_FKS3_FKP3_MKS4` | 100 nF Folie |
| C3 | 1 | 1000u/16V | Siebung 5-V-Zweig | `CP_Radial_D12.5mm_P5.00mm` | 1000 µF / 16 V Elko |
| C4, C5, C6, C9, C10 | 5 | 0.1u | Entkopplung / Siebung | `C_Rect_L10.3mm_W5.0mm_P7.50mm_MKS4` | 100 nF Folie, RM 7,5 mm |
| C7 | 1 | 0.01u | Kompensation TA7179P Pin 3 | `C_Disc_D5.0mm_W2.5mm_P5.00mm` | 10 nF |
| C8 | 1 | 0.01u | Kompensation TA7179P Pin 12 | `C_Disc_D3.0mm_W2.0mm_P2.50mm` | 10 nF |
| C11 | 1 | 470u/16V | Last ±15 V mit R6 | `CP_Radial_D10.0mm_P5.00mm` | 470 µF / 16 V Elko |
| C12, C13 | 2 | 1000u/35V | Siebung ±23 V | `CP_Radial_D16.0mm_P7.50mm` | 1000 µF / 35 V Elko |
| C14, C15, C16 | 3 | 10u/16V | Ausgangssiebung | `CP_Radial_D5.0mm_P2.50mm` | 10 µF / 16 V Elko |
| D1, D2 | 2 | W04 | Brückengleichrichter, rund | `Diode_Bridge_Round_D9.8mm` | Manual: W-02 (200 V); verbaut/ersetzt: W04 (2W04G, 400 V) |
| D3, D4 | 2 | 1S2473 | RAM-Pufferdioden | `D_DO-35_SOD27_P10.16mm_Horizontal` | 1S2473 (Si-Diode); Ersatz z. B. 1N4148 – nicht geprüft |
| F1, F2, F3, F4 | 4 | 250mAT | Feinsicherungen 5×20 mm | `FuseClip_5x20_TF785` | T250 mA / 250 V (CEE, 220/240 V); Clips TF785, Abstand 22,5 mm |
| IC1 | 1 | uA7805 | 5-V-Regler | `TO-220-3_Vertical` | µA7805UC, TO-220, liegend auf dem Kühlwinkel |
| IC2 | 1 | TA7179P | Dual ±15-V-Tracking-Regler | `DIP-14_W7.62mm` | TA7179P (Toshiba), DIP-14 – vermutlich abgekündigt, Verfügbarkeit nicht geprüft |
| Q1 | 1 | 2SB596 | Längstransistor +15 V | `TO-220-3_Vertical` | 2SB596 (PNP, TO-220) |
| Q2 | 1 | 2SD880 | Längstransistor −15 V | `TO-220-3_Vertical` | 2SD880 (NPN, TO-220) |
| R1 | 1 | 47 | Basiswiderstand Q2 | `R_Axial_DIN0207_L6.3mm_D2.5mm_P7.62mm_Horizontal` | 47 Ω |
| R2, R5 | 2 | 3.3 | Strombegrenzung | `R_Axial_DIN0207_L6.3mm_D2.5mm_P10.16mm_Horizontal` | 3,3 Ω |
| R3, R4 | 2 | 15k | Spannungsteiler | `R_Axial_DIN0207_L6.3mm_D2.5mm_P10.16mm_Horizontal` | 15 kΩ |
| R6 | 1 | 220 | Last ±15 V mit C11 | `R_Axial_DIN0207_L6.3mm_D2.5mm_P7.62mm_Horizontal` | 220 Ω |
| R7 | 1 | 47 | Basiswiderstand Q1 | `R_Axial_DIN0207_L6.3mm_D2.5mm_P10.16mm_Horizontal` | 47 Ω |
| X1, X2, X3 | 3 | 2P RM5 | Schraubklemmen 230 V, 2-polig | `TerminalBlock_Phoenix_MKDS-1,5-2_1x02_P5.00mm_Horizontal` | Phoenix MKDS 1,5/2-5,00 (RM 5,0) |
| X4 | 1 | 3P RM5 | Schraubklemme 230 V, 3-polig | `TerminalBlock_Phoenix_MKDS-1,5-3_1x03_P5.00mm_Horizontal` | Phoenix MKDS 1,5/3-5,00 (RM 5,0) |
| P10, P11, P12, P13, P14, P15, P16, P17, P18, P19, P20, P21, P22 | 13 | Lötöse | Anschlüsse 10–22 (Kleinspannung) | `Terminal_Pin` (Eigenbau) | Original: Lötösen; Loch 1,6 mm, Pad 4,4 × 3,4 mm |

## Nicht in der Stückliste (mechanisch / extern)

- **Netztrafo T1:** am Platineneingang über Klemmen 7–9 (primär) und 10–14 (sekundär); Original N-219D (220/240 V), nicht auf der Platine.
- **Netzschalter SW1** (zweipolig), **Batterie 3 × 1,5 V** (zwischen 15 und 16): extern.
- **Kühlkörper 246-101A** (Aluminiumwinkel, drei Stück) mit Schrauben M3, 10 Löcher für die Winkel plus drei Schraubenlöcher der Regler.
- **Befestigung:** vier M3-Bohrungen an den Platinenecken.

## Bauteile mit Risiko

TA7179P, 2SB596, 2SD880 und die 1S2473 sind Teile aus den frühen 1980ern; bei Nachbauten alter Geräte sind solche Typen häufig abgekündigt und am Markt von Fälschungen betroffen. Vor einer Bestellung per Mouser/TME-API prüfen und einen Ersatz für IC2 festlegen (siehe [PRUEFUNG.md](PRUEFUNG.md)).
