# Analysis & AI

## Estratégia

A ordem de implementação privilegia resultados explicáveis e baratos:

1. matemática/DSP determinístico;
2. heurísticas explicáveis;
3. TinyML experimental;
4. IA externa opcional.

## Smart Analysis

Casos iniciais:

- ressonância e SWR mínimo;
- offset para frequência-alvo;
- bandwidth;
- Q estimado;
- insertion loss;
- peaks/notches;
- drift entre sessões;
- cable/TDR helpers;
- detecção de anomalias simples.

Cada diagnóstico deve registrar dados observados e regra utilizada.

## TinyML

Candidato principalmente para ESP32-S3, não para o STM32 como requisito. Só promover se superar heurísticas em dataset real e dentro de orçamento de RAM/latência.

## External AI

Recebe resumo estruturado, não necessariamente todo o sweep bruto. Deve ser opt-in, preservar modo offline e distinguir cálculo medido de interpretação gerada.
