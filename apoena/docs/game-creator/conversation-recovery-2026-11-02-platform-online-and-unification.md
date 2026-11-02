# Registro de continuidade — Game Creator e plataforma unificada Apoena

**Data do registro:** 2026-11-02  
**Fonte:** histórico visível desta conversa no projeto compartilhado historiaegeografia e inspeções documentais do repositório apoenalore/GameCreator realizadas durante a sessão.  
**Tipo:** recuperação conversacional e decisões técnicas; não é transcrição integral de todas as conversas anteriores.  
**Cobertura:** PARCIAL. Preserva o conteúdo disponível neste contexto; não declara acesso a históricos privados externos que não foram apresentados.

## 1. Escopo e separação dos repositórios

- **GameCreator** (apoenalore/GameCreator): código da ferramenta de autoria.
- **Apoena Skill** (apoenalore/apoenaskil): conhecimento, documentação e Skills reutilizáveis.
- **JOGO-APOENA-AGAR-**: runtime/jogo consumidor, distinto do editor.
- O pedido atual foi explicitamente fazer backup no repositório Skill. Este documento registra a continuidade técnica do Game Creator na base de conhecimento, sem copiar o código-fonte do editor para este repositório.

## 2. Histórico recuperado em ordem cronológica

### 2026-11-02 — 00:08 a 00:48 UTC

1. O autor reafirmou a regra de registrar novidades e informações detalhadas do Game Creator no GitHub a cada conversa.
2. Pediu que cada erro de Actions gere relatório com causa, solução adotada e justificativa, sem repetição cega.
3. Esclareceu que iniciador CMD/HTML que apenas redirecionasse para uma página não deveria permanecer se não configurasse nem executasse nada; componente sem função útil só atrapalha o Runner.
4. Solicitou pesquisa para tornar os projetos mais seguros contra invasores, hackers e modders, antecipando uma futura oportunidade comunitária para criação de itens cosméticos/equipamentos com opções limitadas.
5. Pediu pesquisa de segurança de jogos como GTA/Free Fire, vetores de ataque, vulnerabilidades, SQL e SSL.
6. Foi produzido registro técnico sobre anti-cheat, ataques multiplayer, SQL Injection, consultas parametrizadas, TLS moderno, segurança de APIs e defesa em camadas. A documentação de GTA Online/BattlEye não prova arquitetura de GTA 6.
7. O autor esclareceu que a preocupação principal inclui integridade do mundo, economia e experiência do jogador, não apenas anti-cheat. LoL foi citado como exemplo de sistemas de penalidade/decaimento por inatividade.
8. A análise distinguiu ausência casual, AFK durante partida, abandono de fila, decaimento de ranque competitivo e comportamento abusivo. Recomendação registrada: não punir ausência diária casual; decaimento somente se aplicável a ranques de topo, com aviso/tolerância; preservar progresso e economia legítimos; penalidades proporcionais e recurso.
9. O autor perguntou o que é necessário para tornar o jogo online. Foi proposta arquitetura com cliente, API/backend, servidores autoritativos, persistência, segurança, observabilidade e etapas de protótipo.
10. O autor escolheu explicitamente: mundo **híbrido**, teste inicial de **20 a 50 jogadores simultâneos**, plataformas **Android e PC**.
11. A arquitetura proposta prevê regiões compartilhadas, dungeons/arenas instanciadas, servidor autoritativo, API HTTPS, PostgreSQL como candidato, Redis opcional e armazenamento/CDN. A meta de 20–50 é capacidade a testar, não garantia de produção.
12. O autor solicitou auditoria do volume de arquivos e duplicações do Game Creator, especialmente versões antigas e iniciadores. A árvore main foi inspecionada e foi produzido inventário documental.
13. A auditoria apontou divergências entre README e integracao/README sobre V3.9/V4.0/V4.1; múltiplos HTMLs grandes; bundle V4; scripts PowerShell/Python; dois workflows com funções distintas; iniciadores e utilitários de publicação. Não foi possível provar duplicação funcional dos HTMLs grandes pela inspeção textual disponível.
14. Regra de limpeza: não apagar por nome, tamanho ou idade. Rastrear referências, identificar substituto, migrar conteúdo exclusivo, testar e registrar evidência antes de remoção.
15. Foi criada branch de manutenção no GameCreator e PR draft #12 para revisão documental. Nenhum arquivo funcional foi removido; a main permaneceu intacta no estado observado.

### 2026-11-02 — 01:50 a 02:01 UTC

