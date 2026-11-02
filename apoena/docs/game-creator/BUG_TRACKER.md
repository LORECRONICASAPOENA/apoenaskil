# Game Creator — Bug Tracker oficial e registro de correções

**Projeto:** Apoena Game Creator  
**Repositório de código:** https://github.com/apoenalore/GameCreator  
**Base de conhecimento:** https://github.com/apoenalore/apoenaskil  
**Data do registro:** 2026-11-02  
**Hora do registro:** Hora não disponível na fonte  
**Estado:** BACKLOG INICIAL RECUPERADO — VALIDAR. Não certifica que os achados continuam presentes no HEAD atual.

## 1. Regra oficial de status

| Status | Significado | Critério |
|---|---|---|
| RECUPERADO — VALIDAR | Achado veio de relatório anterior; não revalidado no código atual | Confirmar no SHA atual |
| ABERTO — CONFIRMADO | Reproduzido/demonstrado no código atual | Arquivo/linha, cenário e impacto |
| EM INVESTIGAÇÃO | Causa, escopo ou reprodução em apuração | Não declarar correção |
| CORREÇÃO PLANEJADA | Solução aprovada, ainda sem patch | Plano e aceite definidos |
| EM CORREÇÃO | Patch em desenvolvimento | Branch/PR identificado |
| CORRIGIDO — AGUARDANDO TESTE | Patch implementado, validação incompleta | SHA e teste pendente |
| RESOLVIDO — TESTADO | Correção passou nos testes relevantes e regressões exigidas | Evidências, SHA, CI e validação anexados |
| NÃO REPRODUZIDO | Investigação atual não reproduziu | Ambiente e passos documentados; não significa automaticamente falso |
| NÃO É ERRO / INFORMATIVO | Comportamento intencional ou observação sem falha | Justificativa técnica |
| DUPLICADO DE GC-XXX | Mesmo defeito já registrado | Manter alias e proveniência |
| ADIADO / BLOQUEADO | Depende de acesso, ambiente, decisão ou terceiro | Bloqueio e condição de retomada |

**Somente RESOLVIDO — TESTADO significa concluído.** Código alterado, PR aberto, CI verde isolado ou ausência de reprodução não encerram item.

## 2. Campos obrigatórios por ocorrência

ID estável; título; status e histórico; proveniência; repositório/branch/SHA; arquivo e linha atuais; evidência; comportamento observado e esperado; causa raiz ou desconhecida; impacto e gravidade justificada; solução proposta; dependências e risco de regressão; plano de teste e critério de aceite; branch/PR/commit; resultado do CI no SHA correto; validação manual/plataforma; risco residual; responsável e próxima ação.

Nunca incluir tokens, senhas, cookies, chaves, dados pessoais ou conteúdo sensível em relatórios.

## 3. Backlog inicial recuperado

Todos os itens abaixo começam como **RECUPERADO — VALIDAR**. Foram consolidados de relatórios/mensagens fornecidos em 02/11/2026 e precisam ser reexaminados no código e commit atuais. Os aliases preservam os IDs usados nas fontes anteriores.

