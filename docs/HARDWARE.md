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

## Current USB diagnostic

macOS with device powered over USB-C has so far shown no child USB device under `ioreg -p IOUSB -w0` and no new `/dev/cu.*` node. Changing Mac USB-C port did not change the result.

Remaining controlled tests:

1. known-good USB-A → USB-C data cable through adapter/hub;
2. reverse USB-C connector orientation if applicable;
3. known-good USB data cable validated with another device;
4. DFU enumeration without flashing;
5. physical board inspection only if necessary.

## F0 evidence

```bash
system_profiler SPUSBDataType
ioreg -p IOUSB -w0
ls /dev/cu.*
```

If serial appears, collect read-only console output first (`help`, `info`, `version` when available).

Expected STM32 DFU identity from upstream docs is typically `0483:df11`, but record the actual unit before approving flash.

## Components still to confirm

- clock generator/synthesizer on 4.7_ZK;
- mixer;
- LCD controller;
- touchscreen controller;
- USB-C/power implementation;
- flash/RAM headroom of target build.

## Safety rule

No experimental firmware flash before DFU/recovery is verified, upstream clean build succeeds, settings/calibration backup strategy is documented, and correct hardware target is confirmed.
