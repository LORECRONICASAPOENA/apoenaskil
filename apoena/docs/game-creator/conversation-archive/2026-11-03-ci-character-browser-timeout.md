# Incidente CI — Criador Modular de Personagens — 2026-11-02/03

**Run original:** https://github.com/apoenalore/GameCreator/actions/runs/41547503382  
**Commit original:** 11ca300ddf32d979f7742b9278c1c6e281e11d92  
**Run de revalidação:** https://github.com/apoenalore/GameCreator/actions/runs/41551596668  
**Commit com correção do harness:** 9ab514b4edf72dd363d46fd69ed67c7cdc42f552  
**Documento técnico operacional:** [GameCreator docs/ci/INCIDENT-2026-11-02-character-browser-timeout.md](https://github.com/apoenalore/GameCreator/blob/feat/apoena-modular-character-creator-integration/docs/ci/INCIDENT-2026-11-02-character-browser-timeout.md)

## Diagnóstico recuperado

O run original passou build, verificações DOM, sintaxe JS e teste do modelo de personagem. Falhou somente em “Testar Criador Modular no navegador”. O servidor de teste iniciou normalmente e não houve erro de stderr do servidor. O artefato v41-ci-diagnostics foi baixado e examinado.

Mensagem:
`Timeout aguardando fila de operações. Status: Prévia pronta. Revise antes de aplicar.`

O harness tinha timeout interno de 5s em Promise.race enquanto o Chrome era iniciado com --virtual-time-budget=30000. A causa imediata confirmada é que o próprio harness rejeitou a espera pela fila. A hipótese é competição entre timer virtual e operações assíncronas de imagem/canvas. O status sugere que o corte inteligente produziu prévia, mas não identifica definitivamente qual operação anterior deixou a fila pendente.

## Correção escolhida

No arquivo tests/personagens-browser.html, foi removido o timer concorrente de 5s e mantida a espera pela Promise real `whenIdle()`. Isso não desativa o teste nem altera o runtime; evita um timeout artificial enquanto o navegador controla o tempo virtual.

Novo run foi disparado no commit 9ab514b4edf72dd363d46fd69ed67c7cdc42f552. No momento do registro, estava em andamento; portanto, não declarar resolvido até aprovação da etapa de navegador e do workflow completo.

## Governança

O GameCreator contém o relatório técnico operacional e AGENTS.md foi atualizado para exigir relatório de causa, solução, justificativa e revalidação para cada falha do Actions. Apoena Skill mantém este resumo e o histórico/proveniência central, sem copiar código-fonte.
