# Registro de manutenção e backup — Apoena
Data: 2026-11-04
Execução de referência: rodada de manutenção informada às 10:57:59Z; inventário GitHub atualizado nesta gravação.
Escopo deste registro: preservar o relatório e a regra de backup. Não representa snapshot do código-fonte dos demais projetos.

## Inventário atual da organização LORECRONICASAPOENA
Repositórios acessíveis confirmados:
- projeto-apoena-studio-maker-ia
- JOGO-APOENA-AGAR-
- que-projeto-e-esse
- runner
- GameCreator
- APOENA-AI-HUB-IA
- ApoenaBrowser
- ApoenaBrowser-Updates
- Apoena-pixel-art-html
- apoenaskil
- CEREBRO-AMIGO-APOENA

## Estado técnico registrado na rodada
- GameCreator: PR #14 em draft, SHA 4f90fc87; CI aprovado no run 41755565658.
- Pixel Art HTML: PR #7 em draft, SHA 11185504; CI aprovado no run 41656753403.
- Apoena AGAR: PR #36, SHA e5e6031; inventário aprovado no run 41788247586; validação Godot cancelada no run 41788247585.
- Apoena AGAR: PR #37 em draft, SHA 33e66c2; não foi encontrada execução de CI para esse commit.
- Cérebro Amigo Apoena: PR #2 aberta, sem modificação nesta rodada.
- AGENTS.md foi consultado no AGAR e no GameCreator; a leitura no Cérebro retornou 404. Instruções do Apoena Skill também foram consultadas.

## Pendência prioritária
A PR #37 da Arena QWERF ainda precisa de validação automática no SHA exato. A PR aponta para a branch da PR #36, não para main. Não considerar homologada até obter evidência de CI no SHA correspondente.

## Ações desta gravação
- Criada branch de backup documental `backup/apoena-memory-2026-11-04` em apoenaskil.
- Criada branch de backup documental `backup/apoena-memory-2026-11-04` em CEREBRO-AMIGO-APOENA.
- O relatório será gravado em arquivo datado em cada branch.
- Nenhum código de produto foi alterado; nenhum merge, deploy, release ou alteração de permissões foi realizado.
- Este registro é documentação de estado, não cópia integral dos repositórios nem backup binário de artefatos.

## Política permanente de backup solicitada
Antes de qualquer alteração de projeto, criar ponto de restauração remoto identificável e verificável, sem sobrescrever backups anteriores e sem incluir segredos. Após cada marco validado, criar novo ponto de restauração. Todo backup de projeto deve ser registrado em:
1. GitHub: repositório apoenaskil (Apoena Skill).
2. GitHub: repositório CEREBRO-AMIGO-APOENA (memória do Amigo Apoena).
3. Notion: memória/documentação do ecossistema Apoena.

Só declarar um destino como concluído após confirmar o commit/página. Se qualquer destino falhar, informar o bloqueio e não alegar backup completo.
