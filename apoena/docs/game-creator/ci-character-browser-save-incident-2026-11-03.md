# Recuperação parcial — falha do Criador Modular no GitHub Actions

**Data do registro:** 2026-11-03. **Hora:** Hora não disponível na fonte do registro. **Fuso do ambiente:** UTC.  
**Status técnico:** IMPLEMENTADO — VERIFICADO no workflow #374 (run `41565001752`), commit `03382b02e74e2b39da0924bd0ff72ddacdf27e5a` do GameCreator.  
**Status da PR:** PR #14 aberta como draft, branch `feat/apoena-modular-character-creator-integration`, base `feat/apoena-personagem-estudio-main`; não mesclada.  
**Cobertura desta recuperação:** PARCIAL. Preserva as mensagens e evidências acessíveis nesta sessão e resume as ações; não é exportação integral da conversa.

## Fonte e pedidos do autor

Fonte efetivamente consultada: contexto visível desta conversa no ChatGPT, capturas/imagens exibidas nela e arquivos atuais do repositório `apoenalore/GameCreator`. Não foi fornecida exportação completa do histórico.

Mensagens visíveis do autor, na ordem:

1. “quero o stilet do personagem kael” — acompanhada de uma folha de modelo do personagem em três vistas.
2. “gere somente corpo com shorte curto colado cinza sem cabelo”.
3. “preciso de sprite meu amigo”.
4. “desse personagem” — acompanhada de uma imagem do personagem sem cabelo, usando short cinza, em três vistas.
5. “espero resultados assim oq houve?”
6. “tenta de novo pfvr”.
7. “ok tudo bem eu entendo”.
8. “analise e resolva esse erro especificamente alberto preciso que busque ate saidas no google e dentro do creator” — acompanhada de captura do GitHub Actions.
9. “quando terminar faça o backup no git hub apoena skil”.

Referências de contexto de página fornecidas: `90fac787-0e28-4562-a3c1-687d152f3d9b`, `827a2b12-9127-4fe5-adc4-1530adba8f85`, `e8759b5a-c5d3-4551-b80e-1a7b1c81cf2e`, `5b35805d-b33b-477c-a37e-d8944b785374`, `5bbddcb5-d6d1-4411-9737-2704b3aba3b1`, `4f5c6180-5e08-47e1-8c69-1650a87f0978`, `03081670-2a4d-4033-9519-d0f9300e350e`, `aab167b8-574d-40fc-bdeb-29bb5da27255` e `44172c37-1803-42da-9756-d4d139906b17`.

A palavra “alberto” aparece no pedido. O contexto disponível não esclarece se é nome de pessoa, agente ou outro referente; não foi inferido.

## Evidência da falha inicial

A captura mostra o repositório `apoenalore/GameCreator`, workflow `.github/workflows/pixel-art.yml`, job `validar`, falha no passo **Testar Criador Modular no navegador**. O log informa:

```text
Teste funcional do Criador Modular falhou: WAITING: clique save.
Consulte .ci-results/characters-browser.html e .log.
Process completed with exit code 1.
```

O teste ficava esperando o botão Salvar concluir. Execuções subsequentes avançaram a investigação:

- Run #356 (`41562569931`): avançou além do estado RUNNING e falhou aguardando a mensagem de projeto salvo.
- Run #360 (`41563101172`): o rastro do host mostrou `start:saveProject` sem conclusão na versão então testada.
- Run #368 (`41563644284`): o artefato revelou que o teste esperava `ApoenaLibrary.dispatch('listProjects')` antes de atribuir o `src` do iframe. O iframe, portanto, não começava a carregar enquanto o preflight de IndexedDB permanecia pendente no Chromium com relógio virtual.
- Foi removido o preflight de IndexedDB do harness de navegador. A integração visual passou a usar host em memória, e a persistência IndexedDB permaneceu coberta por `tests/asset-library.test.cjs`.
- Run #373 (`41564711737`), commit `03d0ad2d5de0aad47a92c88ad51d132aaae34e38`: o iframe e o salvamento avançaram. A ação de ponte gravou o status de sucesso e o rastro mostrou as chamadas de biblioteca completadas, mas o harness continuou aguardando a Promise `whenIdle()` da fila interna e reportou timeout.

