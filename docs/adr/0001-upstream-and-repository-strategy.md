# ADR-0001 — Upstream and repository strategy

**Status:** Accepted for foundation; firmware import deferred.

## Context

NanoVNA Modern precisa evoluir firmware, bridge web e SmartLink sem perder rastreabilidade do NanoVNA-D nem misturar alterações de RF com UI.

## Decision

`abraaobat/nanovna-modern` será o umbrella repository. O código do `DiSlord/NanoVNA-D` não será copiado imediatamente.

Antes da F1:

1. confirmar licença e obrigações de atribuição;
2. fixar commit/tag upstream;
3. escolher fork/submodule/subtree ou repo separado para firmware;
4. reproduzir `TARGET=F303` sem mudanças;
5. adicionar CI;
6. somente depois abrir branch de Modern UI.

Bridge, web, protocol, SmartLink e hardware ficam no umbrella repository nesta fase.

## Consequences

- preserva origem e facilita upstream sync;
- reduz risco de alterações acidentais no measurement core;
- posterga decisão irreversível de monorepo/submodule até haver evidência prática.
