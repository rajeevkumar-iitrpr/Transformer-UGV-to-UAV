# 🚀 Transformer UGV to UAV

This project showcases a **Transformer Robot** that can switch between two modes:
1. **UGV (Unmanned Ground Vehicle)** – a wheeled robot that moves on the ground.  
2. **UAV (Unmanned Aerial Vehicle)** – a quadcopter that takes off and flies.

The transformation from **ground mode** to **flight mode** is achieved using servo mechanisms and motor control via a flight controller.

---

## ⚙️ Hardware Components

| Component | Quantity | Description |
|------------|-----------|-------------|
| **5010 BLDC Motor** | 2 | Used for driving the ground movement (UGV mode). |
| **Servo Motors (High Torque)** | 2 | Used to transform the chassis and fold/unfold arms during mode switching. |
| **Flight Controller (e.g., Matek F405 / Pixhawk / APM)** | 1 | Controls flight stability and UAV functions. |
| **2205 / 2306 Brushless Motors** | 4 | Used for quadcopter propulsion (UAV mode). |
| **ESCs (Electronic Speed Controllers)** | 4 + 2 | 4 for UAV motors, 2 for ground drive motors. |
| **Battery (LiPo 3S or 4S)** | 1 | Power source for both drive and flight systems. |
| **Receiver / Radio Transmitter** | 1 | For manual or remote control (if used). |
| **ESP32 / Arduino (optional)** | 1 | Used for mode switching or additional sensor integration. |
| **Chassis** | 1 | Custom frame designed to support both ground and flight configurations. |

---

## 🧠 Working Principle

1. **UGV Mode:**
   - Two **5010 BLDC motors** drive the wheels for ground navigation.
   - Controlled via ESCs connected to the flight controller (or an external microcontroller).

2. **Transformation Mode:**
   - Two **servo motors** activate to fold or unfold the frame arms.
   - Once the transformation sequence is complete, the flight motors are activated.

3. **UAV Mode:**
   - Four **quadrotor BLDC motors** take control for aerial flight.
   - The flight controller stabilizes and maneuvers the UAV using standard quadcopter algorithms (PID or ArduPilot).

---

## 🔌 Wiring Overview

- **5010 Motors → ESCs → Flight Controller (Aux Outputs)**  
- **Quadrotor BLDCs → ESCs → Flight Controller (Main Outputs)**  
- **Servos → PWM Pins (Controlled via flight controller or ESP32 GPIOs)**  
- **Battery → Power Distribution Board → ESCs + Flight Controller**  

*(Ensure separate power regulation for servos if required)*

---

## 🧩 Software and Control

- **Firmware:** ArduPilot / Betaflight / iNAV (for flight control)  
- **Mode Switching Logic:** Controlled via auxiliary channel or ESP32 script  
- **Servo Control:** PWM signals triggered based on mode state (Ground ↔ Air)

Example pseudocode for transformation:

```cpp
if (mode == "UGV") {
  stopFlightMotors();
  activateDriveMotors();
  moveServosToGroundPosition();
}

if (mode == "UAV") {
  stopDriveMotors();
  moveServosToFlightPosition();
  activateFlightMotors();
}

<img width="1214" height="781" alt="Screenshot 2025-10-21 210839" src="https://github.com/user-attachments/assets/de9dbdc0-4fd0-41ca-add4-1850af6a2260" />
<img width="1127" height="685" alt="Screenshot 2025-10-21 211517" src="https://github.com/user-attachments/assets/aba14f93-d4f0-4028-ac0b-6726d14d5a70" />
