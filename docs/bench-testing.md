# Hardware bench-testing log

**Project:** Low-Noise Electret Microphone Preamplifier  
**Op-amp:** Analog Devices AD8656ARMZ  
**PCB:** Two-layer, approximately 60 × 40 mm  
**Last updated:** 18 November 2026  
**Current state:** Initial DC bring-up recorded; audio performance not yet validated.

This log records observations from the builder's hardware-testing conversation. Values are digital-multimeter observations, not calibrated laboratory results, and may have been taken at different points in the troubleshooting process.

## Build chronology

| Date | Milestone |
| --- | --- |
| 14 October 2026 | Bare PCB order placed |
| 24 October 2026 | Manufactured PCBs received |
| 12 November 2026 | Hand assembly completed; initial electrical checks performed |
| 18 November 2026 | First hardware status and measurement log added to repository |

## 12 November 2026 — initial DC bring-up

The PCB was assembled and powered. Initial readings were:

| Check or node | Reading / observation | Status or limitation |
| --- | --- | --- |
| Nominal 5 V power rail | **5.20 V** | Supply present; not a load-regulation measurement |
| Buffered mid-supply reference (`VREF`) | **2.60 V** | Approximately half of the observed 5.20 V rail |
| AD8656 pin 8 | **5.20 V** | Positive supply voltage |
| AD8656 pin 1 | **2.60 V** | DC output bias near VREF |
| AD8656 pin 7 | **2.60 V** | DC output bias near VREF |
| AD8656 pin 5 | **2.60 V** | DC bias near VREF |
| Electret microphone positive terminal | **approximately 4.60 V** | Does not by itself demonstrate microphone operation |
| R3 resistor check | **approximately 2 kΩ** | Approximate DMM check, not a precision resistor measurement |
| Power-indicator LED | **Not illuminated** | Unresolved; no root cause confirmed |

The user additionally observed a steady reading around **4.8 V** during testing, but the measurement point and conditions are not sufficiently documented to treat it as a separate characterized supply result.

### Interpretation

- The observations show that DC power reaches the board and the mid-supply reference is present.
- Selected AD8656 nodes were near the reference voltage; this is consistent with the intended single-supply bias scheme, **but does not prove that the amplifier passes or amplifies audio**.
- There is no validated physical measurement of the 30 / 35 / 40 dB gain settings, frequency-response cutoffs, distortion, output noise or power-supply current.
- The power-indicator LED failed to illuminate during initial checks. Neither its polarity nor a specific failure mechanism has yet been confirmed.
- The power switch has not been conclusively verified under its intended operating conditions.

## Functional audio test — prepared, not completed

Available equipment for the next check:

- Bluetooth speaker with a **3.5 mm AUX input**
- Male-to-male 3.5 mm audio cable
- USB-C-to-female-AUX adapter

The discussion stopped **before connecting** the AUX lead to the PCB output.

Planned mono-output wiring between the PCB's `J2` terminal and a 3.5 mm plug (verify the terminal labeling and cable contact continuity before connection):

| PCB terminal | Plug contact |
| --- | --- |
| `AUDIO_OUT` | Tip (left-channel audio contact) |
| `GND` | Sleeve (ground) |
| No PCB connection | Ring (right channel) |

This connects to the speaker's **AUX input**, never to an amplified speaker output. A successful listening test would be a functional indication, not a calibrated gain/noise result.

## Open issues

1. **Power LED:** Not illuminated at initial power-up. Check placement/polarity, resistor and solder connections, and voltage across the LED before identifying a cause.
2. **Power switch:** Verify whether it switches the 5 V rail as intended.
3. **Audio path:** No completed listening test or instrumented amplifier transfer measurement.
4. **Instrumented validation:** No confirmed oscilloscope or calibrated audio-analyzer results yet.

## Remaining hardware validation checklist

- [x] Fabricate and receive the PCB
- [x] Hand-solder the PCB
- [x] Verify that supply voltage is present
- [x] Record VREF and selected AD8656 DC node voltages
- [ ] Verify switch operation
- [ ] Diagnose and repair LED function
- [ ] Connect the output to the speaker's AUX input and verify audio
- [ ] Drive the input with a known low-level 1 kHz signal and measure voltage gain
- [ ] Check the three intended gain settings (~30 / 35 / 40 dB)
- [ ] Sweep frequency and measure the actual -3 dB cutoff points
- [ ] Measure output swing, clipping behavior and supply current
- [ ] Measure output-noise RMS over a stated bandwidth
- [ ] Document test setup, conditions, measurement uncertainty and resulting waveforms
- [ ] Add actual PCB and bench-setup photographs when available

## Simulation versus hardware

The project's **29.5233 dB** simulated 1 kHz full-path gain, approximately **30.8 Hz–19.7 kHz** simulated cutoff frequencies at the 30 dB setting, and **31.88 µV RMS** simulated 20 Hz–20 kHz output noise are LTspice results only. They must **not** be represented as measured performance of the assembled board.

See [the README](../README.md) for circuit details, full simulation context and figures, and [noise-analysis.md](noise-analysis.md) for the measurement approach.

*Images intentionally omitted from this initial log; they will be added separately.*
