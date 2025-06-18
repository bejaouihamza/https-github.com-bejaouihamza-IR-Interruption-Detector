# 🔦 IR Interruption Detector PCB

This project is a complete PCB-based system that detects interruptions between an **IR emitter and receiver**. When an object blocks the IR beam:
- A **buzzer/speaker** is triggered,
- A **7-segment display counter** is incremented,
- A **reset button** clears the count.

The circuit is entirely based on **discrete components**, including **NE555 timers**, **CD40106**, and a **CD4033** counter/decoder. It also includes a **robust regulated power supply**, and can be used in security, object-counting, or automation systems.

---

## 📷 Schematic

_Add your schematic image below:_

![Schematic]([Capture d'écran 2025-06-18 144531.png](https://github.com/bejaouihamza/https-github.com-bejaouihamza-IR-Interruption-Detector/blob/main/Capture%20d'%C3%A9cran%202025-06-18%20144531.png))

---

## 🧩 PCB Layout

_Add your PCB layout image below:_

![PCB](./images/pcb.png)

---

## 🧱 3D Model

_Add your 3D view render here:_

![3D Model](./images/3d.png)

---

## ⚙️ System Overview

### ➤ Power Supply
The power input is **230V AC**, stepped down using a transformer and rectified via a **bridge diode**. The output is regulated to **+12V DC** using a **7812 voltage regulator**.

---

### ➤ IR Transmitter Stage

- **Components**: 2x NE555 + TSAL4400 IR LED
- The first NE555 generates a **square wave** (~38 kHz), modulated by the second NE555 to create an **amplitude-modulated IR beam**.
- Transistor **Q1** amplifies the signal and drives the IR LED with enough current.

---

### ➤ IR Receiver & Detection

- **TSOP2254** is used to receive the modulated IR beam.
- Its digital output goes **LOW** when it detects the 38 kHz signal.
- When an interruption occurs (e.g. hand/object blocks the beam), the output goes **HIGH**, triggering further stages.

---

### ➤ Signal Conditioning & Alarm Logic

- NE555 (U6) is configured in a monostable mode.
- CD40106 Schmitt triggers (U2, U3) are used for **clean signal shaping** and logic handling.
- This ensures only valid interruptions trigger the output.

---

### ➤ Output Stage

- A speaker or buzzer (AST-1732MR-R) is triggered via transistor Q3.
- An LED also indicates the alarm visually.

---

### ➤ Counting Stage

- A **CD4033B** 7-segment BCD counter increments with each IR interruption.
- A **D168K** display shows the count.
- A reset button allows clearing the count manually.

---

## 🔁 Workflow Summary

1. **Idle**: IR signal is received, no object interrupting.
2. **Interrupt**: Object breaks the beam → TSOP output goes HIGH.
3. **Detection**: NE555 monostable timer triggers.
4. **Alarm**: Buzzer sounds + 7segments Display increments count.
5. **Reset**: Pressing the reset button clears the counter.

---

## 🧰 Bill of Materials (BOM)

| Component     | Quantity | Notes                              |
|---------------|----------|------------------------------------|
| NE555         | 3        | Signal modulation and detection    |
| TSOP2254      | 1        | IR receiver                        |
| TSAL4400      | 1        | IR LED                             |
| CD40106       | 1        | Schmitt trigger inverter           |
| CD4033B       | 1        | BCD Counter                        |
| D168K         | 1        | 7-Segment Display                  |
| AST-1732MR-R  | 1        | Buzzer/Speaker                     |
| Q1, Q2, Q3    | 3        | NPN transistors                    |
| TP4056        | 1 (opt.) | Optional for battery version       |
| AMS1117-3.3   | 1 (opt.) | Optional for low-voltage designs   |

---

## 🔧 Tools Used

- **KiCad 9** for schematic and PCB design
- **Open source components**
- **Through-hole components **

---

## 🧠 Author

Designed by **Bejaoui Hamza**  
Date: **18 June 2025**  
Project name: `IR Interruption Detector`

---

## 📂 License

This project is open-source under the [MIT License](LICENSE).

---

