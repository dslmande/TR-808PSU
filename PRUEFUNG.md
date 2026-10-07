# Prüfung gegen Normen und Abnahmekriterien (Rev0.2, Stand 07.10.2026)

**Einordnung:** Das Original stammt von 1984–86 (Service Manual, 3. Auflage Juni 1986; Netzteilplatine PS3116) und wurde
nie gegen heutige Sicherheitsnormen geprüft. Dieser Nachbau ist eine **1:1-Kopie eines historischen Entwurfs**. Die
Normwerte unten dienen der Orientierung, wo der alte Entwurf von heutigen Anforderungen abweicht. Sie sind keine
Abnahmekriterien für die Kopie und kein Anspruch auf Konformität.

Vorgehen nach dem Skill `regelwerk-auf-projekte-anwenden`: erst Normstand recherchieren, dann am
echten Bestand festmachen, Verifizierung (erfüllt es die Vorgabe?) von Validierung (taugt es für den
Zweck?) trennen. **Keine Zertifizierung, kein Konformitätsnachweis:** Die Platine ist ein privater Nachbau
einer Reparaturplatine; die Normtexte sind kostenpflichtig und liegen mir nicht vor.

## Normrahmen (recherchiert)

| Gegenstand | Norm | Stand | Quelle |
|---|---|---|---|
| Sicherheit Audio-/IT-Geräte (löst DIN EN 60065 ab) | DIN EN IEC 62368-1 (VDE 0868-1) | Ausgabe 2024 + A11:2024, VDE 0868-1:2025-01 | [DIN EN IEC 62368-1:2024](https://ib-lenhardt.com/standards/din-en-iec-62368-1-2024-a11-2024), [testxchange](https://www.testxchange.com/pruefnorm/iecen-62368-1/) |
| Luft-/Kriechstrecken, Isolationskoordination | IEC 60664-1 / DIN EN 60664-1 (VDE 0110-1) | Tabellenwerte nicht frei verfügbar; Quellen widersprechen sich (Kriechstrecke 250 V, Verschmutzungsgrad 2, Materialgruppe III: 3,2 bis 4 mm Basis) | [Elektor Teil 1](https://elektormagazine.com/news/pcb-clearance-and-creepage-distances-1), [TI SLUP419](https://www.ti.com/lit/pdf/slup419) |
| Feinsicherungen | DIN EN 60127 (T250mA/250V) | nicht geprüft |  |
| Funkentstörkondensator C1 | DIN EN 60384-14 (X2) | Typ laut Manual ECQ-U2A473MF, nicht geprüft |  |
| Leiterplatten | IPC-2221 / IPC-A-600 | nicht angewandt |  |

Für ein privat gebautes Teil für das eigene Gerät gilt keine Pflicht zur CE-Kennzeichnung; wer es
weitergibt oder verkauft, braucht sie. Das ist keine Rechtsberatung.

## Verifizierung (gemessen)

| Kriterium | Ergebnis |
|---|---|
| ERC | 0 Verstöße |
| DRC (Regel 0,25 mm) | 0 Fehler, 0 offene Verbindungen, 0 Abweichungen Schaltplan/Platine |
| Netz gegen Kleinspannung (Kupfer-Kupfer) | **über 8 mm** (alle Netzleiter-Netze gegen 5-V- und ±15-V-Netze) |
| Netz primär gegeneinander (SW_A gegen SW_B) | Rev0.2: **5,67 mm** (Bahn gegen Bahn); Rev0.1 hatte 3,75 mm |
| Netz primär, Anschluss 8 gegen Anschluss 9 | 6,87 mm |
| Fertigung | Gerber, Bohr- und Positionsdaten, 1:1-Ausdruck vorhanden |

Die Abstandsmessung läuft mit einer temporären Netzklasse von 8 mm (DRC meldet jede Unterschreitung).
In Rev0.1 lagen die beiden geschalteten Netzleiter 3,75 mm auseinander, also über 2 mm (Luftstrecke Basisisolierung
in den Suchtreffern), aber **unter 4 mm**, dem konservativsten gefundenen Wert für die Kriechstrecke
(Materialgruppe III, Verschmutzungsgrad 2, 250 V). In Rev0.2 sind es mindestens 5,67 mm; Netz gegen Kleinspannung liegt
unverändert über 8 mm.

## Validierung (noch nicht gemacht)

Diese Punkte lassen sich nur am Gerät klären; kein Gate gilt als passiert, solange sie offen sind:

1. **Maßstab:** Der Bestückungsplan hat kein Maßband (0,544 mm je pt, ±3 %). Gegen eine echte Platine
   nachmessen (Löcher des Kühlkörpers, Sicherungsclips, Abstand der Anschlüsse).
2. **Unter Last:** +5 V, ±15 V und die RAM-Versorgung am aufgebauten Netzteil messen (Sollwerte im Manual:
   10 V DC aus gelb-gelb, 23 V je Hälfte aus rot-schwarz bei 0,15 A DC).
3. **Netzteil im Gerät:** Passt die Platine in das TR-808-Gehäuse, sitzt der Kühlwinkel 246-101A, passen die
   Steckfahnen zur Verkabelung (Foto des echten Bauteils liegt vor).
4. **Isolation:** Wenn das Netzteil weitergegeben wird, Hochspannungsprüfung durch eine Fachperson.

## Befunde und Nichtkonformitäten

| Nr. | Befund | Schwere | Stand |
|---|---|---|---|
| 1 | Rev0.1: SW_A/SW_B 3,75 mm; heutiger konservativer Wert 4 mm (Abweichung des historischen Entwurfs von der heutigen Norm) | mittel | in Rev0.2 behoben (5,67 mm) |
| 2 | Brücken W04 statt W-02 laut Manual (Typ auf der echten Platine 2W04G) | niedrig | bewusst, in ORIGINAL.md und im Plan vermerkt |
| 3 | Bahnen folgen dem Original-Kupfer nur zu 36 %; zweilagig statt einseitig | niedrig | dokumentiert |
| 4 | Netzliste von Hand aus dem Schaltbild gelesen, 4 Kupferstücke mit zwei Netzen im Scan-Abgleich | mittel | offen |
| 5 | 3D-Modelle für Sicherungshalter und Anschlussfahnen selbst gebaut, Maße geschätzt | niedrig | dokumentiert |
| 6 | DRC-Warnungen: 4 Courtyards, 1 Siebdruck, 7 Footprint-Abweichungen (Elko-Balken) | niedrig | bewusst |

## Risiken (Bauteile)

- **TA7179P** (Toshiba) und **2SB596/2SD880**: bei Nachbauten alter Geräte Regel, dass Schlüsselbauteile abgekündigt
  sind; Graumarkt bedeutet Fälschungen. Vor der ersten Bestellung `BAUTEILE-PRUEFUNG.md` anlegen
  (Lagerbestand und Lebenszyklus per Mouser/TME-API prüfen), Ersatztypen für IC2 festlegen.
- **1S2473** (Si-Diode), **µA7805**: unkritisch, aber ebenfalls prüfen.
- Datenblätter für 2SB596 (MOSPEC) und 2SD880 (DC Components) wurden für die Pinbelegung gelesen, liegen aber
  nicht im Repo (Urheberrecht).

## Versionen

**Rev0.1** ist die historische 1:1-Kopie (Release `Rev0.1`). **Rev0.2** ändert nur die Netzseite: SW_B ist von SW_A und vom Pad F1.1 weiter weggezogen (SW_A/SW_B mindestens 5,67 mm). Jede Layoutänderung ist ein neuer Versionsstand: Dateien umbenannt, Version auf dem Bestückungsdruck, eigenes Release.

## Nächster Schritt (Gate vor der Fertigung)

Muster fertigen lassen, Maße gegen die echte Platine abgleichen (Validierung 1) und erst danach größere Stückzahlen.
Ein Gate wird nicht „vorläufig" passiert. Wer die Platine weitergibt oder verkauft, trägt für Sicherheit und CE selbst
die Verantwortung.