| ID oficial | Alias de origem | Área | Achado recuperado | Próxima verificação |
|---|---|---|---|---|
| GC-SEC-001 | SEC-001 | Creator Bridge | Aceitação de origem null em mensagens entre janelas | Inspecionar origin, source, canal e autorização |
| GC-SEC-002 | SEC-002 | Comunicação | Validação insuficiente do remetente/origem no receptor | Conferir event.source, event.origin e schema |
| GC-SEC-003 | SEC-003 | Comunicação | postMessage com target origin * | Verificar se origem exata pode ser definida |
| GC-DB-001 | DB-005 | Backup/IndexedDB | Restauração/importação pode terminar parcialmente | Simular falha em cada etapa em ambiente isolado |
| GC-SPR-001 | SPR-001 | Assets | Dez caminhos de imagens/sprites referenciados não presentes no ZIP analisado | Comparar catálogo e arquivos no pacote/HEAD corretos |
| GC-SPR-002 | SPR-002 | Importação | Validação MIME possivelmente ampla (image/*) | Verificar magic bytes, decodificação e limites |
| GC-MAP-001 | MAP-001 | Map Editor | Perfil/configuração de tileset não preservado em fluxo descrito | Reproduzir salvar, fechar e reabrir |
| GC-MAP-002 | MAP-002 | Autotiling | Autotiling de água incompleto em combinações descritas | Mapear vizinhanças e testes de borda |
| GC-CI-001 | CI-001 | GitHub Actions | Possível sobreposição de gatilhos/workflows | Inventariar workflows, paths e eventos |
| GC-CI-002 | CI-002 | Testes | Smoke test descrito com JavaScript desativado | Examinar configuração e provar que testa a aplicação |
| GC-CI-003 | CI-003 | Build | Reprodutibilidade de dependências/build precisa ser comprovada | Repetir build limpo e comparar artefatos |
| GC-CI-004 | CI-004 | Build | Diferença de 2 bytes entre resultados foi reportada | Reproduzir e identificar causa |
| GC-DOC-001 | DOC-001 | Documentação | Divergências entre documentos/versões | Comparar fontes, datas e artefatos |
| GC-DOC-002 | DOC-002 | Versionamento | Identificação de versão possivelmente incorreta | Conferir metadados, README, UI e artefato |
| GC-ARCH-001 | ARQ-001/002 | Arquitetura | HTML principal grande e scripts concentrados no núcleo | Medir responsabilidades e dependências |
| GC-SEC-004 | HTML-002 | Segurança | Uso de innerHTML exige revisão contextual | Rastrear origem dos dados e sanitização; ocorrência não prova XSS |
| GC-GODOT-001 | GODOT-001 | Godot | Integração/runtime de gameplay não comprovados ponta a ponta | Importar/exportar e executar projeto consumidor |
| GC-TEST-001 | TEST-001 | Testes | Duas suítes reportadas bloqueadas por fake-indexeddb/auto ausente | Conferir package/lockfile e executar no ambiente correto |
| GC-SEC-005 | SEC-004 | Backup | Ausência de assinatura/autenticidade do backup reportada | Verificar controles atuais; hash não autentica origem |
| GC-SEC-006 | SEC-005 | Upload | Validação de MIME reportada como insuficiente | Correlacionar com GC-SPR-002; evitar duplicar correção |
| GC-SEC-007 | SEC-006 | Distribuição | Integridade do ZIP distribuído não comprovada no fluxo descrito | Inspecionar workflow, manifesto, assinatura e verificação |
| GC-SEC-008 | SEC-007 | Projetos | Validação estrutural de projetos/backups descrita como incompleta | Mapear schema, limites e rejeição segura |
| GC-SEC-009 | Governança | GitHub | Proteção de branch/revisão independente desconhecida no dossiê | Inspecionar rulesets/branch protection atuais |
| GC-TEST-002 | Recuperação | Backup | Testes de falha/rollback e restauração real não comprovados | Planejar teste isolado sem tocar dados reais |

### Observações que não são automaticamente bugs

- **SQL:** nenhum arquivo .sql/banco relacional foi identificado no pacote descrito; a documentação aponta IndexedDB. Classificar como informativo.
- **SSL/TLS:** ausência de certificado no ZIP não prova ausência de HTTPS no ambiente publicado.
- **Assets ausentes:** a constatação de dez sprites é relativa ao ZIP específico examinado; revalidar no HEAD atual.
- **innerHTML:** ocorrência não equivale a XSS sem fluxo explorável.
- **Duplicação:** nomes ou conteúdo semelhantes não autorizam exclusão.

## 4. Melhorias arquiteturais — não misturar com bugs

| ID | Tema | Classificação |
|---|---|---|
| GC-ARCH-002 | Mapa completo de dependências e contratos | Trabalho de arquitetura |
| GC-ARCH-003 | Definição da fonte oficial e build canônico | Decisão/arquitetura |
| GC-ARCH-004 | Modularização progressiva com fachada de compatibilidade | Planejado; não implementado |
| GC-ARCH-005 | Inventário de duplicados, órfãos e obsoletos comprovados | Auditoria pendente |

## 5. Histórico de mudanças

Adicionar uma linha por mudança; não sobrescrever status anterior.

| Data | ID | Status anterior | Status novo | Evidência/PR/commit | Autor |
|---|---|---|---|---|---|
| 2026-11-02 — Hora não disponível na fonte | Todos acima | — | RECUPERADO — VALIDAR | Relatórios e backup recebidos; revalidação atual pendente | Registro inicial |

## 6. Painel inicial

- Resolvido — testado: **0 comprovados neste registro**.
- Confirmado no HEAD atual: **0 comprovados neste registro**.
- Em correção: **0 comprovados neste registro**.
- Recuperado — validar: **24 itens acima**.
- Informativos: SQL e TLS, conforme limites descritos.

## 7. Sincronização entre repositórios

- **Fonte técnica primária:** apoenalore/GameCreator. Tracker operacional em docs/quality/BUG_TRACKER.md.
- **Relatórios detalhados:** docs/apoena-forensic/ no GameCreator.
- **Fichas individuais:** docs/quality/bug-reports/GC-<ID>.md.
- **Evidências:** docs/quality/evidence/ com logs/capturas sanitizados.
- **Base de conhecimento:** espelhar tracker resumido e índices em apoenalore/apoenaskil, dentro de apoena/docs/game-creator/.
- Apoena Skill preserva memória e proveniência; não substitui código, testes, Issues ou PRs do GameCreator.
- Para anexos binários não versionados, registrar nome, SHA-256, tamanho, localização e pendência.
