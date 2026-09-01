# Noise analysis notes

The project uses a low-noise audio op-amp, but the complete preamplifier has **not yet been characterized for total input-referred or output noise**. This note separates the device-level noise specification from a system-level noise claim.

## OPA1652 noise specification

Texas Instruments specifies the OPA1652 typical input-voltage noise density as:

- **4.5 nV/√Hz at 1 kHz**
- **3.8 nV/√Hz at 10 kHz**
- **4.0 µVpp from 20 Hz to 20 kHz**

Source: TI OPA165x datasheet (SBOS477B).

The FET-input architecture also provides very low input-current noise, which is useful for the relatively high impedance around the microphone input.

## Resistor thermal-noise context

At approximately 25 °C, the Johnson-noise density of a resistor is:

$$
e_n = \sqrt{4 k T R}
$$

For several resistors used in the signal path, the individual thermal-noise densities are approximately:

| Component / value | Thermal-noise density |
| --- | ---: |
| R4 = 47 kΩ | 27.8 nV/√Hz |
| R5 = 22 kΩ | 19.0 nV/√Hz |
| R3 = 2.2 kΩ | 6.0 nV/√Hz |
| R6 = 220 Ω | 1.9 nV/√Hz |
| R7 = 330 Ω | 2.3 nV/√Hz |

These values are **individual resistor noise densities only**. They cannot simply be added directly to obtain total preamplifier noise because each source is shaped by a different transfer function and impedance.

## Important system noise sources

A complete noise budget must include at least:

- electret capsule and its internal JFET
- microphone-bias resistor and source impedance
- R4 input-bias resistor
- OPA1652 voltage and current noise
- gain-setting feedback network
- VREF generation and buffer noise
- power-supply noise and coupling
- PCB leakage, grounding and external interference

The electret capsule itself can dominate the practical noise floor, so op-amp noise alone is not sufficient to describe system performance.

## Current claim boundary

The term **low-noise** in this project currently refers to the design intent and the use of a low-noise audio op-amp. It does **not** mean that a complete system noise figure has already been measured.

The published validated results currently cover gain, frequency response and transient operation in simulation. Hardware noise characterization remains pending.

## Planned characterization

After assembly, the useful measurements are:

1. Short or terminate the input in a controlled configuration.
2. Measure output RMS noise over a defined audio bandwidth.
3. Repeat at the approximately 30 dB, 35 dB and 40 dB gain settings.
4. Refer the measured output noise back to the input using the measured gain.
5. Measure the microphone-connected noise separately from the amplifier-only condition.
6. Compare measured results with an analytical or SPICE noise budget where the device models support meaningful noise data.

Any future noise number should always state the **bandwidth, gain setting, input condition and measurement method**.
