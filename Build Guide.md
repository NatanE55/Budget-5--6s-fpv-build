# Comprehensive Build Guide: Budget 5" 6S Freestyle FPV Quad

## Introduction

This repository documents the complete lifecycle of a budget-friendly, high-performance 5" FPV drone. This build leverages a robust analog video system, ExpressLRS control, and 6S power to deliver a versatile freestyle machine.

This guide provides a logical sequence for assembly, reference documentation, and configuration. It is designed to be used in conjunction with the [README.md](../README.md) and [WIRING](../Wiring) files.

---

## 1. Safety Best Practices

FPV building involves exposed soldering, high-current electricity, and sensitive electronics.

*   **Multimeter Usage:** **Never** plug in a battery for the first time without performing a continuity test. Check for dead shorts between **VBAT (+)** and **GND (-)** on the main ESC pads.
*   **Smoke Stopper:** **Always** use a Smoke Stopper (current limiter) for the first few power-up tests.
*   **Propellers Off:** **Never** have propellers installed when plugging in the battery on the workbench. Propellers should **only** be installed at the flying field.
*   **VTX Antenna:** **Never** power up the Video Transmitter (VTX) without its antenna attached. Running a VTX without an antenna will cause irreversible thermal damage to the component within seconds.

---

## 2. Recommended Build Sequence

For the cleanest final result and easiest troubleshooting, follow this build order:

### Phase 1: Frame Preparation & Mechanical Assembly
![Bare MARK5 Frame & TPU bumpers](../media/photos/Frame%20Top.jpeg)
*   **A. Assemble the MARK5 Frame:** Follow the manufacturer's diagram to assemble the base plate, arms, and mid-plate. Use blue threadlocker (Loctite 242) on metal-to-metal screws.
*   **B. Install Motors:** Mount the 2306 1750KV motors to the arms. Use threadlocker. Ensure the motor wires run smoothly toward the center mid-plate.
*   **C. Route Wires:** Protect motor wires along the arms using heat shrink or TPU guards to prevent "prop strikes."

### Phase 2: ESC & Power Stage
![Capacitor Mounting](../media/Frame%20Bottom.jpeg)
*   **A. Power Leads:** Solder the main XT60 connector leads (Red VBAT+, Black GND-) to the main input pads of the 60A 4-in-1 ESC.
*   **B. Capacitor Installation:** Solder the 35V 1000uF Low-ESR capacitor **directly** across the main VBAT+ and GND- pads of the ESC. The stripe on the capacitor indicates the negative side. This capacitor is essential for suppressing voltage spikes on 6S power.
*   **C. Continuity Check:** Use a multimeter to verify **NO continuity** between VBAT+ and GND-.

### Phase 3: Flight Controller & Stack
![Open Stack View](../media/photos/Open%20front.jpeg)
*   **A. Mount the Stack:** Install the ESC to the frame using rubber standoffs (grommets). Mount the Flight Controller (FC) above the ESC. Ensure the stack orientation matches the arrow on the PCB (usually facing forward).
*   **B. JST Connection:** Connect the multi-pin JST harness between the ESC and the FC. This harness carries motor signals, current sensor data, telemetry, and VBAT power to the FC.

### Phase 4: Solder Components
*   **A. Prep Components:** Tin all components and FC pads beforehand.
*   **B. Solder by Schematics:** Solder the Camera, VTX, and ELRS Receiver according to the Master Wiring Matrix located in `../hardware/WIRING.md`.
    *   *Camera wires:* VBAT, GND, CAM.
    *   *VTX wires:* VBAT, GND, VTX, SmartAudio.
    *   *ELRS RX wires:* 5V, GND, T2, R2.
*   **C. Verify T1 physical Connection:** Ensure the Green VTX SmartAudio wire is physically soldered to the **T1 pad** located near the camera 5V input, as verified in our [corrected physical schematic].

### Phase 5: Pre-Flight Configuration
![Powered FC Check](../media/photos/FC_config.jpeg)
1.  **Test Power:** Connect via USB to ensure the FC powers on. Connect via Smoke Stopper + 6S LiPo to ensure ESC and VTX function.
2.  **Betaflight Setup:**
    *   Enable Serial RX on UART2 (for ELRS).
    *   Set Receiver Protocol to `CRSF`.
    *   Set VTX Peripheral on UART1 to `TBS SmartAudio`.
3.  **Final Assembly:** If all tests pass, mount the camera, VTX, and receiver. Route antennas neatly and secure the frame's top plate.

---

## 3. Maintenance Roadmap

| Interval | Action | Reference |
| :--- | :--- | :--- |
| **Pre-Flight** | Prop nut tightness check | N/A |
| **Post-Crash** | Motor continuity check | Multimeter |
| **Monthly** | Frame screw threadlocker check | `Frame Top.jpeg` |
| **Update** | Betaflight CLI diff dump backup | CLI `diff all` |