## Correção aplicada e verificação

No arquivo `pixel-art/personagens.js`, o hook usado pelo teste passou a acompanhar explicitamente operações pendentes: cada ação protegida incrementa o contador e o decrementa no `finally`; o teste aguarda o evento de fila ociosa quando o contador chega a zero. O hook de teste deixou de tratar a Promise interna da fila como único sinal de conclusão.

No arquivo `tests/personagens-browser.html`, foram preservados detalhes diagnósticos do carregamento do iframe para que o watchdog não sobrescreva um erro anterior.

**Resultado final verificado:** workflow #374, run `41565001752`, passou integralmente no commit `03382b02e74e2b39da0924bd0ff72ddacdf27e5a`. A etapa de navegador, incluindo salvar o projeto, salvar na biblioteca, enviar pela ponte ao Creator, navegar/animação e reabrir, passou; os demais passos do workflow também concluíram com sucesso.

O que foi corrigido e confirmado foi a espera do harness/relógio do teste de navegador. A evidência não indica perda de dados do usuário nem confirma defeito de persistência no produto: a suíte específica de biblioteca IndexedDB é executada separadamente no workflow e passou no run #374. A PR continua aberta como draft; esta anotação não declara merge.

## Pesquisa e escopo técnico

A solicitação pediu consulta ao Google e ao Creator. Foram consultados os arquivos atuais do branch da PR: workflow, teste de navegador, `pixel-art/personagens.js`, `shared/creator-bridge.js` e `tests/asset-library.test.cjs`. Também foram consultadas documentação oficial do Chrome Headless sobre `--virtual-time-budget` e documentação MDN sobre o evento `complete` das transações IndexedDB:

- Chrome Headless: https://developer.chrome.com/docs/chromium/headless
- MDN, IndexedDB `complete`: https://developer.mozilla.org/en-US/docs/Web/API/IDBTransaction/complete_event

A documentação do Chrome ajudou a distinguir orçamento de tempo virtual de limite máximo de espera. A identificação das falhas concretas veio dos artefatos/logs dos runs e dos arquivos do Creator; não foi inferida apenas da pesquisa externa.

## Separação entre pedido visual e incidente de CI

As mensagens anteriores sobre Kael, short cinza e sprite registram pedidos de arte do personagem e suas imagens de referência. O incidente de CI foi investigado na sequência desta conversa. As imagens aparecem no contexto visual, mas seus binários não foram localizados como arquivos para copiar ao repositório; esta anotação não afirma que foram preservados como assets.

## Limites da recuperação

- O histórico completo da conversa e as respostas completas anteriores não estão disponíveis como exportação nesta sessão. A cobertura permanece **PARCIAL**.
- Os registros acima são mensagens visíveis e síntese/paráfrase técnica, não transcrição literal de toda a conversa.
- As capturas e imagens foram consultadas visualmente; seus arquivos binários não foram incorporados a este repositório.
- A palavra “alberto” não foi desambiguada.
- O resultado #374 valida o workflow registrado naquele SHA; não substitui revisão/merge da PR nem teste manual no Creator instalado no Windows.

## Proveniência e referências

- Repositório de código: https://github.com/apoenalore/GameCreator
- PR #14: https://github.com/apoenalore/GameCreator/pull/14
- Workflow #374: https://github.com/apoenalore/GameCreator/actions/runs/41565001752
- Branch: `feat/apoena-modular-character-creator-integration`
- SHA validado: `03382b02e74e2b39da0924bd0ff72ddacdf27e5a`
- Repositório deste registro: `apoenalore/apoenaskil`, branch `docs/recovery-gamecreator-ci-2026-11-03`
- PR do backup documental: https://github.com/apoenalore/apoenaskil/pull/18 (aberta como draft; não mesclada).
