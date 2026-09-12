# UI/UX — Modern Instrument Interface

## Objetivo

Modernizar a experiência 480x320 sem transformar o STM32F303 em uma GPU. A referência é a clareza de instrumentos profissionais: hierarquia forte, fundo escuro, cards grandes, seleção em azul e áreas de toque amplas.

## Navegação

`MEASURE | DISPLAY | MARKERS | CAL | PRESETS | SETUP`

A tela principal preserva o gráfico como elemento dominante. Configurações frequentes devem ficar a no máximo dois toques.

## Painel modular

Overlays habilitáveis: Marker/Frequency, Start/Stop, Center/Span, SWR, Return Loss, Phase, R+jX, Magnitude, Group Delay, Calibration, Battery, Sweep Points, Averaging, Smoothing, Trace/Channel, SD e USB.

Layouts usam slots automáticos, não drag-and-drop livre, para reduzir estado e custo de renderização.

## Presets

- `Minimal`
- `Antenna`
- `Filter`
- `Cable`
- `Lab`
- `Studio`

Cada preset pode guardar overlays, traces, escala, markers, range, averaging/smoothing, estilo de gráfico e brilho.

## Graph styles

- `Classic`: mínimo custo.
- `Enhanced`: grade/trace/markers refinados.
- `Studio`: glow simulado e persistência limitada.
- `Diagnostic`: alta densidade técnica.

Efeitos devem usar primitivas, redraw parcial e pequenos buffers. Sem blur real ou framebuffer integral.

## Calibration UX

Fluxo guiado com status explícito de `OPEN`, `SHORT`, `LOAD`, `ISOLN`, `THRU`, apply/save e range de validade da calibração.

## Acessibilidade

Texto crítico deve manter contraste alto; estados não devem depender apenas de cor; alvos de toque devem ser amplos; modo Classic deve permanecer como fallback seguro.
