# NanoVNA Modern — Architecture

## System view

```text
                       ┌───────────────────────────────┐
                       │      Web Dashboard / PWA      │
                       │ Desktop • Tablet • Smartphone │
                       └──────────────┬────────────────┘
                                      │ REST / WebSocket
                         ┌────────────┴────────────┐
                         │                         │
                ┌────────▼────────┐       ┌────────▼─────────┐
                │ NanoVNA Bridge  │       │ SmartLink ESP32  │
                │ macOS/Linux/Win │       │ ESP32-S3 N16R8   │
                └────────┬────────┘       └────────┬─────────┘
                         │ USB CDC/serial          │ USB Host CDC
                         └────────────┬────────────┘
                                      │
                              ┌───────▼────────┐
                              │  NanoVNA-H4    │
                              │ ZN401 4.7_ZK   │
                              ├────────────────┤
                              │ RF / DSP       │
                              │ Calibration    │
                              │ Sweep          │
                              │ Modern UI      │
                              │ microSD        │
                              └────────────────┘
```

## Regra arquitetural

A cadeia crítica `RF → aquisição → DSP → calibração → sweep` permanece desacoplada da UI moderna, web, Wi‑Fi, ML e IA externa. O fork deve primeiro preservar o comportamento upstream.

## Camadas

### 1. Measurement Core

STM32/NanoVNA mantém geração/aquisição RF, S11/S21, calibração, sweep, dados complexos, markers fundamentais e operação standalone.

### 2. Local Modern UI

```text
ui/
├── theme
├── navigation
├── widgets
├── overlays
├── layouts
├── presets
├── screens
└── renderer
```

Renderer com desenho imediato/redraw parcial. Não assumir framebuffer RGB565 integral; 480×320×2 exige ~300 KiB.

Modelo lógico de widget:

```text
Widget
├── id
├── enabled
├── priority
├── slot
├── formatter
├── data_source
└── render()
```

### 3. SD Extension Store

```text
/NANOVNA/
├── profiles/
├── dashboards/
├── themes/
├── scripts/
├── measurements/
├── calibrations/
├── screenshots/
├── languages/
└── analysis/
```

Sem código nativo arbitrário no cartão. Extensões devem ser declarativas ou scripts limitados.

### 4. USB Protocol

Entidades normalizadas: `DeviceInfo`, `SweepConfig`, `SweepFrame`, `ComplexPoint`, `Trace`, `Marker`, `CalibrationState`, `Preset`, `MeasurementSession`.

### 5. NanoVNA Bridge

Serviço CLI-first/headless para descobrir USB, abrir/reabrir sessão, serializar comandos, coletar sweep, normalizar dados, expor REST/WebSocket e registrar diagnósticos.

### 6. Web Dashboard

A UI web deve ser independente do transporte físico e funcionar contra Bridge desktop ou SmartLink.

### 7. SmartLink ESP32-S3

USB Host, Wi‑Fi AP/STA, mDNS, REST/WebSocket, PSRAM buffers, cache/histórico, microSD opcional, Smart Analysis e OTA. Não assume RF/calibração.

### 8. Analysis Engine

Ordem: matemática/DSP determinístico → heurísticas explicáveis → TinyML experimental → IA externa opcional.

## Power architecture for SmartLink

```text
5V input
  ↓
protected regulator / load switch
  ↓
VBUS controlled
  ↓
NanoVNA USB-C

ESP32-S3 USB Host PHY
  ├── D+
  └── D-
```

Evitar backfeed e validar a topologia antes de PCB/enclosure.
