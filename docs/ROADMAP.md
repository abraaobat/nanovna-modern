# NanoVNA Modern — Roadmap Master

Roadmap incremental. Nenhuma fase deve comprometer a precisão RF para entregar recursos visuais ou de conectividade.

## F0 — Hardware Fingerprint & Safety Baseline

**Objetivo:** identificar de forma reproduzível o hardware real do ZN401 4.7_ZK e garantir rota de recuperação.

- [x] Identificar modelo externo: ZeenKo ZN401 / HW 4.7_ZK.
- [x] Identificar firmware atual: NanoVNA-D 1.2.44 `[x401]`.
- [x] Identificar MCU reportado: STM32F303xC / Cortex-M4F.
- [x] Confirmar display 480x320 e microSD funcional.
- [ ] Confirmar enumeração USB normal com cabo/porta compatíveis.
- [ ] Confirmar modo DFU sem gravar firmware.
- [ ] Registrar VID/PID, interface USB e comandos de console disponíveis.
- [ ] Confirmar sintetizador/mixer/LCD quando necessário.
- [ ] Documentar recovery procedure.

**Gate F0:** dispositivo reconhecido em USB/DFU e rota de recuperação testada/documentada.

## F1 — Upstream Reproducible Build

**Objetivo:** produzir firmware equivalente ao upstream sem alteração funcional.

- [ ] Fixar estratégia de fork/upstream do `DiSlord/NanoVNA-D`.
- [ ] Registrar commit/tag baseline.
- [ ] Build macOS para `TARGET=F303`.
- [ ] Gerar `H4.bin` reproduzível.
- [ ] Adicionar CI de build.
- [ ] Medir flash/RAM/headroom.
- [ ] Testar flash/recovery somente após F0.

**Gate F1:** build limpa, CI verde e aparelho operando igual ao baseline.

## F2 — Modern UI Foundation

- [ ] theme/paleta/tipografia/métricas.
- [ ] widgets reutilizáveis.
- [ ] navegação por abas.
- [ ] layout 480x320.
- [ ] redraw por regiões.
- [ ] orçamento explícito de RAM/flash/CPU.
- [ ] modo Classic preservado como fallback.

**Gate F2:** shell de UI navegável sem regressão de sweep.

## F3 — Modular Dashboard & Presets

- [ ] registry de widgets/overlays.
- [ ] enable/disable por item.
- [ ] slots automáticos de layout.
- [ ] Quick Metrics.
- [ ] presets `Minimal`, `Antenna`, `Filter`, `Cable`, `Lab`, `Studio`.
- [ ] persistência interna/SD.

**Gate F3:** troca de preset e overlays sem reinicialização.

## F4 — Enhanced Graphics

- [ ] nova grade cartesiana.
- [ ] Smith chart refinado.
- [ ] espessuras de trace selecionáveis.
- [ ] marker highlight.
- [ ] anti-aliasing leve quando couber.
- [ ] glow falso com 1–2 passes.
- [ ] persistência limitada.
- [ ] `Classic`, `Enhanced`, `Studio`, `Diagnostic`.
- [ ] benchmark de FPS/sweep/CPU/RAM.

**Gate F4:** Enhanced utilizável em tempo real; Studio opcional.

## F5 — microSD Extension Platform

- [ ] estrutura `/NANOVNA/` versionada.
- [ ] presets/layouts externos.
- [ ] temas e idiomas.
- [ ] scripts seguros.
- [ ] calibrações.
- [ ] S1P/S2P/screenshots.
- [ ] histórico de medições e comparação.
- [ ] schema versionado.
- [ ] comportamento seguro sem cartão.

## F6 — USB Protocol & NanoVNA Bridge

- [ ] inventariar comandos USB/serial.
- [ ] protocolo interno normalizado.
- [ ] discovery/reconnect.
- [ ] REST API.
- [ ] WebSocket de sweep.
- [ ] logging/diagnostics.
- [ ] macOS primeiro; Linux/Windows depois.

**Gate F6:** S11/S21 chegam continuamente ao navegador via bridge sem alterar RF core.

## F7 — Web Dashboard / PWA

- [ ] gráfico cartesiano e Smith interativos.
- [ ] markers/cursores.
- [ ] cards configuráveis.
- [ ] presets compartilhados.
- [ ] histórico/comparação.
- [ ] Touchstone import/export.
- [ ] relatório de medição.
- [ ] responsivo/PWA/LAN.

## F8 — Smart Analysis

- [ ] resonance finder.
- [ ] SWR min/max e target offset.
- [ ] bandwidth configurável.
- [ ] Q estimado.
- [ ] insertion loss.
- [ ] peak/notch detection.
- [ ] drift/comparison.
- [ ] cable/TDR helpers.
- [ ] diagnósticos explicáveis.

## F9 — SmartLink ESP32-S3 Proof of Concept

- [ ] ESP32-S3 N16R8 como referência.
- [ ] USB Host CDC-ACM.
- [ ] VBUS protegido / sem backfeed.
- [ ] parser NanoVNA.
- [ ] Wi‑Fi AP/STA.
- [ ] HTTP/WebSocket mínimo.
- [ ] reconexão robusta.

**Gate F9:** celular recebe sweep ao vivo via Wi‑Fi sem computador.

## F10 — Wireless Platform

- [ ] mDNS `nanovna.local`.
- [ ] provisioning Wi‑Fi.
- [ ] BLE opcional.
- [ ] PSRAM ring buffers.
- [ ] microSD adicional.
- [ ] cache/histórico.
- [ ] OTA ESP32.
- [ ] segurança/offline-first.
- [ ] enclosure.

## F11 — Edge Intelligence / TinyML Experimental

- [ ] dataset por features.
- [ ] feature extraction.
- [ ] classificador simples.
- [ ] benchmark RAM/latência/acurácia.
- [ ] fallback determinístico.
- [ ] modelos versionados.

## F12 — External AI Integration

- [ ] resumo estruturado de medição.
- [ ] consentimento explícito para cloud.
- [ ] integração de IA opcional.
- [ ] explicação textual e comparação histórica.
- [ ] relatório técnico.
- [ ] operação local preservada.

## F13 — Hardening & Validation

- [ ] regressão RF/calibração.
- [ ] soak USB/Wi‑Fi.
- [ ] remoção/corrupção SD.
- [ ] brownout/power-cycle.
- [ ] limites de memória.
- [ ] watchdog/fail-safe.
- [ ] matriz de hardware.

## F14 — Packaging & Releases

- [ ] hardware suportado.
- [ ] checksums/releases.
- [ ] release notes.
- [ ] versionamento compatível entre firmware/bridge/web/SmartLink.
- [ ] recovery guide.
- [ ] documentação/screenshots.
- [ ] política de upstream sync.

## Prioridade imediata

1. Fechar F0: USB/DFU/hardware fingerprint.
2. Fechar F1: upstream pin + build original reproduzível.
3. Só então iniciar Modern UI.

Não fazer flash experimental, mudanças de DSP ou integração ESP32 antes dos gates de recuperação e build reproduzível.
