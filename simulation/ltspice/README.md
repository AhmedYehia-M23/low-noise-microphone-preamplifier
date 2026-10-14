# LTspice simulation — earlier OPA165x revision

The saved simulation is `Microphone.asc`. It documents an **earlier OPA165x-based amplifier revision**. The final KiCad PCB uses an **AD8656ARMZ (MSOP-8)** with a power switch and LED indicator. This file and its plots do not simulate that final hardware.

## OPA165x model dependency

This simulation uses Texas Instruments' **OPA165x PSpice Model (Rev. C)**, with subcircuit name:

```text
OPA165x
```

The TI model is intentionally **not redistributed in this repository**. Download it from the official OPA1652 product page:

https://www.ti.com/product/OPA1652

Under **Design & development → Simulation model**, download **OPA165x PSpice Model (Rev. C)** (`SBOMAS4C.ZIP`), then place the extracted `OPA165x.LIB` in this same directory:

```text
simulation/ltspice/
├── Microphone.asc
└── OPA165x.LIB   # locally downloaded from TI; not committed
```

The schematic contains:

```text
.include OPA165x.LIB
```

## Saved analysis configuration

The checked-in schematic is saved for the stepped AC sweep:

```text
.step param Rpot list 1 179 500
.ac dec 100 1 1Meg
.param Rpot=500
```

The transient and operating-point directives are present but commented. Toggle the directives in LTspice as required.

## Useful traces

Amplifier-stage gain:

```text
V(n001,VREF)/V(VBIAS,VREF)
```

Complete microphone-to-output response:

```text
V(AUDIO_OUT)/V(MIC_OUT)
```

## Verified simulation results — earlier model

- `.op`: passes
- transient: passes
- stepped transient: passes
- stepped AC: passes
- Gain settings: approximately 30 / 35 / 40 dB
- At the 30 dB setting, simulated -3 dB bandwidth: approximately 33.9 Hz to 17.8 kHz

**Scope:** These results describe only the original OPA165x-based simulation. They are not AD8656 simulation results or physical measurements. Any AD8656-specific simulation or bench measurements will be documented separately.
