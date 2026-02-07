# FPGA-Based Metal Detector

**Junior Lab Design Project – Team 25**  
**Members:** Eugene Fung, Nicky Xiao, Khoa Vo, Hari Senthil Kumar

---

## Overview
This project implements a **metal detection and localization system** using induction coils and FPGA-based digital signal processing. Changes in inductance caused by nearby metal objects alter the oscillation characteristics of coil-based oscillators. These changes are measured, processed, and displayed in real time using LEDs and seven-segment displays.

The system detects both the **presence** and **approximate position** of a metal object (left, center, or right) by estimating pulse-width (duty cycle) variations from multiple sensing coils.

---

## System Architecture

### 1. Sensing Stage
- Custom-wound inductors act as metal sensing coils  
- Each coil is part of a **Colpitts oscillator**  
- Nearby metal changes inductance, altering oscillator frequency and duty cycle  

### 2. Analog Processing
- Oscillator outputs are fed into **comparators**  
- Comparators convert analog oscillations into clean digital signals for FPGA input  

### 3. Digital Processing (FPGA)
- **Duty cycle estimation** logic measures pulse width of incoming signals  
- A **strength meter** quantifies deviation from baseline (no-metal state)  
- **Detection FSM** determines:
  - No metal (idle)
  - Metal near left coil
  - Metal near right coil
  - Metal near center

### 4. Output Interface
- **LED bar** displays detection strength (2–4 LEDs active)
- **Seven-segment display** shows detected position:
  - `L` – Left
  - `C` – Center
  - `r` – Right
  - Blank – No detection

---

## Detection Logic

| Test Condition | Detected Output | LED Pattern | Notes |
|---------------|----------------|-------------|-------|
| No metal | None | No LEDs | Baseline (idle state) |
| Metal near right coil | L | 2–4 LEDs | Left-side detection |
| Metal near left coil | r | 2–4 LEDs | Right-side detection |
| Metal in the middle | C | 2–4 LEDs | Center detection |

Detection is based on **relative duty cycle changes** between coils rather than absolute frequency, improving robustness against noise and component tolerances.

---

## Key Features
- Real-time metal detection  
- Position estimation (left / center / right)  
- FPGA-based duty cycle measurement  
- Stable baseline and noise-tolerant detection  
- Clear visual feedback via LEDs and seven-segment display  

---

## Results
- Successfully detects metal objects placed near individual coils  
- Correctly identifies object position  
- Provides stable and repeatable output  
- Demonstrates effective integration of analog sensing with digital FPGA logic  

---

## Tools & Technologies
- FPGA (Junior Lab platform)
- VHDL for digital logic and FSM design
- Custom analog front-end (oscillators + comparators)
- Seven-segment display and LED outputs

---

## Future Improvements
- Calibrated strength scaling for distance estimation  
- Digital filtering for improved noise immunity  
- USB/UART output for PC-based visualization  
- Adaptive thresholding based on environment  

---

## References
- Colpitts Oscillator Design Theory  
- Inductive Metal Detection Principles  
- FPGA-Based Digital Signal Measurement Techniques  

---

## Acknowledgments
This project was completed as part of the **Junior Lab Design Course**, demonstrating practical sensing, mixed-signal design, and FPGA-based embedded systems integration.
