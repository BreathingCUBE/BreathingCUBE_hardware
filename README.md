# BreathingCUBE_hardware

In today’s digital world, attention is constantly fragmented. Smartphones, notifications, social media feeds, and endless scrolling compete for our focus every minute of the day. The result is chronic distraction, diminished deep focus, and elevated stress levels.

Now imagine being able to step away from that noise, even for a few minutes, and reconnect with your breath.

The BreathingCube is an IoT-enabled device designed to help individuals integrate meditation into busy daily life. Through guided ambient lighting patterns and subtle sound cues, it encourages intentional breathing and mindfulness practice, helping calm the nervous system and restore a sense of presence.

# HARDWARE
This is a 4-layer PCB with SIGNAL,GND,3V3,SIGNAL+GND stackup. 

This stackup was chosen because most of the digital/analog traces could be fit within the top layer.(Meaning clear return path for most traces)

Many components draw a significant amount of transient current load, so the 3V3 plane offers capacitance to ensure power is drawn local to the component, rather than from far away.

# Controller
Here we used an ESP32-C3-MINI to be able to access the WIFI feature of the board.
90 ohm impedance matching was done on the USB-C differential pair

<img width="824" height="621" alt="image" src="https://github.com/user-attachments/assets/942c0a87-72e7-4f8b-82f1-dd5baa5660b5" />

# BMS
This is a standard OR circuit. Where the 3V3 buck-converter either steps down voltage from the USB-C or the LIPO-battery.
This circuit also contains battery charging, battery protection, and battery measurement
<img width="1223" height="599" alt="image" src="https://github.com/user-attachments/assets/3a52e4d1-2a26-4f2c-80ff-185c3bfa7e52" />

# Application
**Piezo disk** is used as a tap-sensitive input and sampled through an ADC. Because piezoelectric elements can generate relatively high voltages(30V), the front-end includes protection circuitry to keep the ADC input within the 0–3.3 V safe operating range. 

- A series resistor is used to limit surge current into the protection network

- Schottky clamp diodes to 3.3 V and GND prevent the ADC node from exceeding the supply rails. 

- A bleed resistor provides a discharge path for the piezo element, helping the signal settle after each press.


The **buzzer** is driven using a **low-side NMOS switch**, allowing higher current to flow through the load without stressing the MCU GPIO.

- A **series resistor** is included to limit current and provide some control over the buzzer volume  

- A **parallel capacitor** is added across the buzzer to help reduce high-frequency noise and stabilize the supply during switching  

- The NMOS enables efficient switching, allowing the buzzer to be driven using a PWM signal for tone generation

- In addition to this an LED driver and IMU is controlled via I2C

<img width="1063" height="581" alt="image" src="https://github.com/user-attachments/assets/f6bfa5b1-f099-4bcf-8909-5aed50dc8585" />

# Routing
<img width="559" height="608" alt="image" src="https://github.com/user-attachments/assets/7b88c6ae-8b3c-4bd4-a420-3b09a26fcc10" />

<img width="582" height="613" alt="image" src="https://github.com/user-attachments/assets/7ff0c3e3-7d96-47bc-ae35-93fa60b01771" />

# Software/firmware for product can be found here
https://github.com/BrycesDevices/7855_202610_03

# Revision 1 of breathingCUBE can be found here
https://github.com/Parry-Zhuo/BreathingCube
