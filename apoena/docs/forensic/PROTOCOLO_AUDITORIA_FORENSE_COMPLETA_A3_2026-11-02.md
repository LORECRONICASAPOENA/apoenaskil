# APOENA GAME CREATOR — PROTOCOLO DE AUDITORIA FORENSE COMPLETA (A3)

**Data de origem:** 2026-11-02  
**Origem:** instrução do proprietário nesta conversa, complementada por recomendações consultivas.  
**Destino previsto:** Codex / repositório Apoena Game Creator.  
**Tipo:** missão de auditoria somente leitura.  
**Estado:** protocolo proposto pelo proprietário; ainda não executado nesta tarefa.  
**Escopo:** HTML, CSS, JavaScript, sprites/assets, SSL/TLS, SQL quando existir, IndexedDB e demais mecanismos encontrados.

> Este documento registra o escopo solicitado. Não afirma que a auditoria já foi executada, que os arquivos foram examinados ou que vulnerabilidades foram comprovadas.

---

## 1. Objetivo

Examinar o Apoena Game Creator como equipe multidisciplinar de engenharia de software sênior, arquitetura de sistemas, engenharia reversa, segurança da informação, banco de dados e desenvolvimento de jogos.

A missão é determinar, com evidências rastreáveis, o estado real do software, sua estrutura, qualidade, integridade, segurança, limitações e potencial de evolução.

A auditoria deve ser profunda, arquivo por arquivo e módulo por módulo. Não basta avaliação visual ou funcional superficial.

## 2. Preservação e procedimento

Antes de analisar:

- Ler `AGENTS.md` e toda a documentação obrigatória.
- Identificar regras de trabalho, dependências e restrições existentes.
- Preservar integralmente o código original.
- Não executar scripts desconhecidos sem avaliar seus efeitos.
- Não modificar arquivos nesta etapa.
- Não instalar dependências nem alterar configurações.
- Não expor segredos encontrados.

### Controles adicionais recomendados

1. Registrar commit-base, branch e estado da árvore de trabalho.
2. Registrar inventário e hashes SHA-256 dos arquivos relevantes antes da análise.
3. Separar arquivos rastreados, não rastreados, gerados e ignorados.
4. Registrar ferramentas e versões utilizadas na auditoria.
5. Não copiar segredos para relatórios; registrar apenas caminho, tipo e risco, com valores redigidos.
6. Não iniciar commits, alterações de código ou workflows sem autorização.
7. Respeitar WIP = 1 e as regras de execução sequencial de CI já existentes no projeto.

## 3. Inventário forense

Examinar recursivamente o repositório e identificar:

- Arquivos e diretórios.
- Linguagens de programação.
- Frameworks e bibliotecas.
- Dependências e versões.
- Arquivos de configuração.
- Scripts de inicialização e compilação.
- Módulos e componentes.
- Arquivos obsoletos, duplicados ou abandonados.
- Código não utilizado.
- Dependências externas.
- Assets, imagens, sprites, fontes, áudio e modelos 3D.
- Documentação e histórico de versões disponível.

Produzir inventário técnico com caminhos, tamanhos, hashes quando pertinente e responsabilidades.

Não classificar arquivo como descartável apenas por nome, tamanho, idade ou semelhança com outro arquivo.

## 4. Análise do código-fonte

### HTML
- Estrutura semântica.
- Organização dos componentes.
- Acessibilidade.
- Compatibilidade entre navegadores.
- Segurança de conteúdo.
- Integridade da interface.

### CSS
- Arquitetura visual.
- Responsividade.
- Duplicações.
- Conflitos de estilos.
- Desempenho de renderização.

### JavaScript
- Organização modular.
- Fluxo de execução.
- Eventos e estados.
- Gerenciamento de memória.
- Tratamento de exceções.
- Concorrência e operações assíncronas.
- Vazamentos de memória.
- Dependências circulares.
- Código morto e duplicado.

### Sprites e recursos gráficos
- Formatos e dimensões.
- Spritesheets e organização de frames.
- Animações e sequenciamento.
- Transparência e canais de cor.
- Colisões e hitboxes.
- Escalonamento e resolução.
- Compatibilidade com o motor de execução.
- Integridade dos arquivos e referências.

### SQL e persistência
- Identificar se SQL existe efetivamente.
- Estruturas e esquemas de banco de dados.
- Tabelas, campos, índices e relacionamentos.
- Integridade referencial.
- Consultas e operações CRUD.
- Migrações.
- Transações.
- Backup e recuperação.
- Riscos de SQL Injection.
- Consistência entre modelos e dados.

