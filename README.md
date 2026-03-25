# ⚡ ESP32 Flasher

**Flash ESP32 firmware from your browser. No drivers. No Python. No command line.**

![Demo](demo.gif)

> A browser-based ESP32 firmware flashing tool powered by the [WebSerial API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Serial_API) and [esptool-js](https://github.com/espressif/esptool-js). Works entirely in-browser — connect your ESP32 via USB, pick a `.bin` file, and flash.

**[→ Open the flasher](https://mjflanigan5.github.io/esp32-flasher/)**

---

## Browser Requirements

> **Chrome 89+ or Edge 89+ is required.**
> Firefox and Safari do not support the WebSerial API.

The tool will display a warning if your browser is not supported.

---

## Quick Start

1. **Open** [the flasher page](https://mjflanigan5.github.io/esp32-flasher/) in Chrome or Edge
2. **Connect** your ESP32 via USB, then click "Connect to ESP32" and select the serial port
3. **Select firmware** — upload a `.bin` file or pick a preset — then click **▶ Flash Firmware**

That's it. The serial monitor activates automatically after flashing.

---

## Firmware Presets

The presets tab provides quick-reference cards for popular ESP32 firmware projects. Because these projects distribute firmware dynamically, you download the `.bin` from their installer/website, then upload it here.

| Preset | Description | Link |
|--------|-------------|------|
| **ESPHome** | Home automation — configure via YAML | [esphome.io](https://esphome.io) |
| **Tasmota** | Feature-rich IoT open firmware | [tasmota.github.io/install](https://tasmota.github.io/install/) |
| **WLED** | LED strip controller, 100+ effects | [install.wled.me](https://install.wled.me) |
| **MicroPython** | Run Python directly on ESP32 | [micropython.org](https://micropython.org/download/ESP32_GENERIC/) |
| **Arduino OTA Loader** | Enable OTA updates via Arduino | [arduino-esp32](https://github.com/espressif/arduino-esp32) |

---

## Features

- **Zero install** — runs fully in the browser
- **Chip auto-detection** — detects ESP32, ESP32-S2, ESP32-S3, ESP32-C3, and more
- **Drag-and-drop** firmware upload
- **Configurable flash offset** — default `0x0`, `0x1000` for MicroPython, `0x10000` for app partition
- **Erase before flash** option
- **Animated progress bar** with bytes written / total
- **Serial monitor** — real-time output, timestamps toggle, auto-scroll, send commands, 500-line buffer
- **Auto-reset via RTS/DTR** — no manual BOOT button press needed on most boards

---

## Troubleshooting

### Port not showing up
Install the USB-to-serial driver for your board:
- **CP210x** (most ESP32 dev boards): [Silicon Labs driver](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers)
- **CH340** (common on clone boards): [CH340 driver](https://www.wch-ic.com/products/CH340.html)

### Flash failed / timeout
Hold the **BOOT** button on your ESP32 while clicking "Connect to ESP32". Some boards need to be manually put into download mode.

### Wrong baud rate / garbled output
Try **115200** in the baud rate selector on the Connect card, or use 115200 in the Serial Monitor for boot output.

### "WebSerial not supported"
You must use **Chrome 89+** or **Edge 89+**. The WebSerial API is not available in Firefox, Safari, or mobile browsers.

### HTTPS required
WebSerial only works over HTTPS or `localhost`. If you're hosting the file locally, open it via `http://localhost` or use a local server (`python3 -m http.server`), not `file://`.

---

## Technical Details

- **WebSerial API** — direct USB serial communication from the browser
- **[esptool-js 0.5.7](https://unpkg.com/esptool-js@0.5.7/bundle.js)** — Espressif's official JS port of esptool
- No build step, no npm, no Node.js — pure HTML/CSS/JS
- Single-file app (`index.html`) for easy self-hosting

---

## Self-Hosting

Clone the repo and serve with any static file server:

```bash
git clone https://github.com/MJFlanigan5/esp32-flasher
cd esp32-flasher
python3 -m http.server 8080
# then open http://localhost:8080
```

---

## License

MIT License — Copyright (c) 2026 Michael Flanigan

See [LICENSE](LICENSE) for full text.
