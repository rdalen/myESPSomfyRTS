# myESPSomfyRTS

A DIY Somfy RTS controller for my SunRain Awning/Shade, based on the open-source [ESPSomfyRTS](https://github.com/rstrouse/ESPSomfy-RTS) project.

The controller uses an ESP32 together with a CC1101 433 MHz RF transceiver and integrates with my Home Assistant and Node-RED setup.

## How It Works

- **Hardware:** ESP32 microcontroller paired with a CC1101 radio transceiver module.
- **Communication:** Connects to my home Wi-Fi network and sends 433 MHz radio signals compatible with the Somfy RTS (Radio Technology Somfy) protocol.
- **Local Operation:** ESPSomfyRTS provides a built-in web interface for controlling the shade directly from a phone or computer.
- **Smart Home Integration:** The controller integrates with Home Assistant and Node-RED for automation and monitoring.
- **Position Tracking:** Tracks the shade position independently of the physical Somfy remote.

For the firmware, general wiring information and ESPSomfyRTS documentation, see the official [ESPSomfyRTS project](https://github.com/rstrouse/ESPSomfy-RTS).

An instruction video is available on [YouTube](https://www.youtube.com/watch?v=1acVJ0xWJgs).

---

## Repository Contents

This repository contains the files specific to my implementation:

- 📁 **[KiCad](./KiCad)** — Schematic and PCB design files
- 📁 **[nodeRed](./nodeRed)** — Node-RED flows used for control, monitoring and automation

The ESP32 firmware itself is based on the [ESPSomfyRTS](https://github.com/rstrouse/ESPSomfy-RTS) project.

---

## CC1101 433 MHz RF Transceiver

<img width="50%" alt="CC1101 RF transceiver" src="https://github.com/user-attachments/assets/90fb8032-c2f1-48a3-870c-ac696d3649e5" />

<img width="50%" alt="E07-M1101D-SMA module" src="https://github.com/user-attachments/assets/d73b86e1-9320-4c61-8300-7564bcdc1605" />

My version of the CC1101-based module (E07-M1101D-SMA) exposes only a single GDO line, while ESPSomfyRTS is often configured with separate RX and TX signal pins.

By assigning both RX and TX to the same GPIO, ESPSomfyRTS can use the single GDO line for both receiving and transmitting.

The GPIO configuration with the Seeed Studio XIAO ESP32-S3 is:

- **RX Pin = GPIO3**
- **TX Pin = GPIO3** ← same GPIO as RX

### ESP32-S3 XIAO

Pin connections between the CC1101 module and the XIAO ESP32-S3:

<img width="30%" alt="XIAO ESP32-S3 pinout" src="https://github.com/user-attachments/assets/a6c90227-256f-481b-9778-97537742e0fe" />

| CC1101 Pin | Description | ESP Signal | ESP Pin |
| --- | --- | --- | --- |
| 1 | GND | GND | 13 |
| 2 | VCC | 3V3 | 12 |
| 3 | GDO0 - RX/TX | GPIO 03 | 3 |
| 4 | CSN | GPIO 06 | 6 |
| 5 | SCK | GPIO 07 | 9 |
| 6 | MOSI | GPIO 09 | 11 |
| 7 | MISO | GPIO 08 | 10 |
| 8 | Not connected | | |

Here is the corresponding ESPSomfyRTS radio configuration:

<img width="40%" alt="ESPSomfyRTS radio configuration" src="https://github.com/user-attachments/assets/dd554f1b-836c-40dd-8811-f60dbd8e4370" />

---

## Schematic & PCB

I designed a small custom PCB for the controller.

The complete KiCad project is available in the **[KiCad](./KiCad)** folder.

<img width="50%" alt="PCB" src="https://github.com/user-attachments/assets/7d9d914d-bd6e-429b-8e6d-a58af10f896b" />

<img width="50%" alt="ESPSomfyRTS PCB layout" src="https://github.com/user-attachments/assets/423ef278-7971-42b5-91cc-b8556553dec7" />

<img width="50%" alt="PCB" src="https://github.com/user-attachments/assets/06ed107b-ca40-4be6-8069-9680e503d5f3" />

<img width="50%" alt="PCB" src="https://github.com/user-attachments/assets/2bb88ea2-abb1-45a3-ba3d-a320ddaaafa4" />

Before ordering, I panelized the PCB design so I would have enough PCBs to experiment with, sell, or give away ;-)

<img width="30%" alt="image" src="https://github.com/user-attachments/assets/62ccf98f-2daa-4fc9-895d-60d2b5e694f9" />


---

## Enclosure

Finally, I "Boxified" an enclosure for the controller using my [Boxify Parametric Electronics Enclosure Framework](https://cad.onshape.com/documents/2429cd535c2c818681c446f4/w/762b6c313c33766c159c34b3/e/4a0a0d23bcb24ef244694428).

See also my [Boxify Instructable](https://www.instructables.com/-Boxify-a-Parametric-Electronics-Enclosure-Framewo).

The enclosure was then 3D printed.

<img width="50%" alt="3D printed enclosure" src="https://github.com/user-attachments/assets/83b7fad3-78b1-4a7a-a076-bfe6fb64d51a" />

<img width="30%" alt="Enclosure" src="https://github.com/user-attachments/assets/b7a6c785-e766-40a5-a1b2-e2797452935d" />

---

## Controlling the SunRain Shade

The Somfy motor does not provide a motor-running feedback signal.

I therefore derive the motor-running state from a HomeWizard energy plug. The motor uses approximately 200 W while running, making it possible to detect whether the motor is active.

For controlling and monitoring the shade I created a Node-RED dashboard.

The complete Node-RED flow is available in the **[nodeRed](./nodeRed)** folder.

The dashboard allows me to:

- control the shade
- monitor whether the motor is responding
- track the shade position
- detect when the motor is running
- receive a warning when rain is predicted within 30 minutes

<img width="50%" alt="Node-RED dashboard" src="https://github.com/user-attachments/assets/02ed844e-f5a5-471e-83d8-f6b92894fac3" />

## Architecture diagram

<img width="1528" height="1014" alt="image" src="https://github.com/user-attachments/assets/b4402055-987b-4c53-8ccf-51ab9d388ed5" />