Examinar também IndexedDB, LocalStorage, armazenamento de arquivos e outros mecanismos encontrados. Não presumir que SQL esteja implementado.

## 5. Segurança e infraestrutura

### SSL/TLS e HTTPS
- Certificados e configurações identificáveis.
- Comunicação segura.
- Redirecionamentos HTTPS.
- CORS.
- CSP.
- Cookies seguros.
- Headers de segurança.
- Configurações de servidores e proxies.

Diferenciar configurações presentes no código/repositório daquelas que dependem do ambiente de produção. Não afirmar que um certificado está válido ou que o servidor força HTTPS sem evidência do ambiente.

### Segurança da aplicação
- Autenticação e autorização.
- Gerenciamento de sessões.
- Controle de acesso.
- Validação e sanitização de entradas.
- XSS.
- CSRF.
- Injection.
- Upload de arquivos.
- Exposição de informações sensíveis.
- Gestão de credenciais e variáveis de ambiente.
- Dependências vulneráveis.
- Riscos na integração com serviços externos.

### Infraestrutura
- Servidores.
- APIs.
- Endpoints.
- GitHub Actions.
- CI/CD.
- Build e deploy.
- Logs.
- Monitoramento.
- Configurações de produção e desenvolvimento.

Não inventar certificados, servidores, bancos ou mecanismos de segurança que não estejam comprovados.

## 6. Arquitetura do Game Creator

Investigar:

- Arquitetura geral do sistema.
- Separação de responsabilidades.
- Comunicação entre módulos.
- Contratos de dados.
- Dependências entre editores.
- Gerenciamento de projetos.
- Biblioteca de assets.
- Editor Pixel Art.
- Editor de spritesheets.
- Map Editor.
- Editor 2D e recursos 3D.
- Integração Godot 4.
- Runtime e execução dos jogos.
- Importação e exportação.
- Compatibilidade entre versões.
- Persistência e recuperação de projetos.

Verificar separadamente se módulos funcionam individualmente e quando integrados.

## 7. Engenharia reversa e rastreabilidade

Reconstruir os fluxos:

1. Inicialização da aplicação.
2. Criação e abertura de projetos.
3. Criação e edição de sprites.
4. Criação de mapas.
5. Armazenamento de assets.
6. Comunicação entre ferramentas.
7. Exportação de projetos.
8. Integração com Godot.
9. Execução de jogos.

Apresentar diagramas Mermaid para arquitetura, dependências e fluxos principais.

Para cada problema:
- Arquivo e caminho.
- Linha ou trecho relevante.
- Comportamento observado.
- Causa provável.
- Consequência técnica.
- Gravidade.
- Recomendação de correção.
- Evidência reproduzível ou motivo pelo qual não foi possível reproduzir.

## 8. Qualidade e desempenho

Investigar:
- Complexidade desnecessária.
- Gargalos.
- Consumo de memória.
- Carregamento de assets.
- Desempenho de renderização.
- Escalabilidade.
- Compatibilidade de navegadores.
- Compatibilidade de dispositivos.
- Qualidade dos testes.
- Cobertura efetivamente existente.
- Confiabilidade das rotinas de recuperação.

Executar testes somente quando seguros e compatíveis com as regras do projeto. Registrar comando, ambiente, resultado, logs relevantes e limitações.

## 9. Visão de evolução da franquia Apoena

Avaliar viabilidade técnica futura de:

- Apoena Core.
- Apoena Studio.
- Apoena AI.
- Apoena Social.
- Apoena Marketplace.
- Apoena Publishing.
- Apoena Academy.

Avaliar suporte futuro a:
- Jogos 2D e 3D.
- Web.
- Windows, Linux e macOS.
- Android e iOS.
- Multiplayer.
- APIs e integrações.
- Inteligência artificial.
- Distribuição e monetização.

Diferenciar capacidades atuais comprovadas, possibilidades técnicas e funcionalidades que exigiriam desenvolvimento novo.

## 10. Classificação das descobertas

### Gravidade
- **CRÍTICO:** comprometimento, perda de dados ou falha grave.
- **ALTO:** vulnerabilidade ou falha funcional relevante.
- **MÉDIO:** problema que prejudica confiabilidade ou manutenção.
- **BAIXO:** melhoria localizada.
- **INFORMATIVO:** observação sem falha comprovada.

### Estado da funcionalidade
- IMPLEMENTADA.
- PARCIAL.
- NÃO IMPLEMENTADA.
- TESTADA E VALIDADA.
- NÃO VALIDADA.

Não confundir código existente com funcionalidade comprovadamente operacional. Uma função pode estar implementada e ainda não validada.

