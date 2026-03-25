
# 📡 UDP Pulse Monitor v1.0
> **A high-performance, real-time UDP payload analytics dashboard built with PySide2.**

[![Python](https://img.shields.io/badge/Python-3.8+-blue?logo=python)](https://www.python.org/)
[![Framework](https://img.shields.io/badge/Framework-PySide2-green?logo=qt)](https://pypi.org/project/PySide2/)
[![Protocol](https://img.shields.io/badge/Protocol-UDP-orange)](#)
[![Status](https://img.shields.io/badge/Status-Operational-brightgreen)](#)

---

## 🔍 What is this Code?
**UDP Pulse Monitor** is a professional-grade diagnostic tool designed to intercept, monitor, and analyze UDP (User Datagram Protocol) traffic on a specific port. It provides a real-time graphical interface that visualizes incoming payload sizes and cumulative data consumption.

The application utilizes a **Multithreaded Architecture**, separating the network socket listener (back-end) from the UI event loop (front-end) to ensure the interface remains responsive even under high-frequency data bursts.

---

## 🚀 Why Use It?
Standard command-line tools can be difficult to read during rapid data transmission. This dashboard provides:
* **Visual Clarity:** Instant readout of the latest payload size in bytes.
* **Traffic Accumulation:** Automatic conversion of total received data into MB and GB.
* **Non-Blocking Logic:** A dedicated `QThread` handles the socket binding, preventing UI freezes.
* **Live Logging:** A persistent log window tracking every incoming packet.

---

## 💎 Importance
In network debugging and IoT development:
1.  **Bandwidth Monitoring:** Track exactly how much data a device or application is pushing over the network.
2.  **Packet Verification:** Confirm that datagrams are reaching the host and verify their size.
3.  **Stress Testing:** Monitor host performance when subjected to high-volume UDP streams.

---

## ⚙️ How It Works
The monitor operates via a **Signal-Slot Communication Pipeline**:

1.  **The Listener:** The `UDPReceiver` class initializes a low-level Python `socket`. It binds to `0.0.0.0` (all interfaces) on Port `1600`.
2.  **Payload Extraction:** When a datagram is detected, the socket captures the raw bytes using a buffer size of 65,535 (the maximum theoretical UDP packet size).
3.  **Signal Emission:** The data is emitted as a `Signal(bytes)` to the main window.
4.  **Data Processing:** The GUI receives the signal, updates the `total_bytes` counter, calculates MB/GB metrics, and appends the event to the log.

---

## 📊 Comparison: Pulse Monitor vs. CLI

| Feature | standard `netcat` | Pulse Monitor |
| :--- | :--- | :--- |
| **UI** | Text Stream | Dashboard Widgets |
| **Unit Conversion** | Manual | Auto (MB/GB) |
| **History** | Volatile | Persistent Text Log |
| **Interaction** | Command Line | GUI Window |
| **Stability** | Single Threaded | Multithreaded (Qt) |

---

## 🛠️ Installation & Setup

### 1. Prerequisites
* **Python 3.8+**
* **Qt for Python (PySide2)**

### 2. Install Dependencies
```bash
pip install PySide2
```

### 3. Clone & Run
```bash
git clone https://github.com/vikrant-project/UDP-Pulse-Monitor
cd UDP-Pulse-Monitor
python3 udp_monitor.py
```

---

## 🎨 High-End UI Features
* **Grid Alignment:** Clean layout with dedicated status and metric zones.
* **Real-time Metrics:** High-precision floating-point math for data accumulation.
* **Thread Safety:** Graceful shutdown of the receiver thread on application close to prevent port-binding hangups.

---
**Disclaimer:** This tool is for network diagnostic and development purposes only. Ensure you have the necessary permissions to monitor traffic on your network.
I have configured the code to listen on Port **1600**. If you need to monitor a different service, you can simply change the `port=1600` argument in the `MainWindow` class.

**Would you like me to add a "Save Log to File" button so you can export your captured session data?**
