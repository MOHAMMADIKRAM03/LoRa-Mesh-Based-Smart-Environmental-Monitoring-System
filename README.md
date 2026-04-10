# 🌐 LoRa Mesh-Based Smart Environmental Monitoring System

[![GitHub Repo](https://img.shields.io/badge/GitHub-Repository-black?logo=github)](https://github.com/MOHAMMADIKRAM03/LoRa-Mesh-Based-Smart-Environmental-Monitoring-System)
![Platform](https://img.shields.io/badge/Platform-ESP32--S3-blue)
![Communication](https://img.shields.io/badge/Communication-LoRa%20Mesh-green)
![Protocol](https://img.shields.io/badge/Protocol-MQTT-orange)

---

## 🚀 Overview

A **distributed IoT monitoring system** using **LoRa Mesh networking** with multiple sensor nodes and a central master node that aggregates data and publishes it to an **MQTT broker**.

### 🌍 Monitored Domains:

* 💧 Water Quality
* 🚻 Washroom Hygiene
* 🌤 Weather Conditions
* 🌫 Outdoor Air Quality

Designed for **smart cities, environmental monitoring, and industrial IoT applications**.

---

## 📡 System Architecture

![System Diagram](docs/system-diagram.png)

```
[ WATER NODE ] ----\
[ WEATHER NODE ] ---\ 
[ WASHROOM NODE ] ----> LoRa Mesh → MASTER NODE → MQTT → Cloud / Dashboard
[ AIR NODE ] ------/
```

---

## 🧠 How It Works

### 🔹 Node Side

* Collects sensor data
* Converts JSON → HEX
* Sends via LoRa (LR71)

### 🔹 Master Node (ESP32-S3)

* Receives LoRa packets
* Decodes HEX → JSON
* Identifies source node
* Publishes to MQTT topics

---

## 🧩 Nodes Description

### 💧 Water Quality Node (`0002`)

**Sensors:**

* pH Sensor
* TDS Sensor
* Turbidity Sensor
* DS18B20
<p align="center">
  <img src="https://github.com/user-attachments/assets/35026469-a1e8-4002-97b0-27b87e14dbcc" width="350"/>
  <img src="https://github.com/user-attachments/assets/9eaaeee2-9aec-4718-bd4f-71510f922d63" width="350"/>
</p>


**Outputs:**

* Temperature, pH, TDS, Turbidity

---

### 🌤 Weather Node (`0006`)

**Sensors:**

* SparkFun Weather Meter Kit
* BME280

**Outputs:**

* Temperature, Humidity, Pressure
* Wind Speed & Direction
* Rainfall

---

### 🚻 Washroom Hygiene Node (`0004`)

**Sensors:**

* MQ136 (H₂S)
* MQ137 (NH₃)
* CCS811 (CO₂, TVOC)
<p align="center">
  <img src="https://github.com/user-attachments/assets/df8b5742-6c37-4caf-96d7-2c3048a77f7b"  width="350"/>
  <img src="https://github.com/user-attachments/assets/7ce47c0d-6c6b-4e8a-97bf-4a34c2c0096d"width="350"/>
</p>
**Outputs:**

* Gas concentrations
* Hygiene Index
* Status (EXCELLENT → CRITICAL)

---

### 🌫 Outdoor Air Quality Node (`0007`)

**Sensors:**

* SPS30 → PM1, PM2.5, PM10
* SHT4x → Temp & Humidity
* SGP41 → VOC & NOx
* Senseair S8 → CO₂
<p align="center">
  <img src="https://github.com/user-attachments/assets/c5078670-742f-4be8-a0ef-70ed37dac254" width="800"/>
</p>

**Outputs:**

* Air Quality Metrics
* Gas Indices
---

## 🔌 Hardware

* ESP32-S3 (Nodes + Master)
* LR71 LoRa Module
* Environmental Sensors
* Solar Power System (Outdoor Node)

---

## 🔄 Data Flow

### 📤 Transmission

```
JSON → HEX → LoRa TX
```

Example:

```
{src:0002,temp:25.4,ph:7.1,tds:320,turb:120}
```

---

### 📥 Master Processing

```
HEX → JSON → MQTT Publish
```

---

## 📡 MQTT Topics

| Topic         | Data Type     |
| ------------- | ------------- |
| water/data    | Water Quality |
| weather/data  | Weather Data  |
| washroom/data | Hygiene Data  |
| air/data      | Air Quality   |

---

## 📊 Example Output

```
📡 RAW:
at+recv=0002 7B7372633A303030322C74656D703A32352E347D

✅ DECODED:
{src:0002,temp:25.4,ph:7.1,tds:320,turb:120}
```

---

## 🛠 Setup Guide

### 1️⃣ Clone Repository

```
git clone https://github.com/MOHAMMADIKRAM03/LoRa-Mesh-Based-Smart-Environmental-Monitoring-System.git
```

---

### 2️⃣ Install Libraries

**Arduino:**

* OneWire
* DallasTemperature
* PubSubClient
* SparkFun Weather Kit
* SparkFun BME280

**ESP-IDF (Washroom Node):**

* FreeRTOS
* ADC Driver
* I2C Driver

---

### 3️⃣ Configure WiFi & MQTT

```cpp
const char* ssid = "YOUR_WIFI";
const char* password = "YOUR_PASSWORD";
const char* mqtt_server = "BROKER_IP";
```

---

### 4️⃣ Upload Firmware

* Flash node codes individually
* Upload master node
* Power the system

---

## 📈 Features

✔ LoRa Mesh Communication
✔ Multi-node Distributed System
✔ Real-time MQTT Streaming
✔ Environmental Monitoring
✔ Scalable Architecture
✔ Edge Processing
✔ Low Power Design

---

## 🌍 Applications

* Smart Cities
* Industrial Monitoring
* Environmental Research
* Public Hygiene Systems
* IoT Data Analytics

---

## 🔮 Future Scope

* 📊 Dashboard (Node-RED / Grafana)
* ☁️ Cloud Integration (AWS / Firebase)
* 📱 Mobile App
* 🧠 AI Predictions
* 📡 LoRaWAN Upgrade

---

## 👨‍💻 Author

**Mohammad Ikram**
B.Tech IoT — KL University

---

## ⭐ Support

If you like this project:

⭐ Star the repo
🍴 Fork it
📢 Share it

---

## 📬 Contact

* GitHub: https://github.com/MOHAMMADIKRAM03
* Email: [your-email@example.com](mailto:your-email@example.com)
