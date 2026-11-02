# RELATÓRIO TÉCNICO DE ENGENHARIA
## Game Creator / Apoena — Diagnóstico, decisões e plano de resolução

**Data declarada no documento:** 02 de novembro de 2026  
**Projeto:** Game Creator V4.0 / Apoena Pixel Art  
**Foco:** Engenharia reversa, arquitetura, modularização, correção de erros e evolução do software.  
**Origem:** Documento fornecido pelo autor nesta conversa em 2026-11-02.  
**Estado de preservação:** REGISTRO DE FONTE DO AUTOR — alegações técnicas ainda precisam de validação independente.

> Este documento preserva o relatório recebido. Os resultados e diagnósticos aqui descritos não são automaticamente certificados por esta gravação no GitHub. Separar sempre o que foi relatado, o que foi reproduzido e o que foi comprovado por evidência técnica.

---

# 1. OBJETIVO DA ANÁLISE

O objetivo é transformar o Game Creator numa plataforma de criação de jogos mais robusta, modular, escalável e confiável, preservando as funcionalidades existentes e a compatibilidade com projetos anteriores.

A evolução deve obedecer a cinco princípios:

1. Não perder funcionalidades existentes.
2. Não corromper projetos ou bibliotecas.
3. Não introduzir regressões durante a modularização.
4. Eliminar duplicações e inconsistências arquiteturais.
5. Desenvolver novas funcionalidades sobre uma arquitetura sustentável.

# 2. ENTENDIMENTO DO SISTEMA

A análise inicial identificou que o Game Creator é um ecossistema composto por várias ferramentas integradas.

| Subsistema | Responsabilidade |
|---|---|
| Game Creator V4.0 | Aplicação principal |
| Pixel Art Studio | Criação e edição de sprites |
| Map Editor | Construção de mapas e terrenos |
| Asset Library | Armazenamento compartilhado |
| Creator Bridge | Comunicação entre ferramentas |
| Biblioteca | Backup e recuperação |
| Integração Godot | Exportação e integração com jogos |
| Build System | Construção da aplicação integrada |
| Testes | Verificação de funcionalidades |

## Entendimento arquitetural

O projeto possui uma arquitetura parcialmente modular, mas ainda mantém uma concentração significativa de funcionalidades no núcleo HTML integrado.

Isso cria uma contradição arquitetural:

- Existem módulos independentes.
- Existem ferramentas compartilhadas.
- Existem interfaces de comunicação.
- Porém, uma parte importante do funcionamento continua concentrada num arquivo monolítico.

A solução não é reconstruir tudo. É separar gradualmente as responsabilidades existentes.

# 3. RELATÓRIO DE ERROS E RISCOS

## 3.1. Problemas de arquitetura

| ID | Problema | Gravidade | Decisão |
|---|---|---|---|
| ARQ-001 | HTML principal excessivamente grande | Alta | Modularização progressiva |
| ARQ-002 | Scripts incorporados no núcleo | Alta | Separar responsabilidades |
| ARQ-003 | Dependências entre módulos pouco documentadas | Alta | Criar mapa de dependências |
| ARQ-004 | Possível duplicação de funcionalidades | Média | Auditar antes de eliminar |
| ARQ-005 | Histórico de versões complexo | Média | Estabelecer fonte oficial |

## 3.2. Problemas de build e publicação

| ID | Problema | Gravidade | Decisão |
|---|---|---|---|
| BLD-001 | Build Python e PowerShell | Alta | Comparar resultados e estabelecer um build canônico |
| BLD-002 | Workflows sobrepostos | Alta | Consolidar depois de mapear gatilhos |
| BLD-003 | Verificação baseada em tamanho fixo | Média | Substituir por hashes |
| BLD-004 | Ambiguidade entre fonte e artefato publicado | Alta | Definir fonte oficial |

Problema específico reportado:

```python
assert 'full.length!==16324808' in loader
```

A utilização de um tamanho fixo torna a validação sensível a pequenas alterações legítimas.

**Solução proposta:** utilizar manifesto de integridade com SHA-256, tamanho e identificação dos arquivos.

## 3.3. Problemas de testes

