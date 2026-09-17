# myESPSomfyRTS
I made a DIY controller to operate my SunRain shade, based on the open-source ESPSomfyRTS software

## How It Works

- Hardware: It uses an ESP32 microchip paired with a CC1101 radio transceiver module.
- Communication: It connects to my home Wi-Fi network and sends 433 MHz radio signals that match the Somfy RTS (Radio Technology Somfy) protocol.
- Local Operation: It runs a built-in web server so I can control the shade directly from my phone or computer browser.

## Key Features
- Smart Home Integration: It works smoothly with platforms like Home Assistant and nodeRed for local automations and remote access.
- Position Tracking: Tracks the open or closed percentage of the shade, even besides the physical remote

See for the code, wiring guides, and instructions on the official [ESPSomfy-RTS project page](https://github.com/rstrouse/ESPSomfy-RTS).
and an instruction video on [youtube](https://www.youtube.com/watch?v=1acVJ0xWJgs)

### CC1101 433MHz RF transceiver

<img width="50%" alt="image" src="https://github.com/user-attachments/assets/90fb8032-c2f1-48a3-870c-ac696d3649e5" />


<img width="50%" alt="image" src="https://github.com/user-attachments/assets/d73b86e1-9320-4c61-8300-7564bcdc1605" />

My version of the CC1101-based module (E07-M1101D-SMA) exposes only a single GDO line (or internally tie functions together), while ESPSomfy is often configured expecting separate RX and TX signal pins. 

By assigning both RX and TX to the same GPIO, ESPSomfyRTS can use that single GDO line for both receiving and transmitting packet 
The GPIO configuration with a ESP32 S3 Xiao Seeed Studio is as follows;
- RX Pin = GPIO3
- TX Pin = GPIO3 <-- same GPIO as RX

### ESP32 S3 Xiao Seeed Studio
pin connection of the ESP32 S3 Xiao Seeed Studio;

<img width="30%" alt="image" src="https://github.com/user-attachments/assets/a6c90227-256f-481b-9778-97537742e0fe" />

| Pin | Description                  | ESP Signal | ESP pin |
| --- | ---------------------------- | ---------- | ------- |
| 1   | GND                          | GND        | 13      |
| 2   | VCC                          | 3v3        | 12      |
| 3   | GDO0 - This is the Rx/TX Pin | GPIO 03    | 3       |
| 4   | CSN                          | GPIO 06    | 6       |
| 5   | SCK                          | GPIO 07    | 9       |
| 6   | MOSI                         | GPIO 09    | 11      |
| 7   | MISO                         | GPIO 08    | 10      |
| 8   | Not connected                |            |         |

Here a screenshot of my ESPSomfyRTS Radio setting;

<img width="40%" alt="image" src="https://github.com/user-attachments/assets/dd554f1b-836c-40dd-8811-f60dbd8e4370" />

## Schematic & PCB

I made a small PCB for it

<img width="50%" alt="image" src="https://github.com/user-attachments/assets/7d9d914d-bd6e-429b-8e6d-a58af10f896b" />

<img width="50%" alt="ESPSomfyRTS-PcbLayout" src="https://github.com/user-attachments/assets/423ef278-7971-42b5-91cc-b8556553dec7" />


<img width="50%" alt="image" src="https://github.com/user-attachments/assets/06ed107b-ca40-4be6-8069-9680e503d5f3" />


<img width="50%" alt="image" src="https://github.com/user-attachments/assets/2bb88ea2-abb1-45a3-ba3d-a320ddaaafa4" />

Before ordering I panellized the PCB design so I have enough PCB o experiment or sell (or give away ;-) )

<img width="30%" alt="image" src="https://github.com/user-attachments/assets/734ece6a-5fff-45d9-905d-ea23c84c6f4f" />




## Enclosure
At last i "boxified" an [enclosure](https://cad.onshape.com/documents/2429cd535c2c818681c446f4/w/762b6c313c33766c159c34b3/e/4a0a0d23bcb24ef244694428) for it (see also my [Boxify Instructable](https://www.instructables.com/-Boxify-a-Parametric-Electronics-Enclosure-Framewo))

and 3D printed it

<img width="50%" alt="image" src="https://github.com/user-attachments/assets/83b7fad3-78b1-4a7a-a076-bfe6fb64d51a" />

<img width="30%" alt="image" src="https://github.com/user-attachments/assets/b7a6c785-e766-40a5-a1b2-e2797452935d" />

## Controlling the SunRain shade

Because the Somfy motor has no motor running sensor I derived this from a HomeWizard plug - the motor uses ca 200W so it is possible to tell whether the engine is running or not. 

For controlling the shade I made a dashboard in nodeRed where I can see if the motor is responding and where I will be warned when there is rain predicted within 30 minutes


<img width="50%" alt="image" src="https://github.com/user-attachments/assets/02ed844e-f5a5-471e-83d8-f6b92894fac3" />
