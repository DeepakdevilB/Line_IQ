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
  ESP32 Node 1 ←─── UART ───→ ESP32 Node 2
  ACS712 Sensor               ACS712 Sensor
  Relay Module                
       |                            
       └───── Wi-Fi ─────→ Central Dashboard (Live Graphs & Relay Status)
```

---

## ⚙️ Fault Detection Logic

```cpp
// Simplified detection logic in pole1.ino
if (currentPole1 > OVERCURRENT_THRESHOLD || currentPole2 == 0) {
    // Trip the relay immediately (Simulated Line Fault or Overcurrent)
    digitalWrite(RELAY_PIN, HIGH); 
    notifyDashboard("GRID FAULT DETECTED - POWER ISOLATED");
}
```

---

## 🔧 Setup & Flashing

### Prerequisites
- Arduino IDE 2.x
- ESP32 board package installed ([Installation Guide](https://docs.espressif.com/projects/arduino-esp32/en/latest/installing.html))
- Required library: `EmonLib`

### Steps

1. **Clone this repository**
   ```bash
   git clone https://github.com/DeepakdevilB/Line_IQ.git
   ```

2. **Open Arduino IDE** and install the ESP32 board package.

3. **Configure Wi-Fi credentials** in `pole1/pole1.ino`:
   ```cpp
   const char* ssid = "YOUR_WIFI_SSID";
   const char* password = "YOUR_WIFI_PASSWORD";
   ```

4. **Flash `pole1.ino`** to the first ESP32 board (Master Hub).

5. **Flash `pole2.ino`** to the second ESP32 board (Sensor Node).

6. **Connect Hardware:** Wire the UART connection (G17 to G16) between the boards and connect the ACS712 and Relay in series with the AC load.

7. **Access Dashboard:** Connect your device to the Wi-Fi hotspot and navigate to the IP address printed in the Serial Monitor (e.g., `http://10.63.44.228`) to view the live SCADA dashboard!

---

## 📊 System Advantages

| Feature | Traditional Circuit Breaker | This System |
|---|---|---|
| LT Line Break Detection | ❌ Cannot detect | ✅ Detects accurately via node timeouts |
| Fault Location | ❌ Manual inspection | ✅ Node-level precision |
| Auto Isolation | ✅ Overcurrent only | ✅ Line break + overcurrent |
| Real-time Alerts | ❌ None | ✅ Live SCADA Dashboard |
| Cost | Low | Low (ESP32 ~$5 each) |

---

## 🚀 Future Improvements

- [x] Web dashboard with live sensor graphs
- [x] Automatic fault isolation via timeout
- [ ] SMS/Email alerts via Twilio or SMTP
- [ ] GPS-based precise fault location
- [ ] Solar-powered field deployment

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
