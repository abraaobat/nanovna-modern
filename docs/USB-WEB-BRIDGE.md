# USB Bridge & Web Dashboard

## Objetivo

Transformar o protocolo USB/serial do NanoVNA em uma interface moderna e estável sem acoplar navegador ao detalhe do transporte.

```text
NanoVNA USB → Bridge local → REST/WebSocket → Web Dashboard/PWA
```

## Bridge

Primeira implementação: CLI-first/headless no macOS.

Responsabilidades:

- discovery de dispositivo;
- reconnect;
- fila/serialização de comandos;
- aquisição de sweep S11/S21;
- normalização para contratos internos;
- REST para estado/configuração;
- WebSocket para live sweep;
- logs e diagnostics.

## API inicial

Exemplos de recursos:

- `GET /api/device`
- `GET /api/sweep`
- `GET /api/markers`
- `GET /api/calibration`
- `POST /api/sweep`
- `POST /api/marker`
- `POST /api/preset`
- `WS /api/live`

## Dashboard/PWA

Desktop, tablet e telefone compartilham o mesmo cliente. Recursos: gráficos interativos, Smith chart, markers, cards configuráveis, histórico, comparação, Touchstone e relatórios.

O navegador não deve depender de Web Serial; Bridge e SmartLink expõem o mesmo contrato web.
