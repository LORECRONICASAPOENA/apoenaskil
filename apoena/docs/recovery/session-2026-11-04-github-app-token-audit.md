# Backup de conversa — auditoria do novo formato de tokens GitHub App

**Projeto:** Amigo Apoena / Alberto — infraestrutura GitHub e continuidade técnica  
**Origem:** conversa atual do ChatGPT, conta conectada ao ecossistema Apoena  
**Data/hora da solicitação de backup:** 2026-11-04T21:32:57Z (18:32:57, horário de Brasília)  
**Data/hora aproximada do registro:** 2026-11-04T18:33-03:00  
**Formato:** resumo técnico derivado do contexto visível; não é transcrição literal  
**Cobertura:** PARCIAL — houve mensagens e saídas de ferramentas omitidas no contexto recuperável. O texto exato do pedido inicial que motivou a auditoria não está disponível neste recorte; o objetivo recuperado é verificar compatibilidade com o novo formato de GitHub App installation tokens.

## 1. Objetivo recuperado

Verificar se os repositórios Apoena e seus workflows GitHub Actions dependem do formato antigo e curto dos tokens de instalação de GitHub App, especialmente validações de 40 caracteres, regex antiga, truncamento ou armazenamento com tamanho fixo. O pedido incluiu o uso coordenado do Amigo Apoena, GitHub e Notion.

## 2. Mudança técnica registrada

A auditoria anterior registrou que o rollout de tokens stateless de GitHub App foi concluído em 2026-10-02. O formato novo é um JWT com prefixo `ghs_`, aproximadamente 520 caracteres e dois pontos. Permissões, escopo e expiração de uma hora permanecem os mesmos.

O cabeçalho temporário `X-GitHub-Stateless-S2S-Token`, utilizado para forçar o formato em chamadas de criação de installation token durante testes, tem descontinuação anunciada para 2026-11-30. A auditoria não recomendou adicionar esse cabeçalho aos workflows Apoena.

Fontes primárias registradas:
- https://github.blog/changelog/2026-10-02-stateless-github-app-installation-tokens-rolled-out/
- https://github.blog/changelog/2026-05-15-github-app-installation-tokens-per-request-override-header/
- https://cli.github.com/manual/gh_help_environment
- https://cli.github.com/manual/gh_auth_login
- https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/use-github-cli
- https://docs.github.com/en/rest/quickstart

## 3. Escopo da auditoria

Foram examinados metadados e árvores de 11 repositórios da organização `LORECRONICASAPOENA`:
1. `projeto-apoena-studio-maker-ia`
2. `JOGO-APOENA-AGAR-`
3. `que-projeto-e-esse`
4. `runner`
5. `GameCreator`
6. `APOENA-AI-HUB-IA`
7. `ApoenaBrowser`
8. `ApoenaBrowser-Updates`
9. `Apoena-pixel-art-html`
10. `apoenaskil`
11. `CEREBRO-AMIGO-APOENA`

Foram lidos 20 workflows GitHub Actions, agrupados assim:
- GameCreator: 2 workflows.
- Apoena Pixel Art HTML: 2 workflows.
- JOGO APOENA AGAR: 10 workflows.
- Studio Maker IA: 1 workflow.
- ApoenaBrowser: 3 workflows.
- ApoenaBrowser-Updates: 1 workflow.
- `que-projeto-e-esse`: 1 workflow.

Também foram examinados arquivos de autenticação/configuração e scripts de release identificados nas árvores, além dos fontes oficiais de autenticação do `actions/checkout@v4` e `@v5`.

## 4. Achados registrados

- Dois workflows usam explicitamente `GH_TOKEN: ${{ github.token }}`: `ApoenaBrowser/.github/workflows/publicar-canal-atualizacoes.yml` e `ApoenaBrowser-Updates/.github/workflows/publicar-manifesto.yml`. Ambos usam GitHub CLI em `gh release download`, padrão recomendado pela documentação oficial.
- Outros workflows usam `actions/checkout@v4` ou `@v5`; o helper oficial consultado não impõe comprimento fixo de 40 caracteres.
- Nos arquivos inspecionados, não foram encontrados criação manual de installation tokens, validação de comprimento de 40 caracteres, regex legada, truncamento, armazenamento em campo de tamanho fixo ou uso do cabeçalho temporário.
- O `lib/auth.ts` do Studio Maker IA usa HMAC para cookie de sessão próprio; não é token GitHub App.
- Workflows de validação do Pixel Art com `persist-credentials: false` não mantêm credenciais de checkout configuradas no Git após a ação.

