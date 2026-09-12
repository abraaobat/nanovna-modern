# SmartLink ESP32-S3

## Objetivo

Acessório opcional que substitui o computador como bridge e adiciona conectividade/armazenamento/processamento.

```text
NanoVNA USB Device
        ↓
ESP32-S3 USB Host
        ↓
REST / WebSocket
        ↓
Wi‑Fi AP/STA → Browser/PWA
```

## Hardware de referência

ESP32-S3 N16R8: 16 MB flash + 8 MB PSRAM como classe de referência inicial.

## Funções

- USB Host CDC-ACM;
- parser do protocolo NanoVNA;
- Wi‑Fi AP/STA;
- mDNS `nanovna.local`;
- BLE opcional;
- servidor web/API;
- PSRAM ring buffers;
- histórico/cache;
- microSD adicional opcional;
- Smart Analysis;
- OTA do próprio SmartLink.

## Alimentação

VBUS deve ser controlado/protegido. Evitar backfeed entre NanoVNA, ESP32 e fonte. D+/D- e VBUS só serão definidos após validação de bancada.

## Princípio

SmartLink não executa RF/calibração. Se ele falhar, o NanoVNA deve continuar operando standalone.
