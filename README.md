# Operational Amplifier (Op-Amp) Diagnostic Tester

[cite_start]An analog-logic diagnostic tool designed to evaluate the operational status of integrated amplifiers[cite: 6829, 6951]. [cite_start]This project provides a reliable hardware platform to analyze, simulate, and visually indicate whether a given operational amplifier is functioning under normal parameters or experiencing internal component faults[cite: 6832, 6952].

---

## 🚀 Key System Features
* [cite_start]**Dual-Stage Signal Verification:** Integrates twin LM741 operational amplifiers to scale, process, and condition incoming test signals[cite: 6797, 6829].
* [cite_start]**Logic-Driven Hazard Analysis:** Employs a NAND logic gate subsystem to gate outputs and detect circuit anomalies[cite: 6792, 6829].
* [cite_start]**Instant Visual Diagnostics:** Features real-time light-emitting diode (LED) status indicators[cite: 6796, 6830]:
  * [cite_start]**Green LED:** Illuminates when output parameters fall within safe, nominal operating bounds (Functional IC)[cite: 6952, 6956].
  * [cite_start]**Red LED:** Illuminates when output parameters deviate from expected bounds, signaling an internal device fault[cite: 6952, 6961, 6962].
* [cite_start]**No-Equipment Testing Overhead:** Eradicates the requirement for complex diagnostic test equipment like oscilloscopes or multimeters during rapid verification loops[cite: 6963].

---

## ⚙️ Technical Specifications & Requirements
* [cite_start]**DC Power Supply Rails:** +12V DC input[cite: 6789].
* [cite_start]**Operating Frequency Bandwidth:** 1 Hz to 1 MHz[cite: 6790].
* [cite_start]**Thermal Envelope:** 0°C to 50°C[cite: 6790].
* [cite_start]**Active Hardware Current Consumption:** 100mA[cite: 6790].

---

## 🛠️ Bill of Materials (BOM)

| Component Name | Quantity | Hardware Function & Deployment Purpose |
| :--- | :---: | :--- |
| **LM741CM** | 2 | [cite_start]Primary Operational Amplifiers under evaluation[cite: 6797, 6802]. |
| **NAND2 Gate** | 1 | [cite_start]Integrated circuit implementing logic operations[cite: 6792]. |
| **1 kΩ Resistor** | 4 | [cite_start]Sets target voltage dividers and handles current-limiting[cite: 6793, 6801]. |
| **1.5 kΩ Resistor** | 1 | [cite_start]Component dedicated to setting precise bias voltage steps[cite: 6794]. |
| **330 Ω Resistor** | 1 | [cite_start]Protects diagnostic status indicators from overcurrent[cite: 6795, 6801]. |
| **Green LED** | 1 | [cite_start]Status indicator for clean, non-faulty operation[cite: 6796, 6952]. |
| **Red LED** | 1 | [cite_start]Status indicator highlighting faulty conditions[cite: 6796, 6952]. |
| **IC Sockets** | — | [cite_start]Added for rapid, solderless component hot-swapping[cite: 6798, 6931]. |

---

## 📐 Circuit Schematic Architecture

The following block configuration represents the electrical trace interconnect routing of the tester system:

```text
               +12V (VCC) [cite: 6804]
                   │
                   ▼
          ┌────────────────┐
          │  Input Stage   ├─────────┐
          │  LM741CM (U2)  │         │
          └───────┬────────┘         │
                  │                  ▼
                  │ Output      ┌──────────┐      ┌───────────┐
                  ├────────────►│  NAND2   ├─────►│  Red LED  │ (Faulty) [cite: 6962]
                  │             │ Logic U3 │      │  (LED2)   │
                  ▼             └────▲─────┘      └───────────┘
          ┌────────────────┐         │
          │ Control Stage  ├─────────┘
          │  LM741CM (U1)  │ Output
          └───────┬────────┴─────────────────────►┌───────────┐
                  │                               │ Green LED │ (Normal) [cite: 6956]
                  ▼                               │  (LED1)   │
             -12V (VDD) [cite: 6815]              └───────────┘
🔬 Simulation & Fault Injection AnalysisCircuit validation was conducted within NI Multisim to prove diagnostic reliability across distinct input boundaries:  Pre-Fault Baseline (Normal State): The target IC processes the differential voltage successfully, lighting the Green LED to signify a healthy operational profile.  Post-Fault Simulation (Defect Injection): An open-circuit failure is software-injected directly into the Op-Amp pins via the Multisim structural matrix fault panel. The tester correctly isolates the output variance, switches state, and triggers the Red LED warning indicator.  
