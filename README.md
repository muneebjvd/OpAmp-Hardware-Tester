# Operational Amplifier (Op-Amp) Diagnostic Tester

An analog-logic diagnostic tool designed to evaluate the operational status of integrated amplifiers. This project provides a reliable hardware platform to analyze, simulate, and visually indicate whether a given operational amplifier is functioning under normal parameters or experiencing internal component faults.

---

## 🚀 Key System Features
* **Dual-Stage Signal Verification:** Integrates twin LM741 operational amplifiers to scale, process, and condition incoming test signals.
* **Logic-Driven Hazard Analysis:** Employs a NAND logic gate subsystem to gate outputs and detect circuit anomalies.
* **Instant Visual Diagnostics:** Features real-time light-emitting diode (LED) status indicators:
  * **Green LED:** Illuminates when output parameters fall within safe, nominal operating bounds (Functional IC).
  * **Red LED:** Illuminates when output parameters deviate from expected bounds, signaling an internal device fault.
* **No-Equipment Testing Overhead:** Eradicates the requirement for complex diagnostic test equipment like oscilloscopes or multimeters during rapid verification loops.

---

## ⚙️ Technical Specifications & Requirements
* **DC Power Supply Rails:** +12V DC input
* **Operating Frequency Bandwidth:** 1 Hz to 1 MHz
* **Thermal Envelope:** 0°C to 50°C
* **Active Hardware Current Consumption:** 100mA

---

## 🛠️ Bill of Materials (BOM)

| Component Name | Quantity | Hardware Function & Deployment Purpose |
| :--- | :---: | :--- |
| **LM741CM** | 2 | Primary Operational Amplifiers under evaluation. |
| **NAND2 Gate** | 1 | Integrated circuit implementing logic operations. |
| **1 kΩ Resistor** | 4 | Sets target voltage dividers and handles current-limiting. |
| **1.5 kΩ Resistor** | 1 | Component dedicated to setting precise bias voltage steps. |
| **330 Ω Resistor** | 1 | Protects diagnostic status indicators from overcurrent. |
| **Green LED** | 1 | Status indicator for clean, non-faulty operation. |
| **Red LED** | 1 | Status indicator highlighting faulty conditions. |
| **IC Sockets** | — | Added for rapid, solderless component hot-swapping. |

---

## 📐 Circuit Schematic Architecture

The following block configuration represents the electrical trace interconnect routing of the tester system:

```text
               +12V (VCC)
                   │
                   ▼
          ┌────────────────┐
          │  Input Stage   ├─────────┐
          │  LM741CM (U2)  │         │
          └───────┬────────┘         │
                  │                  ▼
                  │ Output      ┌──────────┐      ┌───────────┐
                  ├────────────►│  NAND2   ├─────►│  Red LED  │ (Faulty)
                  │             │ Logic U3 │      │  (LED2)   │
                  ▼             └────▲─────┘      └───────────┘
          ┌────────────────┐         │
          │ Control Stage  ├─────────┘
          │  LM741CM (U1)  │ Output
          └───────┬────────┴─────────────────────►┌───────────┐
                  │                               │ Green LED │ (Normal)
                  ▼                               │  (LED1)   │
             -12V (VDD)                           └───────────┘

🔬 Simulation & Fault Injection Analysis

Circuit validation was conducted within NI Multisim to prove diagnostic reliability across distinct input boundaries:

    Pre-Fault Baseline (Normal State): The target IC processes the differential voltage successfully, lighting the Green LED to signify a healthy operational profile.

    Post-Fault Simulation (Defect Injection): An open-circuit failure is software-injected directly into the Op-Amp pins via the Multisim structural matrix fault panel. The tester correctly isolates the output variance, switches state, and triggers the Red LED warning indicator.
