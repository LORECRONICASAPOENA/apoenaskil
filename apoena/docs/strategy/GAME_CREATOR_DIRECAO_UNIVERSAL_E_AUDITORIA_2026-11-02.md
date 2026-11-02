# Apoena Game Creator — Direção universal e auditoria de evolução
**Data do evento de origem:** 2026-11-02.  
**Hora do evento de origem:** Hora não disponível na fonte.  
**Data/hora do registro desta atualização:** 2026-11-02T10:59:32Z.  
**Origem:** mensagem do proprietário e resposta consultiva nesta conversa.  
**Estado:** registro documental; recomendação arquitetural ainda depende de aprovação explícita do proprietário.

## 1. Contexto apresentado pelo proprietário

O proprietário reapresentou um diagnóstico técnico do pacote `GameCreator-main (1).zip` e um prompt de auditoria para o Codex. O texto informa que o pacote contém:

- Versões Apoena Game Creator 3.9.2 e 4.0.
- Bancada integrada V4.0.
- Documentação de auditoria e recuperação de código.
- Plano geral do Apoena.
- Arquivos JavaScript divididos em módulos.
- Workflows de publicação e integração com GitHub.

O texto também relata que o README identifica o projeto como Apoena Game Creator V4.1 em desenvolvimento, preservando V4.0 e incorporando ferramentas especializadas.

### Componentes relatados no pacote

| Componente | Situação descrita na mensagem |
|---|---|
| Creator principal | Base V4.0 preservada |
| Editor Pixel Art | Implementado |
| Editor de spritesheets | Implementado |
| Biblioteca central | Implementada com IndexedDB |
| Editor de mapas 2.5D | Implementado |
| Tilesets e terrenos | Implementação existente |
| Integração Godot 4 | Catálogo e runtime de referência |
| Inventário e receitas | Implementação existente |
| Creator Bridge | Ponte entre ferramentas implementada |
| Testes automatizados | Seis arquivos principais de testes |
| CI/CD | Workflows GitHub Actions existentes |

**Nota de evidência:** essas são classificações reportadas pelo proprietário/texto de diagnóstico. Não equivalem a validação independente de funcionamento.

## 2. Arquitetura descrita

- Aplicação principal Game Creator.
- Pixel Art Studio para sprites e animações.
- Map Editor para mapas e tilesets.
- Biblioteca para assets e projetos.
- Creator Bridge e Asset Library para compartilhamento e persistência.
- Integração Godot 4 com catálogo e runtime de referência.

O texto diferencia corretamente editor/ferramenta de autoria e motor de execução. A existência de exportação de dados não comprova, por si só, gameplay completo, física, animações, interações ou publicação multiplataforma.

## 3. Quatro questões técnicas levantadas

1. **Editor versus engine:** o Creator contém ferramentas de autoria e integração com Godot, mas isso não prova que possua um motor universal próprio.
2. **Integração de dados versus gameplay:** exportar personagens, mapas e itens não prova que animações, interações, física e mecânicas funcionem no jogo exportado.
3. **Multiplataforma:** há ferramentas Web e integração Godot, mas não há evidência suficiente, no texto fornecido, de publicação completa para Windows, macOS, Linux, Android e iOS.
4. **Documentação existente:** protocolos para evitar duplicação, preservar projetos antigos e controlar execuções do GitHub Actions devem ser lidos e respeitados.

## 4. Prompt de auditoria proposto pelo proprietário

Além de toda a leitura obrigatória definida pelos arquivos `AGENTS.md` aplicáveis e pelo `README.md` do repositório, o proprietário destacou os seis documentos abaixo como leitura adicional específica para esta auditoria. Eles não substituem os protocolos, modos de preservação, legenda de fonte/status, documentos de recuperação de conhecimento e contradições, nem a Skill pertinente exigidos pelas instruções do repositório.

Leitura adicional indicada pelo proprietário:
- `AGENTS.md` e demais instruções aplicáveis ao caminho de trabalho (a leitura permanece obrigatória, conforme a hierarquia do repositório).
- `README.md` e mapas/índices pertinentes.
- `docs/ATUALIZACOES_PENDENTES_LEIA_ANTES_DE_COMECAR.md`
- `docs/PENDENCIAS_ABERTAS_E_LIMPEZA_GITHUB.md`
- `PLANO_GERAL_APOENA.md`
- `ORGANIZACAO_EDITOR.md`

A leitura mandatória do repositório também inclui, conforme `AGENTS.md`: `apoena/docs/MODOS_DE_TRABALHO_E_PRESERVACAO.md`, `apoena/docs/PROTOCOLO_UNIVERSAL_DE_EXTRACAO_E_TRANSFERENCIA.md` quando aplicável, `apoena/docs/source-and-status-legend.md`, `apoena/docs/knowledge-recovery-2026-10-30.md`, `apoena/docs/knowledge-gaps-and-contradictions.md`, referências e índices pertinentes, além da Skill temática aplicável. Se qualquer item não estiver disponível, registrar a limitação; não presumir leitura.

Protocolos: WIP = 1, preservação de código e execução sequencial do CI.

### Objetivo da auditoria