16. O autor autorizou iniciar a auditoria de organização.
17. A inspeção confirmou que ABRIR_GAME_CREATOR.cmd chama o build PowerShell e abre index.html; não é somente redirecionador.
18. legacy/iniciador-anterior.html contém catálogo de poções editável/exportável e links para outras ferramentas; não é somente redirecionador.
19. PUBLICAR_NO_GITHUB.cmd/.ps1 realiza sincronização/cópia e commit/push; precisa revisão de segurança e uso.
20. pixel-art.yml funciona como CI/validação abrangente; publicar-creator-unificado.yml executa publicação do index.html, com permissão de escrita. As funções diferem, embora haja build repetido.
21. Os builds PowerShell e Python têm lógica semelhante, mas paridade não foi comprovada.
22. Conclusão: não remover workflows, scripts, iniciadores, bundle ou fontes sem provar redundância e preservar conteúdo/funções exclusivas.
23. O autor propôs unificar o editor 3D e o Pixel Art porque ambos servem ao mesmo jogo, tornando-os uma plataforma única, e solicitou também editor de mapas 2.5D para uso de assets Pixel Art 2D.
24. Decisão arquitetural registrada: uma plataforma única Apoena Game Creator com Estúdio 3D, Estúdio Pixel Art 2D, Editor de mapas 2.5D, biblioteca central e exportação integrada.
25. O inventário apontou que o repositório já contém map-editor/, pixel-art/, shared/asset-library.js, biblioteca/, bundle-v4/ e fonte V4.0 com bancada 3D. A recomendação é integrar e evoluir o editor 2.5D existente e preservar a bancada 3D após mapear dependências.
26. O contrato proposto usa IDs estáveis e referências à biblioteca compartilhada. Assets 2D e 3D mantêm formatos/variantes próprios; não converter automaticamente um no outro. Mapas referenciam assets por ID, guardando posição, camada, elevação, orientação, escala, profundidade e metadados.
27. Foi criada documentação de arquitetura unificada e atualizada a lista de pendências na branch de manutenção, dentro da PR #12 draft. Nenhum código funcional foi alterado nessa etapa.

### 2026-11-02 — 02:01 a 08:14 UTC

28. O autor reiterou em vários momentos o pedido de backup no GitHub a cada conversa, com registro de novidades e detalhes.
29. Registros anteriores no GameCreator informaram commits/checkpoints em PR #12, incluindo hashes mencionados como e86895c, c081cd8 e outros. Esses hashes são preservados como referências históricas declaradas nas respostas anteriores; não foram todos revalidados nesta execução.
30. Às 08:14, o autor pediu especificamente: “Faça o backup no skil pfvr”, direcionando a atualização para este repositório de Skills.

## 3. Decisões explícitas do autor

- Registrar continuamente conversas, novidades e informações detalhadas no GitHub.
- Relatar erros de Actions com causa, solução e justificativa, sem repetir tentativa cegamente.
- Remover iniciadores comprovadamente inúteis que atrapalhem o Runner.
- Proteger o projeto contra hackers/modders e preservar a segurança da comunidade.
- Considerar economia, integridade do mundo e experiência do jogador, não apenas anti-cheat.
- Mundo online híbrido.
- Meta inicial de teste: 20–50 jogadores simultâneos.
- Plataformas: Android e PC.
- Unificar editor 3D e Pixel Art 2D em uma plataforma única para o mesmo jogo.
- Incluir editor de mapas 2.5D.
- Usar assets Pixel Art 2D no pipeline de criação de mapas.

## 4. Propostas técnicas ainda não aprovadas como implementação

- Godot Dedicated Server/headless como opção, condicionado à confirmação do runtime final.
- Nakama versus backend próprio.
- PostgreSQL como candidato e Redis opcional.
- Arquitetura por região compartilhada e instâncias.
- Política detalhada de AFK/abandono/decaimento e compensação.
- Navegação única e contrato de asset com schema versionado.
- Reorganização de diretórios e remoção de caminhos órfãos.

Nenhuma proposta acima deve ser descrita como código já implementado.

## 5. Arquitetura de plataforma única — estado consolidado

Áreas:
1. **Estúdio 3D:** modelos, personagens, materiais, texturas, rig/ossos, animações, pré-visualização e exportação.
2. **Estúdio Pixel Art 2D:** personagens, spritesheets, quadros, camadas, animações, objetos, vegetação, animais e equipamentos.
3. **Editor 2.5D:** terrenos, tilesets, grade/camadas, elevação, objetos 2D/3D, colisões declarativas, marcadores, biomas, caminhos, cavernas e exportação.

A biblioteca existente é a base a consolidar; não criar três bibliotecas isoladas. Cada asset deve ter ID estável, tipo, versão de schema, referências aos arquivos originais, dimensões, pivô/âncora, escala, tags, formato e variantes.

Regra de preservação: não apagar fontes históricas, bundle, scripts, iniciadores ou módulos antes de rastrear referências, confirmar que o fluxo não depende deles, migrar conteúdo exclusivo, identificar substituto e executar testes de regressão.

