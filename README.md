# 🚓 Arduino Robotic Car with Police Lights and Sound

## 📌 Project Overview

This project is a fully-functional **Bluetooth-controlled robotic vehicle** based on an **Arduino Uno**.  
It combines:

- Differential drive with DC motors
- Police-style **red/blue LED flashing**
- **Dual-tone siren** on a passive buzzer
- External battery power
- Simple serial command protocol (`F`, `B`, `L`, `R`, `S`)

The goal of the project is to design, assemble and document a small robotic system that includes **electrical**, **mechanical**, and **software** components.

---

## 🧠 Main Features

- 🚗 Forward / backward motion  
- ↩️ Left & right turns (tank-style drive)  
- ⛔ Full stop command  
- 🚨 Emergency police LED flashing  
- 🔊 Dual-tone siren  
- 📲 Control via Bluetooth (e.g. HC-05 / HC-06)  
- 🧩 Modular and easily expandable code  

---

## 🛠️ Hardware Used

- **Arduino Uno**
- **2× L298N / L293D-based dual motor drivers** (4 motors total, paired per side)
- **4× DC motors** (2 left, 2 right)
- **5× red LEDs** (grouped as red police light)
- **5× blue LEDs** (grouped as blue police light)
- **Passive buzzer**
- **Bluetooth module** (HC-05 / HC-06 or similar)
- **Li-Ion / AA battery pack(s)** for motors and logic
- Breadboard + jumper wires
- Chassis + wheels

---
<img width="1860" height="1231" alt="image" src="https://github.com/user-attachments/assets/0b557893-1cff-4fd4-87ca-846db449e390" />

## 🧷 Pinout & Wiring

### 🔌 Arduino Pin Assignments (match the code)

| Function                    | Arduino Pin | Notes                                       |
|----------------------------|------------:|---------------------------------------------|
| SoftwareSerial RX (Arduino) | D2          | Connect to TX of Bluetooth module           |
| SoftwareSerial TX (Arduino) | D3          | Connect (via divider) to RX of Bluetooth    |
| Left side motor IN1        | D13         | Motor driver input                          |
| Left side motor IN2        | D12         | Motor driver input                          |
| Right side motor IN1       | D11         | Motor driver input                          |
| Right side motor IN2       | D10         | Motor driver input                          |
| Buzzer                     | D5          | Passive buzzer positive pin                 |
| Red LED group              | D6          | Through resistor(s)                         |
| Blue LED group             | D7          | Through resistor(s)                         |
| Hardware Serial (USB)      | D0, D1      | Used for debug (Serial Monitor)             |

> ⚠️ IMPORTANT: All grounds (Arduino, motor driver, Bluetooth, battery) **must be connected together**.

---

## 🚗 Motor Driver Connection

You use **2 dual H-bridge drivers** for **4 motors total**.  
The Arduino code controls **left side** and **right side** as two channels:

- **Left side motors (both left motors in parallel)**  
  - Connect both left motors to the outputs of **Driver 1**  
  - Driver inputs:  
    - `IN1` → **D13**  
    - `IN2` → **D12**  
  - `ENA` (or `EN1`) → 5V (for full speed) or to a PWM pin if you later add speed control

- **Right side motors (both right motors in parallel)**  
  - Connect both right motors to the outputs of **Driver 2** (or second channel)  
  - Driver inputs:  
    - `IN3` → **D11**  
    - `IN4` → **D10**  
  - `ENB` (or `EN2`) → 5V (for full speed)

> 💡 You can also tie both left motors to one driver and both right motors to the other driver — just make sure both motors on each side spin in the same direction.

---

## 💡 LEDs & Siren Wiring

### Police LEDs

- **Red LED group**  
  - Anodes of red LEDs → **D6** through current-limiting resistors (e.g. 220–330 Ω per LED or per group)  
  - Cathodes → GND

- **Blue LED group**  
  - Anodes of blue LEDs → **D7** through current-limiting resistors  
  - Cathodes → GND

### Buzzer

- Passive buzzer **+** → **D5**  
- Passive buzzer **−** → GND  

The sketch uses `tone()` with two frequencies (≈600 Hz / 900 Hz) to create a simple dual-tone siren.

---

## 📡 Bluetooth Module (HC-05 / HC-06 Example)

The code uses `SoftwareSerial mySerial(2, 3);`:

- Bluetooth **TXD** → **D2** (Arduino SoftwareSerial RX)  
- Bluetooth **RXD** → **D3** (Arduino SoftwareSerial TX, через делитель до 3.3 V желательно)  
- Bluetooth **GND** → Arduino GND  
- Bluetooth **VCC** → 5V (проверь характеристики модуля)

The Bluetooth module sends **single-character commands**:

| Command | Action                  |
|---------|-------------------------|
| `F`     | Move **Forward**        |
| `B`     | Move **Backward**       |
| `L`     | Turn **Left**           |
| `R`     | Turn **Right**          |
| `S`     | **Stop** all motors     |

You can send these from a phone app (e.g. a Bluetooth terminal or custom controller).

---

## 🧾 Arduino Sketch (Summary)

Core logic of the project:

- Read command from `mySerial` (Bluetooth)
- Depending on the character, set motor pins:
  - `F` → left and right motors forward
  - `B` → both backwards
  - `L` / `R` → one side stopped, other side forward
  - `S` → all motor pins LOW (stop)
- Run `policeEffect()` in the main loop to blink LEDs and drive the siren

---

## 🚀 Getting Started

1. **Wire everything** according to the pinout above  
2. Open the `.ino` file in the **Arduino IDE**  
3. Select:
   - Board: **Arduino Uno**
   - Correct **COM port**
4. Click **Upload**
5. Connect with a Bluetooth app on your phone and send commands: `F`, `B`, `L`, `R`, `S`

---

## 🔧 Possible Improvements

- Add **speed control** with PWM on motor enable pins
- Add **battery monitoring** using an analog input
- Add **ultrasonic sensor** for obstacle avoidance
- Add separate command to enable/disable police lights/siren
- Use a custom mobile app UI instead of text commands

---

## 📄 License

You can use, modify, and share this project for learning and hobby purposes.  
Feel free to fork the repo and improve it!
