# Registro de engenharia — Game Creator: A1, fonte oficial e roteiro de estabilização

**Data:** 2026-11-02  
**Projeto:** Apoena Game Creator / Apoena Pixel Art  
**Tipo:** memória técnica e decisões de engenharia  
**Cobertura:** relatório fornecido pelo autor + inspeção independente dos ZIPs anexados nesta conversa.  
**Limite:** o link compartilhado 6ae862fa-d868-83e9-816e-65cdefa204d4 não pôde ser recuperado pelo leitor disponível; os ZIPs anexados foram abertos e verificados localmente.

## 1. Objetivo e princípios

A evolução deve transformar o Game Creator numa plataforma sustentável, modular e multiplataforma sem reconstruir o produto nem destruir funcionalidades, projetos, bibliotecas ou contratos existentes.

Princípios:
1. Preservar funcionalidades e compatibilidade.
2. Não corromper projetos, assets ou dados IndexedDB.
3. Não refatorar antes de conhecer dependências e contratos.
4. Eliminar duplicações somente após provar que não são utilizadas.
5. Distinguir plano, implementação, teste e publicação.
6. Manter WIP = 1 entre GameCreator e Apoena Pixel Art HTML.
7. Nenhuma correção será declarada sem arquivo alterado, justificativa e evidência de teste.

## 2. Entendimento arquitetural registrado

Subsistemas:
- aplicação principal V4.0;
- Pixel Art Studio;
- Map Editor;
- Asset Library;
- Creator Bridge;
- biblioteca e backup;
- integração Godot;
- build e publicação;
- testes.

A arquitetura é parcialmente modular, mas mantém uma base HTML integrada de grande porte e responsabilidades compartilhadas entre ferramentas. A estratégia aprovada é modularização progressiva, não reescrita.

Camadas-alvo propostas:
- entrada/composição;
- domínio;
- casos de uso/aplicação;
- adaptadores de persistência, arquivos, mensagens e Godot;
- interface;
- camada de compatibilidade.

## 3. Auditoria independente do pacote A1

Arquivos recebidos:
- GameCreator-main-original-backup.zip — 60.120.095 bytes; SHA-256 bb40c8419056dfecdf75f9db99ee2deecfe6963a7fbe5b3d5b804b8b7346dfd9.
- GameCreator-arquitetura-v1.zip — 60.134.000 bytes; SHA-256 cbfdec9c63c5b0e3e778fa04153eb2959cddcdda0e34e23b395bdc5cb83231c0.

Os dois ZIPs passaram na verificação de integridade do formato ZIP. A comparação SHA-256 de todos os arquivos originais encontrou 135/135 arquivos idênticos entre o backup original e o pacote A1. Nenhum arquivo original foi removido, renomeado ou alterado. O pacote A1 adicionou seis arquivos, incluindo um .pyc transitório dentro de __pycache__.

A ferramenta tools/architecture_audit.py:
- gerou manifesto determinístico;
- o manifesto contém 139 arquivos (excluindo a si próprio, ruído e arquivos de cache);
- a verificação --check passou;
- os três testes unitários passaram quando executados diretamente como python tests/architecture_audit.test.py -v.

Divergência documental identificada: architecture/IMPLEMENTATION_LOG.md declara 138 arquivos no manifesto; o arquivo module-manifest.json declara 139. Corrigir o registro na próxima atualização documental.

Artefatos:
- architecture/ARCHITECTURE.md;
- architecture/module-manifest.json;
- architecture/IMPLEMENTATION_LOG.md;
- tools/architecture_audit.py;
- tests/architecture_audit.test.py.

## 4. Fonte oficial e artefato de distribuição — conclusão preliminar baseada em código

A inspeção encontrou:
- APOENA_GAME_CREATOR_V4_0_BANCADA_INTEGRADA.html: fonte de entrada preservada usada pelos dois scripts de build. O arquivo mantém o título interno “v3.9.2”, apesar do nome V4.0; o build altera o título para V4.0.
- integracao/build_unificado.ps1: gerador PowerShell usado pelo workflow de validação, pelo workflow de publicação e pelo atalho local descrito no README.
- integracao/build_unificado.py: gerador Python alternativo.
- index.html: resultado integrado gerado, com aba Pixel Art e oito referências externas a módulos compartilhados; não é um loader compacto nem um HTML autossuficiente isolado.

