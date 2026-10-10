# Bill of materials TR-808PSU Rev0.5-110V

> **UNTESTED.** Nothing here has been ordered, built or measured.

Generated from the schematic (`psu/TR-808PSU_Rev0.5-110V_bom.csv`). **No prices, no suppliers:** none of that is checked.
Parts of the power supply per the service manual (PS3116-051, 100/117 V, built for 110 V); the "Remark" column names the original part where the manual gives one.

| Designators | Qty | Value | Function | Package (KiCad) | Remark |
|---|---|---|---|---|---|
| C1 | 1 | 0.047u/X2 | Interference suppression capacitor, 100/117 V | `C_Rect_L26.5mm_W8.5mm_P22.50mm_MKS4` | Original ECQ-UC1A473MC (Panasonic), 47 nF; 110 V: X2 type is also fine |
| C2 | 1 | 0.1u | Decoupling +5 V | `C_Rect_L13.0mm_W4.0mm_P10.00mm_FKS3_FKP3_MKS4` | 100 nF film |
| C3 | 1 | 1000u/16V | Smoothing 5 V branch | `CP_Radial_D12.5mm_P5.00mm` | 1000 µF / 16 V electrolytic |
| C4, C5, C6, C9, C10 | 5 | 0.1u | Decoupling / smoothing | `C_Rect_L10.3mm_W5.0mm_P7.50mm_MKS4` | 100 nF film, 7.5 mm pitch |
| C7 | 1 | 0.01u | Compensation TA7179P pin 3 | `C_Disc_D5.0mm_W2.5mm_P5.00mm` | 10 nF |
| C8 | 1 | 0.01u | Compensation TA7179P pin 12 | `C_Disc_D3.0mm_W2.0mm_P2.50mm` | 10 nF |
| C11 | 1 | 470u/16V | Load ±15 V with R6 | `CP_Radial_D10.0mm_P5.00mm` | 470 µF / 16 V electrolytic |
| C12, C13 | 2 | 1000u/35V | Smoothing ±23 V | `CP_Radial_D16.0mm_P7.50mm` | 1000 µF / 35 V electrolytic |
| C14, C15, C16 | 3 | 10u/16V | Output smoothing | `CP_Radial_D5.0mm_P2.50mm` | 10 µF / 16 V electrolytic |
| D1, D2 | 2 | W04 | Bridge rectifier, round | `Diode_Bridge_Round_D9.8mm` | Manual: W-02 (200 V); fitted/replacement: W04 (2W04G, 400 V) |
| D3, D4 | 2 | 1S2473 | RAM backup diodes | `D_DO-35_SOD27_P10.16mm_Horizontal` | 1S2473 (Si diode); replacement e.g. 1N4148 – not checked |
| F1, F2, F3, F4 | 4 | 0.5A | Miniature fuses 5×20 mm | `FuseClip_5x20_TF785` | SGA 0.5 A (100/117 V); clips TF785, 22.5 mm apart; fuse type per original, not checked |
| IC1 | 1 | uA7805 | 5 V regulator | `TO-220-3_Vertical` | µA7805UC, TO-220, lying on the heat sink angle |
| IC2 | 1 | TA7179P | Dual ±15 V tracking regulator | `DIP-14_W7.62mm` | TA7179P (Toshiba), DIP-14 – probably discontinued, availability not checked |
| P10 | 1 | 10 |  | `Terminal_Pin` |  |
| P11 | 1 | 11 |  | `Terminal_Pin` |  |
| P12 | 1 | 12 |  | `Terminal_Pin` |  |
| P13 | 1 | 13 |  | `Terminal_Pin` |  |
| P14 | 1 | 14 |  | `Terminal_Pin` |  |
| P15 | 1 | 15 |  | `Terminal_Pin` |  |
| P16 | 1 | 16 |  | `Terminal_Pin` |  |
| P17 | 1 | 17 |  | `Terminal_Pin` |  |
| P18 | 1 | 18 |  | `Terminal_Pin` |  |
| P19 | 1 | 19 |  | `Terminal_Pin` |  |
| P20 | 1 | 20 |  | `Terminal_Pin` |  |
| P21 | 1 | 21 |  | `Terminal_Pin` |  |
| P22 | 1 | 22 |  | `Terminal_Pin` |  |
| Q1 | 1 | 2SB596 | Pass transistor +15 V | `TO-220-3_Vertical` | 2SB596 (PNP, TO-220) |
| Q2 | 1 | 2SD880 | Pass transistor −15 V | `TO-220-3_Vertical` | 2SD880 (NPN, TO-220) |
| R1 | 1 | 47 | Base resistor Q2 | `R_Axial_DIN0207_L6.3mm_D2.5mm_P7.62mm_Horizontal` | 47 Ω |
| R2, R5 | 2 | 3.3 | Current limit | `R_Axial_DIN0207_L6.3mm_D2.5mm_P10.16mm_Horizontal` | 3.3 Ω |
| R3, R4 | 2 | 15k | Voltage divider | `R_Axial_DIN0207_L6.3mm_D2.5mm_P10.16mm_Horizontal` | 15 kΩ |
| R6 | 1 | 220 | Load ±15 V with C11 | `R_Axial_DIN0207_L6.3mm_D2.5mm_P7.62mm_Horizontal` | 220 Ω |
| R7 | 1 | 47 | Base resistor Q1 | `R_Axial_DIN0207_L6.3mm_D2.5mm_P10.16mm_Horizontal` | 47 Ω |
| X1, X2, X3 | 3 | 2P RM5 | Screw terminals mains (110 V), 2 poles | `TerminalBlock_Phoenix_MKDS-1,5-2_1x02_P5.00mm_Horizontal` | Phoenix MKDS 1,5/2-5,00 (5.0 mm pitch) |
| X4 | 1 | 3P RM5 | Screw terminal mains (110 V), 3 poles | `TerminalBlock_Phoenix_MKDS-1,5-3_1x03_P5.00mm_Horizontal` | Phoenix MKDS 1,5/3-5,00 (5.0 mm pitch) |
|  | 0 | solder lug | terminals 10–22 (low voltage) | `Terminal_Pin` (own design) | original: solder lugs; hole 1.6 mm, pad 4.4 × 3.4 mm |

## Not in the bill of materials (mechanical / external)

- **Mains transformer T1:** connected through terminals 7–9 (primary) and 10–14 (secondary); original N-218C (117 V), not on the board; 110 V is 6 % below its rating.
- **Mains switch SW1** (two poles, SDG5P-001 for 100/117 V) and **battery 3 × 1.5 V** (between 15 and 16): external.
- **Heat sink 246-101A** (aluminium angles, three pieces) with M3 screws: 6 holes for the angles plus three screw holes for the regulators.
- **Mounting:** four M3 holes at the board corners.

## Parts at risk

TA7179P, 2SB596, 2SD880 and the 1S2473 are early-1980s parts; with rebuilds of old units such types are often discontinued and affected by counterfeits. Before ordering, check them via the Mouser/TME API and settle a replacement for IC2 (see [VERIFICATION.md](VERIFICATION.md)).
