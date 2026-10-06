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
| `psu/TR-808PSU_Rev0.1_pcb_top.pdf`, `_pcb_bottom.pdf`, `_assembly.pdf` | Plots der Platine |
| `psu/placement.json` | Bauteilpositionen aus dem Bestückungsplan (mm) |
| `tools/` | Generator und Werkzeugkette (aus dem Oakley-Projekt) |

## Was „1:1“ hier heißt

* **Schaltung:** Bauteilnummern (C1–C16, R1–R7, D1–D4, F1–F4, Q1, Q2, IC1, IC2),
  Werte und Anschlussnummern 1–22 wie im Original. Der Plan ist wie das Original
  gezeichnet (Netz und Schalter links, Trafo, +5-V-Zweig, ±15-V-Zweig).
* **Platine:** Umriss, vier Befestigungsbohrungen, sechs Kühlkörperbohrungen,
  Anschlusspins, Sicherungsclips und alle Bauteile an den Stellen des Originals.
  Das Original ist einseitig mit einer Drahtbrücke; dieser Nachbau ist
  zweilagig. **Die Leiterbahnen sind neu verlegt, nicht abgetastet.**
* **Maße** sind aus dem Plan abgeleitet (kein Maßband im Manual), Toleranz grob
  ±3 %. Vor einer Fertigung gegen eine echte Platine messen. Einzelheiten und
  weitere offene Punkte in [ORIGINAL.md](ORIGINAL.md).

## Prüfstand (Rev0.1, 06.10.2026)

* **ERC:** 0 Verstöße (`psu/TR-808PSU_Rev0.1-erc.rpt`).
* **DRC:** 0 Fehler, 3 Courtyard-Überlappungen (Warnung: die Bauteile sitzen so
  eng wie im Original); 0 unverbundene Verbindungen; Abgleich Schaltplan–Platine 0.
* **Netz gegen Kleinspannung:** kleinster Abstand 6,5 mm (`tools/pcb/netzabstand.py`).
* **Netzliste gegen das Schaltbild:** vom Schaltbild von Hand gelesen und am
  Plot gegengesehen; kein unabhängiger Abgleich, siehe „Offen“ in ORIGINAL.md.
* Bahnbreite 0,25 mm überall (Ströme unter 0,3 A); Masse GND15 als Fläche auf
  beiden Lagen, GND5 als Bahn.
* **Nicht geprüft:** Aufbau und Messung am Gerät, Fertigung.

## Erzeugen

Plan und Layout werden erzeugt, nicht von Hand gezeichnet:

```bash
python3 tools/pcb/fp_tr808.py psu/TR808PSU.pretty
python3 tools/psu/build_psu.py psu
python3 tools/textplace.py psu/TR-808PSU_Rev0.1.kicad_sch
python3 tools/textfix.py psu/TR-808PSU_Rev0.1.kicad_sch
python3 tools/pcb/original_placement.py psu
python3 tools/pcb/make.py psu --passes=45 --rounds=2 --budget=900
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
