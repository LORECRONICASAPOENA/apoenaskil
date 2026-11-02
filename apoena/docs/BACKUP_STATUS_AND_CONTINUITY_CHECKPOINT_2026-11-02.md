# Checkpoint de preservação e organização contínua — Apoena

**Data:** 2026-11-02  
**Repositório:** `apoenalore/apoenaskil`  
**Branch de origem conferida:** `main`  
**Objetivo:** registrar o estado verificável dos backups e a orientação atual do criador.  
**Natureza:** checkpoint documental. Não é uma cópia binária integral de todos os repositórios, conversas ou anexos.

## 1. Orientação atual do criador

Em 2026-11-02, o criador definiu a seguinte prioridade de trabalho:

> Por enquanto, registrar as ideias de forma organizada. Em uma atualização posterior, verificar o que está duplicado ou desatualizado.

Consequências operacionais:
- Registrar ideias, requisitos, decisões, correções, descobertas e hipóteses conforme forem surgindo.
- Preservar a origem, data, contexto e versão sempre que disponíveis.
- Distinguir decisão do criador, proposta da IA, hipótese, requisito, implementação relatada e implementação validada.
- Não apagar, fundir, substituir ou reescrever registros antigos apenas por parecerem duplicados.
- Não executar agora uma limpeza geral, deduplicação ou atualização de cânone.
- Fazer a auditoria de duplicidade/desatualização em uma fase posterior, explicitamente separada.
- Preservar contradições e versões históricas sem resolvê-las por inferência.

## 2. Verificação dos registros no Apoena Skill

Na consulta à API do GitHub em 2026-11-02, foram identificadas as seguintes PRs abertas em `apoenalore/apoenaskil`:

| PR | Conteúdo | Estado observado |
|---|---|---|
| #16 | Auditoria transversal das conversas e conhecimento do projeto | Aberta; não integrada à main |
| #15 | Inventário/avaliação documental do acervo Apoena | Aberta; não integrada à main |
| #14 | Bug Tracker e mapa de publicação dos relatórios Codex | Aberta; não integrada à main |
| #13 | Registro de recebimento do pacote completo de backup forense | Aberta; não integrada à main |
| #12 | Relatório preliminar de backup de conversa e manifesto | Aberta; não integrada à main |
| #11 | Relatório forense de engenharia do Game Creator | Aberta; não integrada à main |
| #10 | Protocolo de auditoria forense | Aberta; não integrada à main |
| #9 | Direção universal do Game Creator e solicitação de auditoria | Aberta; não integrada à main |
| #8 | Relatório de engenharia do Game Creator | Aberta; não integrada à main |
| #7 | Recuperação do planejamento do Game Creator (6 documentos) | Aberta; não integrada à main |
| #6 | Continuidade/linha de base do Game Creator | Aberta; não integrada à main |
| #3 | Skill de engenharia de jogos Apoena | Aberta; não integrada à main |
| #2 | Transferência do conhecimento do cânone Apoena | Aberta; não integrada à main |

PRs #4 e #5 constavam como integradas/fechadas na consulta. PR #1 estava fechada sem merge.

**Importante:** PR aberta é conteúdo versionado em uma branch, mas ainda não consolidado na branch padrão. Não afirmar que tudo já está na `main`.

## 3. Pacotes binários e limites de armazenamento

### 3.1 Backup forense Game Creator

O documento `apoena/docs/forensic/BACKUP_COMPLETO_CONVERSA_AUDITORIA_FORENSE_RECEBIMENTO_2026-11-02.md` registra:
- Nome do pacote: `Backup_Completo_Conversa_Auditoria_Forense_GameCreator_2026-11-02.zip`.
- Tamanho: 60.163.481 bytes.
- SHA-256: `e5fc11f876f0c2cdacfe94a40981fc70c3d00dc4f4fc14034c8e2b7f43d2d375`.
- Oito entradas.
- Teste ZIP relatado como aprovado.
- ZIP binário não anexado ao GitHub pela operação documentada; o registro e hashes estão em Markdown. O pacote permanece referenciado como anexo da conversa, não como arquivo binário comprovadamente armazenado no repositório.

O ZIP original interno é identificado com SHA-256 `bb40c8419056dfecdf75f9db99ee2deecfe6963a7fbe5b3d5b804b8b7346dfd9`.

### 3.2 Backup documental do acervo narrativo