| ID | Problema | Gravidade | Decisão |
|---|---|---|---|
| TST-001 | Testes de IndexedDB bloqueados por dependência ausente | Alta | Corrigir ambiente de testes |
| TST-002 | Testes de navegador desativam JavaScript | Alta | Criar testes de interação |
| TST-003 | Falta de validação visual completa | Média | Testes reais de navegador |
| TST-004 | Integração Godot não comprovada | Alta | Criar testes de exportação e importação |

A suíte principal ainda não foi integralmente aprovada.

Não devemos considerar um módulo funcional apenas porque sua sintaxe JavaScript está correta.

## 3.4. Segurança e integridade

Foram identificados pontos que exigem revisão:

- Uso de `innerHTML`.
- Mensagens entre janelas com destino `"*"`.
- Validação de arquivos importados.
- Recuperação de backups.
- Integridade dos registros IndexedDB.

Esses elementos representam pontos de investigação, não vulnerabilidades comprovadas.

# 4. DECISÕES DE ENGENHARIA

### DEC-001 — Preservar a aplicação original
Não remover o núcleo V4.0 enquanto não houver substituição comprovadamente compatível.

### DEC-002 — Modularizar progressivamente
Cada módulo deverá ser separado individualmente, com uma fachada de compatibilidade para preservar as chamadas antigas.

### DEC-003 — Preservar contratos de dados
Não modificar silenciosamente:
- Estruturas JSON.
- Identificadores de projetos.
- Banco IndexedDB.
- Stores `assets` e `projects`.
- Eventos.
- Mensagens do Creator Bridge.
- Formatos de exportação.

### DEC-004 — Testes obrigatórios
Toda alteração deverá possuir testes de regressão.

### DEC-005 — Backup antes de modificações
Nenhuma operação destrutiva deverá ser realizada sem cópia recuperável.

### DEC-006 — Uma tarefa de implementação por vez
Manter WIP = 1 para evitar alterações concorrentes no Game Creator e no Pixel Art Studio.

# 5. METODOLOGIA DE ENGENHARIA REVERSA

O método de trabalho será dividido em sete etapas.

1. **Inventário:** identificar arquivos, módulos, versões e responsabilidades.
2. **Dependências:** mapear quem chama quem, quais dados são compartilhados e quais módulos dependem do núcleo.
3. **Contratos:** documentar funções públicas, eventos, APIs, formatos de arquivos e persistência.
4. **Caracterização:** criar testes que reproduzam o comportamento atual antes de qualquer alteração.
5. **Refatoração:** separar o código em módulos independentes, mantendo compatibilidade.
6. **Regressão:** comparar o comportamento antigo com o novo.
7. **Validação:** testar no navegador, nos dispositivos relevantes e na integração Godot.

# 6. ARQUITETURA-ALVO

A arquitetura desejada será organizada da seguinte forma:

```text
GAME CREATOR
│
├── APPLICATION
│   ├── Bootstrap
│   ├── Navigation
│   └── Application Manager
│
├── MODULES
│   ├── Pixel Art Studio
│   ├── Map Editor
│   ├── Animation Studio
│   ├── Asset Manager
│   └── Game Systems
│
├── CORE
│   ├── Event System
│   ├── State Manager
│   ├── Command System
│   └── Plugin Interface
│
├── SERVICES
│   ├── Asset Library
│   ├── IndexedDB
│   ├── Creator Bridge
│   ├── Backup Service
│   └── Import / Export
│
├── INTEGRATIONS
│   └── Godot
│
└── TESTS
    ├── Unit Tests
    ├── Integration Tests
    ├── Regression Tests
    └── E2E Tests
```

Este é o desenho arquitetural proposto, não uma descrição de módulos já implementados.

# 7. PRIMEIRA IMPLEMENTAÇÃO REALIZADA — CONFORME RELATO DO AUTOR

Foi preparada uma versão de trabalho com os seguintes arquivos adicionais:

| Arquivo | Objetivo |
|---|---|
| `architecture/ARCHITECTURE.md` | Documentação arquitetural |
| `architecture/module-manifest.json` | Inventário SHA-256 |
| `architecture/IMPLEMENTATION_LOG.md` | Registro de alterações |
| `tools/architecture_audit.py` | Ferramenta de auditoria |
| `tests/architecture_audit.test.py` | Testes da ferramenta |

## Resultados reportados

