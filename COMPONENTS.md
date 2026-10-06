# Smart LT Line Fault Detection - Hardware Components

This document lists the final hardware components used for the physical prototype demonstration of the **Line_IQ** system.

## 🧠 Core Processing & Sensing
| Component | Quantity | Purpose |
|---|---|---|
| **ESP32 Wroom (38-pin)** | 2 | Main microcontrollers for Pole 1 (Master/Dashboard) and Pole 2 (Slave). |
| **ACS712 Current Sensor** | 2 | Measures the live analog current (Amps) flowing through the power line. *(Note: Replaced the original CT Relay modules to allow for real-time dashboard data).* |
| **5V Relay Module (1 or 2 Channel)** | 1 | Acts as the smart circuit breaker on Pole 1 to physically cut AC power when a fault is detected. |

## 🔌 Power & Prototyping
| Component | Quantity | Purpose |
|---|---|---|
| **Breadboards** | 2 | Solderless base for wiring the sensors and ESP32s. |
| **Jumper Wires** | 1 Set | Male-to-Male and Male-to-Female wires for connections. |
| **Micro-USB / USB-C Cables** | 2 | Used to flash code from the Arduino IDE and power the ESP32s during the demo. |

## 💡 The Physical "Power Grid" Model
| Component | Quantity | Purpose |
|---|---|---|
| **Incandescent Bulb (60W or 100W)** | 1 | Acts as the "house" (load) at the end of the line. We use an incandescent bulb because it draws enough current (~0.25A to 0.4A) for the ACS712 sensors to clearly detect and display on the dashboard. |
| **Bulb Holder** | 1 | To mount the light bulb. |
| **AC Wire / Cable** | 1 Set | To run between the poles, simulating the live LT (Low Tension) power line. |
| **AC Mains Wall Plug (2-pin or 3-pin)** | 1 | To safely connect the grid model to a real wall socket for the demo. |
| **Wooden Poles (15cm)** | 2 | Used as physical props to simulate the street utility poles. |
| **Insulation Tape** | 1 Roll | **CRITICAL SAFETY ITEM.** Used to securely cover any exposed AC wire connections to prevent shocks. |

## 📡 Optional / Aesthetic Components
*(These were purchased for the project and can be mounted on the breadboards for visual complexity during the hackathon pitch, even if not actively driving the core relay logic).*
*   **Voltage Sensors (ZMPT101B)** x2
*   **Vibration Sensors** x2
*   **GPS Module** x1
