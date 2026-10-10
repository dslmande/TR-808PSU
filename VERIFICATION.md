# Verification against standards and acceptance criteria (Rev0.5, 10 Oct 2026)

> **UNTESTED.** Nothing on this page is a conformity statement. The board has not been
> manufactured or tested; the standards were researched only to see where a historical
> design differs from today's requirements.

**Context:** the original dates from 1984–86 (service manual, 3rd printing June 1986;
power supply board PS3116) and was never checked against today's safety standards. This
rebuild is a **1:1 copy of a historical design**. The standard values below are for
orientation: they show where the old design deviates from current requirements. They are
not acceptance criteria for the copy and no claim of conformity.

Approach, following the skill `regelwerk-auf-projekte-anwenden` (applying a rule set to the
real project): research the standard's current edition first, then tie it to the actual
inventory; separate verification (does it meet the specification?) from validation (does it
suit the purpose?). **No certification, no proof of conformity:** the board is a private
rebuild of a repair board; the standards texts are paid and were not available to me.

## Standards framework (researched)

| Subject | Standard | Status | Source |
|---|---|---|---|
| Safety of audio/video and IT equipment (replaces DIN EN 60065) | DIN EN IEC 62368-1 (VDE 0868-1) | edition 2024 + A11:2024, VDE 0868-1:2025-01 | [DIN EN IEC 62368-1:2024](https://ib-lenhardt.com/standards/din-en-iec-62368-1-2024-a11-2024), [testxchange](https://www.testxchange.com/pruefnorm/iecen-62368-1/) |
| Clearance and creepage, insulation coordination | IEC 60664-1 / DIN EN 60664-1 (VDE 0110-1) | table values not freely available; sources disagree (creepage at 250 V, pollution degree 2, material group III: 3.2 to 4 mm basic) | [Elektor part 1](https://elektormagazine.com/news/pcb-clearance-and-creepage-distances-1), [TI SLUP419](https://www.ti.com/lit/pdf/slup419) |
| Miniature fuses | DIN EN 60127 (T250mA/250V) | not checked |  |
| Interference suppression capacitor C1 | DIN EN 60384-14 (X2) | type per manual ECQ-U2A473MF, not checked |  |
| Printed boards | IPC-2221 / IPC-A-600 | not applied |  |

For a privately built part for one's own unit there is no CE marking obligation; anyone who
passes it on or sells it needs it. This is not legal advice.

## Verification (measured)

| Criterion | Result |
|---|---|
| ERC | 0 violations |
| DRC (rule 0.25 mm) | 0 errors, 0 unconnected, 0 schematic/board deviations |
| Mains against low voltage (copper to copper) | **more than 8 mm** (all mains nets against the 5 V and ±15 V nets) |
| Mains conductors against each other (SW_A against SW_B) | Rev0.3: tracks 4.0 to 5.67 mm, adjacent terminal poles 2.4 mm (RM5 pitch); Rev0.1 had 3.75 mm |
| Mains, terminal 8 against terminal 9 | 6.87 mm |
| Manufacturing | Gerber, drill and position data, 1:1 printout available |

The clearance measurement uses a temporary net class of 8 mm (the DRC reports every
shortfall). In Rev0.1 the two switched mains conductors were 3.75 mm apart: more than 2 mm
(basic-insulation clearance in the search hits) but **below 4 mm**, the most conservative
value found for creepage (material group III, pollution degree 2, 250 V). In Rev0.2 and
Rev0.3 they are at least 4.0 mm apart (tracks; 5.67 mm for SW_A/SW_B), mains against low
voltage is unchanged above 8 mm.

## Validation (not done yet)

These points can only be settled on the unit; no gate counts as passed while they are open:

1. **Scale:** the component layout has no scale bar (0.544 mm per pt, ±3 %). Measure against
   a real board (heat sink holes, fuse clips, terminal spacing).
2. **Under load:** measure +5 V, ±15 V and the RAM supply on an assembled supply (nominal
   values in the manual: 10 V DC from yellow–yellow, 23 V per half from red–black at 0.15 A DC).
3. **Supply in the unit:** does the board fit the TR-808 case, does the heat sink angle
   246-101A fit, do the terminals match the wiring (a photo of the real part is on hand).
4. **Insulation:** if the supply is passed on, high-voltage testing by a qualified person.

## Findings and non-conformities

| No. | Finding | Severity | Status |
|---|---|---|---|
| 1 | Rev0.1: SW_A/SW_B 3.75 mm; today's conservative value 4 mm (deviation of the historical design from today's standard) | medium | fixed in Rev0.2 |
| 2 | Bridges W04 instead of W-02 per manual (type on the real board: 2W04G) | low | deliberate, noted in ORIGINAL.md and in the schematic |
| 3 | Tracks follow the original copper only to 37 %; two-layer instead of single-sided | low | documented |
| 4 | Netlist read by hand from the schematic; 4 copper pieces with two nets in the scan fit | medium | open |
| 5 | 3D models for fuse holders and terminal lugs built by hand, dimensions estimated | low | documented |
| 6 | DRC warnings: 4 courtyards, 1 silkscreen, 7 footprint deviations (polarity bars) | low | deliberate |

## Risks (parts)

- **TA7179P** (Toshiba) and **2SB596/2SD880**: with rebuilds of old units it is the rule
  that key parts are discontinued; grey market means counterfeits. Before the first order,
  create a part check (stock and lifecycle via Mouser/TME API) and settle replacement types
  for IC2.
- **1S2473** (Si diode), **µA7805**: uncritical, but check as well.
- Data sheets for 2SB596 (MOSPEC) and 2SD880 (DC Components) were read for the pin
  assignment but are not in the repo (copyright).

## Versions

**Rev0.5** (230 V) and **Rev0.5-110V** change no tracks and no parts positions: all board corners
are rounded to R5 (house rule; DRC unchanged: 0 errors, 0 unconnected, parity 0 for both), a
voltage mark is added to the silkscreen (Rev0.5 moves it clear of the fuse holder outline), and the 110 V variant takes the 100/117 V parts of the
original (fuses 0.5 A, transformer N-218C, switch SDG5P-001). The mains clearance and creepage
figures above apply to both, since the copper is identical; the lower voltage only relaxes the
requirement and is not separately assessed. The 110 V transformer is a 117 V part, 110 V is 6 %
below its rating (not measured).

**Rev0.3** replaces the solder lugs of the 230 V primary side (terminals 1–9: mains lead,
mains switch, transformer input) with four RM5.0 screw terminals (X1 poles 1–2, X2 poles 3–4,
X3 poles 5–6, X4 poles 7–9). The pad spacing of adjacent poles is set by the pitch: 2.4 mm
edge to edge (L and N sit next to each other in X3 and X4). The terminals are built for mains
voltage; whether the board meets today's creepage distances there depends, as with any
terminal block, on the terminal manufacturer and is not demonstrated here. Tracks between the
mains conductors: at least 4.0 mm.

**Rev0.1** is the historical 1:1 copy (release `Rev0.1`). **Rev0.2** changes only the mains
side: SW_B is moved away from SW_A and from pad F1.1 (SW_A/SW_B at least 5.67 mm). Every
layout change is a new version: files renamed, version on the silkscreen, own release.

## Next step (gate before manufacturing)

Have a sample made, compare dimensions against the real board (validation 1) and only then
larger quantities. A gate is not passed "provisionally". Whoever passes the board on or sells
it is responsible for safety and CE marking.