A PR #15 contém dois arquivos Markdown em:
`apoena/archive/source-backups/2026-11-02/`

O inventário declara um pacote local `APOENA_BACKUP_DOCUMENTAL_2026-11-02.zip`, 24 entradas, 11 fontes originais e SHA-256:
`4f1ba34c024ffc7c97642c36988140d10a1224c9ca270b0a8beb4b9fcccf686d`.

O próprio registro esclarece que os binários PDF/DOCX originais estão no ZIP local e que o GitHub recebeu o inventário e a avaliação em Markdown, não os binários. Um PDF contendo credenciais/códigos foi excluído por segurança; não republicar segredos.

### 3.3 Outros pacotes

A PR #12 preserva um relatório preliminar e manifesto em Markdown. A PR #13 preserva um registro de recebimento em Markdown. Esses documentos não demonstram, por si só, que o arquivo ZIP correspondente foi carregado ao GitHub.

## 4. Backups por branch no repositório GameCreator

A consulta de branches de `apoenalore/GameCreator` confirmou a existência destas branches de backup:

| Branch | SHA observado |
|---|---|
| `backup/gamecreator-conversa-20261102-0904-brt` | `c53f6e3f43f8dc6f5eb2af3300d80ae453c3fbe9` |
| `backup/feature-estudio-unificado-pixelart-v41-20261028` | `ba1ba1ebe49edd5999dbdc9db578d251e496511a` |
| `backup/feature-estudio-unificado-pixelart-v41-pre-sync2-20261028` | `1de8536f8332b09215bc69a6f9539a41069c3ecd` |
| `backup/gc-update-009-before-main-sync-20261030` | `7632ceb224f3ad162b2600683902ea2c4a7ab481` |

A consulta confirmou que as referências existem. Isso não equivale a restauração testada nem prova que arquivos locais não rastreados estejam preservados.

O repositório GameCreator também contém:
- `docs/REGISTRO_CONVERSAS_E_BACKUPS.md`
- `docs/relatorios-conversas/2026-11-02-lacunas-backup-auditoria-estatica.md`

O registro do próprio GameCreator afirma que Git não preserva automaticamente IndexedDB, instalação Windows, arquivos não rastreados, estado local do runner ou conversas privadas não exportadas.

## 5. Estado de integridade e limites desta conferência

**Verificado nesta conferência:**
- Existência da branch `main` e das branches listadas.
- Existência e estado das PRs acima no Apoena Skill.
- Arquivos Markdown listados nas PRs #12, #13, #15.
- Presença de registros de backup na árvore principal do GameCreator.
- Metadados e hashes transcritos dos documentos de recebimento.

**Não verificado nesta conferência:**
- Download e revalidação dos ZIPs binários originais.
- Restauração integral de qualquer ZIP em ambiente limpo.
- Backup de IndexedDB, instalação local, arquivos fora do Git ou dispositivos.
- Integridade de cada arquivo dentro dos ZIPs por recálculo independente.
- Merge das PRs abertas.
- Cobertura integral de todas as conversas nativas do ChatGPT.

## 6. Procedimento recomendado daqui em diante

1. Ao fim de uma conversa relevante, registrar um checkpoint Markdown com data, assunto, fonte, decisões, ideias, pendências e anexos.
2. Quando houver arquivo binário, registrar nome, tamanho, SHA-256, número de entradas e resultado do teste de integridade.
3. Guardar o arquivo binário em destino persistente apropriado; não tratar apenas o manifesto como cópia do arquivo.
4. Preservar snapshots e branches antigas; não fazer limpeza ou squash destrutivo.
5. Registrar novos itens sem tentar deduplicá-los nesta fase.
6. Na fase futura de auditoria, comparar registros e propor correções, mantendo o histórico e exigindo aprovação antes de remover/mesclar conteúdo.
7. Não incluir tokens, senhas, códigos de autenticação ou outros segredos em backups compartilhados.

## 7. Conclusão

Há backups documentais e branches de checkpoint disponíveis no GitHub, porém vários ainda estão em PRs abertas e os ZIPs binários mencionados não estão comprovadamente armazenados no GitHub. A preservação atual é útil, mas não deve ser descrita como backup mestre completo e restaurável.

A prioridade aprovada pelo criador é **registrar e preservar agora; auditar duplicações e desatualizações depois**.