## 11. Relatório forense solicitado

Criar documentação em `docs/apoena-forensic/`, respeitando a estrutura existente:

1. `EXECUTIVE_REPORT.md` — resumo executivo.
2. `PROJECT_INVENTORY.md` — inventário completo.
3. `CODE_AUDIT.md` — auditoria de código.
4. `ARCHITECTURE_AUDIT.md` — arquitetura e dependências.
5. `DATABASE_AUDIT.md` — SQL e persistência.
6. `SECURITY_AUDIT.md` — SSL/TLS e segurança.
7. `GAME_ENGINE_AUDIT.md` — editores, sprites, assets e runtime.
8. `PERFORMANCE_AUDIT.md` — desempenho e escalabilidade.
9. `TESTING_AUDIT.md` — testes e validação.
10. `TECHNICAL_DEBT.md` — dívida técnica.
11. `RISK_REGISTER.md` — riscos classificados.
12. `RECOMMENDED_ROADMAP.md` — plano de evolução.
13. `EVIDENCE_INDEX.md` — índice de evidências e arquivos examinados.

Não criar novamente documentos que já existam com conteúdo equivalente sem antes verificar sua finalidade e atualizar somente quando houver evidência nova. Se o protocolo do repositório determinar outra localização ou convenção, registrar o conflito e pedir decisão, sem sobrescrever silenciosamente.

## 12. Conclusão e recomendações

Ao terminar, apresentar:

- Estado real do Apoena.
- Principais pontos fortes.
- Problemas críticos.
- Vulnerabilidades comprovadas.
- Funcionalidades incompletas.
- Componentes que devem ser preservados.
- Componentes que precisam de correção.
- Melhorias arquiteturais necessárias.
- Dez próximas ações priorizadas.

Para cada ação, indicar esforço estimado, dependências, risco e critério de conclusão.

## 13. Restrições finais

Esta é uma auditoria, não uma implementação.

- Não reescrever o sistema.
- Não refatorar código.
- Não remover arquivos.
- Não alterar banco de dados.
- Não modificar configurações.
- Não fazer commits.
- Não ocultar problemas.
- Não apresentar suposições como fatos.

Todo achado importante deve possuir evidência rastreável.

O relatório deve ser tecnicamente rigoroso, mas sua conclusão executiva deve ser compreensível para o proprietário do projeto, que é iniciante em programação.

**Resultado esperado:** conhecer profundamente o Apoena Game Creator, identificar sua condição técnica real e estabelecer uma base confiável para as próximas decisões de engenharia.

---

## 14. Recomendação consultiva registrada após o prompt

O assistente recomendou concluir a auditoria antes de implementar melhorias e destacou três perguntas centrais:

1. O que realmente funciona?
2. O que existe no código, mas ainda não funciona corretamente?
3. O que falta para transformar o Apoena em uma plataforma profissional de criação de jogos?

Também recomendou controles adicionais:
- Identificação de duplicados por hash SHA-256, comparação de conteúdo e referências de uso.
- Mapa de dependências de entrada e saída de cada módulo.
- Auditoria de schemas, migrações e compatibilidade de projetos antigos.
- Avaliação contextual de segurança: por exemplo, encontrar `innerHTML` não comprova XSS sem analisar origem, sanitização e contexto dos dados.
- Separação explícita entre código encontrado, teste executado e comportamento comprovado.

### Limitações de evidência destacadas
A inspeção do repositório pode identificar configurações SSL/TLS, mas não comprova sozinha a configuração efetiva do servidor de produção. O mesmo vale para segurança, testes e desempenho quando dependem de ambientes externos.

### Sequência de trabalho recomendada
1. Preservação e registro do commit-base.
2. Inventário de arquivos e dependências.
3. Engenharia reversa de arquitetura, contratos e fluxos.
4. Auditoria de segurança e dados.
5. Validação segura e rastreável.
6. Produção dos relatórios.
7. Decisão de engenharia sobre preservação, correção, consolidação ou eventual remoção.

---

## 15. Estado e proveniência

- O prompt foi fornecido pelo proprietário em 2026-11-02 10:43:40 UTC.
- O pedido para acrescentar as informações ao backup foi feito em 2026-11-02 10:44:51 UTC.
- Este arquivo é um protocolo documental.
- A auditoria forense ainda não foi executada por este registro.
- Nenhum código do Game Creator foi alterado.
- Nenhum achado de vulnerabilidade é declarado neste documento.
- A execução futura deve respeitar `AGENTS.md`, instruções do repositório, WIP = 1 e restrições de CI/CD.
