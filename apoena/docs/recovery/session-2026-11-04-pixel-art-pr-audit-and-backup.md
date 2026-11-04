# Recuperação e auditoria — Apoena Pixel Art HTML — 2026-11-04

**Registro:** 2026-11-04T17:06:45-03:00  
**Fonte temporal:** mensagem do usuário enviada em 2026-11-04T20:06:45Z.  
**Escopo:** manutenção de Pull Requests, CI, segurança operacional, continuidade da integração HTML/Godot e personagens 2D anime.  
**Status geral:** PARCIAL — auditoria GitHub ao vivo realizada; correções de código e validação final ainda pendentes.  
**Repositório auditado:** [LORECRONICASAPOENA/Apoena-pixel-art-html](https://github.com/LORECRONICASAPOENA/Apoena-pixel-art-html).  
**Branch de documentação:** `docs/pixel-art-pr-audit-20261104` deste repositório de Skills.

## 1. Proveniência e cobertura

- Fonte principal: mensagens visíveis desta conversa e screenshot da página Pull requests do GitHub enviada pelo usuário.
- Screenshot recebido: `image(20261104-200446).png`. Foi visualmente consultado nesta conversa; o binário não foi copiado para este repositório.
- Consulta ao vivo via conexão GitHub: metadados das PRs #3, #4, #5, #6 e #10; comparação de branches; workflows associados aos SHAs consultados; arquivos README, AGENTS e base de CI; comentários e achados CodeRabbit da PR #5; issues #8 e #9.
- Consulta da base Apoena Skill: instruções de raiz, protocolo de preservação, legenda de proveniência, índice e Skills de gameplay/Godot.
- **Limite:** isto não é exportação integral de todo o histórico privado do ChatGPT. É um backup parcial, derivado das mensagens e evidências acessíveis nesta sessão. Não afirmar recuperação integral da conversa.

## 2. Estado observado no GitHub

Referência da consulta: 2026-11-04, aproximadamente 17:06 BRT. Sempre reconsultar antes de novas ações.

| PR | Head consultado | Relação com main no momento da consulta | CI/evidência | Estado e ação recomendada |
|---|---|---|---|---|
| #3 — Offline/LAN | `cd898a82e3d6e0d3c536fea16f25d977b712c8ce` | 17 commits à frente, 40 atrás; divergente | Run 40961954483 = success no SHA consultado | Draft; não integrar. Exige teste LAN em dois dispositivos e validação Android real. Reconciliar branch com main com diff preservado. |
| #4 — Hidrologia 2D | `9e86e5fb705bb3851eaedef3b07ff00e736e2d3a` | 16 à frente, 1 atrás; divergente | Runs 41895912199 e 41895912244 = success | Aberta, não mesclada; GitHub informou mergeable=true na consulta mais recente. Fazer revisão do diff e confirmar testes manuais antes de decidir merge. |
| #5 — Calendário/clima/hidrologia | `539b901a9a9b1aa3f4fc491dee47460a7e9b46d3` | 86 à frente, 15 atrás; divergente | Nenhum run PR associado retornado pelo endpoint consultado | Aberta, não mesclada; mergeable=false. Branch muito divergente e sobreposição com #4. Não fazer merge em massa. Verificar gatilhos, conflitos e findings no HEAD atual. |
| #6 — Diário técnico | `dae2581fe9c70c407c3f564c78f6942e56548eeb` | 5 à frente, 22 atrás; divergente | Nenhum run PR associado retornado pelo endpoint consultado | Aberta, não mesclada; mergeable=false. Conteúdo documental sobreposto; reconciliar com main e preservar ambas as versões. |
| #10 — Finais de linha | `78926f01a9cf7f38b7d84e403cf49ea353e39ea4` | PR encerrada | Mesclada, confirmou `.gitattributes` | Integrada. A PR não normalizou automaticamente os arquivos locais; cada clone deve preservar alterações não commitadas antes de normalização controlada. |

**Nota:** status vazio no endpoint de combined commit status não equivale a falha; para as PRs sem runs associados, a validação continua não comprovada. Não confundir mergeable, checks verdes, aprovação e merge.

## 3. Issues e riscos de governança

- [Issue #8 — Habilitar proteção da branch main](https://github.com/LORECRONICASAPOENA/Apoena-pixel-art-html/issues/8): registro existente informa `main protected=false`. A leitura das regras foi bloqueada por 403; a sessão não expôs operação de escrita para configurar branch protection/rulesets. Manter o repositório privado; não contornar plano/permissão tornando-o público. Confirmar entitlement e permissão administrativa, depois exigir PR, checks, resolução de conversas e bloquear force-push/exclusão quando disponível.
- [Issue #9 — Desbloquear validação da PR #7](https://github.com/LORECRONICASAPOENA/Apoena-pixel-art-html/issues/9): job #27 estava queued com runner_id=0, sem started_at. Ação depende do computador Windows: preservar `_diag`, conferir `Runner-Pixel-Art` e iniciar apenas o serviço ou a única instância `run.cmd`, nunca ambos. Não foi confirmado nesta sessão que o runner foi reparado.
- Regra do projeto: WIP=1 combinado entre GameCreator e Pixel Art. Não disparar workflows equivalentes nem duplicar runner.

## 4. Findings de CodeRabbit na PR #5

Os comentários disponíveis incluem uma revisão anterior com findings e uma solicitação posterior do autor para revisar o HEAD `539b901a9a9b1aa3f4fc491dee47460a7e9b46d3`. O resultado dessa revisão mais recente não foi retornado nesta consulta. Portanto, os itens abaixo são **achados a revalidar no HEAD atual**, não uma afirmação de que todos ainda persistem:

1. Smoke test Godot deve falhar também diante de `SCRIPT ERROR:` ou `ERROR:`, mesmo com exit code zero.
2. Separar grupos de concorrência entre push e pull_request.
3. Isolar código não confiável de PR em runner hospedado/efêmero; `persist-credentials: false` não isola máquina self-hosted persistente.
4. Rejeitar valores de tile não suportados (4–999) ou implementar renderização válida.
5. Validar entradas de `data.objects` contra null, primitivos e arrays antes de aceitar projeto.
6. Corrigir usos residuais de `MAX` para `MAX_X`/`MAX_Y` e clamp independente por eixo em `exploracao.html`.
7. Usar número da PR no concurrency group para evitar cancelamento entre PRs distintas.
8. Manter verificações compartilhadas apenas no workflow canônico, evitando duplicação de testes.
9. Sincronizar documentação com gatilhos e concorrência do workflow real.
10. Corrigir documentação do runner de `validar-godot.yml`.
11. Registrar hora de identificação dos incidentes; se não preservada, declarar explicitamente.
12. Usar runner efêmero/hospedado para execução de código de PR ou provar isolamento real do host persistente.
13. Garantir que atalhos de teclado não bloqueiem Space para controles focados.
14. Usar evento `click` no botão Atacar para suportar teclado e tecnologia assistiva.
15. Separar visualmente/funcionalmente os botões Atacar e Semear, que foram apontados como sobrepostos.
16. Impedir que o botão TEMPO retenha foco indevido e capture Space.
17. Revisar findings relacionados ao workflow auxiliar `validar-ambiente-windows.yml`, pois o histórico do review inclui esse arquivo e o estado atual pode ter mudado.

O comentário de 2026-11-04 19:55:52Z pediu explicitamente nova revisão no HEAD #5, verificando se o workflow dispara, se PRs ficam isoladas do self-hosted e se os findings antigos continuam válidos. Não há resultado novo de CodeRabbit confirmado neste registro.

## 5. Evidências técnicas adicionais

- O workflow canônico em `.github/workflows/validar-pixel-art-windows.yml` na main usa runner `[self-hosted, Windows, X64, pixel-art]`, com triggers push/main e pull_request/main; `cancel-in-progress: true`.
- Na branch #5, o workflow foi alterado para escolher `windows-latest` para pull_request e runner self-hosted para outros eventos. Isso é uma mudança de segurança positiva em princípio, mas precisa validar YAML, paths, evento e execução real.
- O workflow auxiliar `.github/workflows/validar-godot.yml` na main ainda usa self-hosted Windows. A branch #5 mudou para `windows-latest` e removeu testes compartilhados em uma versão consultada. Validar se o filtro de paths da workflow base realmente permite que a alteração do próprio workflow dispare o check.
- #4 e #5 compartilham arquivos de hidrologia/exploração; #5 contém `hidrologia_browser.js` e altera `exploracao.html`, enquanto #4 adiciona o motor de hidrologia. A sequência de integração deve resolver dependências e conflitos sem duplicar/descartar funcionalidades.
- README da main esclarece que o projeto é HTML + Godot 4 + Android; HTML é protótipo/teste rápido e Godot é destino de produção. Nenhum APK foi produzido ou validado conforme o README.
- O GameCreator é repositório separado. Ele exporta sprites e dados; o runtime Pixel Art é consumidor. Não confundir os workflows, runners, commits ou validações dos dois repositórios.

## 6. Catálogo de 500 cenários

A Skill instalada `diagnostico-erros-github` possui um catálogo de 500 cartões práticos, organizados em 50 famílias × 10 contextos (PowerShell, Git Bash, macOS/Linux, VS Code, GitHub Desktop, CLI, Actions, REST API, interface web/PR e Codespaces). O catálogo não é uma lista de 500 mensagens literais oficiais. Usar como índice de hipóteses e confirmar a causa pela mensagem/log real, documentação atual e estado do repositório. Não disparar 500 buscas nem aplicar correções genéricas em lote.

## 7. Personagens e sprites 2D anime

- Requisito visual do projeto: personagens Apoena em anime 2D; não converter automaticamente para pixel art estrita.
- Formato de folha padrão Apoena já registrado na Skill de sprites: grade 4 colunas × 6 linhas, 24 células idênticas, PNG RGBA com transparência real, sem guias/fundo/quadriculado no export.
- Preservar identidade, rosto, cabelo, roupas, paleta, acessórios e escala entre quadros; manter cada personagem centralizado na célula e impedir cruzamento entre células.
- Para cada personagem, manter a referência original, ficha aprovada, dimensões da célula, mapa de vistas/animações e validação de importação no Godot.
- O README do runtime informa caminhos de exportação em `assets/personagens/<id>/spritesheet.png`; conferir `assets/LEIA-ME.md` e contrato do GameCreator antes de afirmar importação.
- Não há nesta sessão um sprite binário novo recebido ou importado; o pedido “personagens em sprites 2D anime” permanece requisito de continuidade, não implementação concluída.

## 8. Próximas ações priorizadas

1. Reconsultar PR #5 e aguardar/obter a revisão CodeRabbit do SHA atual; confirmar quais findings persistem.
2. Resolver primeiro a segurança do runner de PR e o disparo do workflow canônico. Não executar código de PR não confiável em host persistente.
3. Escolher uma sequência de integração entre #4 e #5, pois compartilham arquivos; comparar diffs atuais e reconciliar com main.
4. Corrigir e testar findings funcionais confirmados: limites X/Y, tiles/objetos inválidos, botões e atalhos.
5. Reconciliar #6 com main preservando a documentação útil, sem sobrescrever alterações posteriores.
6. Manter #3 em Draft até testes LAN em dois dispositivos, sincronização autoritativa e validação Android real.
7. Tratar proteção da main (#8) e runner (#9) como bloqueios externos que exigem configuração/ação no GitHub ou no PC.
8. Registrar cada correção com SHA, run ID, job/step, log causal, teste e resultado. Só declarar resolvido depois de CI no SHA final e teste de dispositivo quando aplicável.

## 9. Estado deste backup

**Salvo:** este registro parcial de auditoria e continuidade, com links e SHAs consultados.  
**Não salvo:** screenshot binário original, exportação integral da conversa, nem alterações de código no repositório Pixel Art.  
**Não executado:** merge das PRs #3–#6, mudança de proteção da main, reinicialização do runner físico, teste em dois dispositivos, exportação APK e importação de novos sprites.  
**Classificação final:** PARCIAL / IMPLEMENTAÇÃO PENDENTE / NÃO DECLARAR PROJETO CONCLUÍDO.


## 10. Revalidação dirigida dos findings no HEAD #5

**Inspeção adicional registrada:** 2026-11-04T17:11:51-03:00.  
**Branch:** `feat/tempo-biomas-hidrologia`.  
**HEAD:** `539b901a9a9b1aa3f4fc491dee47460a7e9b46d3`.

A leitura direta dos arquivos da branch mostrou que vários findings antigos já foram tratados no HEAD atual consultado:

| Finding antigo | Evidência no HEAD #5 | Resultado |
|---|---|---|
| Limites `MAX` removidos e uso de `MAX_X/MAX_Y` | `exploracao.html`: render usa MAX_X/MAX_Y; rio termina em MAX_X; pointerdown limita X e Y separadamente | CORRIGIDO no código consultado |
| Atalho Space bloqueando controles | handler verifica se o alvo está dentro de button/input/select/textarea/contenteditable e retorna antes do atalho | CORRIGIDO no código consultado |
| Botão Atacar não acessível por teclado/assistive tech | listener usa `click` no botão Atacar | CORRIGIDO no código consultado |
| Tiles 4–999 aceitos indevidamente | `mapa_creator_browser.js` rejeita valores fora de 0–3 e 1000–2023 | CORRIGIDO no código consultado |
| Objetos nulos/primitivos em `data.objects` | `mapa_creator_browser.js` rejeita null, não-objetos e arrays | CORRIGIDO no código consultado |
| Botão TEMPO retendo foco | `tempo_btn.focus_mode = Control.FOCUS_NONE` | CORRIGIDO no código consultado |
| Sobreposição Atacar/Semear no Godot | Atacar ocupa offsets verticais -75 a -14; Semear -145 a -84 | NÃO REPRODUZIDO no HEAD atual; áreas verticais separadas |
| Smoke test Godot aceita erro de script com exit code zero | workflow captura output e falha se encontrar `SCRIPT ERROR:` ou `ERROR:` | CORRIGIDO no código consultado |
| Concurrency de PRs por nome de branch | workflows consultados usam `github.event.pull_request.number || github.ref` | CORRIGIDO no código consultado |
| Execução de PR no self-hosted persistente | workflow canônico da branch #5 seleciona `windows-latest` para pull_request; workflow especializado de sessões também usa `windows-latest` | CORRIGIDO no desenho da branch consultada; ainda falta comprovar run efetivo |
| Testes compartilhados duplicados no workflow especializado | `validar-godot.yml` da branch #5 mantém apenas teste específico de sessões | CORRIGIDO no código consultado |

**Ainda pendente:**
- Não há run PR associado ao SHA #5 retornado pela consulta `fetch_commit_workflow_runs`; por isso não se pode afirmar que a alteração de runner e os workflows executaram no HEAD.
- A PR #5 permanece `mergeable=false`, com 86 commits à frente e 15 atrás de main. A divergência/conflicto precisa ser reconciliada preservando o código de ambas as linhas de trabalho.
- A revisão CodeRabbit mais recente solicitada pelo autor em 2026-11-04 ainda não teve resultado visível nesta consulta.
- A revisão acima confirma somente os trechos inspecionados; não substitui execução, teste de navegador, teste Godot, revisão integral do diff ou aprovação humana.

**Conclusão da revalidação:** findings antigos não devem ser tratados como defeitos atuais sem checar o SHA. Diversas correções já estão presentes na branch #5. O bloqueio central mudou de “corrigir todos os findings antigos” para “obter validação CI no HEAD atual e reconciliar a grande divergência com main sem perda”.


## 11. Backup complementar desta conversa — 2026-11-04T20:15:18Z

**Solicitação:** o usuário pediu explicitamente backup da conversa usando Amigo Apoena, GitHub e Notion.

**Ações realizadas nesta etapa:**
- Localizada a página Notion existente **“Backup de Conversa — Apoena, GitHub Actions e Runners — 04/11/2026”** para atualizar o registro canônico, evitando criar uma página duplicada.
- Confirmada a existência da PR [#20 — Registrar auditoria e continuidade do Apoena Pixel Art](https://github.com/LORECRONICASAPOENA/apoenaskil/pull/20), aberta, Draft, não mesclada, base `main`, branch `docs/pixel-art-pr-audit-20261104`.
- A PR #20 contém três arquivos documentais: relatório de auditoria, Skill de prototipagem Godot e índice da Skill. O HEAD consultado foi `e3a040fe77781b4b371fc2934062e7db435f1a7f`.
- O conteúdo da conversa atual foi consolidado para ser anexado ao relatório GitHub e à página Notion existente.

**Estado preservado:**
- A auditoria anterior das PRs #3, #4, #5, #6 e #10 do Pixel Art permanece como descrita nas seções anteriores.
- Dez correções antigas foram encontradas já presentes na branch consultada da PR #5; a validação CI no SHA atual e a reconciliação da divergência com `main` continuam pendentes.
- A PR #20 permanece Draft. Nenhuma aprovação, merge, alteração de branch principal ou mudança de código de runtime foi feita nesta etapa.
- A solicitação de backup não equivale a resolver os problemas de CI nem a concluir a integração Pixel Art/GameCreator.

**Limites do backup:**
- Registro textual parcial do conteúdo e das evidências acessíveis nesta conversa.
- Não é exportação integral de todos os chats do usuário.
- Não inclui cópia binária da captura de tela anterior, nem sprites ou arquivos locais não anexados nesta etapa.
- Nenhuma credencial, token, segredo ou arquivo de configuração sensível foi incluído.

**Próxima continuidade:** manter a PR #20 em Draft até revisão documental; depois retomar a validação do HEAD #5, runner/workflows, reconciliação #4/#5 e testes Godot/Android, sempre registrando SHA, run e resultado.
