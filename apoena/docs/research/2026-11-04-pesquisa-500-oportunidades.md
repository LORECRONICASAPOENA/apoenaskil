# Pesquisa de oportunidades para o jogo Apoena — 2026-11-04

Pedido do autor: pesquisar 500 formas de evoluir o jogo e salvar backup.

## Escopo pesquisado
GameCreator, Apoena Pixel Art HTML/Godot 4 e JOGO-APOENA-AGAR- Godot 4.

## 20 frentes do catálogo de 500 oportunidades
25 oportunidades por frente (500 no total): arquitetura modular; personagens e habilidades; controles; sprites e animações; combate e colisões; IA; mapas e exploração; Floresta Viva/ecologia; progressão/economia; interface; áudio; desempenho; saves; coop/rede; segurança; testes; GameCreator/exportação; build/distribuição; runners/observabilidade; design/tutorial/retenção.

## Recomendações priorizadas
1. Fechar a validação do GameCreator/PR #14, confirmar CI no SHA corrigido e preservar backup.
2. Criar contrato declarativo de heróis/habilidades, mantendo Aurium (AUR), cooldowns, custos, alcance, hitboxes e efeitos separados da UI.
3. Adaptar os poderes do AGAR 3D ao Pixel Art 2D/2.5D; não copiar cenas/scripts 3D diretamente.
4. Padronizar spritesheets em 4 colunas × 6 linhas (4×6), 24 quadros, com metadados de direção/animação; definir resolução por quadro no pipeline.
5. Manter paridade HTML/Godot e validar Android em aparelho real antes de declarar APK pronto.
6. Adotar testes unitários, integração, regressão de saves, smoke tests por modo, profiling e orçamento de memória.
7. Coordenar runners por labels e workspace isolado; respeitar WIP=1 entre GameCreator e Pixel Art.

## Fontes técnicas consultadas
- Godot Android export: https://docs.godotengine.org/en/stable/tutorials/export/exporting_for_android.html
- Android Developers Godot export: https://developer.android.com/games/engines/godot/godot-export
- Godot profiling: https://contributing.godotengine.org/en/latest/development/engine/optimization.html
- Godot input lag: https://docs.godotengine.org/en/latest/tutorials/rendering/jitter_stutter.html
- MDN Canvas animation: https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Basic_animations
- MDN JavaScript performance: https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Performance/JavaScript
- MDN web technologies for games: https://mdn.github.io/web-tech-games/index.html

## Proveniência
Foram consultados os documentos recuperados de game design e parâmetros de gameplay, a skill de gameplay, os READMEs atuais do Pixel Art e AGAR e AGENTS.md do GameCreator. As 500 oportunidades são backlog para investigação, não funcionalidades implementadas nem 500 defeitos confirmados. Nenhum código, build ou teste de gameplay foi alterado/executado nesta pesquisa.
