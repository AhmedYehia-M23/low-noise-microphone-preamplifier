# Low-Noise Electret Microphone Preamplifier — Assembly BOM

This component list is derived from the final [KiCad schematic](kicad/Microphone.kicad_sch) and [PCB](kicad/Microphone.kicad_pcb) sources. It covers **one populated board** and lists design values and footprints, **not** confirmed part selections or purchased components. The machine-readable version is [BOM.csv](BOM.csv).

**22 populated parts across 17 grouped BOM lines**, plus **5 integrated test-point pads** that require no separate component. The KiCad PCB has **27 footprints in total**.

## Populated components

| Reference(s) | Qty | Value / specification | KiCad footprint | Function |
| --- | ---: | --- | --- | --- |
| R1 · R2 | 2 | 10 kΩ | `Resistor_SMD:R_0603_1608Metric_Pad0.98x0.95mm_HandSolder` | Mid-supply divider |
| R3 · R9 | 2 | 2.2 kΩ | `Resistor_SMD:R_0603_1608Metric_Pad0.98x0.95mm_HandSolder` | Microphone bias and LED limiting |
| R4 | 1 | 47 kΩ | `Resistor_SMD:R_0603_1608Metric_Pad0.98x0.95mm_HandSolder` | Amplifier input bias |
| R5 | 1 | 22 kΩ | `Resistor_SMD:R_0603_1608Metric_Pad0.98x0.95mm_HandSolder` | Gain feedback |
| R6 | 1 | 220 Ω | `Resistor_SMD:R_0603_1608Metric_Pad0.98x0.95mm_HandSolder` | Gain-setting resistor |
| R7 | 1 | 330 Ω | `Resistor_SMD:R_0603_1608Metric_Pad0.98x0.95mm_HandSolder` | Low-pass series resistor |
| R8 | 1 | 100 kΩ | `Resistor_SMD:R_0603_1608Metric_Pad0.98x0.95mm_HandSolder` | Output reference / load resistor |
| C1 · C4 | 2 | 100 nF | `Capacitor_SMD:C_0603_1608Metric_Pad1.08x0.95mm_HandSolder` | Supply bypass and microphone AC coupling |
| C2 · C3 | 2 | 10 µF | `Capacitor_SMD:CP_Elec_5x5.4` | Supply bulk and VREF_RAW filtering |
| C5 | 1 | 27 nF | `Capacitor_SMD:C_0603_1608Metric_Pad1.08x0.95mm_HandSolder` | Low-pass shunt capacitor |
| C6 | 1 | 4.7 µF | `Capacitor_SMD:CP_Elec_4x5.8` | AC-coupled output capacitor |
| D1 | 1 | LED | `LED_SMD:LED_1206_3216Metric` | Power-on indicator |
| J1 · J2 | 2 | 2-position terminal block; 5.08 mm pitch | `TerminalBlock_Phoenix:TerminalBlock_Phoenix_MKDS-1,5-2-5.08_1x02_P5.08mm_Horizontal` | 5 V power input and audio output |
| MK1 | 1 | EMY-6027P/N-R-42 electret microphone | `AudioPreamp:Microphone_EKULIT_EMY-6027PNR-42` | Electret capsule |
| RV1 | 1 | 500 Ω | `Potentiometer_THT:Potentiometer_Piher_PT-10-H01_Horizontal` | Variable gain control |
| SW1 | 1 | SPDT slide switch | `AudioPreamp:SW_ESP1010_SPDT_Vertical` | 5 V power switch |
| U1 | 1 | AD8656ARMZ; dual operational amplifier | `Package_SO:MSOP-8_3x3mm_P0.65mm` | Main gain stage and VREF buffer |
| **Total** | **22** | | | |

The CSV includes the complete KiCad footprint names and individual assembly/fit notes. **U1 is one physical dual-op-amp IC**, although the schematic represents its amplifiers and power pins as separate symbol units.

## Integrated PCB test points — no additional parts

| Reference | Signal | PCB feature |
| --- | --- | --- |
| TP1 | VREF | 2.0 mm through-hole pad; 1.0 mm drill |
| TP2 | AMP_OUT | 2.0 mm through-hole pad; 1.0 mm drill |
| TP3 | LPF_OUT | 2.0 mm through-hole pad; 1.0 mm drill |
| TP4 | AUDIO_OUT | 2.0 mm through-hole pad; 1.0 mm drill |
| TP5 | GND | 2.0 mm through-hole pad; 1.0 mm drill |

The TP footprints are copper pads usable with probes or optional pins; no test-point pins are part of the required BOM.

## Assembly checks before selecting individual parts

- **C2, C3, C6:** Polarized electrolytic capacitors; verify polarity, lead/pad geometry, can dimensions and voltage ratings. The schematic specifies capacitance but **not** voltage rating or tolerance.
- **RV1:** **500 Ω**, not 500 kΩ. The PCB uses a horizontal PT-10-H01 footprint; verify physical fit, pinout and adjustment access for the chosen component.
- **SW1:** Three-pin vertical SPDT; the third terminal is intentionally not connected. Confirm the selected switch matches the custom footprint and that the on/off direction is correct.
- **MK1:** Match the specified electret capsule and verify its polarity against the custom footprint before soldering.
- **D1:** 1206 power-indicator LED; green was intended, but the KiCad symbol value is simply `LED`. Check polarity and physical dimensions.
- **J1/J2:** Two horizontal 2-pin through-hole terminal blocks at **5.08 mm pitch**; verify exact terminal geometry.
- **U1:** One AD8656 dual amplifier in **MSOP-8, 0.65 mm pitch**. Confirm the pin-1 indicator and 5 V operating conditions.
- **R1–R9 / C1, C4, C5:** Hand-solderable 0603 footprints. Tolerances, power ratings, dielectric classes and manufacturer part numbers are **not specified** by this BOM; choose and verify them for the actual assembly.
- **Input power:** The board expects a **regulated 5 V DC supply**. The supply itself, probes, cables, solder and other tools are external to this PCB component BOM.

**Status:** The electrical values and reference-to-footprint mapping match the current KiCad schematic and PCB files. Exact selectable components, mechanical fit and assembly have not been independently verified. No bench-test results are implied.
