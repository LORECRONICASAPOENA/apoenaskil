# Apoena Game Creator — conhecimento técnico e operacional

**Escopo:** ferramenta de autoria local do projeto Apoena. Este diretório documenta o editor, seus módulos, integração, distribuição, segurança e estado de validação. Não é fonte de cânone narrativo do mangá.

## Identificação e contexto recuperado

- Repositório de código: [apoenalore/GameCreator](https://github.com/apoenalore/GameCreator).
- Repositório desta base de conhecimento: [apoenalore/apoenaskil](https://github.com/apoenalore/apoenaskil).
- Plataforma operacional informada pelo autor: Windows.
- Execução informada: local.
- Utilização informada: equipe.
- Compartilhamento informado: GitHub.
- Distribuição informada: ZIP produzido por GitHub Actions.
- GitHub Actions: habilitado.
- Aprovação independente obrigatória: não, conforme declaração registrada na sessão.
- Proteção da branch `main`: desconhecida na fonte da auditoria; não presumir configuração atual.
- A versão V4.1 e o commit `0bd916157d9bfab6c6c9b121c26050f94918cf80` foram identificados no dossiê recebido; tratá-los como referência histórica daquela entrega, não como HEAD atual.

## Documentos deste domínio

- [Dossiê de recuperação da auditoria de segurança de 2026-11-02](security-audit/conversation-dossier-2026-11-02.md): preserva o conteúdo recuperado, achados, limitações, decisões e pendências.
- [Skill de engenharia GameCreator](../../skills/apoena-gamecreator-engineering/SKILL.md): fluxo de trabalho, arquitetura, continuidade, versionamento e validação.
- [Skill de segurança GameCreator](../../skills/apoena-gamecreator-security/SKILL.md): threat model, achados estáticos e roteiro de hardening.

## Limites de proveniência

O dossiê foi fornecido pelo autor como extração forense de uma conversa anterior. Ele declara que o link compartilhado não disponibilizou o texto, que dois anexos de imagem não foram reexaminados visualmente, que três entregas ZIP não tiveram seu conteúdo integralmente extraído e que cinco arquivos-fonte foram examinados naquela conversa. Portanto, este repositório registra uma **recuperação parcial baseada no dossiê fornecido**, não uma auditoria integral independente do GameCreator.

Não afirmar que todos os 76 arquivos de runtime foram auditados. Não declarar que os achados preliminares foram explorados. Não declarar que V4.2 existe ou que qualquer hardening foi aplicado sem evidência de código, commit e teste.

## Separação de produtos

- **GameCreator:** ferramenta/editor de autoria.
- **Apoena Pixel Art HTML:** módulo integrado ao ambiente de autoria conforme requisito do autor; coordenar alterações pelo protocolo WIP = 1 definido no repositório GameCreator.
- **JOGO-APOENA-AGAR-:** runtime/produto consumidor. Exportar assets ou metadados não prova integração funcional no runtime.
- **Apoena Skill:** base de conhecimento e Skills; não é código do editor nem cânone narrativo.

## Estado no momento da recuperação

- Auditoria estática inicial dos cinco arquivos: relatada no dossiê, sem reexecução independente nesta atualização.
- Correções de segurança SEC-001 a SEC-007: pendentes de implementação e validação, exceto onde o dossiê identifica apenas ausência/risco.
- Proteção da branch `main`, aprovação independente, workflows e permissões atuais: precisam de inspeção direta no GitHub.
- Testes dinâmicos, testes de exploração, validação Windows real e recuperação de backup: não comprovados pelo dossiê.
- A tarefa GC-UPDATE-009 permanece em PR #7 aberto em draft no repositório GameCreator; consultar o estado atual da PR e seus checks antes de continuar. Não presumir que um workflow de Pixel Art valida o atualizador.

## Regra de atualização

Toda descoberta nova deve registrar fonte, data/hora original se disponível, data/hora de registro se disponível, repositório, branch, commit, arquivo/linha, teste e resultado. Atualize este diretório de forma aditiva; preserve dossiês históricos e não transforme proposta em implementação.


## Continuidade registrada — plataforma online e unificada (2026-11-02)

- [Registro de continuidade da conversa](conversation-recovery-2026-11-02-platform-online-and-unification.md): histórico parcial com decisões do autor sobre mundo híbrido, 20–50 jogadores de teste, Android/PC, segurança, economia, auditoria de arquivos e unificação do Game Creator.
- **Decisão de produto:** um único Game Creator com Estúdio 3D, Estúdio Pixel Art 2D e Editor de mapas 2.5D, biblioteca central e exportação integrada. O editor de mapas existente deve ser evoluído; preservar a bancada 3D e módulos ativos.
- **Online:** arquitetura híbrida com regiões compartilhadas e dungeons/arenas instanciadas; servidor autoritativo; 20–50 simultâneos como meta de teste, não capacidade garantida.
- **Limpeza:** remover apenas caminhos vazios/órfãos ou duplicações comprovadas após rastrear referências, migrar conteúdo exclusivo e testar. Não apagar fontes, bundles ou iniciadores apenas por idade/tamanho.
- **Proveniência:** recuperação parcial a partir do contexto disponível; não é transcrição integral nem auditoria atual do HEAD do código.


## Arquivo histórico e proveniência — 2026-11-02

- [Arquivo de conversa sobre governança documental](conversation-archive/2026-11-02-security-audit-governance.md).
- [Manifesto de extração, fontes, cobertura e lacunas](conversation-archive/extraction-manifest-2026-11-02.md).
- O dossiê histórico da auditoria continua em [security-audit/conversation-dossier-2026-11-02.md](security-audit/conversation-dossier-2026-11-02.md).
- Política: Apoena Skill é a memória central; GameCreator mantém apenas documentação técnica operacional. O registro de conversa permanece PARCIAL quando a fonte original ou anexos não estão integralmente acessíveis.


## Baseline de engenharia e estabilização — 2026-11-02

- [Baseline de engenharia A1, fonte/build/artefato, riscos e roteiro P0–P5](architecture/engineering-baseline-2026-11-02.md).
- Próxima tarefa técnica registrada: A2 — mapa de dependências e contratos do GameCreator.
