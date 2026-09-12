# NanoVNA Modern — Hardware Fingerprint

## Unit under test

| Field | Observed value |
|---|---|
| Brand | ZeenKo |
| Commercial model | ZN401 |
| Family | NanoVNA-H4 |
| External HW label | `4.7_ZK` |
| Serial on label | `H4-2603769` |
| Display | 480x320 class |
| microSD | Present and recognized by firmware |
| Current firmware | NanoVNA-D 1.2.44 `[x401]` |
| Build date shown | 2025-05-26 |
| MCU shown by firmware | STM32F303xC |
| Architecture | ARMv7E-M Cortex-M4F |
| TXCO shown | 26.000000 MHz |

## USB runtime diagnostic

Runtime USB enumeration on macOS is now **confirmed** with a known-good/compatible cable.

Observed device identity:

| Field | Observed value |
|---|---|
| Product | `NanoVNA-H4` / `NanoVNA_H4` |
| Manufacturer | `nanovna.com` |
| USB serial | `400` |
| VID | `0x0483` (1155) |
| PID | `0x5740` (22336) |
| USB speed | 12 Mbit/s (Full Speed) |
| Device class | 2 (CDC/communications) |
| macOS serial node | `/dev/cu.usbmodem4001` |

Evidence from `ioreg -p IOUSB -l -w 0` shows the device as `NanoVNA-H4@02100000`, and `ls /dev/cu.*` exposes `/dev/cu.usbmodem4001`.

Earlier direct USB-C tests with other cables powered the unit but produced no USB child device and no serial node. Successful enumeration with a different cable strongly indicates cable/path compatibility was a material factor; this does not by itself prove the previous cables were defective.

## F0 evidence

Runtime capture commands:

```bash
system_profiler SPUSBDataType
ioreg -p IOUSB -l -w 0
ls /dev/cu.*
```

Next read-only console inventory:

```bash
screen /dev/cu.usbmodem4001 115200
```

Then query only non-destructive commands such as `help`, `info` and `version` when supported.

### DFU

DFU enumeration remains pending. F0 DFU work is enumeration/recovery validation only; do not write firmware.

Expected STM32 DFU identity from upstream docs is typically `0483:df11`, but record the actual unit before approving flash.

## Components still to confirm

- clock generator/synthesizer on 4.7_ZK;
- mixer;
- LCD controller;
- touchscreen controller;
- board-level USB-C/power implementation;
- flash/RAM headroom of target build.

## Safety rule

No experimental firmware flash before DFU/recovery is verified, upstream clean build succeeds, settings/calibration backup strategy is documented, and correct hardware target is confirmed.