Portanto, a separação funcional observada é:
**fonte de entrada:** APOENA_GAME_CREATOR_V4_0_BANCADA_INTEGRADA.html  
**artefato integrado:** index.html  
**build operacional predominante:** integracao/build_unificado.ps1

A documentação do README que chama index.html de “carregador compacto” contradiz o arquivo real: o index.html do pacote tem cerca de 16,3 MB e contém a aplicação principal completa, além de referências relativas a módulos externos. A distribuição integrada precisa preservar também as pastas referenciadas; não se deve distribuir o index isoladamente.

Há uma diferença reproduzível de dois bytes entre o index.html fornecido e o resultado do build Python: o gerador Python insere uma quebra de linha antes de </main>, enquanto o artefato existente não a contém. A diferença é localizada, mas demonstra que os dois geradores ainda não produzem saída byte a byte idêntica. A equivalência PowerShell/Python precisa ser testada e normalizada antes de anunciar um build multiplataforma canônico.

O documento LEIA_PRIMEIRO_V4_0.md também recomenda abrir o HTML original diretamente, o que descreve um fluxo standalone distinto do pacote integrado index.html + módulos externos. A documentação deve diferenciar claramente esses dois modos.

## 5. CI e build observados

O pacote contém:
- .github/workflows/pixel-art.yml;
- .github/workflows/publicar-creator-unificado.yml.

Ambos chamam o build PowerShell em contexto Windows. O workflow de validação também executa smoke tests de navegador, mas usa a opção --disable-javascript; portanto, essa etapa verifica DOM/estrutura estática, não interação JavaScript real. A existência de smoke test não deve ser descrita como validação funcional de interação.

A auditoria anterior também relata testes IndexedDB bloqueados pela ausência de fake-indexeddb/auto. A1 não comprova testes de restauração real em navegador.

## 6. Problemas e riscos a resolver

- ARQ-001: HTML principal grande e responsabilidades concentradas.
- ARQ-002: scripts e componentes integrados ao núcleo.
- ARQ-003: dependências e contratos pouco documentados.
- ARQ-004: duplicações potenciais ainda sem prova de inutilização.
- ARQ-005: fonte, loader e artefato de distribuição descritos de forma contraditória.
- BLD-001: Python e PowerShell não produzem saída idêntica.
- BLD-002: dois workflows com áreas de gatilho sobrepostas; avaliar responsabilidades sem apagar nenhum antes de mapear dependências.
- BLD-003: validação por tamanho literal do bundle (16324808) é frágil; substituir por hash/manifesto, com migração e testes.
- TST-001: testes IndexedDB dependem de fake-indexeddb/auto.
- TST-002: smoke test do browser desativa JavaScript e não cobre interação.
- TST-003: ausência de regressão visual manual completa.
- TST-004: integração Godot precisa de validação de exportação/importação e runtime.
- SEC: bridge, importação de arquivos, backup, validação de imagens e integridade dos pacotes exigem revalidação conforme docs/security/.

Esses itens são riscos e problemas de engenharia a investigar; não são todos vulnerabilidades confirmadas.

## 7. Decisões de engenharia

- Preservar o HTML original e o núcleo atual até existir substituição compatível.
- Modularizar um componente por vez, com fachada de compatibilidade.
- Tratar JSON, IDs, IndexedDB, stores assets/projects, eventos e mensagens do Creator Bridge como contratos.
- Criar testes de caracterização antes de extrair módulos.
- Não mudar formatos de exportação sem fixtures de regressão.
- Manter backup recuperável antes de qualquer intervenção destrutiva.
- Não apagar versões históricas nem caminhos antigos até provar ausência de referências.
- Manter WIP = 1.

## 8. Roteiro aprovado pelo autor

P0 — Estabilizar a versão principal:
- confirmar fonte oficial, artefato, build e caminho real de distribuição;
- alinhar documentação com o comportamento observado;
- tornar o build reproduzível e rastreável.

