# SOLICITAÇÃO OFICIAL AO CODEX — AUDITORIA, BUG TRACKER E RASTREABILIDADE DO APOENA GAME CREATOR

**Solicitante:** proprietário do Apoena Game Creator  
**Data:** 2026-11-02 — hora não disponível na fonte  
**Tipo:** auditoria técnica/documental e implantação de controle documental. Não autoriza correções de código nesta execução.  
**Repositório de código:** https://github.com/apoenalore/GameCreator  
**Base de conhecimento:** https://github.com/apoenalore/apoenaskil

## 1. Missão

Atue como engenheiro de software sênior, arquiteto de sistemas, auditor de segurança e responsável por qualidade. Leia os protocolos existentes, recupere os erros/riscos/pendências já relatados, revalide cada achado no commit atual, separe fatos de hipóteses, crie/atualize o Bug Tracker e publique os relatórios nos caminhos oficiais abaixo.

**Não implemente correções de código nesta tarefa.** A autorização é para auditoria e documentação. Correções futuras serão tarefas separadas e respeitarão WIP = 1.

## 2. Leitura obrigatória

No repositório GameCreator, ler:
- AGENTS.md
- README.md
- docs/ATUALIZACOES_PENDENTES_LEIA_ANTES_DE_COMECAR.md
- docs/PENDENCIAS_ABERTAS_E_LIMPEZA_GITHUB.md
- PLANO_GERAL_APOENA.md
- ORGANIZACAO_EDITOR.md
- demais instruções locais referenciadas.

Na base Apoena Skill, consultar:
- AGENTS.md e apoena/AGENTS.md
- apoena/docs/MODOS_DE_TRABALHO_E_PRESERVACAO.md
- apoena/docs/PROTOCOLO_UNIVERSAL_DE_EXTRACAO_E_TRANSFERENCIA.md
- apoena/docs/source-and-status-legend.md
- apoena/docs/game-creator/README.md
- apoena/docs/game-creator/security-audit/conversation-dossier-2026-11-02.md
- apoena/skills/apoena-gamecreator-engineering/SKILL.md
- apoena/skills/apoena-gamecreator-security/SKILL.md
- apoena/docs/game-creator/BUG_TRACKER.md, se já existir.

Se não tiver acesso a algum documento, repositório ou branch, declarar a limitação. Não fingir leitura.

## 3. Preservação e procedimento

Antes de auditar:
- Registrar URL, branch, commit SHA e estado da árvore de trabalho.
- Inventariar arquivos/documentos existentes.
- Não alterar código, assets, projetos, banco, configurações, workflows ou dependências.
- Não instalar pacotes.
- Não executar scripts desconhecidos sem revisar seus efeitos.
- Não executar operações destrutivas nem testes que possam alterar dados reais.
- Não expor secrets, tokens, cookies, chaves ou dados pessoais.
- Respeitar WIP = 1; não iniciar outra tarefa de implementação.
- Não disparar workflows redundantes, fazer merge, release ou publicação.
- Testes somente se seguros e já suportados; registrar comandos, ambiente, logs e limitações.

## 4. Revalidação do backlog

Importar e conferir o backlog inicial do Bug Tracker. Cada achado anterior começa como **RECUPERADO — VALIDAR**. Não herdar automaticamente gravidade ou status de relatório antigo.

Para cada item:
1. Procurar o arquivo/código no HEAD atual.
2. Registrar caminho e linha atuais.
3. Verificar se o trecho ainda existe.
4. Analisar origem dos dados, fluxo, pré-condições e impacto.
5. Reproduzir de forma segura quando possível.
6. Conferir testes e lacunas.
7. Consultar histórico/PRs para saber se já foi corrigido.
8. Não chamar de resolvido sem patch identificável e teste pertinente.

Revisar pelo menos os grupos: SEC-001 a SEC-007; DB-005; SPR-001/002; MAP-001/002; CI-001 a CI-004; DOC-001/002; ARQ-001/002; HTML-002; GODOT-001; TEST-001; observações SQL/TLS.

Se IDs forem o mesmo defeito, preservar aliases e criar referência cruzada; não apagar histórico.

## 5. Status oficiais

Use:
- RECUPERADO — VALIDAR
- ABERTO — CONFIRMADO
- EM INVESTIGAÇÃO
- CORREÇÃO PLANEJADA
- EM CORREÇÃO
- CORRIGIDO — AGUARDANDO TESTE
- RESOLVIDO — TESTADO
- NÃO REPRODUZIDO
- NÃO É ERRO / INFORMATIVO
- DUPLICADO DE GC-XXX
- ADIADO / BLOQUEADO

