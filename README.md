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