P1 — Corrigir a organização:
- mapear duplicações, arquivos obsoletos, documentação contraditória e caminhos antigos;
- preservar backups;
- só excluir depois de provar que nenhum fluxo, teste ou referência usa o arquivo.

P2 — Consertar o editor de mapas:
- autotiling;
- tilesets;
- interface;
- persistência e reabertura de projetos;
- compatibilidade com dados existentes.

P3 — Validar integração:
- biblioteca;
- itens e receitas;
- personagens;
- mapas;
- importação/exportação Godot.

P4 — Testar Android e PC:
- salvamento e recuperação;
- desempenho;
- navegação e interação;
- instalação e funcionamento em dispositivos reais.

P5 — Expandir:
- somente depois de estabilizar e validar as etapas anteriores.

## 9. Próxima tarefa técnica

A2 — mapa completo de dependências e contratos:
- funções e variáveis globais;
- eventos e listeners;
- APIs públicas;
- imports/exports e dependências entre scripts;
- estruturas JSON;
- banco e stores IndexedDB;
- mensagens e ações do Creator Bridge;
- pontos de entrada e rotas de navegação;
- referências a arquivos históricos/duplicados.

A2 deve ser levantamento documental e testes de caracterização; não iniciar extração do monólito antes de fechar o mapa.

## 10. Limites de validação

- A1 foi inspecionado em ZIP e os hashes dos 135 arquivos originais coincidiram.
- Os três testes da ferramenta arquitetural passaram.
- O manifesto passou em --check.
- O build Python foi executado em cópia temporária; a saída diferiu do index recebido em dois bytes.
- Não houve nesta inspeção execução do PowerShell, runner Windows, navegador real, IndexedDB real, Android ou Godot.
- O link compartilhado informado pelo autor não foi recuperado; os anexos ZIP disponíveis foram usados como fonte.
- Nenhuma correção funcional ou exclusão de arquivos foi feita por esta auditoria.

## 11. Regra de atualização

Este documento é um registro de engenharia e proveniência. Atualizações devem preservar estados anteriores, incluir data, SHA, arquivos, testes e evidências. Não chamar proposta de implementação nem teste estático de validação de runtime.


## 12. Continuidade e estado do GitHub — 2026-11-02, após 10:43 UTC

Verificação independente por leitura de PRs, branches, commits e GitHub Actions.

- GameCreator `main`: `1b95d036c31dfb4ca9f9ce6859510be2c9f7e8cd`, sem mudança observada.
- GameCreator PR [#12](https://github.com/apoenalore/GameCreator/pull/12): aberta, draft, HEAD anterior a esta atualização `05ef347335ae8009b96480b471436f1fe2b32218`. Alterações recentes documentais; não há comprovação de correção funcional.
- Apoena Skill PR [#6](https://github.com/apoenalore/apoenaskil/pull/6): aberta, draft, HEAD anterior a esta atualização `feb653a4f1369a5129b205276d18d40eca891f6b`.
- Novo achado operacional: execução [GameCreator Actions #41429123726](https://github.com/apoenalore/GameCreator/actions/runs/41429123726), workflow `pixel-art.yml`, evento `pull_request`, SHA `05ef347335ae8009b96480b471436f1fe2b32218`, iniciada `2026-11-02T10:28:46Z`, concluída `2026-11-02T10:43:40Z`, resultado `failure`. Job `validar` iniciou `10:33:39Z` e terminou `10:43:39Z`; a API consultada não retornou etapas. A causa **não está diagnosticada**.
- O workflow usa runner próprio Windows x64; há execuções anteriores canceladas pela política de concorrência, que não são equivalentes a falhas de teste.
- Próximo passo: recuperar logs completos no runner/GitHub Actions e identificar a primeira etapa com erro. Não marcar o pipeline como validado nem modificar o workflow com base em suposição.
- A continuidade documental não inclui dados locais IndexedDB, assets fora do repositório ou transcrição integral de conversas não acessíveis. Nenhuma alteração funcional foi executada nesta verificação.
