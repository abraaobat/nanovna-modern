# microSD Extension Platform

O microSD amplia armazenamento e modularidade, não RAM do STM32.

## Layout proposto

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

## Recursos

- presets e dashboards declarativos;
- temas/idiomas;
- scripts `.cmd` restritos;
- calibrações;
- Touchstone S1P/S2P;
- histórico e comparação de medições;
- screenshots;
- assinaturas/modelos compactos de análise.

## Regras

- Firmware deve funcionar plenamente sem cartão.
- Arquivos terão `schemaVersion`.
- Conteúdo inválido não pode bloquear boot.
- Não executar código nativo arbitrário do SD.
- Escritas críticas devem ser atômicas quando possível.
- Histórico deve permitir rotação/limites para evitar desgaste e corrupção.
