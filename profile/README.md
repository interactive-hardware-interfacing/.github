# Interactive Hardware Interfacing

**Instruments that run in the browser and talk to real hardware.**

This organization collects educational demos and labs for working with hardware. Each project is designed to be used from a single web page. Most connect to a microcontroller over USB using the browser's built-in [Web Serial](https://developer.mozilla.org/en-US/docs/Web/API/Web_Serial_API) API, so there is nothing to install and no server to run: open the page, plug in the board, click **Connect**. Every tool also has a **Try without hardware** mode, so you can explore it with nothing plugged in.

🌐 **Live site:** https://interactive-hardware-interfacing.github.io/ — the landing page for all demos and projects.

---

## Sample Projects

### Wireless communication demos

A series of hands-on demos built around pairs (or small swarms) of **Seeed XIAO ESP32-C3** boards talking over **ESP-NOW**. Each one isolates a single idea about how wireless data actually moves.

| Demo | What it teaches | Hardware | Live |
|---|---|---|---|
| [**morse-key-demo**](https://github.com/interactive-hardware-interfacing/morse-key-demo) | Signaling and encoding. Tap a key, hear a beep, watch the input decode into letters in real time. Wired mode (one board + button + buzzer) or wireless mode (key board → bridge board). A keyboard-only mode uses the spacebar and needs no hardware at all. | 1–2 × XIAO ESP32-C3 | [▶ Open](https://interactive-hardware-interfacing.github.io/morse-key-demo/) |
| [**packet-inspector-demo**](https://github.com/interactive-hardware-interfacing/packet-inspector-demo) | What's inside a packet. A "Wireshark lite": color-coded hex dump of each 32-byte ESP-NOW packet, decoded fields, CRC pass/fail, and live counters for packets/sec, sequence-gap losses, and RSSI. | 2 × XIAO ESP32-C3 (bridge + TX) | [▶ Open](https://interactive-hardware-interfacing.github.io/packet-inspector-demo/) |
| [**wireless-address-demo**](https://github.com/interactive-hardware-interfacing/wireless-address-demo) | Addressing: unicast vs. broadcast. Send a message to one node or to all; only the addressed node's LED responds. Unicast messages return an ACK; broadcasts don't. | 4 × XIAO ESP32-C3 (bridge + 3 nodes) | [▶ Open](https://interactive-hardware-interfacing.github.io/wireless-address-demo/) |
| [**telemetry-demo**](https://github.com/interactive-hardware-interfacing/telemetry-demo) | Sensor data over the air. An HC-SR04 ultrasonic sensor measures distance on one board and streams it to another; the page shows the live reading beside the raw bytes with the distance field highlighted. Swap in your own sensor by editing one function. | 2 × XIAO ESP32-C3 + HC-SR04 | [▶ Open](https://interactive-hardware-interfacing.github.io/telemetry-demo/) |
| [**rssi-demo**](https://github.com/interactive-hardware-interfacing/rssi-demo) | Range and signal degradation. Walk one board away from the other and watch RSSI fall and packets drop. Step the TX power with a button; mark taped floor distances to build a signal-vs-distance chart. | 2 × XIAO ESP32-C3 (bridge + battery-powered TX) | [▶ Open](https://interactive-hardware-interfacing.github.io/rssi-demo/) |
| [**espsdr-demo**](https://github.com/interactive-hardware-interfacing/espsdr-demo) | The spectrum itself. Turns a XIAO ESP32-C3 into a simple 2.4 GHz software-defined radio with live spectrum, waterfall, and raw I/Q views. An optional second board acts as a "jammer" to give you something to look at. Uses stock [ESPARGOS](https://espargos.net/) ESP-SDR receiver firmware. | 1–2 × XIAO ESP32-C3 | [▶ Open](https://interactive-hardware-interfacing.github.io/espsdr-demo/) |

### Electronics lab instruments

| Lab | What it does | Hardware | Live |
|---|---|---|---|
| [**led-iv-lab**](https://github.com/interactive-hardware-interfacing/led-iv-lab) | A browser-based curve tracer for an undergraduate electronics lab. Pick one of four LEDs (red, amber, green, blue), sweep the drive voltage, and plot forward voltage vs. current live. Firmware in Arduino C++ with a CircuitPython alternative. | Adafruit ItsyBitsy M4 + lab LED board | [▶ Open](https://interactive-hardware-interfacing.github.io/led-iv-lab/) |

### Site

| Repo | Purpose |
|---|---|
| [**interactive-hardware-interfacing.github.io**](https://github.com/interactive-hardware-interfacing/interactive-hardware-interfacing.github.io) | The landing page that links to all of the tools above. |

---

## How these work

- **One page per instrument.** Each tool is a self-contained HTML/JS page in its own repository, served by GitHub Pages. No build step, no framework, no backend.
- **Plain-text protocols.** Boards speak simple line-based commands (e.g. `SET 2.4`, `MEAS`), so every instrument also works from a serial terminal or a Python script. Each repo documents its protocol in `PROTOCOL.md`.
- **Browser APIs, not drivers.** Web Serial (and WebUSB where needed) replace per-OS driver installs. Chrome or Edge on a desktop/laptop is required for hardware mode; the simulator mode runs in any browser.
- **Firmware included.** Each repo ships the microcontroller code (mostly CircuitPython) plus wiring diagrams in `wiring/`.

## Running locally

Web Serial requires a secure context, so pages must be served from `https://` or `localhost` (ES modules also won't load from `file://`). From any repo:

```bash
python -m http.server 8000
# then open http://localhost:8000
```

## Contributing

Issue reports are welcome on the individual repositories. Pull requests will be reviewed but are not actively solicited, since this material was developed to accompany specific course labs and demos. Forking a project for your own course or demo is highly encouraged.

## License

Most projects are released under **GPL-2.0**.

`espsdr-demo` is **GPL-3.0-or-later** because it borrows structure from ESPARGOS's `esp-web-sdr`; the ESP-SDR receiver firmware remains under ESPARGOS's own license.

See each repository's `LICENSE` file for details.

## Maintainer

Built and maintained by [LC Linkous](https://lc-linkous.github.io/).
