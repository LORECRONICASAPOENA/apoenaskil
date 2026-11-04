# Manutenção técnica — PRs, Godot MOBA, proteção de branches e backups

**Data:** 2026-11-04
**Origem:** sessão de manutenção ChatGPT, conexão GitHub `apoena` / perfil `apoenalore`.
**Organização:** `LORECRONICASAPOENA`.
**Cobertura:** registro derivado PARCIAL. Não é exportação integral da conversa, backup do computador local nem teste em dispositivo Android.

## 1. Auditoria do GameCreator — PR #14

- PR: https://github.com/LORECRONICASAPOENA/GameCreator/pull/14
- Estado: aberta, draft, não mesclada.
- Branch head: `feat/apoena-modular-character-creator-integration`.
- Head SHA: `4f90fc8739b4af351c929a97d8ed73c094477c36`.
- Base: `feat/apoena-personagem-estudio-main`, SHA `0447ea9dc9d9310e985247325e3af1d1c726519a`.
- Run #392: https://github.com/LORECRONICASAPOENA/GameCreator/actions/runs/41755565658 — job `validar` concluiu `success`; runner `Game-Creator-Runerr`; 23 etapas funcionais concluídas com sucesso, mais etapas de pós-execução.
- O PR #13 também permanece aberto, com escopo relacionado ao Criador Modular, mas aponta para `main`. Não foi fechado nem redirecionado: é necessário reconciliar o escopo entre PR #13, PR #14 e a branch intermediária do PR #11 antes de mesclar.
- Nenhum código do GameCreator foi alterado nesta manutenção.

## 2. Auditoria e correção do Pixel Art — PR #7

- PR: https://github.com/LORECRONICASAPOENA/Apoena-pixel-art-html/pull/7
- Estado: aberta, draft, não mesclada.
- Branch: `feat/agar-character-powers-water-depth-20261103`.
- SHA corrigido: `0af5ab3e9f1945d3f669d5153287f4d3f3cd1c25`.

### Falha encontrada

O run #25 (https://github.com/LORECRONICASAPOENA/Apoena-pixel-art-html/actions/runs/41656753403) terminou com `success`, mas seu log continha `SCRIPT ERROR: Parse Error: Closing "]" doesn't have an opening counterpart.` em `res://scripts/mundo_2_5d.gd:206`. A causa era um `]` excedente no bloco que compõe o HUD do modo MOBA. O workflow não carregava explicitamente esse script em um teste que falhasse diante de erro de parse; portanto, o `success` antigo era um falso positivo para a compilação do MOBA.

### Alterações feitas

1. `scripts/mundo_2_5d.gd`: removido o colchete excedente, sem alterar a lógica do HUD.
   - Commit: `12d7454803b8f1b818632fb72df4e32600f4daa4`.
2. `tests/testar_moba_habilidades.gd`: novo teste headless com `preload` explícito do script e verificações Q/W/E/R/F e ataque básico de Apoena, Oriom, Serena, Aqua e Ubirara.
   - Commit: `983679e3e8dba5662af83ec8864de347324fae3a`.
3. `.github/workflows/validar-pixel-art-windows.yml`: acrescentada etapa de compilação/teste do MOBA ao workflow Windows existente; nenhum workflow paralelo criado.
   - Commit final da etapa: `0af5ab3e9f1945d3f669d5153287f4d3f3cd1c25`.

### Validação em andamento

- O GitHub Actions iniciou automaticamente o run #27: https://github.com/LORECRONICASAPOENA/Apoena-pixel-art-html/actions/runs/41838404125.
- SHA testado: `0af5ab3e9f1945d3f669d5153287f4d3f3cd1c25`.
- Job ID: `126603246344`; estado observado: `queued`.
- O run #26, disparado no commit intermediário, foi cancelado automaticamente pela política de concorrência ao chegar o commit final. O run #27 é a validação pertinente ao estado corrigido.
- Ainda não declarar a correção validada até o run #27 concluir com `success` e sem erro de parse.

## 3. Backups Git do Pixel Art

- Backup pré-correção: branch `backup/pr7-before-gdscript-parse-fix-20261104`, criada no SHA original `1118550420bbd89513410bcfe26ce46053b4e4db`; registro `backups/2026-11-04-pr7-before-gdscript-parse-fix.md`; commit do registro `13656963c620e0f04e2042323d4f80662b0e5b64`.
- Backup pós-correção: branch `backup/pr7-after-gdscript-fix-20261104`, criada no SHA corrigido `0af5ab3e9f1945d3f669d5153287f4d3f3cd1c25`; registro `backups/2026-11-04-pr7-after-gdscript-fix.md`; commit do registro `de796489c79ae3b46762dd97b3d0e3637a3dfdc4`.
- Os dois checkpoints preservam o estado completo do repositório nos respectivos SHAs. Não são backups de IndexedDB, disco local ou APK.

## 4. Revisão automática

- Comentário manual solicitado ao CodeRabbit na PR #7: ID `6631902197`, texto `@coderabbitai review` com foco no parser e nos testes MOBA.
- Resultado do CodeRabbit ainda não confirmado nesta sessão.

## 5. Proteção das branches

### GameCreator

- A branch `main` retornou `protected=true`.
- Ruleset ativo `26338198`, nome `Copilot review for default branch`, inclui `deletion`, `non_fast_forward` e `copilot_code_review`.
- O ruleset consultado não declara `required_status_checks` nem `required_pull_request_reviews`. A proteção existe, mas não exige explicitamente CI obrigatório nem aprovação humana independente.
- Issue de acompanhamento: https://github.com/LORECRONICASAPOENA/GameCreator/issues/15.

### Pixel Art

- A branch `main` retornou `protected=false`.
- A consulta ao endpoint clássico de proteção retornou `403 Resource not accessible by integration`; a consulta a rulesets retornou `403` com indicação de requisito de GitHub Pro ou repositório público.
- Issue de acompanhamento: https://github.com/LORECRONICASAPOENA/Apoena-pixel-art-html/issues/8.
- Não tornar o repositório público para contornar a limitação. Não foi possível alterar a proteção via conexão atual.

## 6. Runners

- Run #25 do Pixel Art havia sido executado no runner `Runner-Pixel-Art` e terminou `success`, apesar do erro de parse citado acima.
- O run #27, que contém a correção, estava `queued`; o job ainda não tinha `runner_name`/`runner_id` atribuído.
- O endpoint de listagem de runners não foi aceito pelo conector. Não afirmar que o runner está online/idle neste instante.

## 7. Pendências que permanecem

1. Aguardar e inspecionar o run #27; corrigir qualquer falha causal e repetir somente após nova alteração pertinente.
2. Conferir o resultado da revisão manual do CodeRabbit.
3. Fazer validação Android/APK e teste em dispositivo real; o workflow atual valida Windows/Godot headless, não o APK nem toque/performance em aparelho.
4. Configurar proteção de `main` no Pixel Art quando houver plano/permissão compatível, mantendo o repositório privado.
5. Fortalecer o ruleset do GameCreator para exigir checks e revisão, conforme issue #15.
6. Reconciliar PR #13, PR #14 e PR #11 antes de qualquer merge do Criador Modular.

## 8. Ações não realizadas

- Nenhum PR foi mesclado, fechado ou marcado como pronto para revisão.
- Nenhuma proteção de branch, permissão, secret, runner ou configuração de produção foi alterada.
- Nenhum workflow foi disparado manualmente; o run #27 iniciou automaticamente após o push.
- Nenhum APK foi exportado nem instalado em dispositivo Android.
- Nenhum dado local/IndexedDB foi copiado.