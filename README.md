WindMood Presentation Overview

Introduction

WindMood is an interactive emotional lighting prototype in the form of a windmill-inspired lamp. Designed for indoor desk use, it serves as an ambient emotional cue light, reflecting different moods through RGB lighting and windmill movement. The lamp is contextually placed in a cozy, private environment such as a home or studio desk, offering mood enhancement and emotional feedback to solo users, particularly students or creatives.

The device allows the user to switch between three emotional states using proximity (IR sensor) or a physical button. Each state changes the color and behavior of the light and servo-driven windmill head. The user can also control brightness using a rotary angle unit.

Audience:

Students / remote workers

Creatives working at a desk

People seeking mood-based ambiance

Concept Sketches: Include 1-2 scanned sketches from Part 1 showing the windmill lamp design and initial hardware layout.

Implementation

Hardware (Electronics)

M5Stack AtomS3 Lite — microcontroller

NeoPixel 30-LED RGB strip — visual output of mood states

360-degree Continuous Rotation Servo — animates the windmill head

IR Reflective Sensor — detects user proximity for mode switching

Button (M5 Bottom Button) — physical trigger to switch modes

Angle Unit (Rotary potentiometer) — adjusts brightness in modes 0 and 1

Breadboard + jumper wires — for prototyping connections

Firmware (MicroPython Code)

Inputs: IR sensor, button, angle knob

Outputs: RGB LED, servo

Modes:

Mode 0: Morning — White light, brightness via angle, servo slow

Mode 1: Afternoon — Warm yellow light, brightness via angle, servo medium

Mode 2: Night — Blue-purple breathing light, fixed brightness, servo nearly still

Code uses PWM, ADC, UART and NeoPixel libraries

UART is used to communicate with ProtoPie for live feedback visuals

Software (ProtoPie)

Receives serial data (mode:0, mode:1, mode:2) via UART

Shows mode icon, label, and animated feedback in the app interface

Enclosure & Mechanical Design

Modeled in Rhino and sliced for 3D printing

Form resembles a modern windmill with a base, body, and removable blade head

Printed in PLA and hand-assembled

Servo placed horizontally inside the top with custom axle to spin fan blades

State Diagram

[Power ON]
   |
[Idle Mode]
   |-- (IR or Button Trigger) --> [Mode 0 - Morning]
   |         - White Light
   |         - Brightness via Angle Unit
   |         - Servo Slow
   |-- (Trigger again) --> [Mode 1 - Afternoon]
   |         - Warm Yellow
   |         - Brightness via Angle
   |         - Servo Medium
   |-- (Trigger again) --> [Mode 2 - Night]
   |         - Breathing Blue-Purple
   |         - Fixed Brightness
   |         - Servo 74 (slow/static)
   |
   +-- (Loop)

Hardware Code: All logic on the ATOM S3 board.Software Feedback: UI state reflects current mode:X sent via UART to ProtoPie.

Hardware List

M5Stack AtomS3 Lite

NeoPixel RGB LED strip (30 LEDs)

360-degree servo motor

IR reflective sensor (input)

Rotary angle unit

Button (on M5 Bottom)

Breadboard, jumper wires, USB-C cable

Wiring Diagram

Include labeled photo or diagram showing:

Servo → Pin 38 (PWM)

IR sensor → Pin 1 (ADC)

Angle unit → Pin 6 (ADC)

NeoPixel → Pin 7 (Digital)

Button → Pin 41 (Digital)

Firmware Code

Include uploaded main.py code file separately.

Key Logic Explanation:
