# NanoVNA Modern — Repository Plan

## Repository

`abraaobat/nanovna-modern`

Umbrella repository for architecture, firmware integration, desktop bridge, web dashboard and ESP32-S3 SmartLink while boundaries are still evolving.

## Tree

```text
nanovna-modern/
├── README.md
├── project-status.json
├── docs/
│   ├── ARCHITECTURE.md
│   ├── ROADMAP.md
│   ├── HARDWARE.md
│   ├── UI-UX.md
│   ├── SD-EXTENSIONS.md
│   ├── USB-WEB-BRIDGE.md
│   ├── SMARTLINK-ESP32.md
│   ├── ANALYSIS-AI.md
│   └── adr/
├── firmware/
├── bridge/
├── web/
├── smartlink/
├── protocol/
├── hardware/
└── tools/
```

## Firmware upstream policy

Source upstream: `DiSlord/NanoVNA-D`.

Before importing source:

1. confirm license/attribution;
2. choose fork/submodule/subtree/separate repo;
3. pin commit/tag;
4. document `upstream` remote;
5. separate UI changes from RF/DSP changes.

## Branch policy

- `main` — stable project baseline.
- `feature/*` — implementation delimitada.
- `spike/*` — experimentos.
- `upstream-sync/*` — sincronização controlada.

## Primeiros PRs

1. `docs/project-foundation` — documentação e contratos.
2. `build/f303-baseline` — upstream build + CI.
3. `ui/foundation` — theme/widgets/navigation sem RF changes.
4. `bridge/usb-probe` — discovery read-only e inventário do protocolo.
