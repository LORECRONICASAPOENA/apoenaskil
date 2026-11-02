# Desenvolvimento técnico — Apoena Game Creator

## Direção de produto
Ecossistema multiplataforma de criação de jogos, orientado a iniciantes, com visão ampla de jogos e ferramentas 2D/3D. Godot foi indicada pelo proprietário como engine principal.

## Arquitetura proposta pela IA — não aprovada formalmente
1. Experience: interface, editor, painéis e assistente.
2. Application: projetos, cenas, assets, usuários e publicação.
3. Core: contratos, eventos, extensões, persistência e permissões.
4. Infrastructure: engine/runtime, banco, cloud e exportação.

A IA recomendou modularidade interna e contratos explícitos, evitando microsserviços sem necessidade comprovada.

## Módulos sugeridos
Apoena Core; Project Manager; Game Editor; Scene System; Runtime Engine; Asset Manager; Visual Scripting; Apoena AI Assistant; Export System; Plugin System; Apoena Cloud; Apoena Marketplace.

Prioridades sugeridas: P0 fundação, projetos, cenas e runtime; P1 assets, assistente, scripting visual e exportação; P2 plugins e cloud; P3 marketplace. Sequência depende do diagnóstico real.

## Tecnologias e caminhos reportados no inventário do ZIP
HTML, CSS, JavaScript; IndexedDB; bundle-v4 com 24 partes; testes Node.js, integração e GDScript; scripts Python e PowerShell; GitHub Actions; integração inicial Godot 4/GDScript.

Caminhos citados: PLANO_GERAL_APOENA.md; AUDITORIA_CODIGO_EXISTENTE.md; docs/AUDITORIA_TECNICA_ESTRATEGICA_2026-10-30.md; docs/AUDITORIA_ORGANIZACAO_E_LIMPEZA_2026-11-02.md; docs/ATUALIZACOES_PENDENTES_LEIA_ANTES_DE_COMECAR.md; docs/PLANO_JOGO_ONLINE_APOENA.md; docs/SEGURANCA_APOENA_500_CONTROLES.md; integracao/catalogo.js; integracao/godot/ApoenaCatalogo.gd; integracao/godot/project.godot; integracao/godot/dados/apoena_catalogo.json; map-editor/; pixel-art/; shared/asset-library.js; shared/creator-bridge.js.

## Precisão do inventário
O pacote foi reportado com 155 entradas incluindo diretórios. bundle-v4/: 24 arquivos JS (parte_000.js a parte_023.js). tests/: 6 arquivos; integracao/testes/: 4; integracao/godot/tests/test_catalogo.gd: 1 teste GDScript. Total identificado: 11 arquivos de teste. Uma resposta anterior citou apenas seis; isso não representa todos os testes listados.

HTMLs citados: APOENA_GAME_CREATOR_V4_0_BANCADA_INTEGRADA.html (16.332.595 bytes); index.html (16.333.266 bytes); v3_9_2 (16.299.833 bytes). Tamanho não determina fonte ativa; conferir README, AGENTS, workflows e scripts.

## Integração Godot
A presença reportada de ApoenaCatalogo.gd, project.godot, catálogo JSON e teste GDScript sugere ponte inicial, não integração completa de gameplay nem exportação completa.

## PoC proposta
Apoena Bridge — Creator to Godot: criar recurso no Creator; exportar contrato versionado; importar na Godot 4; consumir em cena real; executar interação; validar comportamento e persistência; testar dados inválidos.

## Primeiro MVP proposto
Criar projeto → editar cena → adicionar objetos → executar → salvar → reabrir. Meta proposta, não implementação verificada.