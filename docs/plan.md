# Atomic Absorption Spectrometer (AAS) Modernization Project

Modernization and digital conversion framework for legacy **Atomic Absorption Spectrometer (AAS)** analytical instruments. This project replaces obsolete interface hardware (such as legacy SLN Technologies PCI interface cards) with a modern, high-performance **STM32F769** microcontroller platform while preserving proven optical and analog measurement chains.

---

## 📌 Project Overview

Legacy spectroscopy instruments frequently suffer from PC interface obsolescence despite having intact, high-quality optical components and stable high-voltage lamp supplies. This repository houses the schematics, firmware drivers, and hardware specifications required to drive and read the spectrometer's core modular subsystems:

1. **400Hz Modulated Light Source Control:** Precise driving of the hollow cathode / tungsten-halogen lamp supply.
2. **Quad DAC Interface:** Interfacing the **TLC5620C 8-bit DAC** for current setpoint reference control.
3. **High-Precision Photodetector Pipeline:** DMA-based synchronous sampling of PMT/photodiode analog channels.
4. **Wavelength Selection & Drive:** Stepper motor driver timing for precise monochromator grating positioning.

---

## 🏗️ Hardware Architecture & Peripherals

| Subsystem | Legacy Configuration | Modernized Architecture |
| :--- | :--- | :--- |
| **Main Processing Unit** | SLN Technologies PCI Board | **STM32F769 (ARM Cortex-M7)** |
| **Lamp DAC** | TLC5620C 8-bit Quad DAC | Controlled via STM32 GPIO/SPI Interface |
| **Lamp Modulation** | 400 Hz Pulsed Current | Hardware Timer (PWM / Interrupt Trigger) |
| **Analog Sampling** | External PCI ADC | Synchronized Internal High-Speed ADC via DMA |
| **Display & UI** | PC Host Software | Standalone Local LCD / Embedded UI Interface |

---

## 📂 Repository Structure

```text
├── docs/
│   ├── plan.md                 # Detailed project milestones and status tracking
│   ├── circuit_tracing.md      # Pinout logs and legacy backplane trace diagrams
│   └── datasheets/             # Reference technical datasheets (TLC5620C, STM32F769)
├── firmware/
│   ├── Core/                   # STM32 initialization and main loops
│   ├── Drivers/
│   │   ├── tlc5620c.c          # Driver logic for the TLC5620C quad DAC
│   │   ├── lamp_pulse.c        # 400Hz pulse generator and timer logic
│   │   └── stepper_grating.c   # Monochromator stepper motor drive
│   └── Middlewares/            # Signal acquisition and DSP buffers
└── hardware/
    ├── schematics/             # KiCad / Gerber schematics for the interface card
    └── BOM.csv                 # Bill of Materials

