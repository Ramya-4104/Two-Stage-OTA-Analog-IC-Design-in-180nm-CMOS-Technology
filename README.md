# Two-Stage OTA Design in 180 nm CMOS

A transistor-level design and physical-layout study of a **two-stage, single-ended Miller-compensated Operational Transconductance Amplifier (OTA)** implemented in **180 nm CMOS technology** using **Cadence Virtuoso**. The single-ended design uses a **gm/ID-based methodology** for systematic transistor sizing and bias-point selection, followed by DC, AC, transient, and stability simulations. The design was also extended to a **fully differential OTA with resistive and buffered-resistive common-mode feedback (CMFB)**.

> **Project Status:** Two-stage single-ended OTA design, simulation, and full-custom layout work completed. The design was also extended to a fully differential OTA with resistive and buffered-resistive CMFB circuits.

---

## 1. Project Overview

This project focuses on the design of a **two-stage single-ended OTA** targeting high DC gain, adequate bandwidth, stable closed-loop operation, good common-mode rejection, and useful output swing in a 180 nm CMOS process.

The design was developed at transistor level using **Cadence Virtuoso**, with device dimensions and operating points selected using the **gm/ID methodology** rather than relying only on iterative transistor-width/length tuning.

### Design Flow

The OTA design was developed in the following stages:

1. **Initial fully differential OTA design:** A two-stage fully differential OTA was first designed using the **gm/ID methodology** for systematic transistor sizing and operating-point selection.
2. **CMFB implementation and extension:** The design was then extended using **Buffered Resistive Common-Mode Feedback (CMFB)** and **Resistive CMFB** circuits to establish and control the required common-mode operating point.
3. **Single-ended OTA implementation:** The design was further developed as a **two-stage single-ended OTA** and evaluated through transistor-level simulations and physical-design steps.
4. **Learning/reference:** The design approach and CMFB concepts were developed by following the NPTEL course **“Analog IC Design” by Dr. Nagendra Krishnapura**.


---

## 2. Objective

The main objectives of the design are:

- Design a two-stage single-ended **Miller-compensated CMOS OTA** in a 180 nm technology.
- Obtain high DC/open-loop gain using cascaded gain stages.
- Achieve adequate gain-bandwidth performance and phase margin.
- Maintain stable operation under unity-gain negative feedback.
- Evaluate common-mode rejection and input offset.
- Verify the output voltage range through DC analysis.
- Establish a systematic transistor-sizing methodology using **gm/ID**.
- Implement a full-custom layout using matching-aware techniques and verify the physical design through the DRC/LVS/PEX flow.
- Extend the architecture to a fully differential OTA using resistive and buffered-resistive CMFB.

---

## 3. Motivation

Two-stage OTAs are widely used as building blocks in analog integrated circuits such as operational amplifiers, switched-capacitor circuits, data converters, filters, voltage regulators, and sensor interfaces.

The main design challenge is balancing several conflicting parameters simultaneously:

- DC gain
- Bandwidth / unity-gain frequency
- Phase margin and stability
- Power consumption
- Output swing
- Device area
- Process-dependent transistor behavior

A systematic sizing methodology is therefore preferred over repeatedly changing MOSFET dimensions without a clear design target.

---

## 4. Key Features

- Two-stage single-ended **Miller-compensated CMOS OTA**
- 180 nm CMOS technology and Cadence Virtuoso implementation
- **gm/ID-based transistor sizing methodology**
- Approximately **75 dB DC/low-frequency gain**
- Approximately **35 MHz UGB**
- Approximately **80 dB CMRR**
- **PSRR > 60 dB** at frequencies below 50 kHz
- Approximately **60° phase margin**
- Full-custom layout with **common-centroid and interdigitation** for matching-critical devices
- DRC/LVS/PEX-oriented physical verification flow
- Extended fully differential OTA with **resistive and buffered-resistive CMFB**

---

# 5. Architecture

The OTA is a **two-stage single-ended Miller-compensated architecture** consisting of two cascaded gain stages and a compensation network:

