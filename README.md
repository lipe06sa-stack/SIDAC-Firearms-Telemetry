# Project SIDAC: Intelligent Diagnostic & Telemetry System for Handgun Failure Detection

**Conceptual Design Document & Proof of Concept**

**Author:** Filipe José Martins de Sá, Mechanical Engineer

**Status:** R&D Portfolio Concept

## 1. Problem Statement
Modern striker-fired handgun platforms, such as the Glock G22 Gen 5, are highly reliable but not immune to mechanical degradation. Subtle failures—including recoil spring fatigue, striker channel fouling, and sear surface wear—often manifest as minute changes in the firearm's kinematic signature before a catastrophic malfunction (e.g., failure to feed, failure to return to battery) occurs. Currently, there is no embedded, real-time diagnostic tool for operators or armorers to predict these failure modes purely from the weapon's dynamic response during the firing cycle.

## 2. The Solution: SIDAC
SIDAC is a conceptual Picatinny-rail-mounted telemetry unit that leverages a low-cost, high-fidelity Inertial Measurement Unit (IMU) and a microcontroller to perform edge-computing diagnostics. The system captures the complete high-G recoil impulse and slide velocity profile to algorithmically distinguish a "healthy" baseline from anomalous mechanical behavior. This transforms the handgun into an IoT-enabled diagnostic platform, providing predictive maintenance data without altering the firearm's internal mechanics.

## 3. System Architecture
- **Sensing Layer:** MPU6050 (6-axis IMU: 3-axis accelerometer ±16g, 3-axis gyroscope) for high-frequency motion capture.
- **Processing Layer:** ESP32 microcontroller for I2C data acquisition, digital signal processing, and Bluetooth Low Energy (BLE) telemetry broadcast.
- **Power:** 3.7V 300mAh LiPo battery with onboard charging management.
- **Enclosure:** Topology-optimized 3D-printed polymer housing, mechanically isolated from the Picatinny rail.

## 4. R&D Roadmap
1.  **Phase I: Theoretical Validation (Current)**
    - Development of a 1-DOF recoil kinematics mathematical model.
    - Python simulation of normal vs. anomalous recoil impulse signatures.
2.  **Phase II: Static Hardware-in-the-Loop**
    - Benchtop I2C validation and noise floor characterization of the ESP32/MPU6050 stack.
    - Implementation of Madgwick/Mahony sensor fusion for absolute orientation tracking.
3.  **Phase III: Dynamic Live-Fire Proof-of-Concept**
    - Shock survivability testing of the cantilevered PCB enclosure.
    - Dataset collection of live-fire cycles to train anomaly detection thresholds.
    - BLE telemetry streaming to a companion mobile application for real-time visualization.
  
graph TD
    %% Initialization
    START((System Boot)) --> INIT[Initialize MPU6050: <br>±16g Range, 1kHz Sample Rate]
    INIT --> I2C_READ[Read Raw I2C Data Buffer: <br>Ax, Ay, Az, Gx, Gy, Gz]
    
    %% Signal Processing Stage
    subgraph DSP [Digital Signal Processing]
        I2C_READ --> FILTER[Low-Pass Butterworth Filter <br>fc = 200Hz: Remove high-freq handling noise]
        FILTER --> MAG[Compute Resultant Acceleration Magnitude: <br>|A| = sqrt(Ax^2 + Ay^2 + Az^2)]
        MAG --> THRESH{Static Threshold Detection: <br>|A| > 5g?}
    end

    %% Detection & Pattern Matching
    THRESH -- No --> IDLE[Idle Mode / Log Background Noise]
    THRESH -- Yes (Recoil Event Detected) --> PEAK_DETECT[Peak Detection Algorithm: <br>Find Max |A| and Time to Peak]
    
    subgraph Diagnostic_Pattern [Pattern Matching Engine]
        PEAK_DETECT --> EXTRACT[Extract Feature Vector: <br>1. Peak G-Force <br>2. Impulse Duration (ms) <br>3. Damping Ratio]
        EXTRACT --> COMPARE{Anomaly Detection: <br>Compare Feature Vector <br>against Baseline Profile}
        
        COMPARE -->|Peak < 700g & Duration > 25ms| FAIL_SPRING[Classification: <br>Recoil Spring Fatigue]
        COMPARE -->|Irregular Damping & High Std Dev| FAIL_FRICTION[Classification: <br>Slide Rail Friction / Fouling]
        COMPARE -->|Within Normal Tolerances| NORMAL[Classification: <br>Normal Firing Cycle]
    end

    %% Telemetry Output
    NORMAL --> PACKET[Format BLE Data Packet: <br>Type: Normal, Stats: JSON]
    FAIL_SPRING --> PACKET
    FAIL_FRICTION --> PACKET
    
    PACKET --> TX[Transmit Telemetry via BLE <br>to Mobile / Armorer Dashboard]
    TX --> I2C_READ
  

Designing a rail-mounted diagnostic unit requires careful consideration of parasitic mass and shock propagation to avoid inducing malfunctions.

1. Mass Budget & Center of Gravity (CG)

Constraint: The complete SIDAC unit (enclosure + PCB + battery) must not exceed 120 grams. Exceeding this limit, particularly on the front of a polymer-frame pistol, significantly alters the moment of inertia, impeding the muzzle's natural return from recoil and potentially causing "muzzle dip."

CG Position: The CG of the SIDAC module must be located directly over the Picatinny clamp's transverse slot. A forward-biased CG induces a cantilevered moment on the rail under recoil, which can crack polymer frame rails on the Glock 22 Gen 5.

2. Shock Isolation Strategy (Low-Pass Mechanical Filter)

Direct Coupling Avoidance: The PCB must not be rigidly screwed into the enclosure. Recoil forces exceeding 1000 G acting on rigid standoffs will shear solder joints and crack MLCC (Multilayer Ceramic Capacitor) components.

Implementation: Design the enclosure with a "suspended tray" mount using Sorbothane (durometer 40 Shore OO) grommets. The grommets act as a mechanical low-pass filter, attenuating high-frequency (>500 Hz) shock transient spikes from the slide's steel-on-steel impact, protecting the MEMS sensor and oscillator.

3. 3D-Printing Design for Additive Manufacturing (DfAM)

Wall Thickness: Minimum 2.5mm walls with a 30% gyroid infill using PA-CF (Carbon Fiber Nylon) or tough resin. This prevents resonant buzzing that distorts accelerometer data.

Serviceability: Design a sliding dovetail cover for the battery compartment, secured by a captured M3 locking bolt. Avoid snap-fit closures in the recoil impulse path; they will fail instantly under live-fire vibration, ejecting the battery.
