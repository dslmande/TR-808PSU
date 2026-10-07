# TR-808PSU

Nachbau der Netzteilplatine **PS3116 (PCB 291-405A)** des Roland TR-808 als
KiCad-Projekt: Schaltplan nach dem Service Manual von 1981, Platine mit
Umriss, Bohrungen, Anschlüssen und Bauteillagen wie im Bestückungsplan des
Originals. Variante **220/240 V** (PS3116-054).

Stand: **Rev0.1**, nicht gefertigt, nicht am Gerät erprobt.

| Datei | Inhalt |
|---|---|
| [ORIGINAL.md](ORIGINAL.md) | Quelle, Blätter, Varianten, Schaltungsbeschreibung, was offen ist |
| `psu/TR-808PSU_Rev0.1.kicad_pro` / `.kicad_sch` / `.kicad_pcb` | KiCad-Projekt |
| `psu/TR-808PSU_Rev0.1_schaltplan.pdf` | Plot des Schaltplans |
| `psu/gerber/`, `psu/TR-808PSU_Rev0.1_gerber.zip` | Gerber, Bohrdaten, Bestückungsliste |
| `psu/TR-808PSU_Rev0.1_bom.csv` | Stückliste |
| `psu/TR-808PSU_Rev0.1_ausdruck_1zu1.pdf` | 1:1-Ausdruck auf A4 quer: Bestückungsseite, Lötseite, Bohrschablone (100 % drucken, Messstrecke prüfen) |
| `psu/TR-808PSU_Rev0.1_3d_oben.png`, `_3d_schraeg.png` | 3D-Ansichten (KiCad-Raytracing; Regler, Sicherungshalter und Anschlusspins ohne 3D-Modell) |
| `psu/TR-808PSU_Rev0.1_pcb_top.pdf`, `_pcb_bottom.pdf`, `_assembly.pdf` | Plots der Platine |
| `psu/placement.json`, `psu/placement_scan.json` | Bauteilpositionen aus dem Bestückungsplan bzw. am Scan ausgerichtet (mm) |
| `psu/kupfer.npz`, `psu/leitkarte.npz` | Kupfermaske und Netzgebiete des Originals (aus dem Scan) |
| `psu/TR-808PSU_Rev0.1_ueberlagerung.png` | Original-Kupfer gegen die Bahnen dieser Platine |
| `tools/` | Generator und Werkzeugkette (aus dem Oakley-Projekt) |

## Was „1:1“ hier heißt

* **Schaltung:** Bauteilnummern (C1–C16, R1–R7, D1–D4, F1–F4, Q1, Q2, IC1, IC2),
  Werte und Anschlussnummern 1–22 wie im Original. Der Plan ist wie das Original
  gezeichnet (Netz und Schalter links, Trafo, +5-V-Zweig, ±15-V-Zweig).
* **Platine:** Umriss, vier Befestigungsbohrungen, sechs Kühlkörperbohrungen (je Regler ein Paar, 21,3 mm Abstand, mittig) und drei Schraubenlöcher M3 der Regler,
  Anschlusspins, Sicherungsclips und alle Bauteile an den Stellen des Originals,
  fein am abgetasteten Kupfer des Scans ausgerichtet (`tools/scan/`).
  Das Original ist einseitig mit einer Drahtbrücke; dieser Nachbau ist
  zweilagig.
* **Leiterbahnen: vom Original geführt, nicht Zug um Zug übernommen.** Das Kupfer des
  Originals wird aus dem Scan gewonnen (Halbtonraster → Maske → Netzgebiete) und dient
  dem Router als Kostenkarte: Kupfer des Originals ist billig, alles andere teuer, die
  Vorderseite fast gesperrt. Das ergibt eine DRC-saubere Platine, die dem Original
  folgt, wo der Scan es hergibt. **36 % der Bahnlänge liegen im Original-Kupfer**, der
  Rest ist neu verlegt (breite Bahnen und das Glätten rücken die Wege vom Original ab); das Bild `psu/TR-808PSU_Rev0.1_ueberlagerung.png` zeigt das
  Original-Kupfer (grau) und die Bahnen (rot Lötseite, blau Vorderseite). Eine reine
  Abtastung ohne Router scheitert an der Rasterqualität des Scans (Kurzschlüsse
  zwischen Nachbarbahnen, Padlagen nur auf ±0,3 mm).
