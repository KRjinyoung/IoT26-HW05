# 🏠 Raspberry Pi 4 & Home Assistant GPIO Control (HW5)

This project implements a smart home control system using Home Assistant (HA) installed on a Raspberry Pi 4.  
The system runs in a Docker container and controls GPIO pins to operate LEDs and external devices.

![Operation Result Screenshot](./images/capture.png)

---

## 🛠️ Development Environment

- **Hardware**: Raspberry Pi 4
- **OS**: Raspberry Pi OS (64-bit)
- **Platform**: Home Assistant Core (Docker Container)
- **Integration**: `rpi_gpio` (Custom Component)

---

## 🎬 Demo Video

https://youtube.com/shorts/8EMWgGG7DFY?feature=share

https://github.com/user-attachments/assets/62d44536-d774-40ea-b8c4-9a91d2416cdc

---

## 🔌 Hardware Setup (Wiring)

The GPIO pins were connected as shown below to control LEDs and external devices.

| Component | BCM Pin | Physical Pin | Description |
|-----------|---------|--------------|-------------|
| **LED 1** | GPIO 11 | Pin 23       | Fan Office  |
| **LED 2** | GPIO 12 | Pin 32       | Light Desk  |

> **Note:** A 220Ω resistor was connected in series with each output pin to protect the LEDs.

---

## ⚙️ Configuration

The following switch control settings were added to the `configuration.yaml` file in Home Assistant.

```yaml
# configuration.yaml
switch:
  - platform: rpi_gpio
    ports:
      11: Fan Office
      12: Light Desk
```

---

## 🐳 Docker Run Command (Deployment)

The Home Assistant container was launched using the following command.  
The `--privileged` option was used to allow GPIO hardware access, and the configuration directory was mounted to preserve settings.

```bash
docker run -d \
  --name homeassistant \
  --privileged \
  --restart=unless-stopped \
  -e TZ=Asia/Seoul \
  -v ~/homeassistant/config:/config \
  --network=host \
  ghcr.io/home-assistant/home-assistant:stable
```

---
