# myESPSomfyRTS
I made a DIY controller to operate my SunRain shade, based on the open-source ESPSomfyRTS software

## How It Works

- Hardware: It uses an ESP32 microchip paired with a CC1101 radio transceiver module.
- Communication: It connects to my home Wi-Fi network and sends 433 MHz radio signals that match the Somfy RTS (Radio Technology Somfy) protocol.
- Local Operation: It runs a built-in web server so I can control the shade directly from my phone or computer browser.

## Key Features
- Smart Home Integration: It works smoothly with platforms like Home Assistant and nodeRed for local automations and remote access.
- Position Tracking: Tracks the open or closed percentage of the shade, even besides the physical remote
- See for the code, wiring guides, and instructions on the official ESPSomfy-RTS project page.
