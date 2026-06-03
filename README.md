# ESP32 RTC Clock with DS3231 & 4-Digit 7-Segment Display

## Overview

A real-time digital clock built using **ESP32-WROOM-32**, **DS3231 RTC module**, and a **4-digit 7-segment display** driven through a **74HC595 shift register**.

The system reads accurate time data from the DS3231 over I2C communication and continuously displays the current time in **HH:MM** format using multiplexed 7-segment control.

This project demonstrates:

* Embedded C/C++ programming
* I2C communication
* RTC interfacing
* Shift register control
* Multiplexed display driving
* Real-time embedded system design

---

## Hardware Used

* ESP32-WROOM-32
* DS3231 RTC Module
* 4-Digit 7-Segment Display
* 74HC595 Shift Register
* Breadboard / Custom PCB
* Jumper Wires
* USB Power Supply

---

## Features

* Real-time clock display
* Accurate DS3231 timekeeping
* Blinking colon effect
* Multiplexed 7-segment control
* Serial debugging output
* Automatic RTC recovery after power loss
* Low GPIO usage using shift register

---

## Working Principle

1. ESP32 communicates with DS3231 using I2C protocol.
2. Current time is read every second.
3. Time is converted into HH:MM digits.
4. Digits are displayed using multiplexing technique.
5. 74HC595 shift register controls segment data efficiently.

---

## Pin Configuration

| ESP32 Pin | Function             |
| --------- | -------------------- |
| GPIO26    | SDA (DS3231)         |
| GPIO27    | SCL (DS3231)         |
| GPIO23    | Shift Register Data  |
| GPIO22    | Shift Register Latch |
| GPIO21    | Shift Register Clock |
| GPIO19    | Digit 1 Select       |
| GPIO18    | Digit 2 Select       |
| GPIO5     | Digit 3 Select       |
| GPIO4     | Digit 4 Select       |

---

## Serial Monitor Output

```text
ESP32 RTC Clock Starting...
RTC OK. Display running.

Time: 09:41:00 | Temp: 29.5 C
Time: 09:41:01 | Temp: 29.5 C
```

---

## Technologies Used

* Embedded C++
* Arduino Framework
* ESP32
* I2C Communication
* RTC Systems
* Digital Electronics

---

## Future Improvements

* 12H / 24H mode selection
* Alarm functionality
* Automatic brightness control
* WiFi time synchronization (NTP)
* PCB implementation
* Battery backup monitoring

---

## Author

**Yash Bachhav**
Electronics & Telecommunication Engineering
Embedded Systems | IoT | Hardware Design
