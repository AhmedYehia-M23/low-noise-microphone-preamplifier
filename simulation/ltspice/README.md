# LTspice simulations

The project includes two separate simulation schematics. Only the final KiCad sources represent the production PCB.

## AD8656 schematic

[Microphone_Preamplifier_AD8656.asc](Microphone_Preamplifier_AD8656.asc) models the microphone preamplifier signal path with `AD8656` values assigned to both op-amp symbols. It includes the directive:

```text
.include ad8656.cir
```

To run it, place an appropriate AD8656 SPICE macro-model named `ad8656.cir` in the same directory. The vendor model is not redistributed here.

**Validation:** The supplied schematic has been preserved as provided, but the accompanying model was not supplied for independent verification. The model's `.SUBCKT` name, pin mapping and simulation results must be checked before claiming AD8656-validated performance.

The currently enabled analysis is `.tran 0 3m 0 50n` with `Rpot=1`. The stepped and AC analysis directives are commented out. The schematic includes some AC measurement commands; run an AC analysis before interpreting those measurements. The on-board power switch and LED are omitted from this analog signal-path model.

## Earlier OPA165x schematic

[Microphone_Preamplifier_OPA165x.asc](Microphone_Preamplifier_OPA165x.asc) preserves the previous simulation, which uses Texas Instruments' **OPA165x PSpice Model (Rev. C)** with subcircuit name `OPA165x`. It is retained for traceability and comparison, **not** as validation of the final AD8656 PCB.

The original vendor model is not included. Download the OPA165x PSpice model from:

https://www.ti.com/product/OPA1652

Extract `OPA165x.LIB` to the same folder as the earlier schematic. It contains:

```text
.include OPA165x.LIB
```

The original AC sweep was configured with:

```text
.step param Rpot list 1 179 500
.ac dec 100 1 1Meg
.param Rpot=500
```

Historical results from that model:

- Operating-point analysis: passed
- Transient analysis: passed
- Stepped transient analysis: passed
- Stepped AC analysis: passed
- Gain settings: approximately 30 / 35 / 40 dB
- Simulated −3 dB bandwidth at the 30 dB setting: approximately 33.9 Hz to 17.8 kHz

These values are **not** measurements of assembled hardware or results from an AD8656 simulation.
