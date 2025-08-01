---
layout: page
title: IoT Temperature Sensor
description: Raspberry Pi-based temperature monitoring system with real-time data transfer and visualization.
img: assets/img/iot-temp.png
importance: 1
category: fun
---

This project is an **IoT Temperature Sensor** system implemented using a Raspberry Pi, focused on providing real-time and historical temperature readings for monitoring environments. Data is transmitted at regular intervals using a combination of efficient networking and messaging protocols, and visualized for immediate insights.

The solution leverages multiple technologies:
- **gRPC** for fast, efficient device-to-server data transfer.
- **MQTT** for lightweight publish/subscribe messaging between devices and receivers.
- **MS SQL Server** for robust time-series data storage.
- **C#** for the back-end service logic, handling ingestion and data persistence.
- **Python** for front-end system interaction and input management.
- **Power BI** for live and historical dashboard visualization.

[🔗 View the code on GitHub](https://github.com/hero1601/IOT-Temperature)

---

### Project Goals

- Automate and digitize household temperature tracking for improved comfort and safety.
- Achieve dependable, low-latency data delivery across the home network.
- Build a scalable pipeline from sensing to user dashboarding.
- Enable alerts for abnormal temperature fluctuations.

---

### System Architecture

<div class="col-sm mt-3 mt-md-0" style="text-align: center">
    {% include figure.liquid path="assets/img/iot-arch.png" class="img-fluid rounded z-depth-1 w-50"%}
</div>

*Raspberry Pi → gRPC (C# backend) → MS SQL Server, MQTT broker for real-time notifications, Power BI for analytics.*

- **Hardware:** Raspberry Pi with a temperature sensor placed in the living area.
- **Communication:** gRPC for direct backend communication, MQTT for broadcast updates.
- **Storage & Backend:** C# server persists data to MS SQL Server.
- **Frontend/Data collection:** Python scripts handle data acquisition and send readings.
- **Visualization:** Power BI dashboards accessible from anywhere in the home network.

---

### Implementation Details

- **Data Collection:** The Raspberry Pi reads and sends temperature data every 3–5 minutes.
- **Home Integration:** The device monitors ambient temperature in your living space and detects rapid changes.
- **Notifications:** If temperature thresholds are crossed (e.g., room gets unusually hot), MQTT-based instant alerts sent to any subscribed device (such as your phone or a smart display).
- **Storage & Visualization:** All records are time-stamped and stored in SQL. Power BI dashboards display current and historical readings, letting you view patterns (e.g., daytime heat, night cooling).

---

### Challenges & Solutions

- Ensured **low latency** for timely in-home alerts using gRPC and MQTT.
- Integrated all components (sensor, C# backend, SQL Server, Power BI) with clear APIs to operate seamlessly within a home Wi-Fi network.
- Maintained **messaging reliability** by configuring MQTT QoS and resilient reconnection strategies.
- Designed for **plug-and-play extensibility** to support additional sensors or expand monitoring to other rooms.

---

### Results & Impact

- **Consistent temperature monitoring** provided peace of mind and enabled proactive climate control.
- **Automated alerts** reduced risk of uncomfortable or damaging temperature extremes—especially during heatwaves.
- **Accessible dashboards** empowered household members to participate in managing home comfort.
- **Energy efficiency** gains by aligning HVAC/fan use with real data, not just guesswork.

---

### Key Takeaways

- Combining **gRPC and MQTT** delivers reliable, efficient communication for home IoT.
- Power BI enables quick deployment of informative dashboards, even on a small home network.
- Proactive environmental monitoring enhances comfort, saves energy, and increases home safety.
- Raspberry Pi and open protocols enable powerful custom smart home solutions on an affordable budget.