Somente **RESOLVIDO — TESTADO** significa concluído. CI verde isolado, PR aberto, alteração sem teste ou ausência de reprodução não encerram o item.

Cada ocorrência precisa de ID, origem, branch/SHA, arquivo/linha, evidência, observado/esperado, causa, gravidade, solução, dependências, risco de regressão, teste, critério de aceite, PR/commit, CI, validação manual e risco residual.

## 6. Locais oficiais para publicar

### A. Repositório de código — apoenalore/GameCreator

Relatórios detalhados em **docs/apoena-forensic/**:
1. EXECUTIVE_REPORT.md
2. PROJECT_INVENTORY.md
3. CODE_AUDIT.md
4. ARCHITECTURE_AUDIT.md
5. DATABASE_AUDIT.md
6. SECURITY_AUDIT.md
7. GAME_ENGINE_AUDIT.md
8. PERFORMANCE_AUDIT.md
9. TESTING_AUDIT.md
10. TECHNICAL_DEBT.md
11. RISK_REGISTER.md
12. RECOMMENDED_ROADMAP.md
13. EVIDENCE_INDEX.md

Controle de qualidade:
- **docs/quality/BUG_TRACKER.md** — fonte operacional dos status.
- **docs/quality/bug-reports/GC-<ID>.md** — ficha detalhada por problema confirmado.
- **docs/quality/evidence/README.md** — índice de evidências/logs/capturas sanitizados.
- **docs/quality/README.md** — processo, status e relação entre tracker, testes e relatórios.

Se os caminhos já existirem, leia e atualize aditivamente. Se o repositório tiver convenção obrigatória diferente, registre e peça decisão; não crie estrutura concorrente.

### B. Base de conhecimento — apoenalore/apoenaskil

Espelhar de forma aditiva:
- **apoena/docs/game-creator/BUG_TRACKER.md** — tracker resumido com links para fontes técnicas.
- **apoena/docs/game-creator/forensic-audits/YYYY-MM-DD/README.md** — índice, commit auditado, links para relatórios, cobertura e limitações.
- **apoena/docs/game-creator/README.md** — links para tracker, solicitação e auditorias.
- **apoena/skills/apoena-gamecreator-engineering/SKILL.md** — atualizar apenas se surgir regra reutilizável nova.

Apoena Skill é a base de memória e proveniência. GameCreator é a fonte primária do código, testes, Issues e relatórios técnicos detalhados. Não confundir os dois repositórios.

## 7. Ficha individual de bug

Cada GC-<ID>.md deve conter:
1. Identificação/título.
2. Status atual e histórico.
3. Proveniência e relatórios anteriores.
4. Repositório, branch e SHA.
5. Arquivo/linha atual.
6. Evidência e passos para reprodução.
7. Resultado observado e esperado.
8. Causa raiz ou desconhecida.
9. Gravidade justificada.
10. Solução recomendada.
11. Risco e dependências.
12. Testes e critério de aceite.
13. PR/commit e resultado CI.
14. Validação em ambiente real.
15. Risco residual e próxima ação.

## 8. Relatório final ao proprietário

Em português claro, informar:
- Quantos achados históricos foram revisados.
- Quantos foram confirmados no HEAD atual.
- Quantos já estavam corrigidos antes da auditoria, com evidência.
- Quantos continuam abertos.
- Quantos não foram reproduzidos.
- Quantos são informativos.
- Testes executados e resultados.
- Testes não executados e motivos.
- Cinco prioridades reais seguintes.
- Caminho e link de cada documento publicado.

Não inventar contagens. Se a revisão for parcial, informar cobertura e pendências exatas.

## 9. Critério de conclusão

Concluir somente quando documentos obrigatórios tiverem sido lidos ou suas lacunas registradas; commit-base e inventário estiverem documentados; backlog tiver sido revisado item a item ou cobertura parcial declarada; tracker e relatórios estiverem nos locais corretos; links entre repositórios estiverem registrados; nenhuma correção de código tiver sido feita; e PRs/commits documentais estiverem identificados.

**Regra central: nenhum erro desaparece. Ele muda de status com histórico e evidência. Nenhum relatório pode ser chamado de completo se a cobertura real foi parcial.**
