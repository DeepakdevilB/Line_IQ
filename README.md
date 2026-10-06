<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=24,20,12&height=200&section=header&text=Smart%20LT%20Line%20Fault%20Detection&fontSize=40&fontColor=ffffff&animation=fadeIn&fontAlignY=38&desc=IoT%20%7C%20ESP32%20%7C%20Real-Time%20Fault%20Monitoring&descAlignY=58&descAlign=62" />

  <br />

  [![C++](https://img.shields.io/badge/C++-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white)](https://isocpp.org/)
  [![ESP32](https://img.shields.io/badge/ESP32-E7352C?style=for-the-badge&logo=espressif&logoColor=white)](https://espressif.com/)
  [![Arduino](https://img.shields.io/badge/Arduino-00979D?style=for-the-badge&logo=arduino&logoColor=white)](https://www.arduino.cc/)
</div>

---

## ⚡ About

**Line_IQ -** A **Smart Line Fault Detection & Monitoring System** designed for **Low Tension (LT) power lines** using **ESP32 microcontrollers**. The system detects line faults, locates their position, and automatically isolates the faulty section while sending real-time alerts to the control center.

> Developed by **Team Runtime Hackers** — addressing the critical gap where traditional circuit breakers fail to detect LT line breaks.

---

## 🔌 Working Principle

1. **ACS712 Current Sensors** at each pole continuously measure the RMS current flowing through the LT power line
2. **ESP32 Node 1 (Pole 1 — Master Hub)** reads its own sensor, hosts the live SCADA web dashboard over Wi-Fi, and monitors Pole 2's health via UART
3. **ESP32 Node 2 (Pole 2 — Sensor Node)** reads its sensor and transmits the current data to Pole 1 over a hardwired UART serial link
4. If Pole 1 detects **overcurrent** or **loses communication** with Pole 2 (4-second timeout), it automatically **trips the relay** to isolate the faulty section
5. The live web dashboard displays real-time current graphs for both poles, relay status, and fault alerts — accessible from any device on the network

---

## 🛠️ Hardware Components

| Component | Quantity | Purpose |
|---|---|---|
| ESP32 Wroom (38-pin) | 2 | Main microcontrollers — Pole 1 (Master/Dashboard) & Pole 2 (Sensor Node) |
| ACS712 Current Sensor (5A) | 2 | Measures live AC current (Amps) at each pole |
| 5V Relay Module | 1 | Smart circuit breaker — physically cuts AC power on fault detection |
| Incandescent Bulb (60W/100W) | 1 | Simulates the household load at the end of the line |
| Bulb Holder | 1 | Mounts the light bulb |
| AC Wire / Cable | 1 set | Simulates the LT power line between poles |
| 3-Pin AC Plug | 1 | Safe connection to mains power |
| Breadboards | 2 | Solderless prototyping base |
| Jumper Wires | 1 set | Male-to-Male and Male-to-Female connections |
| USB Cables | 2 | Flashing code & powering ESP32s |

> See [`COMPONENTS.md`](COMPONENTS.md) for detailed wiring diagrams and pin mappings.

---

## 📁 Project Files

| File | Description |
|---|---|
| `pole1/pole1.ino` | Master Hub — hosts the SCADA web dashboard, reads Pole 1 sensor, receives Pole 2 data over UART, controls the relay |
| `pole2/pole2.ino` | Sensor Node — reads Pole 2 sensor and transmits current data to Pole 1 via UART |
| `COMPONENTS.md` | Detailed hardware list, wiring overview, and pin mapping |

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

<div align="center">
  Made with ❤️ by Deepak Sharma & Team Runtime Hackers
</div>