1. **First stage — Differential transconductance stage**
   - Converts the differential input voltage into a current.
   - Provides the primary differential gain.
   - Uses an active load/current-mirror structure.

2. **Second stage — Gain/output stage**
   - Provides additional voltage gain.
   - Drives the output node.
   - Works together with the compensation network to establish the required frequency response.

3. **Frequency compensation**
   - Miller compensation is used to control the dominant pole and improve closed-loop stability.

The transistor-level schematic used for the design is shown below.

## 5.1 Circuit Diagram

Single Ended Two-Stage OTA Schematic 
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/502bfc52-8cb8-456b-be3f-e1c62227dd65" />

Fully Differential Two-Stage OTA Schematic 
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/e7cc8e27-53d3-43ba-9419-56343c96f662" />

Buffered Resistive CMFB Circuit
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/a6e868e0-ee8f-4c99-942e-bc5917ee383a" />

Resistive CMFB Circuit
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/d70dc85b-0fcf-4c18-8416-eeb24739fd9e" />

---

## 5.2 Design Methodology — gm/ID Approach

### Why gm/ID?

The **gm/ID methodology** was used for transistor sizing instead of randomly tuning MOSFET widths and lengths through repeated simulations.

The key quantity is:

$$
\frac{g_m}{I_D}
$$

which relates the transistor's transconductance efficiency to its bias current. For a given technology, gm/ID curves provide a practical way to select the operating region of a MOSFET and then determine suitable device dimensions and bias conditions.

### Design Procedure

The general design flow was:

1. Characterize the 180 nm MOSFETs using **gm/ID curves**.
2. Select a suitable inversion level / gm/ID target based on the required gain, speed and current efficiency.
3. Determine the required bias currents from the target transconductance.
4. Select transistor dimensions corresponding to the selected gm/ID and current density.
5. Establish the bias points and verify the DC operating region.
6. Simulate the complete OTA for DC and AC performance.
7. Adjust the design based on measurable specifications rather than arbitrary device-size changes.

### Why it is more efficient than random transistor-size tuning

Randomly changing MOSFET width and length can require many simulation iterations because **W/L, bias current, gm, output resistance, parasitic capacitance, gain and bandwidth are strongly coupled**.

The gm/ID approach makes the sizing process more systematic because it provides a direct connection between:

- Required transconductance and bias current
- Device inversion level
- Current efficiency
- Expected gain and speed trade-offs
- Transistor dimensions

This reduces trial-and-error iterations and makes the design process easier to reproduce and optimize for a given technology.

### GM/ID Design Plots

The gm/ID characterization plots used for device sizing will be added to the repository here:

NMOS
<img width="1920" height="1080" alt="Screenshot 2026-06-05 165724" src="https://github.com/user-attachments/assets/2383ae97-c881-4bf9-91b5-8f5d8bf05cb9" />

PMOS
<img width="1920" height="1080" alt="Screenshot 2026-06-06 122339" src="https://github.com/user-attachments/assets/e6d8f117-462a-4dc4-9b9c-4bd13d76de89" />


## 5.3 Technology

| Parameter | Value |
|---|---|
| Technology | CMOS 180 nm |
| Design Environment | Cadence Virtuoso |
| Circuit Level | Transistor level |
| OTA Type | Two-stage, single-ended Miller-compensated |
| Supply used in simulation | 1.8 V |
| Compensation | Miller compensation |

---

## 5.4 Specifications / Reported Results

The project description reports the following key performance values for the two-stage single-ended OTA. The detailed Cadence plots provide the corresponding measured values where available.

| Parameter | Reported / Measured Result |
|---|---:|
| Low-frequency loop gain | **76.86 dB** at 2.57 Hz |
| Resume-level DC gain | **75 dB** |
| Unity-gain bandwidth (UGB) | **~35 MHz** |
| CMRR | **~80 dB** (79.936 dB from documented calculation) |
| PSRR | **>60 dB** at frequencies below 50 kHz |
| Phase margin | **~60°** (61.464° measured) |
| Input offset | **0.391 mV** |
| Output DC sweep | Approximately **0 V to 1.743 V** in the shown simulation |

