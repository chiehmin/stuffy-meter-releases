# Stuffy Meter

> **Just got a Stuffy Meter? Start here to set up your device:**
>
> - **English:** **[Quickstart Guide](https://github.com/chiehmin/stuffy-meter-releases/wiki/Quickstart)** · [Wiki Home](https://github.com/chiehmin/stuffy-meter-releases/wiki)
> - **繁體中文**： **[快速入門指南](https://github.com/chiehmin/stuffy-meter-releases/wiki/Quickstart-zh-Hant)** · [說明首頁](https://github.com/chiehmin/stuffy-meter-releases/wiki/Home-zh-Hant)
> - **Already on Wi-Fi?** Open **[cmwang.dev/stuffy-meter](https://cmwang.dev/stuffy-meter)** on the same network to find your monitor and open its dashboard automatically.

Official firmware releases, 3D-printable enclosures, and user guides for the
**Stuffy Meter** — an ESP32-C3 Wi-Fi CO₂ and VOC air-quality monitor available
in two hardware editions (the board revision is printed on the PCB):

- **USB edition** (board rev `3.2`) — USB-C powered
- **Battery edition** (board rev `4.1`) — USB-C + 18650 backup battery

## Guides & Integrations

- **Setup & Quickstart:** [English](https://github.com/chiehmin/stuffy-meter-releases/wiki/Quickstart) · [繁體中文](https://github.com/chiehmin/stuffy-meter-releases/wiki/Quickstart-zh-Hant)
- **Telegram Alerts:** [English](https://github.com/chiehmin/stuffy-meter-releases/wiki/Telegram-Alerts) · [繁體中文](https://github.com/chiehmin/stuffy-meter-releases/wiki/Telegram-Alerts-zh-Hant)
- **Prometheus & Grafana (Docker):** [English](https://github.com/chiehmin/stuffy-meter-releases/wiki/Prometheus-and-Grafana) · [繁體中文](https://github.com/chiehmin/stuffy-meter-releases/wiki/Prometheus-and-Grafana-zh-Hant)
- **Smart Home & APIs:** [Home Assistant (HACS)](https://github.com/chiehmin/ha-stuffy-meter) · [MQTT & Home Assistant](https://github.com/chiehmin/stuffy-meter-releases/wiki/MQTT-and-Home-Assistant) · [REST API](https://github.com/chiehmin/stuffy-meter-releases/wiki/REST-API) · [Prometheus Metrics](https://github.com/chiehmin/stuffy-meter-releases/wiki/Prometheus-Metrics)

## Firmware & Monitoring Releases

Download the latest release from the [Releases](https://github.com/chiehmin/stuffy-meter-releases/releases/latest) page. Each release contains:

| File | For |
| --- | --- |
| `stuffy_meter_fw<version>_board<rev>.bin` | updating a monitor with board rev `<rev>` (3.2 or 4.1) over Wi-Fi |
| `stuffy_meter_fw<version>_board<rev>_factory.bin` | a new or erased board: the complete image, flashed over USB-C at `0x0` (erases settings) |
| `manifest.json` | automatic updates: the version and image URLs |
| `stuffy_meter_usb_{base,lid}.stl` | USB edition: 3D-printable enclosure |
| `stuffy_meter_battery_{base,lid}.stl` | Battery edition: 3D-printable enclosure |
| `stuffy_meter_monitoring_v<version>.tar.gz` | Prometheus + Grafana Docker Compose stack, pre-built dashboards & alert rules |
| `SHA256SUMS` | checksums: `shasum -a 256 -c SHA256SUMS` |

## Updates

From version 1.6.0 on, monitors read
https://github.com/chiehmin/stuffy-meter-releases/releases/latest/download/manifest.json
and install a newer release of the same major version by themselves at night
(02:00 to 05:00 in the monitor's time zone, UTC+8 unless changed; the Battery
edition only on USB power), unless automatic updates are turned off. A new
major version is installed by hand. The Firmware page of a monitor's dashboard
turns automatic updates off, moves the window, or installs a release right
away. A monitor only takes an image built for its circuit, checks its SHA-256,
and goes back to its previous firmware by itself when a new one fails.

A monitor on an older version cannot download from GitHub: upload the `.bin`
of its board once on the dashboard's Firmware page, and it updates itself from
then on.

<details>
<summary><strong>Advanced: flashing a blank or erased board over USB-C</strong></summary>

```sh
python3 -m esptool --chip esp32c3 write_flash 0x0 stuffy_meter_fw<version>_board<rev>_factory.bin
```

Browser flashers (ESP Web Tools, esptool-js) take the `_factory.bin` image at offset `0x0`.
Then join the `StuffyMeter-xxxxxx` Wi-Fi with a phone to set the monitor up
(see the [Quickstart Guide](https://github.com/chiehmin/stuffy-meter-releases/wiki/Quickstart)).

</details>

These releases are built and published automatically from the project's source
repository.
