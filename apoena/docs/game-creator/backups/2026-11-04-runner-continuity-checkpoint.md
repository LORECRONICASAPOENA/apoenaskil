# Checkpoint de continuidade — Apoena Skill, Cérebro e runners
Data de registro: 2026-11-04 (horário exato não confirmado).
Status: BACKUP DOCUMENTAL; não é cópia binária integral nem restauração testada.

## Decisões do criador
- Manter o banco de conhecimento atualizado consultando repositórios, branches, SHA, PRs, logs, artefatos e pendências reais.
- Há vários runners no ecossistema; verificar sua disponibilidade, labels e compatibilidade antes de usá-los. Apoena Skill e Cérebro também podem possuir runners, mas o estado online e os nomes não foram verificados nesta sessão.
- Amigo Apoena coordena; Alberto executa análise técnica sênior.
- Antes de alterações: backup verificável. Após marcos: checkpoint e validação no SHA exato.
- WIP=1 para GameCreator e Pixel Art HTML combinados; não duplicar workflows nem compartilhar workspaces mutáveis.
- Próxima etapa criativa: spritesheets de personagens em grade fixa 4 colunas × 6 linhas (24 células), após integrar poderes ao Pixel Art.

## Evidência atual confirmada
- GameCreator PR #14: https://github.com/LORECRONICASAPOENA/GameCreator/pull/14
- Head da PR #14: `4f90fc8739b4af351c929a97d8ed73c094477c36`.
- Workflow `41755565658` nesse SHA: `completed/success`, job `validar` também `completed/success` (consulta GitHub nesta rodada).
- Correções recentes da PR: `55f3cf8189dccbebd774f129af0d002b7a6fed9b` e `4f90fc8739b4af351c929a97d8ed73c094477c36`.
- Backup pré-correção no GameCreator: `backups/2026-11-04-pr14-character-browser-before-fix.md`, commit `8fd76ffb7acf3054c6c4c3aba0a6431ec661f799`.
- No Cérebro, skill Alberto recebeu protocolo de consulta viva do banco/runners no commit `a3b3a7b62796b16105e4d97833f116719c446749`; `docs/PROTOCOLO-BANCO-E-RUNNERS.md` foi criado no branch main.
- Os repositórios `LORECRONICASAPOENA/apoenaskil` e `LORECRONICASAPOENA/CEREBRO-AMIGO-APOENA` são destinos canônicos distintos; este registro deve permanecer em ambos, sem misturar cânone com implementação.

## Escopo não concluído
- Integração dos poderes no Pixel Art e criação de spritesheets ainda não validadas neste checkpoint.
- Runner online/ocupação/labels de Apoena Skill e Cérebro não comprovados; verificar jobs e configurações autorizadas antes de executar.
- A publicação do plugin privado ativo não ocorre automaticamente quando o backup GitHub muda.
- Nenhum merge, deploy, release, alteração de secrets, exclusão ou force-push autorizado.

## Recuperação
Restaurar este registro pela branch `backup/2026-11-04-apoena-runner-continuity` e comparar com `main` antes de qualquer aplicação. Preservar os arquivos históricos. Conferir SHA, workflows e logs novamente no momento de retomar o trabalho.
