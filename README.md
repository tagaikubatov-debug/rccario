#**🚓 Arduino Robotic Car with Police Lights and Sound**
---
📌 Project Overview

This project is a fully-functional robotic vehicle controlled by Arduino Uno.
It includes:

4 DC motors (dual driver configuration)

Police-style LED flashing system (red & blue)

Passive buzzer siren

External battery power

Custom wiring and mechanical assembly

The goal of the project was to design, assemble, and document a small robotic system with electrical, mechanical, and software components.
---

#**🛠️ Hardware Used**

Arduino Uno

2× L298/L293-based dual motor drivers (4 motors total)

4× DC motors

5 red LEDs (grouped)

5 blue LEDs (grouped)

Passive buzzer

Li-Ion / AA battery pack

Breadboard + jumper wires

#**🔌 Wiring Diagram**
___

<img width="1332" height="1183" alt="image" src="https://github.com/user-attachments/assets/b70894ed-8650-47b2-a3b5-9cfb29d85d11" />

Key connections:

Motor Driver 1 (Left side)
Signal	Pin
EN1	D3
IN1	D2
IN2	D4
EN2	D5
IN3	D6
IN4	D7
Motor Driver 2 (Right side)
Signal	Pin
EN1	D11
IN1	D12
IN2	D13
EN2	A0
IN3	A1
IN4	A2
LEDs & Buzzer
Component	Pin
Red LED group	D8
Blue LED group	D9
Passive buzzer	D10

__
#**💡 Features**

Forward / backward motion

Left & right turns

Emergency police LED flashing

Dual-tone siren

Modular code structure

Expandable system
