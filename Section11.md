# Fa25 Firmware Lab: Button + Potentiometer LED Control

Welcome to your first firmware project! 🎉  
In this lab, you’ll learn how to connect simple input devices (a **button** and a **potentiometer**) to an **ESP32** and use code to control an **LED**.  
This project introduces **GPIO basics**, **analog inputs**, and **PWM duty cycle control**, which are essential skills for future work on the solar car.

---

## 🧾 Deliverables
- LED toggles on/off with button press (includes software debouncing).  
- LED brightness responds smoothly to potentiometer when active.  
- Serial Monitor prints `"LED ON/OFF"` messages.  
- Screenshot or video demo of working circuit in **Wokwi**.  

---


## ⚙️ Circuit Setup

1. Go to [https://wokwi.com/](https://wokwi.com/) → Select **ESP32** → Scroll down for **Starter Templates** → Select **ESP32** (the very first one).
3. When you open a new project, you’ll see something like this:
![ESP32 Template Circuit](images/ESP%20Template.png)
   - For now, ignore the left half (code editor).  
   - Let’s first make our circuit on the right half.  

### Toolbar Overview
- ▶️ **Run** – compiles and runs your code.  
- 🧩 **Add Part** – adds circuit components.  
- 🧱 **Workspace Tools** – affects only layout/view; safe to explore.  

---

## 🧰 Parts for This Lab

- **ESP32 Board** – our “mini-computer.” It runs your code and controls the rest of the circuit.  
- **LED (Light Emitting Diode)** – output device that lights up, dims, or turns off depending on the firmware.  
- **Resistor** – protects the LED from excess current (use 220–330 Ω).  
- **Push Button** – input device; pressing it sends a signal to toggle the LED.  
- **Potentiometer (variable resistor)** – input device; turning the knob adjusts the LED’s brightness.  
- **Wires** – connect all the components to allow current and signals to flow.

---

## 🧩 To-Do

Use the **Add Part** button to add:
- 1 × LED  
- 1 × Resistor (220–330 Ω recommended)  
- 1 × Push Button  
- 1 × Potentiometer
For your reference:
![Component Reference](images/Component%20Reference.png)

Once all parts are placed on the canvas, we’ll move on to wiring them together.  

*(Don’t worry — we’ll go step by step!)*

---
## 🔗 Connecting the Circuit

### LED + Resistor
- Long leg (anode) → through **220 Ω resistor** → **GPIO 15** on ESP32.  
- Short leg (cathode) → **GND**.  

> **Why:** GPIO 15 is a general-purpose digital output. The resistor ensures the LED doesn’t burn out.

---
### Push Button
- One side → **GPIO 4**.  
- Other side → **GND**.  

> ⚠️ **Important:** Connect the **diagonal pins**; otherwise you’re shorting the button!  
> **Why:** GPIO 4 reads **LOW** when pressed (connected to GND) and **HIGH** when released, thanks to the internal pull-up.

---
### Potentiometer
- Middle pin → **GPIO 34** (analog input).  
- One outer pin → **3.3 V**.  
- Other outer pin → **GND**.  

> **Why:** GPIO 34 is an ADC pin that reads a range of values (0–4095) representing the potentiometer’s position.

---

### Power & Ground
Make sure **all components share the same 3.3 V and GND** connections.  

> Without a common reference, current won’t flow and the ESP32 can’t control or sense components.

---

When finished, your circuit should look similar to this (feel free to make it look neater!):  
![circuit setup](images/Circuit%20Setup.png)

# Actual Firmware Stuff :)

Okay, the circuit’s all hooked up — now let’s sprinkle some code magic on it!

---

On the left half of your screen, you should see two important functions:

1. setup()

   - Runs once at the very beginning.
   - Think of it like *“initialization.”*  
     This is where you configure pins, start communication, or print a startup message.
   - Example here:  
     Serial.begin(115200) -> sets up the USB serial connection so the ESP32 can talk to your computer.

2. loop()

   - Runs over and over forever.
   - This is where your main program logic lives.  
     If you want the ESP32 to blink an LED, read a button, or check a sensor, that code will go here.

---

In this starter code, the only thing inside loop() is a short delay(10);. That doesn’t do much, but it prevents the simulation from running unnecessarily fast.