**Conclusão técnica registrada:** nenhuma incompatibilidade foi detectada nos arquivos inspecionados; nenhuma alteração de código ou workflow foi considerada necessária nesta etapa.

## 5. Limitações e estado de validação

- A busca de código do GitHub retornou zero resultados para termos como `ghs_`, `GITHUB_TOKEN`, `github.token`, `create-github-app-token`, `token.length` e `X-GitHub-Stateless-S2S-Token`, mas a API informou `incomplete_results=true`. O resultado não prova ausência global.
- A auditoria não certifica todos os arquivos-fonte, bundles, dependências, secrets privados, configurações de instalação de Apps, credenciais locais ou o código interno do conector.
- Nenhum segredo foi solicitado, lido ou registrado.
- Não houve alteração de código/workflow; portanto, não foi executada CI nesta etapa. Não declarar testes ou builds aprovados.
- Estado: **AUDITORIA ESTÁTICA CONCLUÍDA PARA O ESCOPO LISTADO; COBERTURA INTEGRAL NÃO CERTIFICADA.**

## 6. Decisão e orientação preservadas

1. Manter `GH_TOKEN: ${{ github.token }}` nos workflows que usam GitHub CLI.
2. Não impor tamanho fixo de 40 caracteres; tratar tokens como strings opacas.
3. Se algum serviço Apoena passar a criar installation tokens manualmente, aceitar tokens longos, não truncar cabeçalhos e testar o fluxo de autenticação.
4. Não adicionar o cabeçalho temporário aos workflows existentes.
5. Verificar qualquer dependência desse cabeçalho antes de 2026-11-30.

## 7. Relatórios técnicos relacionados

O relatório detalhado anterior foi salvo em dois repositórios e relido. Os dois arquivos tinham conteúdo idêntico, blob SHA `36448456b5041de124cb130ead58b7fe0d71651e`:
- [Apoena Skill — auditoria detalhada](https://github.com/LORECRONICASAPOENA/apoenaskil/blob/audit/github-app-token-format-2026-11-04/apoena/docs/security-audit/github-app-installation-token-format-2026-11-04.md)
- [Cérebro Amigo Apoena — auditoria detalhada](https://github.com/LORECRONICASAPOENA/CEREBRO-AMIGO-APOENA/blob/audit/github-app-token-format-2026-11-04/docs/auditorias/2026-11-04-github-app-token-format.md)

Estado atual verificado das PRs documentais:
- [Apoena Skill — PR #21](https://github.com/LORECRONICASAPOENA/apoenaskil/pull/21): aberta, não draft, não mesclada.
- [Cérebro Amigo Apoena — PR #3](https://github.com/LORECRONICASAPOENA/CEREBRO-AMIGO-APOENA/pull/3): aberta, não draft, não mesclada.

Correção de precisão: um resumo anterior nesta conversa descreveu essas PRs como draft; a consulta atual ao GitHub confirmou `draft=false` para ambas. Permanecem abertas e sem merge.

## 8. Backup desta etapa

- Branch de backup criada a partir de `main` em ambos os repositórios: `backup/conversation-2026-11-04-2132`.
- Este arquivo registra a conversa e os achados; não altera código de runtime, workflows ou a branch `main`.
- O registro canônico do Notion é a página [Backup de Conversa — Apoena, GitHub Actions e Runners — 04/11/2026](https://app.notion.com/p/40e0da6873c8816dbe55f353d0303542). A seção da auditoria de tokens já estava registrada; o pedido atual de backup será acrescentado à mesma página.

## 9. Lacunas e próximos passos

- A recuperação é parcial porque o histórico bruto completo desta conversa e algumas saídas intermediárias não estão disponíveis neste recorte.
- Para uma transcrição literal, fornecer exportação oficial da conversa em HTML/JSON/Markdown.
- Revisar as PRs #21 e #3 antes de qualquer merge; não mesclar automaticamente.
- Não alterar workflows nem código sem nova evidência concreta de incompatibilidade.
- Manter os relatórios históricos e esta captura separados; não substituir um pelo outro.

**Status final deste registro:** BACKUP PARCIAL — RESUMO DERIVADO, COM FONTES, COMMITS/PRs E LIMITAÇÕES IDENTIFICADOS. Não é exportação integral da conversa.
