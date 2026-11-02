# Pendências e próximos passos

## Acesso e recuperação
1. Obter exportação/conteúdo da conversa externa “Analisar segurança do repositório”.
2. Verificar anexos/imagens não visíveis no contexto.
3. Ler integralmente documentos técnicos do ZIP, especialmente AGENTS.md, README.md, PLANO_GERAL_APOENA.md, auditorias e pendências.
4. Auditar código e workflows atuais para confirmar fonte de verdade e comandos reais de build/teste.

## Arquitetura
1. Definir versão minor/patch da Godot 4.x.
2. Escolher integração: EditorPlugin, processo externo, APIs/contratos de arquivo ou combinação.
3. Definir interface: própria, Godot customizada ou híbrida.
4. Definir contrato de projeto, versionamento e migração de schemas.
5. Determinar fonte de verdade de cada módulo e versão HTML/JS.
6. Validar salvamento, backup, restauração e compatibilidade de projetos antigos.
7. Validar exportação por plataforma.
8. Definir limites e permissões do assistente IA.
9. Formalizar modelo comercial híbrido.
10. Formalizar separação entre Game Creator universal e jogo Apoena/Agar.

## Prova de conceito
Apoena Bridge — Creator to Godot, com criação de recurso, exportação versionada, importação na Godot, consumo em cena, interação executada, persistência e erro claro para dados inválidos.

## Primeiro MVP proposto
Criar projeto → editar cena → adicionar objetos → executar → salvar → reabrir. Ainda não demonstrado.