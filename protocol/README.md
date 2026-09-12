# Protocol

Contratos versionados entre firmware, desktop bridge, SmartLink e web client. Entidades principais: DeviceInfo, SweepConfig, SweepFrame, ComplexPoint, Marker, CalibrationState, Preset e MeasurementSession.

## Hardware/firmware observado

Unidade de referência:

- `NanoVNA-H 4` / ZeenKo ZN401 HW `4.7_ZK`;
- firmware `1.2.44`;
- build `May 26 2025 - 16:00:15`;
- `p:401`, `IF:12k`, `ADC:384k`, `Lcd:480x320`;
- `ARMv7E-M / Cortex-M4F`;
- `STM32F303xC Analog & DSP`;
- USB CDC runtime: VID `0x0483`, PID `0x5740`, Full Speed 12 Mbit/s;
- macOS node observado: `/dev/cu.usbmodem4001`;
- shell prompt: `ch>`.

## Comandos expostos pelo firmware 1.2.44 [x401]

Inventário obtido diretamente com `help` no hardware:

```text
scan scan_bin data frequencies freq sweep power offset bandwidth time
sd_list sd_read sd_delete saveconfig clearconfig dump touchcal touchtest
pause resume msg cal save recall trace marker edelay s21offset capture
measure refresh touch release vbat tcxo reset smooth config usart_cfg usart
vbat_offset transform threshold help info version color
```

### Relevância para o Bridge

Leitura/telemetria de maior interesse inicial:

- `info` / `version` — identificação e compatibilidade;
- `frequencies` — eixo de frequência;
- `data` — dados complexos medidos;
- `scan` / `scan_bin` — aquisição remota de sweep; `scan_bin` é candidato principal para streaming eficiente;
- `vbat` / `tcxo` — estado do instrumento;
- `capture` — captura da tela para diagnóstico/integração;
- `sd_list` / `sd_read` — acesso controlado ao conteúdo do microSD.

Comandos que alteram configuração, calibração, estado persistente ou reinicializam o equipamento não devem ser usados pelo Bridge em modo discovery/read-only sem ação explícita do usuário.

## Próxima validação

1. registrar saída de `version`;
2. confirmar formato de uma aquisição read-only pequena via `scan` e/ou `scan_bin` com sintaxe verificada no upstream;
3. definir parser e fixture determinística para `DeviceInfo` e `SweepFrame`;
4. só depois iniciar o primeiro `bridge/usb-probe`.
