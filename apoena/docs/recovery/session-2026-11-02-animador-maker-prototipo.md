# Complemento de recuperação — Animador Maker Apoena e protótipo visual

**Data do registro:** 2026-11-02; hora não disponível no contexto desta execução.  
**Repositório consultado:** `apoenalore/apoenaskil`, branch `main`, commit-base `cc1a1bf10be52d2479abc8eca8674138914ffafa`.  
**Estado da recuperação:** **PARCIAL**.  
**Tipo:** complemento derivado do contexto visível desta conversa; não é transcrição literal integral nem implementação do GameCreator.

## 1. Fonte e cobertura

Fonte disponível: conversa atual do ChatGPT sobre a criação de um animador de personagens para o Apoena Game Creator, somada ao resumo de contexto anterior que aponta para o registro `session-2026-11-02-gamecreator-personagens-e-interface.md`.

Mensagens explicitamente visíveis nesta etapa:

1. O autor enviou o artigo [A brand new way to create 3D rotations for pixel art](https://smackstudio.com/a-brand-new-way-to-create-3d-rotations-for-pixel-art/).
2. O autor enviou a página [Characters — Smack Studio](https://smackstudio.com/characters/).
3. O autor declarou: **“sim chamaremos isso de animador de personagens maker apoena ele sera um outro tipo de editor de personagens pois vai animar monstros e humanoides”**.
4. O autor pediu: **“pode montar um prototipo para eu ver?”**.
5. O autor pediu o backup desta conversa.

**Limite:** a conversa está disponível por contexto atual, com parte do histórico anterior representada por resumo e registros pré-existentes. Não foi fornecida uma exportação integral independente do histórico. A lista anterior das 500 possibilidades está preservada/referenciada no registro anterior e não foi reconstruída item a item nesta etapa. Portanto, não declarar cobertura integral.

## 2. Decisão explícita do autor

- O nome aprovado para a ferramenta é **Animador de Personagens Maker Apoena**.
- Ela será **outro tipo de editor de personagens**, separado conceitualmente do gerador.
- O escopo expresso inclui animar **monstros e humanoides**.

Classificação: **DECISÃO DO AUTOR** no escopo do conceito/nome. Isso não confirma implementação, integração ou arquitetura técnica.

## 3. Referência Smack Studio

As duas páginas fornecidas pelo autor foram abertas nesta conversa. O artigo descreve sprites de partes do corpo associados a ossos de um rig e a geração de poses ao movimentar o esqueleto; a página de personagens apresenta a combinação de animação gerada pelo movimento com edição quadro a quadro, importação e exportação.

- [Artigo sobre rotações 3D para pixel art](https://smackstudio.com/a-brand-new-way-to-create-3d-rotations-for-pixel-art/)
- [Página de personagens](https://smackstudio.com/characters/)

A referência serve para orientar o fluxo de uso. O desenvolvimento do Apoena deve ter implementação e assets próprios; não se afirma acesso ao código interno do Smack Studio nem se propõe copiar mecanismos proprietários.

## 4. Protótipo visual criado nesta conversa

Foi criado o arquivo HTML independente **animador-personagens-maker-apoena.html**, salvo na Biblioteca do ChatGPT:

- ID da Biblioteca: `libfile_1c7b485691548191b023c25d4bfebc7e`.
- Link: [Abrir o protótipo visual](https://chatgpt.com/library?file_id=libfile_1c7b485691548191b023c25d4bfebc7e&account_id=personal).
- Caminho local de trabalho desta execução: `/workspace/scratch/414dcde0dd82/animador-personagens-maker-apoena.html`.

A tela demonstra uma direção de interface com palco central, painel de partes, painel de configuração e timeline. Inclui controles demonstrativos para alternar humanoide/monstro, exibir/ocultar ossos, grade e onion skin, ajustar ângulo/profundidade/zoom, selecionar/adicionar quadros e baixar metadados JSON.

**Limites funcionais do protótipo:** os ossos e a timeline são elementos de demonstração visual; ainda não existe rigging real, deformação pixel a pixel, animação exportável nem integração com a biblioteca central/Game Creator. O botão de spritesheet apenas apresenta uma mensagem; não gera spritesheet PNG. O JSON baixado contém configuração demonstrativa, não um projeto de personagem pronto para o runtime.

Classificação: **PROTÓTIPO VISUAL — NÃO INTEGRADO**.

## 5. Separação entre decisão e proposta

### Decisão do autor

- Nome da ferramenta.
- Existência como outro editor.
- Abrangência de personagens humanoides e monstros.

### Propostas técnicas derivadas da conversa

As ideias abaixo são propostas para discussão e não devem ser tratadas como requisitos aprovados além do escopo acima:

- Criar rigs predefinidos para humanoides, quadrúpedes e criaturas aladas, além de permitir rigs personalizados.
- Vincular camadas/partes a ossos e pivôs ajustáveis.
- Combinar rigging com correções manuais quadro a quadro.
- Construir gradualmente vistas direcionais e rotação 2.5D.
- Fazer integração de ida e volta com o Gerador de Personagens Pixel e a biblioteca do Game Creator.
- Validar exportação e uso no runtime separadamente.

O registro anterior `session-2026-11-02-gamecreator-personagens-e-interface.md` contém o inventário maior de possibilidades, os requisitos de malha/limpeza do spritesheet, a sequência incremental proposta e o histórico técnico GC-CHAR-001/PR #13. O estado da PR e do código mencionado lá continua **não revalidado** neste complemento.

## 6. Alterações e validação

- Criado este complemento de recuperação; o registro anterior foi preservado sem sobrescrita.
- Nenhum código do GameCreator ou Apoena Pixel Art HTML foi alterado.
- Nenhuma PR de código foi criada ou modificada.
- O protótipo HTML permanece como artefato da Biblioteca; não foi copiado como arquivo binário para este repositório.
- Validação executada nesta operação: conferência das instruções do repositório, do registro anterior e dos caminhos/IDs usados. Não foram executados testes de build, browser ou Godot.

## 7. Pendências

1. Obter exportação integral da conversa original caso seja necessário comprovar todas as mensagens e recuperar integralmente a lista de 500 itens.
2. Debater os fluxos e ferramentas técnicas antes de transformar as propostas em requisitos fechados.
3. Inspecionar o GameCreator, a branch/PR atual e seus módulos antes de planejar implementação.
4. Testar a interface/protótipo em navegador e evoluir as interações somente após escolha explícita de direção.
5. Definir o formato de projeto, persistência compartilhada e exportação para o runtime; ainda não definidos nem validados.

**Resultado: PARCIAL.** O nome, o escopo humanoides/monstros, as páginas de referência, o artefato produzido e seus limites estão registrados. O histórico integral da conversa de origem não foi reextraído.
