# Registro de continuidade — banco Apoena Skill, Cérebro e runners

- Data/hora do registro: 2026-11-04T01:50:30Z (horário informado na mensagem do usuário).
- Fonte: conversa atual do ChatGPT e consultas GitHub autorizadas realizadas nesta sessão.
- Cobertura: PARCIAL — registra as mensagens e ações acessíveis nesta conversa; não representa exportação integral de outros históricos privados.

## Pedido explícito do autor

O autor determinou que o Amigo Apoena/Alberto deve manter o banco de conhecimento atualizado antes e durante o trabalho, considerar os vários runners ativos do ecossistema e salvar backups tanto no repositório Apoena Skill quanto no Cérebro do Amigo Apoena. Também autorizou considerar os runners de Apoena Skill e Cérebro para trabalho quando compatíveis.

## Contexto técnico preservado

### GameCreator — PR #14

- Repositório: `LORECRONICASAPOENA/GameCreator`.
- PR #14: `feat/apoena-modular-character-creator-integration`, aberta, draft, não mesclada no último estado consultado.
- Correção de teste enviada em dois commits:
  - `55f3cf8189dccbebd774f129af0d002b7a6fed9b`: hook de avanço determinístico de animação para o harness.
  - `4f90fc8739b4af351c929a97d8ed73c094477c36`: assertion de reprodução de quadros sem depender exclusivamente do relógio do navegador.
- Workflow observado para o novo SHA: run `41755565658`, estado `pending` na última consulta. Não declarar correção validada até resultado final do run e revisão dos jobs/logs.
- Checkpoint pré-correção: `backups/2026-11-04-pr14-character-browser-before-fix.md`, commit `8fd76ffb7acf3054c6c4c3aba0a6431ec661f799`.
- Próximo passo: acompanhar run pendente no SHA exato; confirmar se o teste do browser passou e se as etapas subsequentes executaram. Se falhar, usar o log novo como evidência e continuar diagnóstico. Não fazer merge.

### Integração de poderes do AGAR no Pixel Art

- Pedido do autor: examinar poderes e botões de cada personagem no AGAR e adaptá-los ao Pixel Art sem perder funcionalidades existentes.
- AGAR é projeto Godot 3D; Pixel Art é runtime HTML/Godot 2D/2.5D. Não copiar scripts/cenas 3D diretamente.
- Catálogo de cinco personagens e habilidades foi levantado em análise anterior; alguns kits são provisórios e não devem ser promovidos a cânone sem confirmação.
- A integração de gameplay ainda não foi iniciada porque o fluxo GameCreator/Pixel Art está sujeito a WIP=1 e a PR #14 aguarda validação.
- Após encerrar a PR #14, abrir branch isolada para portar/adaptar habilidades, com contrato de habilidade, controles, custos, cooldowns, efeitos, animações, colisões e testes HTML/Godot/Android.

### Kael — personagem da conversa

- Nome corrigido pelo autor: **Kael** (substitui Ruf no contexto desta conversa).
- Idade: 12 anos; Tribo da Terra; afinidades Terra e Água; estilo Floresta.
- Poderes informados: Q Esfera de Terra; W Avalanche; E Escudo de Terra; R Magia da Floresta; A Artes Marciais; S Especial Floresta Mirim, veneno de -5% da vida a cada 10 segundos.
- Falta decidir se os 5% incidem sobre vida máxima ou atual.
- Sprite enviado pelo autor; ainda não transferido como binário ao repositório nesta etapa.
- Regra visual explicitada pelo autor: cada personagem terá spritesheet de **4 colunas de largura × 6 linhas de altura (4×6), 24 quadros**, preservando grade, proporções e transparência conforme asset final. Isso é requisito de produção de sprites; não confundir com dimensões em pixels, que devem ser definidas por quadro/asset.

## Banco de conhecimento e runners

- Repositório `apoenaskil`: privado? **Público**, branch padrão `main`, permissão de escrita/admin confirmada para a conexão utilizada.
- Repositório `CEREBRO-AMIGO-APOENA`: privado, branch padrão `main`, permissão de escrita/admin confirmada.
- Em ambos, consulta REST de `actions/runs?per_page=10` retornou zero workflows registrados. A tentativa de consultar `actions/runners` pela ferramenta disponível foi rejeitada como endpoint não permitido. Portanto, **não foi possível verificar online/offline, labels ou capacidade dos runners** nesta execução.
- A listagem `.github/workflows` não foi encontrada via Contents API nos dois repositórios. Isso não prova que não existam runners organizacionais; indica apenas que não há workflow de repositório confirmado nesta consulta.
- Não foi disparado job artificial nem criado workflow vazio. Para usar runners nesses repositórios, primeiro identificar workflow real e compatível, confirmar runner/labels e isolamento do workspace; só então executar teste de documentação/build adequado.
- O runner do GameCreator e o runner do Pixel Art não devem ser presumidos livres nem compatíveis com Apoena Skill/Cérebro sem verificação.
- Limite de concorrência: manter WIP=1 entre GameCreator e Pixel Art; tarefas documentais independentes podem ser preparadas em branches isoladas, sem escrever no mesmo workspace ou alterar arquivos concorrentes.

## Diretriz operacional solicitada pelo autor