- 139 arquivos no manifesto atualizado.
- 3 testes arquiteturais aprovados.
- Verificação do manifesto aprovada.
- 62 arquivos JavaScript anteriormente analisados sintaticamente.
- 4 testes funcionais anteriormente reportados como aprovados.
- 2 testes da biblioteca ainda bloqueados pela dependência ausente.

**Limitação de evidência:** o registro anterior declarou preservação de 135/135 arquivos originais, mas a comparação independente dos hashes não ficou demonstrada na execução registrada. Essa verificação deverá ser refeita antes de certificar a preservação integral.

Também não houve teste completo no navegador, Windows ou Godot.

# 8. PLANO DE RESOLUÇÃO PRIORIZADO

| Prioridade | Intervenção | Resultado esperado |
|---|---|---|
| P0 | Confirmar backup e integridade | Segurança |
| P0 | Mapear dependências | Conhecimento estrutural |
| P0 | Recuperar testes IndexedDB | Testabilidade |
| P1 | Definir build oficial | Reprodutibilidade |
| P1 | Mapear APIs públicas | Compatibilidade |
| P1 | Separar primeiro módulo | Modularização |
| P2 | Consolidar workflows | CI/CD confiável |
| P2 | Melhorar segurança | Proteção dos dados |
| P3 | Evoluir interface | Usabilidade |
| P3 | Ampliar funcionalidades | Expansão do produto |

# 9. CRITÉRIOS DE ACEITAÇÃO

Uma melhoria somente será considerada concluída quando:

- O código novo estiver implementado.
- Os testes correspondentes passarem.
- As funcionalidades antigas continuarem operacionais.
- Os projetos antigos puderem ser abertos.
- Os backups puderem ser restaurados.
- Os formatos de exportação forem compatíveis.
- O build for reproduzível.
- Não existirem erros novos não justificados.

# 10. CONCLUSÃO TÉCNICA

O Game Creator possui uma base que merece ser preservada.

O principal desafio é transformar uma aplicação que cresceu por integração de funcionalidades numa plataforma com responsabilidades bem definidas.

A decisão estratégica é não reconstruir o produto, mas evoluí-lo através de engenharia reversa, documentação, modularização progressiva e testes de regressão.

**Próxima tarefa técnica indicada: A2 — construir o mapa completo de dependências e contratos do projeto.**

Esse levantamento determinará qual módulo poderá ser extraído primeiro com o menor risco.

**Responsabilidade técnica:** evolução incremental, preservação de compatibilidade, rastreabilidade das decisões e validação das alterações.

**Estado geral declarado:** auditoria inicial e infraestrutura de documentação implementadas; modularização do núcleo ainda pendente.

# 11. CAPACIDADES DE ENGENHARIA A APLICAR

O relatório define seis capacidades a serem aplicadas:

| Capacidade | Aplicação no Game Creator |
|---|---|
| Engenharia reversa | Reconstruir como o programa funciona |
| Análise estática | Encontrar dependências e problemas no código |
| Análise arquitetural | Identificar acoplamento e duplicação |
| Engenharia de testes | Verificar se as correções funcionam |
| Refatoração | Melhorar código sem alterar o comportamento esperado |
| Análise de regressão | Garantir que melhorias não destruam funcionalidades antigas |

Regra de evidência: nenhum erro deve ser declarado corrigido sem apresentar o arquivo alterado, o motivo da alteração e o resultado do teste correspondente.

# 12. PRÓXIMA INVESTIGAÇÃO

Antes de adicionar funcionalidades, responder com evidências:

- Qual é a verdadeira fonte oficial do Game Creator?
- Quais funções ainda estão duplicadas?
- Quais módulos dependem diretamente do HTML principal?
- Quais dados podem ser compartilhados sem gerar conflitos?
- Qual módulo pode ser separado primeiro sem quebrar o restante?

A recomendação do relatório é começar pelo mapa completo de dependências do JavaScript e das APIs compartilhadas. Esse será o instrumento para decidir onde decompor o monólito com segurança.

---

## NOTA DE PRESERVAÇÃO E VALIDAÇÃO

Este arquivo registra fielmente o conteúdo técnico fornecido pelo autor, com ajustes apenas de organização e formatação. Os números, testes, caminhos e diagnósticos são **resultados reportados na fonte**. A auditoria independente do commit, dos arquivos, dos hashes e da execução dos testes permanece pendente.

Não foi realizada aqui qualquer alteração no código do Game Creator. Este commit é exclusivamente documental.
