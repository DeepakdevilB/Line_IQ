<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=24,20,12&height=200&section=header&text=Smart%20LT%20Line%20Fault%20Detection&fontSize=40&fontColor=ffffff&animation=fadeIn&fontAlignY=38&desc=IoT%20%7C%20ESP32%20%7C%20Real-Time%20Fault%20Monitoring&descAlignY=58&descAlign=62" />

  <br />

  [![C++](https://img.shields.io/badge/C++-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white)](https://isocpp.org/)
  [![ESP32](https://img.shields.io/badge/ESP32-E7352C?style=for-the-badge&logo=espressif&logoColor=white)](https://espressif.com/)
  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)
</div>

---

## ⚡ About

**Line_IQ -** A **Smart Line Fault Detection & Monitoring System** designed for **Low Tension (LT) power lines** using **ESP32 microcontrollers**. The system detects line faults, locates their position, and automatically isolates the faulty section while sending real-time alerts to the control center.

> Developed by **Team Runtime Hackers** — addressing the critical gap where traditional circuit breakers fail to detect LT line breaks.

---

## 🔌 Working Principle

1. **Sensors** at each LT pole continuously measure current, voltage, and vibration
2. **ESP32 Node 1 (`pole1.ino`)** detects abnormal readings and identifies potential line breaks
3. **ESP32 Node 2 (`pole2.ino`)** receives the signal, triggers the **relay** to isolate the faulty section
4. Both nodes log data and send real-time alerts to a **central dashboard** via Wi-Fi
5. Fault location is estimated using timing differences between node responses

---

## 🛠️ Hardware Components

| Component | Quantity | Purpose |
|---|---|---|
| ESP32 Microcontroller | 2 | Main processing & Wi-Fi |
| Current Transformer (CT) Sensor | 1 per node | Current monitoring |
| Voltage Sensor | 1 per node | Voltage monitoring |
| Vibration Sensor | 1 per node | Line break vibration detection |
| Relay Module | 1 | Auto fault isolation |
| GPS Module *(optional)* | 1 | Precise fault location |
| Power Supply / Solar Module | 1 | Field deployment power |
| Jumper Wires & Breadboard | - | Prototyping |

---

## 📁 Project Files

| File | Description |
|---|---|
| `pole1.ino` | Main ESP32 node — monitors sensors, detects faults, transmits data to control center |
| `pole2.ino` | Secondary ESP32 node — receives fault signals, controls relay for section isolation |

---

## 📡 System Architecture

```
LT Power Line
     |
  [Pole 1]                    [Pole 2]
  ESP32 Node 1 ←─── Wi-Fi ───→ ESP32 Node 2
  CT Sensor                    Relay Module
  Voltage Sensor               CT Sensor
  Vibration Sensor             Voltage Sensor
       |                            |
       └──────── Central Dashboard (Real-Time Alerts) ────────┘
```

---

## ⚙️ Fault Detection Logic

```cpp
// Simplified detection logic in pole1.ino
if (current < FAULT_THRESHOLD || vibration > VIBRATION_THRESHOLD) {
    sendFaultAlert(pole2);         // Notify secondary node
    logFaultData(timestamp, readings);
    notifyDashboard(faultDetails);
}
```

---

## 🔧 Setup & Flashing

### Prerequisites
- Arduino IDE 2.x
- ESP32 board package installed ([Installation Guide](https://docs.espressif.com/projects/arduino-esp32/en/latest/installing.html))
- Required libraries: `WiFi.h`, `HTTPClient.h`

### Steps

1. **Clone this repository**
   ```bash
   git clone https://github.com/mystzoro/LT_Linefault-Detection.git
   ```

2. **Open Arduino IDE** and install the ESP32 board package

3. **Configure Wi-Fi credentials** in both `.ino` files:
   ```cpp
   const char* ssid = "YOUR_WIFI_SSID";
   const char* password = "YOUR_WIFI_PASSWORD";
   ```

4. **Flash `pole1.ino`** to the first ESP32 board

5. **Flash `pole2.ino`** to the second ESP32 board

6. **Connect sensors** per the hardware table above

7. **Power both nodes** and monitor the serial output

---

## 📊 System Advantages

| Feature | Traditional Circuit Breaker | This System |
|---|---|---|
| LT Line Break Detection | ❌ Cannot detect | ✅ Detects accurately |
| Fault Location | ❌ Manual inspection | ✅ Estimated automatically |
| Auto Isolation | ✅ Overcurrent only | ✅ Line break + overcurrent |
| Real-time Alerts | ❌ None | ✅ Dashboard + notification |
| Cost | Low | Low (ESP32 ~$5 each) |

---

## 🚀 Future Improvements

- [ ] SMS/Email alerts via Twilio or SMTP
- [ ] Web dashboard with live sensor graphs
- [ ] GPS-based precise fault location
- [ ] Solar-powered field deployment
- [ ] Machine learning for predictive fault detection

---

## 👥 Team

**Team Runtime Hackers**

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

<div align="center">
  Made with ❤️ by Deepak Sharma & Team Runtime Hackers
</div>
