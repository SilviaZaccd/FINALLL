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
<img width="761" alt="截屏2025-04-28 下午4 09 49" src="https://github.com/user-attachments/assets/6bf6d611-6ba4-46a9-86a1-0e6d542a6df6" />


---

## State Diagram （How my interactive prototype should behave）

<img width="4032" alt="Core project Ideation+ Research" src="https://github.com/user-attachments/assets/e32e721b-86ee-4dc2-8a3f-27ea4f464937" />

## Concept Sketches

<img width="623" alt="截屏2025-04-28 下午4 01 31" src="https://github.com/user-attachments/assets/9257101a-a012-4be4-a3f8-011bd6bc8f78" />



---

## Implementation

### Hardware
M5Stack AtomS3 Lite — microcontroller

NeoPixel 30-LED RGB strip — colorful mood lighting

360-degree Continuous Servo — drives windmill head rotation

IR Reflective Sensor — detects user proximity

Button (M5 Bottom) — manual mode switch

Rotary Angle Unit — brightness control

Breadboard & jumper wires — prototyping setup


<img width="740" alt="截屏2025-04-28 下午4 19 01" src="https://github.com/user-attachments/assets/b0033ea1-bf34-414d-8ce6-78fd2c3e3bcf" />

---
### Build 3d Modle 

![8501745881428_ pic](https://github.com/user-attachments/assets/fad4b70b-b7fe-4ec7-b425-6d0aa3c64660)
![8491745881417_ pic](https://github.com/user-attachments/assets/b41ff494-f206-4c6a-b832-119ea1d53677)


---
### Process (Hand make)


<img width="280" alt="截屏2025-04-28 下午4 07 07" src="https://github.com/user-attachments/assets/2b3ba673-f26b-4f9b-973d-f8ab9b715deb" />
<img width="295" alt="截屏2025-04-28 下午4 07 24" src="https://github.com/user-attachments/assets/cfe25ad5-42bf-4def-b62d-66470f3b3335" />
<img width="280" alt="截屏2025-04-28 下午4 07 39" src="https://github.com/user-attachments/assets/9013bb7c-641d-4d75-8aef-93652ff6df6a" />


<img width="677" alt="截屏2025-04-28 下午4 22 24" src="https://github.com/user-attachments/assets/a4ca343f-589b-46cf-9694-c9f8847531af" />


---
### My complete Prototype（Code）
from machine import Pin, ADC, PWM, UART
from time import sleep_ms
from neopixel import NeoPixel

# ------------ 硬件初始化 ------------
np = NeoPixel(Pin(7), 30)  # NeoPixel 灯带（10颗）
angle = ADC(Pin(6))
angle.atten(ADC.ATTN_11DB)

ir_sensor = ADC(Pin(1))
ir_sensor.atten(ADC.ATTN_11DB)

btn = Pin(41, Pin.IN, Pin.PULL_UP)
servo = PWM(Pin(38), freq=50)
uart = UART(1, baudrate=115200)

# ------------ 参数设置 ------------
mode = 0
IR_THRESHOLD = 1500  # 红外感应阈值


windmill_angle = 0
windmill_speed = 0

# ------------ 工具函数 ------------
def scale_brightness(val):
    return int((val / 4095) * 255)

def set_color_all(r, g, b):
    for i in range(30):
        np[i] = (r, g, b)
    np.write()

def set_servo_duty(duty_val):
    servo.duty(duty_val)

def send_mode_to_protopie(current_mode):
    uart.write("mode:" + str(current_mode) + "\n")
    print("🛰️ Sent mode:", current_mode)

# ------------ 模式控制 ------------
def run_mode(mode, brightness):
    global windmill_speed
    if mode == 0:
        # ☀️ Mode 0: 白光 + 慢速风车 + Angle 控制亮度
        set_color_all(brightness, brightness, brightness)
        set_servo_duty(67)
        windmill_speed = 7
        print("Morning Mode")
        print('windmill_angle||' + str(windmill_speed))
    elif mode == 1:
        # 🪟 Mode 1: 黄光 + 中速风车 + Angle 控制亮度
        r = brightness
        g = int(brightness * 0.7)
        set_color_all(r, g, 0)
        set_servo_duty(60)
        windmill_speed = 4
        print("Sunset Mode")
        print('windmill_angle||' + str(windmill_speed))
    elif mode == 2:
        
        windmill_speed = 1
        
        # 🌌 紫色 ↔ 蓝色 呼吸渐变
        for i in range(0, 21):  # 紫 → 蓝 (分成20步)
            r = int(100 - i * (100 / 20))   # R: 100 → 0
            g = 0
            b = int(100 + i * (155 / 20))   # B: 100 → 255
            set_color_all(r, g, b)
            set_servo_duty(65)
            print("Night Mode")
            print('windmill_angle||' + str(windmill_speed))
            sleep_ms(30)


        for i in range(0, 21):  # 蓝 → 紫
            r = int(i * (100 / 20))         # R: 0 → 100
            g = 0
            b = int(255 - i * (155 / 20))   # B: 255 → 100
            set_color_all(r, g, b)
            set_servo_duty(65)
            print("Night Mode")
            print('windmill_angle||' + str(windmill_speed))
            sleep_ms(30)

        #print("Night Mode")


# ------------ 主循环 ------------
while True:
    angle_val = angle.read()
    #print('angle_val = ', angle_val)
    
    brightness = scale_brightness(angle_val)
    #print(ir_sensor.read())

    # 模式切换（IR靠近或按钮按下）
    if ir_sensor.read() < IR_THRESHOLD or btn.value() == 0:
        mode = (mode + 1) % 3
        send_mode_to_protopie(mode)
        sleep_ms(500)  # 防抖延迟

    # 模式执行
    if mode in [0, 1]:
        run_mode(mode, brightness)
    elif mode == 2:
        run_mode(mode, 200)  # mode 2 不使用旋钮，使用固定亮度

    #windmill_angle += int(angle_val/1000)
    #windmill_angle += windmill_speed
    #print('windmill_angle||' + str(windmill_angle))
    #print('windmill_angle||' + str(windmill_speed))
    
    
    sleep_ms(200)


##  Final Note


