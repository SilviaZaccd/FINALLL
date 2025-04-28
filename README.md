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




---

## Audience

- **Creatives** working at a desk
- **Anyone** seeking ambient mood enhancement

---

## Concept Sketches

<img width="623" alt="截屏2025-04-28 下午4 01 31" src="https://github.com/user-attachments/assets/9257101a-a012-4be4-a3f8-011bd6bc8f78" />



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

<img width="4032" alt="Core project Ideation+ Research" src="https://github.com/user-attachments/assets/e32e721b-86ee-4dc2-8a3f-27ea4f464937" />



---

## 🚀 Final Note

WindMood demonstrates a playful, intuitive way to integrate **physical interaction** with **digital feedback**  
in a personalized, everyday object. ✨

---

*(Remember to replace all `insert-...-link-here` with your actual image uploads.)*

