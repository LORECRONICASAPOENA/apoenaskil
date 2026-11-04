# Backup completo do ecossistema Apoena — 04/11/2026

**Registro:** 2026-11-04 20:15 UTC (17:15, horário de Brasília)  
**Responsável operacional:** Amigo Apoena / Alberto  
**Conta GitHub:** conexão apoena — organização LORECRONICASAPOENA  
**Objetivo:** preservar o estado remoto dos 11 repositórios e registrar continuidade, sem sobrescrever backups anteriores.

## 1. Snapshot GitHub

Foi criada a branch `backup/full-project-2026-11-04-2015` a partir de `main` nos 11 repositórios abaixo. A comparação `main` → branch de backup retornou `identical`, `ahead_by=0`, `behind_by=0`, sem diferenças de arquivos. Os SHAs abaixo são os commits preservados.

| Repositório | SHA preservado |
|---|---|
| [projeto-apoena-studio-maker-ia](https://github.com/LORECRONICASAPOENA/projeto-apoena-studio-maker-ia/tree/backup/full-project-2026-11-04-2015) | `393297711818255872669b88893c8cd015867ecd` |
| [JOGO-APOENA-AGAR-](https://github.com/LORECRONICASAPOENA/JOGO-APOENA-AGAR-/tree/backup/full-project-2026-11-04-2015) | `d9862c5f52fbfedc7d226b66f7abf810ba02d2eb` |
| [que-projeto-e-esse](https://github.com/LORECRONICASAPOENA/que-projeto-e-esse/tree/backup/full-project-2026-11-04-2015) | `bbcd15514959fd73f9e10e9943740a9f99ccb6bc` |
| [runner](https://github.com/LORECRONICASAPOENA/runner/tree/backup/full-project-2026-11-04-2015) | `d098446606451558408cf3365508d22b08e05f2d` |
| [GameCreator](https://github.com/LORECRONICASAPOENA/GameCreator/tree/backup/full-project-2026-11-04-2015) | `a4e1b1884e0e877621fc699193fe755b764a095a` |
| [APOENA-AI-HUB-IA](https://github.com/LORECRONICASAPOENA/APOENA-AI-HUB-IA/tree/backup/full-project-2026-11-04-2015) | `566e8d0115a8b1f0806eb837d3e2e20bcc0e48b4` |
| [ApoenaBrowser](https://github.com/LORECRONICASAPOENA/ApoenaBrowser/tree/backup/full-project-2026-11-04-2015) | `40139333f7ed2fecb20b39fdf25c5d60da22150c` |
| [ApoenaBrowser-Updates](https://github.com/LORECRONICASAPOENA/ApoenaBrowser-Updates/tree/backup/full-project-2026-11-04-2015) | `2d6b19a52434bd7543f34cd4eb6d11dc200b452d` |
| [Apoena-pixel-art-html](https://github.com/LORECRONICASAPOENA/Apoena-pixel-art-html/tree/backup/full-project-2026-11-04-2015) | `f7075cff70c98f1cadf2693263890924c3ee376f` |
| [apoenaskil](https://github.com/LORECRONICASAPOENA/apoenaskil/tree/backup/full-project-2026-11-04-2015) | `912fbe003976a68c6d2a1937f988bdc07bff6a2d` |
| [CEREBRO-AMIGO-APOENA](https://github.com/LORECRONICASAPOENA/CEREBRO-AMIGO-APOENA/tree/backup/full-project-2026-11-04-2015) | `7185f1dd573c29703d6427d1a6aad83f56e1becc` |

**Resultado:** 11/11 branches criadas e 11/11 comparações idênticas confirmadas no momento da criação. Nenhuma branch `main` foi modificada; nenhum merge, deploy ou exclusão foi executado.

## 2. Registro de continuidade e proteção

- Backups anteriores foram preservados; nenhuma branch antiga foi sobrescrita.
- No Pixel Art HTML, também existe a branch `backup/2026-11-04-pos-correcao-lf`, criada na etapa imediatamente anterior, a partir de `main`.
- O backup de GameCreator preserva `main`; trabalhos em PRs/branches de funcionalidade permanecem separados. A PR #14 deve continuar aberta em draft e sem merge até validação completa e revisão.
- Os resultados recentes conhecidos do CI não foram reexecutados nesta operação; este registro não declara nova aprovação de testes.
- As branches Git são snapshots versionados no próprio GitHub, não cópias offline independentes.

## 3. Conversa, sprites e referências visuais

O inventário de Library contém os seguintes registros de continuidade:

- Referência do personagem posteriormente corrigido para **Kael** (mencionado inicialmente como Ruf): [abrir referência](https://chatgpt.com/library?file_id=libfile_1ace5f6f862c8191934f2b7f4d6953fe&account_id=personal). O arquivo binário do sprite gerado de Kael/Ruf não foi localizado no inventário consultado.
- Folha pixel art 4×4 de caminhada: [abrir na Library](https://chatgpt.com/library?file_id=libfile_2016face708481919c40c8fcd1d3fa99&account_id=personal).
- Sprite sheet de herói pixelado: [abrir na Library](https://chatgpt.com/library?file_id=libfile_6f29fd2cf1288191b41303c3290b2c0b&account_id=personal).
- Blin — sprite pixel art: [abrir](https://chatgpt.com/library?file_id=libfile_007a4d72ca788191911b88f4950beac2&account_id=personal).
- Blin — folha de sprites: [abrir](https://chatgpt.com/library?file_id=libfile_7871999f51908191a892a3e250d9f46d&account_id=personal).
- Blin — caminhada em quatro direções: [abrir](https://chatgpt.com/library?file_id=libfile_324be6881f7081918812738c53e4649a&account_id=personal).
- Referência original da Blin: [abrir](https://chatgpt.com/library?file_id=libfile_7c7cb4828590819193be17f7566831e7&account_id=personal).
- Personagem de cabelo branco — folha pixel art 4×4: [abrir](https://chatgpt.com/library?file_id=libfile_f23e031e78708191abc7d0aa0f4b5cea&account_id=personal).
- Referência do personagem de cabelo branco: [abrir](https://chatgpt.com/library?file_id=libfile_73bfe44d26dc8191899942f5e0c64f01&account_id=personal).
- Envio mais recente da Blin: [abrir](https://chatgpt.com/library?file_id=libfile_b7972bd9c1688191b628a0d298f0874a&account_id=personal).

O resumo histórico anterior está salvo na Library como `backup-conversa-sprites-apoena-2026-11-03.md`. Os links acima apontam para os originais na Library pessoal; não significam que os PNGs binários tenham sido copiados para os repositórios GitHub.

## 4. Limitações que permanecem explícitas

- O GitHub Desktop do computador local indicou sete arquivos modificados ainda não enviados. O conector remoto não acessa essas alterações locais; portanto, elas **não estão incluídas** neste snapshot.
- Esta operação não exportou toda a conversa bruta nem copiou os binários dos sprites da Library para o GitHub. O histórico textual e os links de referência foram registrados para continuidade.
- Para concluir uma cópia integral dos sete arquivos locais e dos PNGs, será necessário disponibilizar esses arquivos ao fluxo de backup e verificar a integridade após a cópia.
- A tentativa de materializar os PNGs da Library para envio binário ao GitHub foi bloqueada por ausência de caminho autorizado de bytes brutos; portanto, os PNGs permanecem na Library e apenas seus links/identificadores foram registrados.
- Não foram incluídos tokens, senhas, credenciais de runner ou segredos.

## 5. Próxima regra operacional

Manter backups sem sobrescrita antes de cada etapa arriscada; após marcos validados, criar novo snapshot; registrar data, branch, SHA, testes e limitações; nunca considerar uma branch de backup como cópia local/offline. Preservar PRs em draft e não mesclar sem validação e revisão exigidas.
