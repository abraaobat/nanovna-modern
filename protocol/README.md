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
- shell prompt: `ch>`;
- `version` observado: `1.2.44`.

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

## Primeira fixture real de sweep

Comando validado no ZN401 de referência:

```text
scan 140000000 150000000 11 7
```

O formato textual observado é uma linha por ponto, com cinco campos separados por espaço:

```text
frequency_hz s11_re s11_im s21_re s21_im
```

Exemplo real:

```text
140000000 0.995901824 -0.003665643 0.000011592 0.000010958
```

No firmware upstream, a sintaxe de `scan` é `scan {start(Hz)} {stop(Hz)} [points] [outmask]`. O `outmask` observado/usado como referência é composto por bits: frequência `1`, S11 `2`, S21 `4`; portanto `7` solicita os três conjuntos. O comando executa o sweep solicitado e pausa o sweep após a aquisição, sem implicar gravação persistente de configuração.

Fixtures adicionadas:

- `protocol/fixtures/zn401-1.2.44-scan-140-150mhz-11.txt` — saída textual normalizada;
- `protocol/fixtures/zn401-1.2.44-scan-140-150mhz-11.json` — representação estruturada para testes de parser.

Essas fixtures são referência de **protocolo e parsing**, não de precisão metrológica: DUT, terminação dos ports e estado completo de calibração não foram registrados na captura.

## Contrato inicial sugerido para `SweepFrame`

```text
SweepFrame
├── deviceId / capability profile
├── startHz
├── stopHz
├── pointCount
├── calibration metadata
└── points[]
    ├── frequencyHz
    ├── s11.re
    ├── s11.im
    ├── s21.re
    └── s21.im
```

A derivação de SWR, return loss, magnitude, fase e impedância deve ocorrer em camada superior a partir dos valores complexos, preservando os dados brutos recebidos do instrumento.

## Próximas validações

1. confirmar enumeração DFU/recovery sem gravação;
2. capturar `scan_bin` para comparar eficiência e framing com `scan` textual;
3. implementar o primeiro `bridge/usb-probe` contra as fixtures;
4. transformar `info` + `version` em `DeviceInfo` normalizado;
5. depois fixar o upstream NanoVNA-D/F303 usado como baseline do firmware.
