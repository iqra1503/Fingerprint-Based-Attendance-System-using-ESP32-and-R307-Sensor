# Fingerprint-Based Attendance System using ESP32 and R307 Sensor

## 📌 Overview

The **Fingerprint-Based Attendance System** is a biometric attendance solution designed using an **ESP32 microcontroller**, **R307 fingerprint sensor**, and a **web-based frontend** for real-time attendance visualization. This project currently simulates fingerprint matching through a browser interface but is structured for future integration with real hardware and backend systems.

This system replaces traditional manual attendance with a **secure, automated, scalable** biometric workflow.

---

## 🚀 Features

* **Simulated fingerprint enrollment & matching**
* **Dynamic student registration** via modal form
* **Real-time attendance tracking**
* **Present / Absent statistics** displayed instantly
* **CSV export feature** for attendance records
* **Responsive user interface** for desktop and mobile
* **Ready for hardware integration (ESP32 + R307)**

---

## 🛠️ System Architecture

### Current Implementation

* HTML, CSS, JavaScript frontend
* Simulation of fingerprint matching using randomized IDs
* Local temporary storage of attendance data
* CSV export module

### Planned Hardware/Backend Integration

* ESP32 + R307 fingerprint sensor
* MySQL / cloud database
* Secure login/authentication
* Excel/PDF export
* Deployment on Firebase/GitHub Pages

---

## 🔧 Hardware Components (Future Integration)

* **ESP32 Dev Board**
* **R307 Fingerprint Sensor**
* Breadboard & jumper wires
* 5V power supply / USB

### 🧩 Fingerprint Sensor (R307) to ESP32 Connections

| R307 Pin       | ESP32 Pin |
| -------------- | --------- |
| VCC            | 3.3V / 5V |
| GND            | GND       |
| TX             | GPIO 17   |
| RX             | GPIO 16   |
| RST (optional) | EN pin    |

---

## ⚙️ Working Principle

1. Students are added through the web interface.
2. Each student receives a unique simulated fingerprint ID.
3. When "Scan Finger" is pressed, the system randomly assigns a fingerprint match.
4. Attendance is recorded with timestamp.
5. Statistics update instantly on the dashboard.
6. Attendance can be exported as a CSV file.

---

## 💻 Arduino Code (For Real Hardware Integration)

The project includes full ESP32 code for:

* Fingerprint enrollment
* Model creation & storage
* Fingerprint matching
* Real-time match feedback over serial

> The complete Arduino code is available in the project report.

---

## 🖥️ Frontend Features

* Add student form
* Fingerprint scan simulation
* Present/Absent count
* CSV export
* Status indicators for:

  * System
  * ESP32 connection
  * Database connection

---

## 📤 CSV Export Example

```
Name, Roll, Status, Timestamp
Iqra, 2110030, Present, 2025-07-26 10:32 AM
```

---

## 📈 Software Integration

### Components

* ESP32 → Backend (future)
* Backend → Frontend
* Database → Export/Analytics
* Optional mobile app

### Communication Methods

* REST API / MQTT (planned)
* HTTPS secure transport

---

## 🧪 Results

* Student registration successful
* Fingerprint matching simulated correctly
* Real-time attendance statistics functioning
* CSV export verified
* Fully responsive UI

---

## ⭐ Advantages

* Accurate simulation of biometric attendance
* Fast & secure process
* Portable, offline-ready
* Scalable architecture
* Future-ready for IoT hardware

---

## ⚠️ Limitations

* No backend (data resets on refresh)
* No authentication yet
* Hardware integration pending

---

## 🔮 Future Enhancements

* ESP32 + R307 real-time integration
* MySQL/PHP backend
* Admin login system
* Excel/PDF export
* Deployment on cloud platforms

---

## 📝 Conclusion

This project demonstrates a complete simulation of a fingerprint attendance system and provides a strong foundation for building a **full biometric IoT-based attendance solution**. With planned integration of ESP32 hardware, cloud storage, and secure authentication, the system is capable of becoming a reliable, scalable attendance management tool.

---

## 📚 References

* DonskyTech – ESP32 & R307 tutorials
* Adafruit Fingerprint Sensor Library
* ESP32 IoT guides and documentation

---