> The low-frequency loop-gain plot shows **76.8574 dB at 2.5704 Hz**. The **75 dB** value used in the project/resume description is therefore a rounded design-performance figure rather than a different design result.

---

# 6. Simulation Results

## 6.1 AC Gain Response and Phase

The AC response shows the OTA output magnitude over frequency. The documented plot reaches approximately **176.773 V/V** at low frequency. The separate loop-gain plot shows **76.8574 dB at 2.5704 Hz**, which is the low-frequency gain figure used for the project-level summary.

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/61224558-49bc-43cf-985a-d81983ea0e97" />

## 6.2 Phase Margin and Unity Gain Frequency

The documented stability measurement gives:

- **Phase Margin:** 61.464° (reported as approximately **60°** in the project description)
- **Unity-gain / phase-margin frequency:** approximately **35 MHz**

Phase Margin
<img width="489" height="590" alt="image" src="https://github.com/user-attachments/assets/9aedc97e-aa84-49fc-91a8-1e6996f801ec" />

Phase Margin Frequency
<img width="483" height="595" alt="image" src="https://github.com/user-attachments/assets/15308d6c-171c-4a03-b55f-906a3ae407cf" />


## 6.3 Common-Mode Response and CMRR

The differential-mode and common-mode responses were used to calculate CMRR as:

$$
CMRR = 20\log_{10}\left(\frac{A_{dm}}{A_{cm}}\right)
$$

The documented values are:

- $A_{dm} = 176.773$
- $A_{cm} = 0.017807$
- **CMRR = 79.936 dB**

Common Mode Gain (Acm)
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/5dfd0998-8790-4ce3-984e-8feab1ae06ed" />

Differential Mode Gain (Adm)
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/fc6bb5e2-e67f-46f3-ba60-e4b3241cbf11" />

---

## 6.4 Input Offset

The reported input offset voltage from the current simulation results is:

**Input Offset = 0.391 mV**

---

## 6.5 Output Voltage Sweep

A DC sweep was performed to observe the output voltage response across the input range.

The shown simulation reaches approximately **1.743 V** at an input value of approximately **1.789 V**.

Output Voltage Sweep
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/f7f45867-be47-42ba-99a9-8cd52bc597f6" />


---

# 7. Layout / Verification

The next stage of the project is physical implementation of the transistor-level OTA.

### Layout / Verification Flow

```text
Schematic
   ↓
Transistor-Level Simulation
   ↓
Layout Design
   ↓
DRC
   ↓
LVS
   ↓
Parasitic Extraction (PEX)
   ↓
Post-Layout Simulation
```

### Layout Considerations

The layout stage will focus on:

- Matching-critical transistor placement
- Symmetric routing where required
- Minimizing parasitic effects on high-impedance nodes
- Appropriate power and ground routing
- Compact and systematic placement of the two gain stages
- Verification of connectivity against the schematic

### Layout Techniques

- **Common-centroid placement** for matching-critical transistor groups
- **Interdigitation** for improved matching of differential-pair and current-mirror devices
- Symmetric and parasitic-aware routing around sensitive analog nodes
- Full-custom layout following **DRC/LVS/PEX** guidelines

### Verification Status

| Verification | Status |
|---|---|
| Schematic design | Completed |
| DC analysis | Completed |
| AC analysis | Completed |
| Gain / phase analysis | Completed |
| CMRR / PSRR analysis | Completed |
| Full-custom layout | Completed |
| DRC/LVS/PEX flow | Completed  |

---
Layout
<img width="917" height="642" alt="Screenshot 2026-07-12 145154" src="https://github.com/user-attachments/assets/2dbfac48-517d-4568-a59a-15a251e6732d" />

# 8. Tools

- **Cadence Virtuoso** — schematic design and analog simulation
- **Spectre** — transistor-level circuit simulation
- **180 nm CMOS PDK** — device models and physical implementation
- **Calibre / equivalent verification flow** — DRC/LVS, where applicable

---

# 9. Author

**K Ramya**  
B.Tech — Electronics and Communication Engineering  
Indian Institute of Technology Guwahati



