# ESP32 Real-Time Clock — DS3231 + 7-Segment Display

A custom PCB project featuring an **ESP32-WROOM-32** microcontroller, **DS3231 RTC module** (I2C), and a **4-digit 7-segment display** to show real-time HH:MM with a blinking colon. Designed in **EasyEDA** and programmed using **Arduino IDE (Embedded C++)**.

---

## Features

- Real-time HH:MM display with blinking colon (0.5s toggle)
- DS3231 precision RTC with battery backup (CR2032) — keeps time even when power is off
- Multiplexed 7-segment display driven via **74HC595 shift register** (saves GPIO pins)
- RTC temperature readout printed to Serial Monitor
- Auto time-set from compile time if RTC loses power
- Custom 2-layer PCB with decoupling capacitors and proper power traces

---

## Hardware

| Component | Value / Part | Quantity |
|---|---|---|
| Microcontroller | ESP32-WROOM-32 | 1 |
| RTC Module | DS3231 (SOP-16) | 1 |
| Shift Register | 74HC595 (DIP-16) | 1 |
| Display | 4-Digit 7-Segment, Common Cathode, 0.56" | 1 |
| Transistors | 2N2222 NPN (TO-92) | 4 |
| Resistors | 330Ω (seg), 1K (base), 10K (I2C pull-up) | 15 |
| Capacitors | 100nF, 10µF | 4 |
| Battery | CR2032 (RTC backup) | 1 |
| Connector | USB Micro-B | 1 |

Full BOM: [`pcb/BOM.csv`](pcb/BOM.csv)

---

## Circuit Overview

```
ESP32-WROOM-32
├── GPIO26 (SDA) ──[10K]── 3.3V
├── GPIO27 (SCL) ──[10K]── 3.3V
│       └──── DS3231 RTC (I2C) ──── CR2032 backup battery
│
├── GPIO23 (DATA)  ──┐
├── GPIO22 (LATCH) ──┤── 74HC595 Shift Register ──[330R x7]── Segments a-g
├── GPIO21 (CLOCK) ──┘
│
├── GPIO19 ──[1K]── Q1 (2N2222) ── Digit 1 Common Cathode
├── GPIO18 ──[1K]── Q2 (2N2222) ── Digit 2 Common Cathode
├── GPIO5  ──[1K]── Q3 (2N2222) ── Digit 3 Common Cathode
└── GPIO4  ──[1K]── Q4 (2N2222) ── Digit 4 Common Cathode
```

Full pin table: [`pcb/pin_connections.md`](pcb/pin_connections.md)

---

## PCB Design

- Designed in **EasyEDA**
- 2-layer board (Top: signal traces, Bottom: GND pour)
- Decoupling capacitors placed close to VCC pins of each IC
- Gerber files ready for JLCPCB / PCBWay fabrication

📁 [`pcb/gerbers/`](pcb/gerbers/) — submit to any PCB manufacturer

---

## Software

### Dependencies (Arduino IDE)

Install via Library Manager:
- `RTClib` by Adafruit

### How to Flash

1. Open `firmware/esp32_rtc_clock.ino` in Arduino IDE
2. Select board: **ESP32 Dev Module**
3. Set Upload Speed: `115200`
4. Flash and open Serial Monitor at `115200 baud`

---

## How It Works

1. On boot, ESP32 initializes I2C and checks DS3231
2. If RTC lost power, time is auto-set to compile time
3. Every 1 second, ESP32 reads HH:MM from DS3231 over I2C
4. The 4 digits are **multiplexed** — each digit is ON for 2ms in rotation (fast enough for persistence of vision)
5. Segment patterns are sent to the **74HC595** via SPI-like shift register protocol
6. Colon blinks every 500ms using the dp segment of digit 2

---

## Serial Monitor Output

```
ESP32 RTC Clock Starting...
RTC OK. Display running.
Time: 10:35:42 | Temp: 28.5 C
Time: 10:35:43 | Temp: 28.5 C
```

---

## Project Structure

```
esp32-rtc-clock/
├── firmware/
│   └── esp32_rtc_clock.ino     # Main Arduino firmware
├── pcb/
│   ├── BOM.csv                 # Bill of Materials
│   ├── pin_connections.md      # Wiring reference table
│   └── gerbers/                # Gerber files for PCB fabrication
│       ├── esp32_rtc_clock-F_Cu.gtl
│       ├── esp32_rtc_clock-B_Cu.gbl
│       ├── esp32_rtc_clock-F_SilkS.gto
│       ├── esp32_rtc_clock-Edge_Cuts.gm1
│       └── esp32_rtc_clock.drl
└── README.md
```

---

## Author

**Yash Bachhav**
B.E. Electronics & Telecommunication, LGNSCOE Nashik
- GitHub: [github.com/bachhavyash](https://github.com/bachhavyash)
- LinkedIn: [linkedin.com/in/yash-bachhav-4a54b0253](https://www.linkedin.com/in/yash-bachhav-4a54b0253/)

---

## License

MIT License — free to use, modify, and share with attribution.