Avaliar a distância entre a implementação atual e a visão de longo prazo:
- Game Creator profissional.
- Ferramentas 2D e 3D.
- Apoena AI.
- Criação assistida por linguagem natural.
- Exportação e publicação multiplataforma.
- Comunidade e compartilhamento.
- Marketplace de recursos.
- Ecossistema de produtos Apoena.

### Escopo de investigação solicitado

1. Estado real de cada módulo.
2. Classificação IMPLEMENTADO, PARCIAL, PENDENTE e VALIDADO.
3. Contratos de dados entre Creator, biblioteca, Pixel Art, Map Editor e Godot.
4. Duplicações e consolidação.
5. Persistência, compatibilidade com projetos antigos e segurança.
6. Limitações 2D, 3D e publicação multiplataforma.
7. Integração de IA sem comprometer a arquitetura.
8. Riscos de desempenho e escalabilidade.

A documentação não deve ser tratada como prova de funcionamento: confirmar no código e nos testes.

### Planejamento solicitado

Prioridades propostas pelo proprietário:
1. Estabilidade e integridade dos projetos.
2. Consolidação das ferramentas existentes.
3. Fluxo completo de autoria, exportação e execução.
4. Evolução dos recursos 2D e 3D.
5. Integração de IA.
6. Publicação multiplataforma.
7. Comunidade e marketplace.

Entregáveis: análise executiva e técnica, estado atual, funcionalidades comprovadas, lacunas prioritárias, arquitetura recomendada, roadmap revisado e cinco próximas tarefas prioritárias.

Restrições:
- Não implementar funcionalidades nessa auditoria.
- Não reescrever o Creator.
- Não criar módulos ou sistemas duplicados.
- Não remover funcionalidades existentes.
- Não alterar contratos de dados sem necessidade demonstrada.
- Não enfraquecer testes.
- Não iniciar workflows redundantes.
- Não validar funcionalidades sem evidência de execução.
- Atualizar documentos apenas com novas evidências ou decisões aprovadas.

## 5. Separação estratégica entre produto e franquia

O texto do proprietário coloca uma questão estratégica: manter o Game Creator como produto principal para que terceiros criem seus próprios jogos, e a franquia Apoena como universo de produtos, jogos, ferramentas, serviços e comunidade.

A recomendação consultiva apresentada foi manter os dois objetivos e separá-los claramente:
- **Game Creator:** produto/plataforma de autoria para terceiros.
- **Apoena:** franquia, universo e ecossistema de produtos próprios.

## 6. Recomendação arquitetural apresentada pela IA — NÃO APROVADA AINDA

Foi recomendada uma arquitetura universal desde o início, com desenvolvimento progressivo por gêneros:

- Núcleo comum e extensível.
- Sistemas compartilhados: física, animação, áudio, IA, inventário, mapas, eventos, salvamento e exportação.
- Primeiro foco de validação: RPG, aventura e exploração.
- Expansão posterior: plataforma, estratégia, simulação, MOBA e demais gêneros.

A justificativa é evitar que a arquitetura fique limitada a RPG e exija reconstrução posterior. O foco inicial em RPG/aventura/exploração foi proposto por serem gêneros capazes de exercitar personagens, mapas, animações, inventários e interações.

MOBA foi recomendado para fase posterior, após maturidade de rede, sincronização e servidores.

### Separação de responsabilidades proposta

1. Game Creator: ferramenta de criação.
2. Godot: motor responsável pela execução dos jogos.
3. Apoena: franquia, universo, produtos e experiências próprias.

### Registro de aprovação

O assistente perguntou se o proprietário aprova a direção “arquitetura universal desde o início, começando o desenvolvimento pelos gêneros RPG, aventura e exploração”. No momento deste registro, **não há resposta de aprovação**. Portanto:
- Arquitetura universal: recomendação pendente de aprovação formal.
- Primeiro foco RPG/aventura/exploração: recomendação pendente de aprovação formal.
- Godot: engine previamente indicada pelo proprietário em mensagem anterior; versão e estratégia de integração continuam a definir.

## 7. Salvaguarda para limpeza e modularização

Foi recomendada uma classificação de arquivos antes de qualquer exclusão:
- Essencial.
- Utilizado.
- Duplicado comprovado.
- Obsoleto comprovado.
- Experimental.
- Desconhecido — preservar até investigar.

Não excluir por antiguidade, tamanho ou aparência de duplicação. Confirmar referências, funcionalidades exclusivas, dependências e uso real.

## 8. Próximos passos documentais e técnicos

1. Executar auditoria somente leitura conforme o prompt do proprietário.
2. Ler os seis documentos obrigatórios e respeitar AGENTS/protocolos.
3. Gerar mapa de dependências e contratos.
4. Confirmar a fonte oficial e o estado real de cada módulo.
5. Comprovar persistência e compatibilidade com projetos antigos.
6. Demonstrar fluxo real de autoria → exportação → execução Godot.
7. Documentar lacunas de publicação por plataforma.
8. Submeter a direção universal e a priorização de gêneros à aprovação do proprietário.

## 9. Controle de proveniência

Este documento registra a mensagem do proprietário de 2026-11-02 e a recomendação consultiva que se seguiu. Não é uma auditoria independente do ZIP ou do repositório. Não houve nesta tarefa leitura dos arquivos do Creator, execução de testes, alteração de código ou confirmação de funcionamento. Nenhuma decisão pendente foi convertida em decisão aprovada.
