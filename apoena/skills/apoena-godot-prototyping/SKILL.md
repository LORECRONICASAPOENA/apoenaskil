---
name: apoena-godot-prototyping
description: Orienta prototipagem e transferência de ideias do teste HTML para o projeto Godot Apoena, sem confundir prova rápida com entrega final.
---
# Skill — Prototipagem HTML e produção Godot

## Decisão explícita do autor
HTML serve para **testar rapidamente no celular**. O jogo pronto deve seguir para **Godot**. Preserve essa separação ao sugerir arquitetura, organizar tarefas ou documentar entregas.

## Regras de trabalho
- O HTML pode servir como protótipo rápido de interação e validação de ideia; não o trate como entrega final do jogo.
- A versão Godot é o destino de produção. Antes de declarar paridade, testar cada implementação: HTML e Godot podem ter código, saves e comportamento separados.
- Não afirme que um APK foi produzido ou validado sem evidência de exportação e teste em dispositivo.
- O protótipo Pixel Art documenta câmera 2.5D inicial: câmera 2D elevada, acompanhamento do personagem, zoom e ordenação por Y. Isso não é uma câmera 3D 360° nem isometria completa.
- O autor levantou preocupação sobre mapas muito grandes no Godot. Não há, no registro recuperado, decisão de arquitetura de mundo gigantesco. Técnicas como regiões, chunks, carregamento sob demanda e limites de simulação devem ser apresentadas como opções a avaliar, não como arquitetura aprovada.
- Separar o jogo Pixel Art do projeto Godot 3D `JOGO-APOENA-AGAR-`, do GameCreator e do Studio Maker.
- Manter ativos, fontes e dados no repositório proprietário correto; evitar copiar código de ferramenta de autoria para o runtime.

## Checklist de transferência de protótipo
1. Descrever o comportamento que o HTML comprovou e o que não comprovou.
2. Identificar dados, estados e regras que devem migrar.
3. Reimplementar no Godot de forma compatível com a arquitetura existente, sem presumir conversão automática de HTML para Godot.
4. Comparar o comportamento e registrar diferenças.
5. Executar testes automatizados disponíveis e, quando relevante, teste manual em aparelho.
6. Registrar limitações e deixar pendências visíveis.

## Referências
- `docs/game-design-notes.md`
- Repositório `apoenalore/Apoena-pixel-art-html`, especialmente `docs/ORGANIZACAO.md` e `docs/ECOSSISTEMA.md`.
- Repositório `apoenalore/JOGO-APOENA-AGAR-`, somente quando a tarefa for desse projeto.


## Continuidade técnica — auditoria de PRs do Pixel Art HTML (2026-11-04)

- Antes de editar, confirme o HEAD real de cada PR e compare sua branch com `main`; PR antiga pode estar muito à frente e atrás, com arquivos e decisões posteriores sobrepostos.
- Não confunda `mergeable`, checks verdes, aprovação de review e merge. Um run de outro SHA/branch não valida o HEAD atual.
- Para PRs que compartilham arquivos de clima/hidrologia/exploração, defina sequência de integração e preserve o comportamento exclusivo de cada branch. Não faça merge em massa.
- Em Actions, diferencie `queued`, `in_progress`, `failure`, `cancelled` e `success`. Job queued sem runner_id não é falha de código.
- Não execute código de pull request não confiável em runner self-hosted persistente. Prefira runner hospedado/efêmero para PRs; `persist-credentials: false` não isola o host.
- Use concurrency group com número da PR para eventos pull_request e ref/evento para push, evitando cancelamento cruzado.
- Mantenha uma única workflow canônica para testes compartilhados; workflows especializados devem executar apenas verificações exclusivas da funcionalidade.
- Smoke test Godot deve observar código de saída e saída textual, incluindo `SCRIPT ERROR:` e `ERROR:`; exit code zero sozinho não garante inicialização válida.
- Valide importação de mapas: aceitar apenas valores de tile que o renderer reconhece e rejeitar objetos nulos, primitivos ou arrays quando o contrato exige objetos.
- Em canvas 2D, manter limites horizontais e verticais independentes (`MAX_X`, `MAX_Y`); validar clamp e renderização em mapas retangulares, não só quadrados.
- Controles de jogo devem funcionar por toque, mouse, teclado e tecnologia assistiva. Preferir `click` para ações de botão; atalhos como Space não devem bloquear ativação normal de controles focados; evitar sobreposição de hitboxes.
- Em Godot, evitar que botões de HUD retenham foco indevido quando isso interfere em atalhos globais; validar navegação por teclado e controle touch separadamente.
- Para cada finding CodeRabbit, verificar se ainda se aplica ao SHA atual antes de corrigir; findings antigos não são prova de defeito atual. Registrar os findings descartados com razão.
- Para erros GitHub/Git, usar o catálogo de 500 cenários da Skill de diagnóstico como índice de hipóteses (50 famílias × 10 contextos), não como 500 erros oficiais. Confirmar com logs, código, documentação oficial e reprodução.
- Manter WIP=1 combinado entre GameCreator e Pixel Art; não disparar execuções equivalentes em paralelo.
- Não declarar Android pronto sem exportação APK e teste físico. HTML é protótipo rápido; Godot é destino de produção.
- Para personagens anime 2D Apoena, preservar o formato de spritesheet 4×6 (4 colunas × 6 linhas) da Skill de sprites: 24 células iguais, transparência RGBA real e identidade visual consistente. Validar o caminho de importação do GameCreator para `assets/personagens/<id>/spritesheet.png` no runtime antes de declarar integração.

**Registro de continuidade:** `../docs/recovery/session-2026-11-04-pixel-art-pr-audit-and-backup.md`. O registro é parcial e inclui os SHAs, runs, PRs, findings, bloqueios e pendências verificados em 2026-11-04; não representa implementação ou merge.
