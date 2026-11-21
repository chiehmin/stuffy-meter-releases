# Stuffy Meter releases

Firmware for the Stuffy Meter, a small CO2 and VOC monitor built around an
ESP32-C3, in two editions: the USB edition (board rev 3.2) and the Battery
edition (board rev 4.1, with an 18650 backup battery). The board revision is
printed on the PCB. Each release has:

| File | For |
| --- | --- |
| `stuffy_meter_fw<version>_board<rev>.bin` | updating a monitor with board rev `<rev>` (3.2, 4.0 or 4.1) |
| `stuffy_meter_fw<version>_board<rev>_factory.bin` | a new or erased board: the complete image, flashed over USB-C at 0x0 (erases the settings) |
| `manifest.json` | the monitors: the version and where its images are |
| `Stuffy_Meter_Quickstart_v<version>.pdf` | setting up a monitor and the dashboards |
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

A new board, over USB-C:

```sh
python3 -m esptool --chip esp32c3 write_flash 0x0 stuffy_meter_fw<version>_board<rev>_factory.bin
```

Browser flashers (ESP Web Tools, esptool-js) take the factory image at offset 0.
Then join the `StuffyMeter-xxxxxx` Wi-Fi with a phone to set the monitor up (the
quick start explains it).

These releases are built and published automatically from the project's source
repository.