Antes de cada tarefa:
1. Atualizar estado do repositório, branch, commit, PRs, Actions, issues e documentação relevante.
2. Consultar o banco Apoena Skill e o Cérebro para recuperar decisões e pendências.
3. Verificar jobs e runners acessíveis; registrar runner/labels/run ID/SHA quando observáveis.
4. Distribuir apenas tarefas independentes e compatíveis entre runners disponíveis; nunca iniciar concorrência sobre o mesmo workspace/arquivo.
5. Após cada marco, salvar checkpoint no repositório dono do projeto e confirmar relendo o arquivo.
6. No final, reconciliar o registro de conhecimento com commits e testes reais.

## Estado deste backup

Este documento registra o estado de continuidade e os limites de observação. Não declara que os runners foram usados, que o run #41755565658 terminou, que os poderes foram integrados ao Pixel Art ou que o sprite binário foi salvo. Esses itens permanecem pendentes até evidência verificável.

## Evidência visual adicional de runners — 2026-11-04T01:51:42Z

O autor forneceu uma captura de tela dos terminais Windows dos runners. A inspeção visual identifica quatro terminais/processos de runner conectados ao GitHub:
1. Terminal CMD à esquerda: executou o job `validar`; a tela mostra início às `2026-11-04 01:48:17Z` e conclusão `Succeeded` às `2026-11-04 01:50:10Z`.
2. Terminal CMD superior à direita: mostra `Connected to GitHub` e `Listening for Jobs` às `01:42:43Z`.
3. Terminal PowerShell central: mostra `Connected to GitHub` e `Listening for Jobs` às `01:46:39Z`.
4. Terminal PowerShell inferior à direita: mostra `Connected to GitHub` e `Listening for Jobs` às `01:47:55Z`.

**Classificação:** evidência visual fornecida pelo autor; confirma quatro terminais/processos conectados no instante mostrado, um deles tendo concluído com sucesso o job `validar`. A captura não mostra nomes individuais dos runners, labels, grupos, repositórios autorizados, nem comprova que todos continuem online neste momento. Consultar a atribuição real dos jobs e os labels antes de despachar tarefas. Esta evidência corrige a limitação da consulta anterior, que não conseguira ler a API de runners.

## Checkpoint de continuidade — 2026-11-04T11:30:03Z

### Estado da conversa e decisões do autor
- O autor pediu pesquisa de layouts mais limpos e modernos para menus e interfaces do jogo Apoena.
- Foram discutidas referências e uma proposta preliminar de redesign para Pixel Art e AGAR 3D. A análise de código confirmou que o AGAR já possui hub ilustrado com hotspots em `scripts/hub_agar.gd`; o Pixel Art tem menu Godot e runtime HTML distintos, conforme `docs/ORGANIZACAO.md`.
- **Decisão explícita do autor:** “AINDA VAMOS PENSAR NISSO”. Portanto, o redesign está **adiado/em avaliação**. Não alterar menus, cenas, HUD, cores ou navegação até nova aprovação. As referências são inspiração, não decisão de identidade visual nem especificação aprovada.
- O autor solicitou agora backup da conversa. Este checkpoint preserva a decisão e o estado; não representa alteração de código.

### Pesquisa de 500 oportunidades
- Catálogo arquivado em Apoena Skill: `apoena/docs/research/2026-11-04-pesquisa-500-oportunidades.md` e documento extenso de 500 itens em `apoena/docs/research/500-oportunidades-jogo-apoena-2026-11-04.md` (se disponível nesta branch).
- Cópia no Cérebro: `backups/pesquisas/2026-11-04-pesquisa-500-oportunidades.md`.
- São oportunidades de backlog, não 500 bugs confirmados nem recursos implementados. Nenhum código foi alterado durante essa pesquisa.

### Regras visuais e de gameplay preservadas
- Spritesheet de cada personagem: grade de **4 colunas × 6 linhas (4×6), 24 células**. A resolução em pixels de cada quadro ainda precisa ser definida no pipeline; 4×6 significa quantidade de células, não tamanho em pixels.
- Kael: 12 anos, Tribo da Terra, afinidades Terra e Água, estilo Floresta; kit descrito pelo autor anteriormente. Não inferir mudanças de cânone.
- A integração dos poderes do AGAR ao Pixel Art permanece pendente; adaptar mecânicas 3D para 2D/2.5D, sem copiar cenas/scripts diretamente.

### Runners
- Captura de tela fornecida pelo autor às 01:51:42Z mostrava quatro terminais Windows conectados: um concluiu job `validar` com `Succeeded` às 01:50:10Z e três aguardavam jobs. Evidência histórica, não disponibilidade atual. Verificar online/labels/grupos/repositórios antes de atribuir novas tarefas.

### Segurança de continuidade
- Preservar WIP=1 entre GameCreator e Pixel Art quando compartilharem a mesma linha de implementação.
- Antes de cada nova tarefa, atualizar branch/SHA/PR/Actions e consultar as bases Apoena Skill e Cérebro.
- Backups e documentos devem ser confirmados por releitura. Não afirmar que o plugin instalado foi atualizado só porque o repositório de origem mudou.

### O que NÃO foi feito neste checkpoint
- Nenhum redesign foi implementado.
- Nenhum menu ou HUD foi modificado.
- Nenhuma alteração de código ou build foi feita.
- Não foi executado novo teste de jogo nesta rodada.
