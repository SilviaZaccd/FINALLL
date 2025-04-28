# WindMood — Interactive Desk Lamp

## Introduction

**WindMood** is an interactive emotional lighting prototype shaped like a windmill-inspired lamp.  
It provides ambient emotional cues through **RGB lighting** and **servo-driven movement**, designed for cozy environments like:

- Home desks
- Studio spaces
- Private corners for students or creatives
<img width="736" alt="截屏2025-04-28 下午3 55 08" src="https://github.com/user-attachments/assets/e0d7c596-345a-4dac-b6a1-5b7167a789cc" />




Users can **switch between three emotional states** (Morning, Afternoon, Night) using **proximity (IR sensor)** or a **physical button**.  
Additionally, **brightness control** is available via a **rotary angle unit** in certain modes.

<img width="4032" alt="Core project Ideation+ Research" src="https://github.com/user-attachments/assets/e32e721b-86ee-4dc2-8a3f-27ea4f464937" />



---

## Audience

- **Creatives** working at a desk
- **Anyone** seeking ambient mood enhancement

---

## Concept Sketches

![Concept Sketch 1](insert-sketch1-link-here)
![Concept Sketch 2](insert-sketch2-link-here)

*(Early designs showing windmill form and hardware layout.)*

---

## 🛠️ Implementation

### 🔌 Hardware (Electronics)

- **M5Stack AtomS3 Lite** — microcontroller
- **NeoPixel 30-LED RGB strip** — colorful mood lighting
- **360-degree Continuous Servo** — drives windmill head rotation
- **IR Reflective Sensor** — detects user proximity
- **Button (M5 Bottom)** — manual mode switch
- **Rotary Angle Unit** — brightness control
- **Breadboard & jumper wires** — prototyping setup

### 🧠 Firmware (MicroPython)

- **Inputs:** IR sensor, Button, Angle unit
- **Outputs:** NeoPixel LEDs, Servo
- **Libraries:** `PWM`, `ADC`, `UART`, `NeoPixel`
- **Serial Communication:** UART → ProtoPie
- **Modes:**
  - **Morning (Mode 0):** White light + Angle brightness + Slow windmill
  - **Afternoon (Mode 1):** Warm yellow light + Angle brightness + Medium speed
  - **Night (Mode 2):** Breathing purple-blue + Fixed brightness + Very slow/stop windmill

### 🖥️ Software (ProtoPie)

- Receives `mode:0`, `mode:1`, `mode:2` via **UART**
- Displays **animated icons + matching feedback**

### 🏢 Enclosure & Mechanical Design

- Designed in **Rhino 3D**
- 3D-printed using **PLA**
- Hollow tower with inner servo mounting system
- Fan blades removable via top mounting

![WindMood Enclosure](insert-enclosure-photo-link-here)

---

## 🔄 State Diagram

![WindMood State Diagram](insert-state-diagram-image-link-here)

```plaintext
[Power ON]
    ↓
[Idle Mode]
    ↓ (IR detected / Button pressed)
[Morning Mode - White Light]
    ↓
[Afternoon Mode - Warm Light]
    ↓
[Night Mode - Breathing Purple/Blue]
    ↓
(Loop back)
```

- **Hardware Code:** IR detection + Button input + Servo control + LED output
- **Software Feedback:** Mode update shown on ProtoPie App

---

## ⚙️ Hardware List

- M5Stack AtomS3 Lite
- NeoPixel 30-LED strip
- 360-degree Servo
- IR Reflective Sensor
- Rotary Angle Unit
- Bottom Button
- Breadboard + Jumpers

---

## 🪛 Wiring Overview

| Component         | Connection  |
|-------------------|--------------|
| Servo             | Pin 38 (PWM) |
| IR Sensor         | Pin 1 (ADC)  |
| Angle Unit        | Pin 6 (ADC)  |
| NeoPixel LEDs     | Pin 7        |
| Button            | Pin 41       |

![Wiring Diagram](insert-wiring-diagram-link-here)

---

## 🧰 Firmware Key Logic

```python
# Switch mode on IR or button
# Adjust brightness via angle (modes 0/1)
# Update NeoPixel colors accordingly
# Control servo speed for each mode
# Send mode info over UART to ProtoPie
```

---

## 🚀 Final Note

WindMood demonstrates a playful, intuitive way to integrate **physical interaction** with **digital feedback**  
in a personalized, everyday object. ✨

---

*(Remember to replace all `insert-...-link-here` with your actual image uploads.)*

