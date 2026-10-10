# The original: power supply board PS3116 of the Roland TR-808

> **UNTESTED.** This describes how the rebuild relates to the original; nothing here was
> verified on a real unit. See [VERIFICATION.md](VERIFICATION.md).

Source is the service manual "TR-808 Service Notes" (Roland, 15 June 1981, 3rd printing),
archive.org scan `Roland_TR-808_Service_Manual.pdf` (MD5 `77ac6c77c9e0d92ea67b2021ecc97623`,
16 pages). The manual is not part of this repo; to check the work, download it yourself and
put it under `vorlage/` (German for "template"; excluded there by `.gitignore`).

| Sheet | Contents | Used for |
|---|---|---|
| 2 | pin assignments (TA7179P, µA7805) | symbols IC2, IC1 |
| 10 | parts list | component types, board numbers |
| 12 | component layout POWER SUPPLY PS3116-051/-054, PCB 291-405A | board outline, component positions |
| 13 | schematic (top left: POWER SUPPLY) | schematic |
| 15 | design changes | read, does not concern the power supply |

## Variants

The board is the same for all mains voltages; only the fitting and accessories differ:

| Mains | Board | T1 | Switch | C1 | Fuses F1–F4 |
|---|---|---|---|---|---|
| 100 V | PS3116-051 | N-217N | SDG5P-001 | ECQ-UC1A473MC | SGA 0.5 A |
| 117 V | PS3116-051 | N-218C | SDG5P-001 | ECQ-UC1A473MC | SGA 0.5 A |
| 220 V | PS3116-054 | N-219D | SDG5P-502 | ECQ-U2A473MF | CEE 250 mAT |
| 240 V | PS3116-054 | N-219D | SDG5P-502 | ECQ-U2A473MF | CEE 250 mAT |

**This repo models both: the 220/240 V variant (PS3116-054, files `Rev0.5`) and, from Rev0.5,
the 100/117 V variant (PS3116-051) built for 110 V (files `Rev0.5-110V`, transformer N-218C,
117 V tap; 110 V is 6 % below its rating).** Only parts change (C1, F1–F4, T1, switch); the copper
is identical. The schematic of each variant carries its own values. According to the manual F2 and F3 are
fitted differently on late 100/117 V units; the note in the plan is hard to read at that
spot, see "Open".

## Circuit

* **Mains:** terminals 3 (W1) and 1 (W3) are the mains lead. 3 and 4, and 1 and 2, are
  connected on the board. The mains switch (two poles, not on the board) connects 4–5 and
  2–6. C1 (47 nF, interference suppression) sits between 5 and 6, F1 from the switch to
  terminal 8. T1 connects to 7, 8, 9 (primary) and 10–14 (secondary).
* **+5 V:** winding yellow–yellow (10, 11) → F2 → bridge D1 → C3 1000 µ/16, C4 100 n → IC1
  µA7805 → +5 V. C2 100 n and C16 10 µ at the output. Terminal 19 is +5 V, 15 and 18 are the
  5 V ground.
* **RAM backup:** D3 (1S2473) from +5 V, D4 (1S2473) from the 3 × 1.5 V battery (terminal 16,
  minus at 15), both cathodes to terminal 17.
* **±15 V:** winding red–black–red (12, 13 centre tap, 14) → F3/F4 → bridge D2 → C13, C12
  1000 µ/35 each → ±23 V. IC2 TA7179P (dual tracking regulator) with the pass transistors
  Q1 2SB596 (+) and Q2 2SD880 (−), a 47 Ω base resistor each (R7, R1) with 100 n (C10, C9),
  3.3 Ω current limit (R2, R5), divider R3/R4 15 k, C7/C8 10 n compensation. Outputs +15 V
  (22), 0 V (21), −15 V (20). C5, C14, C6, C15 smoothing, C11 470 µ/16 with R6 220 Ω as load.
* **Secondary voltages according to the plan at 0.15 A DC:** 10 V (yellow–yellow), 23 V per
  half (red–black).

## What the rebuild changes

* The original is **single sided** (wire jumper J1). This rebuild is **two-layer**, the
  jumper is dropped; board outline, holes, terminals and component positions follow the
  component layout and are adjusted to the scan copper; the tracks **follow the original
  copper only to 37 %** (router with a cost map from the scan, see the README), the rest is
  routed anew.
* The two grounds (5 V branch: terminals 15/18; ±15 V branch: 13/21) are **not** connected
  in the plan and are not connected here either. They meet only outside the board, probably
  on the main board.
* Transformer T1, mains switch and battery are not on the board (from Rev0.3 mains, switch
  and transformer input use RM5 screw terminals instead of solder lugs) and appear in the
  schematic only as external symbols.
* Bridges D1/D2: **W04** (400 V; the unit shows 2W04G) instead of W-02 (200 V) from the
  manual. The W04 is a permissible replacement in the same package.

## Open / not proven

* **Scale:** the component layout has no scale bar. The scale (0.544 mm per pt) is derived
  from the TO-220 lead pitch (2.54 mm) and the DIP-14; the board is 142.9 × 119.4 mm, with a
  tolerance of roughly ±3 %. Measure against a real board before manufacturing (holes of the
  heat sink 246-101A, distance of the fuse clips 22.5 mm).
* **Labelling in the component layout deviates from the schematic** at R1/R7 and C9/C10 (the
  assignment to Q1/Q2 is swapped). The netlist follows the schematic; the parts sit by
  function in the layout.
* **Lead spacing of the parts** (resistors, film capacitors) was chosen from the scan copper
  (pads must lie on copper pieces that carry only one net), not from the manual; four copper
  pieces still show a net conflict in the fit (AC15_A/AC15_RAW_A and others, probably
  connected copper because of the scan quality). The manual gives no package types.
* **Packages:** bridge as a round package ø 9.8 mm (Vishay WOG), electrolytics by measured
  diameter; the manual gives no package types.
* Pin assignment of 2SB596 / 2SD880: B-C-E (MOSPEC resp. DC Components data sheets, from
  archive.org/distributors, not in the repo).
* The footnote on the fuses ("F2–F3 on later 100/117V versions … 10 ohm 1/4W (fusing
  resistor)") is cut off in the scan and not clearly legible.
