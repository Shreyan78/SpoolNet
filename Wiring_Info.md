# SpoolNet Tracking Hub — Electrical Hardware & Wiring

## Components

* **ESP32-S3FH4R2** — main MCU + Wi-Fi
* **MT6701** — magnetic rotary encoder for filament measurement
* **PN532** — NFC reader for spool identification
* **SSD1306 128×64** — OLED display
* **BMG gear + magnet** — measures filament movement through the MT6701
* **Status LED + resistor**
* **USB-C power input**

## Pinout

### I²C — OLED + MT6701

| Signal |   ESP32-S3 |
| ------ | ---------: |
| SCL    | **GPIO 2** |
| SDA    | **GPIO 6** |
| VCC    |  **3.3 V** |
| GND    |    **GND** |

The OLED and MT6701 share the same I²C bus.

### SPI — PN532

| PN532 |    ESP32-S3 |
| ----- | ----------: |
| SCK   |  **GPIO 8** |
| MISO  | **GPIO 12** |
| MOSI  |  **GPIO 7** |
| SS    | **GPIO 11** |
| VCC   |   **3.3 V** |
| GND   |     **GND** |

### Status LED

| Component |   ESP32-S3 |
| --------- | ---------: |
| LED       | **GPIO 4** |

```text
GPIO 4 ── resistor ── LED ── GND
```

GPIO 4 is dedicated to the status LED; GPIO 2 remains dedicated to I²C SCL.

## Power

The current prototype is powered directly through USB:

```text
USB-C 5 V
   │
   ├── ESP32-S3
   │
   └── 3.3 V peripherals
       ├── PN532
       ├── MT6701
       └── SSD1306
```

## System

```text
                    ┌─────────────────────┐
                    │   SPOOLNET HUB      │
                    │                     │
Filament ──────────►│ BMG Gear            │
                    │      │              │
                    │    MT6701           │
                    │      │ I²C          │
                    │      ▼              │
                    │   ESP32-S3          │
                    │    │  │  │          │
                    │    │  │  └─ SPI ─ PN532
                    │    │  └──── I²C ─ OLED
                    │    └─────── GPIO 4 ─ LED
                    └──────────┬──────────┘
                               │
                             Wi-Fi
                               │
                               ▼
                         SpoolNet Server
```

### Communication

* **ESP32 ↔ MT6701/OLED:** I²C
* **ESP32 ↔ PN532:** SPI
* **ESP32 ↔ Server:** Wi-Fi + HTTP webhook
* **Server:** SQLite + SpoolNet Web UI