* **Maße** sind aus dem Plan abgeleitet (kein Maßband im Manual), Toleranz grob
  ±3 %. Vor einer Fertigung gegen eine echte Platine messen. Einzelheiten und
  weitere offene Punkte in [ORIGINAL.md](ORIGINAL.md).

## Prüfstand (Rev0.1, 06.10.2026)

* **ERC:** 0 Verstöße (`psu/TR-808PSU_Rev0.1-erc.rpt`).
* **DRC (Abstandsregel 0,25 mm):** 0 Fehler, 3 Courtyard-Überlappungen (Warnung: die Bauteile sitzen so
  eng wie im Original); 0 unverbundene Verbindungen; Abgleich Schaltplan–Platine 0.
* **Netz gegen Kleinspannung:** kleinster Abstand 6,5 mm (`tools/pcb/netzabstand.py psu/TR-808PSU_Rev0.1.kicad_pcb /MAINS_A /MAINS_B /SW_A /SW_B /PRI_8 /PRI_9`).
* **Netzliste gegen das Schaltbild:** vom Schaltbild von Hand gelesen und am
  Plot gegengesehen; kein unabhängiger Abgleich, siehe „Offen“ in ORIGINAL.md.
* Bahnbreite 1,0 mm überall (`tools/pcb/verbreitern.py` setzt auch die vom Router schmal
  gelassenen Netze GND5, GND15 und COL1 auf 1,0 mm, nur 7 Stücke an engen Pads bleiben bei
  0,5–0,8 mm); Haarnadeln und Stummel in den Pads sind entfernt (`tools/pcb/padstummel.py`); geglättet mit dem Skill pcb-glaetten (45°, Bögen,
  `tools/pcb/glaetten.py`, in `make.py` eingehängt). Keine Masseflächen, wie im Original.
  Fünf Durchkontaktierungen, sonst läuft das meiste auf der Lötseite, rund 440 mm der Bahnen liegen auf der
  Vorderseite (im Original gab es dafür die Drahtbrücke J1).
* **Bestückungsdruck:** nur Bezeichner (keine Werte), Anschlussnummern P1–P22, Elko-Polarität
  als Balken am Minuspol wie im Original, die vier Sicherungshalter F1–F4 auf einer Höhe
  (`tools/pcb/silk.py`, `tools/pcb/polaritaet.py`, beide am Ende von `make.py`).
* **Nicht geprüft:** Aufbau und Messung am Gerät, Fertigung.

## Erzeugen

Plan und Layout werden erzeugt, nicht von Hand gezeichnet:

```bash
python3 tools/pcb/fp_tr808.py psu/TR808PSU.pretty
python3 tools/psu/build_psu.py psu
python3 tools/textplace.py psu/TR-808PSU_Rev0.1.kicad_sch
python3 tools/textfix.py psu/TR-808PSU_Rev0.1.kicad_sch
python3 tools/pcb/original_placement.py psu
python3 tools/scan/kupfer.py vorlage/Roland_TR-808_Service_Manual.pdf psu/kupfer.npz
python3 tools/scan/fit2.py psu psu/kupfer.npz          # Bauteile am Scan ausrichten
python3 tools/psu/build_psu.py psu                      # Plan mit den Bauformen aus dem Abgleich
python3 tools/scan/leitkarte.py psu psu/kupfer.npz
python3 tools/pcb/make.py psu --passes=60 --rounds=1 --budget=900   # glättet am Ende
```

Benötigt KiCad 9 (`kicad-cli`) und Python 3.

## Quelle und Rechte

Schaltung und Maße stammen aus dem Roland TR-808 Service Manual (15.06.1981).
Das Manual selbst und die Datenblätter sind nicht Teil dieses Repos
(Urheberrecht Roland bzw. der Hersteller). Dieses Repo enthält eine eigene
Nachzeichnung für Reparatur und Nachbau. „Roland“ und „TR-808“ sind Marken von
Roland Corporation; dieses Projekt ist nicht mit Roland verbunden.

Datenblätter, die zur Prüfung der Pinbelegung dienten:
2SB596 (MOSPEC), 2SD880 (DC Components), TA7179P und µA7805 (Service Manual Blatt 2).