## 6. Arquitetura online — estado consolidado

- Mundo híbrido: regiões compartilhadas + instâncias de dungeons/arenas.
- Android e PC no mesmo ecossistema.
- Teste inicial de 20–50 jogadores simultâneos.
- Servidor autoritativo; cliente envia intenção, servidor valida posição, combate, inventário, economia e resultados.
- API HTTPS/TLS para autenticação e operações não realtime.
- Transporte realtime seguro compatível com engine; não presumir que HTTPS protege automaticamente pacotes UDP.
- Persistência central e trilha de auditoria.
- Capacidade real depende de teste de carga, tick rate, latência, densidade de entidades, CPU/RAM e tráfego.

## 7. Segurança, economia e experiência

- SQL parametrizado, privilégio mínimo, transações e ledger para economia.
- TLS moderno, validação de certificados, gestão de segredos e controle de APIs.
- Anti-cheat em camadas, com validação autoritativa no servidor.
- Não confiar em dados do cliente para dano, moeda, item, posição final ou recompensa.
- Distinguir ausência casual, AFK durante partida, abandono de fila, decaimento competitivo e comportamento abusivo.
- Não punir login ausente em modos casuais; preservar personagem e riqueza legítimos.
- Em modos competitivos, considerar penalidades proporcionais, avisos, tolerância, reconexão, recurso e compensação quando houver abandono confirmado.
- Conteúdo comunitário deve ser limitado, validado, moderado e não receber capacidade de executar código arbitrário nem alterar atributos competitivos fora das regras.

## 8. Auditoria e limpeza do repositório GameCreator

Achados documentais:
- divergência entre README e integracao/README sobre fonte V3.9/V4.0/V4.1;
- HTMLs grandes e bundle ainda sem comparação binária/funcional conclusiva;
- CI e workflow de publicação têm finalidades diferentes;
- build PowerShell/Python sem prova de paridade;
- iniciador legado contém conteúdo funcional de catálogo;
- launcher CMD tem função local de build/abertura;
- scripts de publicação exigem revisão antes do uso.

Estado: auditoria documental parcial; nenhum arquivo funcional foi excluído durante as etapas descritas. Comparação de HTMLs grandes exige clone/ambiente de trabalho e hashes/diffs reproduzíveis.

## 9. Documentos relacionados no repositório de código

- GameCreator: https://github.com/apoenalore/GameCreator
- PR #12 (auditoria/organização documental, draft no último estado registrado): https://github.com/apoenalore/GameCreator/pull/12
- Plano online: https://github.com/apoenalore/GameCreator/blob/main/docs/PLANO_JOGO_ONLINE_APOENA.md
- Arquitetura de plataforma única: https://github.com/apoenalore/GameCreator/blob/main/docs/ARQUITETURA_PLATAFORMA_UNICA_APOENA.md
- Auditoria de organização: https://github.com/apoenalore/GameCreator/blob/main/docs/AUDITORIA_ORGANIZACAO_E_LIMPEZA_2026-11-02.md

Os links para main podem não conter alterações que estejam apenas na branch/PR; consultar a PR e o commit antes de assumir merge.

## 10. Limites e lacunas

- Este registro não é transcrição literal da conversa completa; preserva o histórico disponível no contexto e resumos de checkpoints anteriores.
- As mensagens de backup repetidas entre 02:01 e 08:14 não trouxeram novas decisões técnicas, apenas reiteraram a política de backup; foram agrupadas sem apagar o fato da repetição.
- Não houve auditoria direta do HEAD atual do GameCreator nesta atualização do Skill.
- Não foi executado código, teste de runtime, teste de carga, pentest ou validação Android/PC.
- Não houve alteração nem exclusão de arquivos no repositório GameCreator nesta operação.
- Assets locais, dados IndexedDB e projetos armazenados no navegador não são incluídos automaticamente no GitHub.

## 11. Próxima sequência registrada

1. No GameCreator, concluir inventário de navegação/rotas/dependências e confirmar estado da PR #12.
2. Identificar bancada 3D real e módulos ativos do Pixel Art.
3. Mapear editor 2.5D existente e biblioteca compartilhada.
4. Definir entrada e navegação únicas sem duplicar módulos.
5. Unificar contratos de asset e projeto com migração/backup.
6. Integrar assets 2D/3D ao mapa por ID.
7. Remover apenas rotas vazias e duplicações comprovadas, com testes.
8. Em tarefa separada, iniciar protótipo online com dois clientes e servidor dedicado.

**Princípio de continuidade:** uma tarefa ativa por vez (WIP = 1), preservação antes de limpeza, e distinção entre decisão do autor, proposta, implementação e validação.
