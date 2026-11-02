# RELATÓRIO FORENSE DE ENGENHARIA DE SOFTWARE
## Apoena Game Creator — arquitetura, código, dados, sprites, segurança, integração e operação

**Data da análise (conforme documento de origem):** 2026-11-02; hora: Hora não disponível na fonte.  
**Data/hora deste registro de proveniência:** 2026-11-02T10:59:32Z.  
**Repositório de origem analisado:** `apoenalore/GameCreator` (`https://github.com/apoenalore/GameCreator`).  
**Branch e commit Git correspondentes aos ZIPs analisados:** não disponíveis na fonte; os arquivos ZIP recebidos não fornecem vínculo verificável com uma branch ou SHA.  
**SHA-256 do terceiro arquivo (`Backup_GameCreator_Auditoria_2026-11-02.zip`):** não disponível na fonte consultada; não inferir nem reutilizar o hash dos dois ZIPs idênticos.  
**Escopo recebido:** `GameCreator-main (1)(7).zip`, `GameCreator-main (1)(6).zip` e cópia de preservação `Backup_GameCreator_Auditoria_2026-11-02.zip`.  
**Natureza:** auditoria estática e testes locais controlados.  
**Regra de preservação:** os arquivos originais não foram alterados. Testes/builds anteriores foram feitos em extração temporária. Este relatório não representa pentest externo nem homologação de produção.

> Proveniência: documento enviado pelo proprietário nesta conversa como arquivo Markdown. Os achados abaixo são preservados como resultados reportados pela auditoria anexada; não foram reexecutados independentemente durante esta operação de backup.

---

# 1. Parecer executivo

O Apoena Game Creator é, pelo conteúdo analisado, predominantemente uma aplicação **client-side/offline**, construída com HTML, CSS e JavaScript, com persistência local via IndexedDB/localStorage, troca de mensagens entre janelas e integração inicial com Godot por JSON/GDScript.

Não encontrei no ZIP uma aplicação servidor tradicional, um banco SQL, um serviço de autenticação, configuração de certificado TLS/SSL ou uma infraestrutura própria de API. Isso não é necessariamente um defeito: para um editor offline, a arquitetura local pode ser adequada. Porém, significa que não se deve afirmar que o projeto já possui backend seguro, SQL, autenticação centralizada ou multiplayer autoritativo.

## 1.1 Resultados objetivos

| Área | Resultado forense |
|---|---|
| Integridade dos dois ZIPs de origem | Idênticos; SHA-256 `bb40c8419056dfecdf75f9db99ee2deecfe6963a7fbe5b3d5b804b8b7346dfd9` |
| Integridade estrutural do ZIP | `testzip()` sem erro; nenhum caminho de extração suspeito detectado |
| Entradas do ZIP | 155 entradas incluindo diretórios; 135 arquivos |
| Tipos de arquivo | 62 JS, 9 CJS, 11 HTML, 28 MD, 12 TXT, 3 JSON, 2 YML, 2 CMD, 2 PS1, 2 GDScript, 1 Python e 1 projeto Godot |
| SQL / banco relacional | Nenhum arquivo `.sql`, SQLite, MySQL, PostgreSQL ou MariaDB encontrado |
| SSL/TLS próprio | Nenhum certificado `.pem`, `.crt`, `.cer`, chave `.key`, configuração de servidor TLS ou endpoint backend encontrado |
| Sprites binários no ZIP | Nenhum PNG, WebP, JPG ou outro arquivo de imagem como arquivo independente |
| Catálogo de sprites | 10 caminhos de imagem referenciados; nenhum dos 10 está presente no ZIP analisado |
| JavaScript | 71 arquivos JS/CJS passaram em `node --check` na auditoria anterior |
| Testes locais | 8 suítes passaram; 2 ficaram bloqueadas por dependência ausente no ambiente local (`fake-indexeddb`) |
| Godot / Android | Não homologados nesta auditoria |
| GitHub Actions atual | Código do workflow inspecionado; não foi consultado o estado remoto ao vivo nesta execução |

**Parecer:** há uma base de editor e ferramentas reais, mas o produto não deve ser descrito como sistema completo com backend SQL, autenticação, SSL próprio ou pacote autossuficiente de sprites. Existem pendências funcionais e de segurança que merecem tratamento antes de expansão para comunidade, multiplayer ou distribuição de conteúdo externo.

---

# 2. Identidade, integridade e cadeia de custódia

## 2.1 Arquivos recebidos

Os dois arquivos `GameCreator-main (1)(7).zip` e `GameCreator-main (1)(6).zip` possuem:
- 60.120.095 bytes cada;
- SHA-256 idêntico: `bb40c8419056dfecdf75f9db99ee2deecfe6963a7fbe5b3d5b804b8b7346dfd9`.

Isso comprova que os dois ZIPs são cópias binariamente idênticas, não duas versões diferentes.

A cópia `Backup_GameCreator_Auditoria_2026-11-02.zip` tem hash diferente, portanto não é uma cópia binária idêntica do ZIP original. Seu conteúdo deve ser tratado como artefato separado até uma comparação de arquivos internos.

## 2.2 Verificações do contêiner ZIP

- Teste de CRC/estrutura: sem arquivo corrompido detectado.
- Caminhos absolutos: nenhum.
- Componentes `..` em caminhos: nenhum.
- Caminhos duplicados: nenhum.
- Nenhum indício de Zip Slip nos nomes de entrada analisados.

Isso avalia o contêiner ZIP, não garante que todo arquivo de dentro seja seguro para executar.

## 2.3 Preservação

- Nenhum arquivo original foi editado.
- Nenhum arquivo foi removido.
- Nenhum workflow foi iniciado.
- Nenhum commit foi criado.
- Nenhuma instalação do usuário foi alterada.
- A execução de build e testes ocorreu em ambiente temporário, não no ZIP original.

---

# 3. Arquitetura real encontrada

## 3.1 Camadas

| Camada | Tecnologia encontrada | Função |
|---|---|---|
| Interface | HTML/CSS | Telas do Creator, biblioteca, mapas e Pixel Art |
| Lógica de aplicação | JavaScript | Edição, validação, catálogo, exportação, integração |
| Persistência local | IndexedDB | Assets e projetos locais |
| Persistência auxiliar | localStorage | Rascunho/autosave de algumas ferramentas |
| Comunicação | `window.postMessage` e `BroadcastChannel` | Sincronização entre janelas e abas |
| Formato de intercâmbio | JSON | Projeto editável, mapa, catálogo, manifesto e backup |
| Runtime de integração | Godot 4 / GDScript | Leitura de catálogo, inventário e fabricação em estágio inicial |
| Automação | GitHub Actions, PowerShell, Python | Build, testes, pacote e publicação |
| Banco de dados servidor | Não encontrado | Não há evidência de backend SQL no ZIP |
| Autenticação central | Não encontrada | Não há serviço de login/autorização de usuário no pacote |
| Transporte TLS próprio | Não encontrado | Não há servidor HTTPS próprio ou configuração de certificados |

## 3.2 Consequência arquitetural

O projeto funciona principalmente no dispositivo do usuário. Isso é positivo para uso offline e reduz dependência de servidor, mas impõe limites:

1. Dados no IndexedDB pertencem ao navegador/perfil/dispositivo.
2. Limpar dados do navegador pode apagar a biblioteca local se não houver backup.
3. A sincronização entre ferramentas não equivale a sincronização entre usuários.
4. `postMessage` é comunicação entre contextos do navegador, não uma API autenticada.
5. Um JSON exportado é um arquivo de dados, não um banco de dados central.
6. O Godot recebe um catálogo exportado; isso não significa conexão automática e contínua ao Creator.

---

# 4. HTML, CSS e JavaScript — revisão de engenharia

## 4.1 HTML

Foram encontrados 11 arquivos HTML. Os principais são:
- `index.html`;
- `APOENA_GAME_CREATOR_V4_0_BANCADA_INTEGRADA.html`;
- `APOENA_GAME_CREATOR_v3_9_2_PROJETOS_SEGUROS_COMPLETO.html`;
- `pixel-art/estudio.html`;
- `map-editor/index.html`;
- `biblioteca/index.html`;
- `integracao/index.html`;
- páginas de acesso ao legado.

### Achados

**HTML-001 — Divergência de versão interna**

O nome `APOENA_GAME_CREATOR_V4_0_BANCADA_INTEGRADA.html` não corresponde ao título interno observado, que ainda identifica v3.9.2. O build ajusta o título da página integrada, mas a fonte original continua com a identificação anterior.

**Risco:** confusão sobre qual arquivo é fonte, qual é build e qual versão está aberta.

**Ação sugerida:** definir nomenclatura oficial de fonte, build e legado; não renomear arquivos históricos sem manter compatibilidade.

**HTML-002 — HTML com muito JavaScript inline**

As páginas principais contêm grandes blocos inline. Isso facilita distribuição offline em um arquivo, mas dificulta:
- análise estática granular;
- isolamento de módulos;
- aplicação de Content Security Policy rígida;
- testes unitários sem extração de funções;
- revisão de dependências e ordem de carregamento.

**Ação sugerida:** migrar gradualmente módulos novos para arquivos JS separados, mantendo o HTML monolítico de distribuição se esse for um requisito do produto.

**HTML-003 — Uso de `innerHTML`**

Há muitos usos de `innerHTML` para renderizar listas, opções, painéis e elementos da interface. O uso não é automaticamente vulnerável: várias rotinas escapam nomes e textos antes de montar HTML.

O risco aparece quando dados importados ou metadados não escapados chegam a templates HTML.

**Ação sugerida:**
- preferir `textContent` para texto;
- criar elementos com `document.createElement`;
- manter uma única função de escape por contexto;
- testar strings com aspas, tags, atributos, caracteres Unicode e conteúdo HTML malicioso;
- nunca tratar um nome de arquivo ou campo de JSON como HTML confiável.

Não foi demonstrada exploração XSS nesta auditoria. O achado é uma superfície de revisão, não uma vulnerabilidade explorada.

## 4.2 JavaScript

A análise anterior verificou sintaxe de 71 arquivos `.js` e `.cjs`, sem erro de parser.

Isso comprova sintaxe aceita pelo Node.js, não funcionamento integral no navegador.

### Pontos positivos

- Separação crescente de módulos em `shared/`, `pixel-art/`, `map-editor/` e `integracao/`.
- Testes unitários e de contrato para alguns módulos.
- Uso de schemas/versionamento em JSON.
- Limites explícitos para vários uploads e metadados.
- Tratamento de exceções em fluxos importantes.

### Pontos de atenção

- A aplicação ainda depende de contratos implícitos entre módulos.
- O mesmo dado pode existir no estado do Creator, no IndexedDB, em JSON exportado e no runtime Godot.
- É necessário distinguir claramente estado em memória, persistência local e exportação.
- O teste sintático não substitui teste de interação no navegador.
- A ordem de scripts e a existência de `window.opener` influenciam a integração.

---

# 5. Banco de dados, SQL e persistência

## 5.1 SQL: resultado da busca

Não foram encontrados:
- arquivos `.sql`;
- banco SQLite `.db`/`.sqlite`;
- código de conexão MySQL;
- código de conexão PostgreSQL;
- MariaDB;
- migrações SQL;
- ORM;
- servidor de banco de dados;
- credenciais de banco.

Duas ocorrências que pareciam conter `SELECT`/`FROM` eram trechos de dados codificados em Base64, não comandos SQL.

**Conclusão:** não existe evidência de banco SQL no pacote analisado.

## 5.2 O banco real é IndexedDB

Arquivo: `shared/asset-library.js`.

### Estrutura observada

| Linhas | Função |
|---|---|
| 7–11 | Define canal, nome do banco, versão 1 e stores `assets` e `projects`. |
| 69–98 | Abre IndexedDB, cria object stores e índices durante upgrade. |
| 100–118 | Consulta registros individuais ou listas completas. |
| 120–132 | Persiste registros em transações `readwrite`. |
| 134–143 | Exclui registros em transações `readwrite`. |
| 167–207 | Salva assets e metadados. |
| 208–220 | Lista assets com filtros e ordenação. |
| 227–246 | Salva projetos e metadados. |
| 248–260 | Lista projetos. |
| 262–266 | Exclui projetos. |
| 268–280 | Centraliza operações permitidas por `dispatch`. |

### Pontos positivos

- Usa IndexedDB, adequado para dados estruturados e blobs locais.
- Separa assets e projetos.
- Cria índices por categoria, nome e atualização.
- Usa transações para gravação e exclusão.
- Tem fallback em memória para testes Node.
- Mantém metadados e timestamps.
- Não exige um servidor SQL para funcionar offline.

### Riscos e limites

**DB-001 — Sem backup automático garantido**

A biblioteca local depende do armazenamento do navegador. O backup manual existe, mas o pacote não comprova backup automático externo ou sincronização em nuvem.

**DB-002 — Banco local não é banco multiusuário**

Não há controle de usuário, permissões por conta, auditoria central ou concorrência entre clientes.

**DB-003 — Versão do schema**

`DB_VERSION = 1`. A evolução futura precisa de migrações de IndexedDB cuidadosamente testadas. Uma mudança de schema sem migração pode deixar dados antigos incompatíveis.

**DB-004 — Fallback em memória**

Em ambiente Node, a biblioteca usa mapas em memória. Isso é apropriado para testes, mas não simula persistência real em disco.

## 5.3 Backup e restauração

Arquivo: `shared/library-backup.js`.

| Linhas | Comportamento |
|---|---|
| 3–5 | Define schema, máximo de registros e limite de texto de 120 MB. |
| 7–18 | Exporta assets, blobs e projetos para snapshot JSON. |
| 20–22 | Valida formato de imagem data URL. |
| 23–35 | Valida schema, listas, IDs e duplicidade. |
| 37–53 | Importa assets e projetos um por um. |

### Achado DB-005 — Importação do backup não é transação global

O backup é validado antes, mas a importação grava cada asset e projeto individualmente. Se a importação falhar no meio, parte dos registros pode já ter sido gravada.

**Impacto:** restauração parcial. O usuário pode acreditar que recuperou tudo, mas alguns registros podem faltar.

**Correção recomendada:**
1. Importar para uma área temporária ou banco staging.
2. Validar todos os blobs e projetos antes de confirmar.
3. Usar transação única quando viável ou mecanismo de rollback por lote.
4. Registrar progresso e itens importados.
5. Se interromper, permitir retomar ou desfazer.
6. Testar falha simulada no 1º, 10º e último registro.

**Estado:** recomendação; não aplicada.

## 5.4 Se um SQL for necessário no futuro

Não recomendo inserir SQL apenas para “ter banco de dados”. A escolha depende da necessidade:

- **Uso individual/offline:** IndexedDB continua adequado.
- **Sincronização entre dispositivos:** API + banco servidor.
- **Comunidade, contas e projetos compartilhados:** backend com autenticação e autorização.
- **Multiplayer/economia competitiva:** servidor autoritativo; o cliente nunca deve decidir saldo, inventário, recompensa ou ranking.

Uma arquitetura futura poderia usar PostgreSQL no servidor, API HTTPS, autenticação, autorização por projeto e armazenamento separado para arquivos binários. Isso é proposta arquitetural, não recurso atual.

---

# 6. SSL, TLS e segurança de transporte

## 6.1 Resultado da busca

Não foram encontrados:
- certificados `.pem`, `.crt` ou `.cer`;
- chaves privadas `.key`;
- configuração de Nginx/Apache/IIS;
- servidor HTTPS;
- configuração de TLS do backend;
- endpoint de API própria;
- política de rotação de certificados.

Foi encontrada uma URL HTTPS para baixar Godot no workflow e URLs HTTPS do GitHub.

## 6.2 O que isso significa

O projeto pode ser distribuído e aberto localmente sem possuir certificado próprio. Quando hospedado no GitHub Pages ou em outro serviço, o TLS pode ser fornecido pela plataforma.

Mas não se pode afirmar, com base no ZIP, que:
- existe SSL próprio do Apoena;
- existe API protegida por TLS;
- existe login seguro;
- existe criptografia de dados em trânsito entre clientes e servidor.

## 6.3 TLS: requisitos para uma futura API

Se o projeto ganhar backend:
- HTTPS obrigatório em produção;
- TLS 1.2 ou superior, preferencialmente TLS 1.3;
- certificados válidos e renovação automatizada;
- HSTS quando aplicável;
- cookies `Secure`, `HttpOnly` e `SameSite` se usar sessão por cookie;
- CORS com origens explicitamente permitidas;
- autenticação e autorização no servidor;
- segredos fora do repositório;
- logs sem tokens, senhas ou dados sensíveis.

**Importante:** TLS protege o transporte. Não substitui autorização, validação de dados ou segurança da aplicação.

---

# 7. Segurança da comunicação entre janelas

## 7.1 Arquivo `shared/creator-bridge.js`

O protocolo usa `postMessage` para sincronizar ferramentas com a janela principal.

### Achado SEC-001 — Aceitação de origem `null`

No código:
- linhas 47–48: registra listener;
- linhas 49–52: lê dados e origem;
- linha 53: aceita origem igual à origem esperada **ou** origem `"null"`;
- linha 54: valida canal, tipo, ID e remetente diferente da própria janela;
- linhas 55–59: encaminha ação e devolve resposta.

A aceitação de `"null"` é um risco porque origens opacas podem ser usadas por contextos sandboxed ou arquivos locais. O canal e o ID da mensagem não autenticam o remetente.

### Achado SEC-002 — Falta de vínculo explícito do remetente autorizado

A rotina verifica que existe um `event.source`, mas não comprova em todos os casos que ele é a janela específica autorizada pelo fluxo de abertura.

### Achado SEC-003 — `postMessage` usa target origin `"*"`

Há chamadas com target origin `"*"`. Em uma referência de janela conhecida, isso pode funcionar, mas o ideal é restringir a origem quando ela é conhecida e combinar com validação do remetente.

### Testes existentes

`tests/creator-bridge.test.cjs`:
- testa request/response;
- testa ação desconhecida;
- testa origem externa `https://evil.example`;
- não testa origem `null`;
- não testa remetente diferente da janela autorizada;
- não testa replay, excesso de payload ou payload malformado.

### Correção recomendada

1. Criar handshake de sessão entre Creator e ferramenta.
2. Autorizar a janela por referência `event.source`.
3. Não confiar em `channel` como segredo.
4. Rejeitar `null` por padrão.
5. Se houver necessidade legítima de origem opaca, exigir token de sessão imprevisível e de curta duração, com capacidades limitadas.
6. Validar schema e tamanho de cada payload.
7. Adicionar testes negativos e de replay.

**Severidade:** alta para uma aplicação que venha a aceitar conteúdo comunitário ou dados de origem externa.  
**Certeza:** risco confirmado por leitura estática; exploração não executada.

---

# 8. Sprites, Pixel Art, spritesheets e animações

## 8.1 O que existe no código

O módulo `pixel-art/estudio.js` contém funcionalidades de:
- importação de imagem;
- corte em quadros;
- edição em canvas;
- desfazer alterações;
- montagem de spritesheet;
- geração de manifesto;
- exportação PNG;
- importação de projeto JSON;
- salvamento de asset na biblioteca;
- sincronização com Creator.

## 8.2 Limites de imagem encontrados

No `pixel-art/estudio.js`:
- linha 243: aceita PNG, WebP e JPEG até 22 MB;
- linha 243: rejeita imagens com mais de 32 milhões de pixels;
- linha 246: limita arquivo de projeto JSON a 18 MB;
- linha 99: limita metadados específicos a 50 KB;
- linha 100: cria manifesto com schema `apoena.pixelart.v1`, versão, frames, FPS, transparência, âncora e coordenadas;
- linha 126: adiciona dados PNG de cada frame em data URL;
- linha 134: valida data URL PNG/WebP na importação;
- linhas 200–216: salva asset e tenta sincronizar com Creator; PNG acima de 10 MB não é copiado em Base64 para a sessão V4.0.

### Pontos positivos

- Limites de tamanho e dimensão existem.
- O projeto usa canvas e gera PNG.
- O manifesto preserva coordenadas e ações/direções.
- Há fluxo de desfazer em lote.
- A biblioteca mantém blob e metadados.
- Há distinção entre arquivo original e imagem processada em partes do fluxo.

## 8.3 Achado SPR-001 — Catálogo referencia sprites que não estão no ZIP

O arquivo `pixel-art/catalogo_assets_agar.json` lista 10 caminhos:

- `apoena/apoena_andar.webp`
- `apoena/apoena_correr.webp`
- `apoena/apoena_esfera_azul.webp`
- `animais/javali_agar_sprites.webp`
- `animais/abelha_agar_sprites.webp`
- `animais/colmeia_tronco_frente.webp`
- `animais/colmeia_tronco_direita.webp`
- `animais/colmeia_tronco_costas.webp`
- `animais/colmeia_tronco_esquerda.webp`
- `apoena/energia_azul_efeitos.png`

Nenhum desses 10 arquivos está presente no ZIP analisado.

O próprio JSON diz que os binários estão distribuídos localmente e ainda não versionados no GitHub. Portanto, o catálogo é uma lista de referências, não uma entrega autossuficiente dos sprites.

**Impacto:** uma instalação limpa pode ter os nomes e caminhos dos assets sem ter os arquivos gráficos.

**Ação recomendada:** criar um manifesto de assets com:
- caminho relativo;
- nome lógico;
- tipo MIME;
- largura/altura;
- tamanho;
- SHA-256;
- licença/origem;
- versão do asset;
- status (presente, opcional, importado pelo usuário).

Não incorporar assets autorais ou privados sem autorização. O pacote deve explicar claramente quais sprites são exemplos e quais precisam ser importados pelo usuário.

## 8.4 Achado SPR-002 — Biblioteca aceita qualquer MIME `image/*`

Em `shared/asset-library.js`, linhas 167–175:
- recebe blob/data URL;
- converte para Blob;
- exige MIME começando com `image/`.

Isso é mais amplo que PNG/WebP/JPEG. O SVG é um formato de imagem, mas pode conter conteúdo ativo e referências externas.

Em `shared/library-backup.js`, linhas 20–22, a expressão de validação de imagem também aceita subtipos genéricos `image/...`.

**Risco:** entrada de SVG ou outro formato não previsto no fluxo pode ampliar a superfície de ataque, especialmente se futuramente for exibida, transformada ou exportada de forma insegura.

**Ação recomendada:**
- allowlist de MIME: PNG, WebP e JPEG, se forem os formatos oficialmente suportados;
- validar a assinatura binária real, não só o MIME informado;
- limitar dimensões e bytes descomprimidos;
- tratar SVG como formato separado, com sanitização rigorosa ou rejeição;
- testar arquivos com MIME falso, extensão falsa e conteúdo malformado.

## 8.5 Achado SPR-003 — Manifesto não equivale a animação funcional no jogo

O manifesto descreve quadros, ações, direções e FPS. Isso é metadado de animação, não prova que o runtime Godot ou o jogo HTML já executa todas as animações.

É necessário testar:
- importação de spritesheet;
- mapeamento de frames;
- pivô/âncora;
- colisão;
- estados;
- transições;
- FPS;
- escala;
- orientação;
- gameplay real.

---

# 9. Mapas, tilesets e terreno

## 9.1 Persistência do mapa

`map-editor/index.html`:
- linhas 342–350: lista projetos de mapa na biblioteca;
- linhas 352–370: salva mapa na biblioteca e tenta sincronizar com sessão V4.0;
- linhas 372–381: reabre mapa salvo;
- linhas 383–395: valida e aplica dados do mapa;
- linhas 397–403: importa JSON com limite de 18 MB;
- linhas 405–410: exporta PNG;
- linhas 412–414: autosave local em localStorage.

### Limites importantes

- O autosave local só grava quando o JSON tem menos de 3,5 MB.
- O salvamento na biblioteca e a sincronização da sessão V4.0 são operações distintas.
- O código avisa que a sessão V4.0 precisa ser salva pelo botão de projeto editável.
- A importação de mapa filtra assets para PNG/WebP em data URL.

## 9.2 Achado MAP-001 — Perfil de tileset é perdido ao carregar

No handler `loadTileset`, linhas 295–300:
- carrega o asset;
- define `sheetProfile='manual'`;
- não restaura o perfil salvo em `item.metadata.profile`;
- restaura colunas e linhas.

**Impacto:** perfil automático pode ser perdido após salvar e reabrir.

## 9.3 Achado MAP-002 — Autotiling de água incompleto

A função `smartWaterTile()` nas linhas 154–161:
- considera vizinhos cardeais;
- trata centro e uma borda;
- trata quatro pares adjacentes;
- não modela todas as combinações opostas, triplas e diagonais.

O autotiling da água só é ativado em condição específica do perfil `agar24`, conforme a documentação do projeto.

**Impacto:** não é autotiling universal e não reconhece automaticamente qualquer atlas.

**Ação recomendada:** tabela configurável de peças por perfil, pré-visualização, suporte a vizinhança completa e testes de regressão. Preservar o modo de peça individual.

---

# 10. Integração com Godot

## 10.1 O que existe

- `integracao/catalogo.js`;
- `integracao/godot/ApoenaCatalogo.gd`;
- fixture `integracao/godot/dados/apoena_catalogo.json`;
- testes de catálogo e contrato Godot.

## 10.2 O que o GDScript implementa

`ApoenaCatalogo.gd`:
- linhas 25–37: carrega e valida JSON/schema;
- linhas 39–72: valida itens, receitas e referências;
- linhas 85–97: coleta e remove itens;
- linhas 99–126: inicia fabricação, consome ingredientes e ouro;
- linhas 128–138: processa fila de fabricação;
- linhas 140–144: conclui receita;
- linhas 149–182: implementa três tipos de efeitos instantâneos;
- linhas 184–192: salva sessão;
- linhas 194–215: restaura sessão.

## 10.3 Limites

O código não prova:
- inventário visual conectado;
- equipagem real;
- combate;
- multiplayer;
- loja;
- NPCs autônomos;
- economia segura;
- sincronização em nuvem;
- integração com cenas completas do jogo.

### Achado GODOT-001 — Sessão precisa de validação adicional

A restauração verifica schema, `game_id`, tipos básicos e referências de itens, mas precisa de testes de:
- números negativos;
- valores extremos;
- tipos inesperados;
- fila com tempos negativos;
- dados truncados;
- arquivos corrompidos;
- compatibilidade entre versões de catálogo.

**Ação recomendada:** validar intervalos, tipos e limites antes de atribuir o estado carregado.

---

# 11. CI/CD, build e distribuição

## 11.1 Workflows

Foram encontrados dois workflows:
- `.github/workflows/pixel-art.yml`;
- `.github/workflows/publicar-creator-unificado.yml`.

Ambos usam runner Windows self-hosted. O workflow canônico executa build/testes; o workflow de publicação também pode executar build e publicar `index.html`.

## 11.2 Achados

**CI-001 — Sobreposição de gatilhos**

Há paths que podem disparar os dois workflows no mesmo push. O canônico possui concorrência por branch; o de publicação não declara o mesmo controle.

Não há prova de colisão real nesta auditoria, mas existe risco de disputa por runner ou execução paralela.

**CI-002 — Smoke test desliga JavaScript**

O workflow usa `--disable-javascript` no browser headless. Isso valida abertura e estrutura DOM, não a interação funcional.

**CI-003 — Dependência sem lockfile**

O workflow instala com `npm install --no-package-lock`. O `package.json` fixa `fake-indexeddb` em `6.2.6`, mas não há lockfile no pacote.

**CI-004 — Build Python e PowerShell**

O build Python foi executado em cópia temporária. A saída ficou 2 bytes maior que o `index.html` recebido. A causa exata não foi isolada. O PowerShell não foi executado nesta máquina.

**CI-005 — Publicação automática**

O workflow de publicação tem `contents: write`, checkout com credenciais persistentes e `git push`. Isso é intencional para publicar o HTML gerado, mas exige proteção de branch, revisão de mudanças e confirmação de que o commit publicado é o mesmo que foi validado.

Não se deve remover esse workflow sem analisar o fluxo real de publicação.

---

# 12. Segredos, credenciais e dados sensíveis

## 12.1 Busca estática

Não foram encontrados nomes explícitos de variáveis de autenticação como `password`, `senha`, `token`, `secret`, `authorization` ou `bearer` nos arquivos de código analisados.

Também não foram encontrados arquivos típicos de segredo:
- `.env`;
- `.pem`;
- `.key`;
- `.p12`;
- `.pfx`;
- certificados `.crt`/`.cer`.

Isso não é garantia de ausência de segredo: um segredo pode estar codificado, em histórico Git, em arquivo não textual ou em variável do runner. O ZIP não permite auditar configurações privadas do GitHub.

## 12.2 Recomendações

- Executar secret scanning no histórico Git completo.
- Nunca versionar tokens de publicação ou credenciais do runner.
- Rotacionar qualquer credencial que tenha sido exposta em logs.
- Restringir `contents: write` ao workflow que realmente publica.
- Proteger branch e exigir revisão para alterações de workflow.

---

# 13. Matriz de riscos priorizada

| ID | Achado | Prioridade histórica (não revalidada) | Status da evidência no ZIP |
|---|---|---|---|
| SEC-001 | Ponte aceita origem `null` | Crítica/Alta — classificação histórica, pendente de revalidação | RECUPERADO — VALIDAR |
| SEC-002 | Remetente não está vinculado a janela autorizada em todos os cenários | Alta — classificação histórica, pendente de revalidação | RECUPERADO — VALIDAR |
| SEC-003 | `postMessage` usa `*` | Média/Alta — classificação histórica, pendente de revalidação | RECUPERADO — VALIDAR |
| DB-005 | Importação de backup pode ficar parcial | Alta — classificação histórica, pendente de revalidação | RECUPERADO — VALIDAR |
| SPR-001 | 10 sprites referenciados ausentes do ZIP | Alta para distribuição de assets — classificação histórica | RECUPERADO — VALIDAR |
| SPR-002 | MIME `image/*` amplo, incluindo SVG potencial | Alta para importação não confiável — classificação histórica | RECUPERADO — VALIDAR |
| MAP-001 | Perfil do tileset é perdido ao carregar | Alta funcional — classificação histórica | RECUPERADO — VALIDAR |
| MAP-002 | Autotiling incompleto | Alta visual — classificação histórica | RECUPERADO — VALIDAR |
| GODOT-001 | Validação de sessão requer limites adicionais | Média/Alta — classificação histórica | RECUPERADO — VALIDAR |
| CI-001 | Workflows com sobreposição de gatilhos | Média/Alta operacional — classificação histórica | RECUPERADO — VALIDAR |
| CI-002 | Smoke test não executa JS | Média — classificação histórica | RECUPERADO — VALIDAR |
| CI-003 | Dependência sem lockfile | Média — classificação histórica | RECUPERADO — VALIDAR |
| CI-004 | Diferença de 2 bytes no build Python | Média — classificação histórica | RECUPERADO — VALIDAR |
| HTML-001 | Identificação de versão divergente | Média — classificação histórica | RECUPERADO — VALIDAR |
| HTML-002 | Grandes blocos inline dificultam manutenção | Média — classificação histórica | RECUPERADO — VALIDAR |
| HTML-003 | Muitos `innerHTML` exigem revisão contextual | Média — classificação histórica | RECUPERADO — VALIDAR |
| SQL-001 | Não há SQL/backend no pacote | Informativo — inventário histórico | RECUPERADO — VALIDAR |
| TLS-001 | Não há configuração TLS própria | Informativo — inventário histórico | RECUPERADO — VALIDAR |

**Nota de proveniência e interpretação da matriz:** todos os resultados acima descrevem exclusivamente o conteúdo dos ZIPs recebidos na auditoria histórica. Nenhum deles deve ser interpretado como achado confirmado no HEAD atual do GameCreator até que seja revalidado contra um commit identificado. As prioridades são as classificações históricas do relatório e também permanecem sujeitas a reavaliação.

---

# 14. Plano profissional de correção

O projeto documenta WIP = 1 entre Game Creator e Apoena Pixel Art HTML. Portanto, a auditoria não autoriza iniciar diversas implementações paralelas.

## Fase 1 — Fechar a tarefa ativa

1. Confirmar estado remoto atual de GC-UPDATE-009.
2. Validar atualizador em sandbox.
3. Verificar preservação de biblioteca, assets, configurações e runner.
4. Só encerrar WIP 1 após evidência no commit correto.

## Fase 2 — Segurança e integridade de dados

1. Corrigir autorização da ponte.
2. Adicionar testes para origem `null` e remetente não autorizado.
3. Restringir formatos de imagem.
4. Fazer restauração de backup transacional/recuperável.
5. Validar limites de dados importados.
6. Fazer secret scanning do histórico Git.

## Fase 3 — Assets e sprites

1. Inventariar os 10 assets ausentes.
2. Definir se são arquivos que devem ser entregues, exemplos opcionais ou importação do usuário.
3. Gerar manifesto com SHA-256.
4. Testar spritesheet e manifesto.
5. Validar frames e animações no runtime real.

## Fase 4 — Mapas

1. Corrigir restauração do perfil.
2. Criar testes de ida e volta de tileset.
3. Especificar autotiling completo.
4. Manter modo manual.
5. Testar atlas personalizado.
6. Validar exportação e reimportação.

## Fase 5 — Godot

1. Validar sessão JSON.
2. Testar fila de fabricação.
3. Testar efeitos e inventário.
4. Integrar cenas reais.
5. Validar Android físico.

## Fase 6 — Infraestrutura futura

Somente se houver necessidade real:
- API HTTPS;
- autenticação;
- banco PostgreSQL;
- autorização por usuário/projeto;
- armazenamento de arquivos;
- sincronização;
- servidor autoritativo para multiplayer/economia.

Não implantar SQL ou servidor apenas por aparência de arquitetura profissional.

---

# 15. Testes de aceitação que faltam

## Segurança
- Origem `null`.
- Janela não autorizada.
- Replay de mensagens.
- Payload excessivo.
- JSON malformado.
- SVG ativo.
- MIME falso.
- Arquivo de imagem corrompido.
- Backup adulterado.

## Persistência
- Fechar e abrir navegador.
- Reiniciar dispositivo.
- Banco em upgrade.
- Falta de espaço.
- Falha durante gravação.
- Importação interrompida.
- Backup e restauração em outro perfil.

## Sprites
- PNG, WebP e JPEG.
- Imagem com dimensões máximas.
- Spritesheet com quadros incompletos.
- Frames duplicados.
- Animação com FPS diferentes.
- Exportar/importar manifesto.
- Preservar imagem original.

## Mapa
- Perfil salvo e restaurado.
- Autotiling em todas as orientações.
- Curvas e cruzamentos.
- Desfazer/refazer.
- Limite do mapa.
- Exportação JSON e PNG.

## Godot
- Catálogo inválido.
- Sessão incompatível.
- Ingredientes insuficientes.
- Ouro insuficiente.
- Fabricação instantânea e temporizada.
- Fila salva e restaurada.
- Runtime em desktop e Android.

## Distribuição
- ZIP limpo.
- Arquivos obrigatórios.
- Assets presentes ou claramente declarados como externos.
- Build reproduzível.
- Atualização sem apagar dados.
- Hashes de release.

---

# 16. Conclusão técnica

O Game Creator é uma aplicação de autoria local com persistência no navegador e uma ponte inicial de integração com Godot. A arquitetura é compatível com um editor offline, mas ainda não representa uma plataforma cliente-servidor.

As principais descobertas desta análise são:

1. **Banco:** a persistência existente é IndexedDB/localStorage, não SQL.
2. **SSL:** não existe configuração de TLS próprio no pacote; o uso de HTTPS observado é para serviços externos, como GitHub.
3. **Sprites:** o editor possui lógica de importação/edição/exportação, mas o ZIP não inclui os 10 arquivos gráficos listados no catálogo de assets.
4. **Segurança:** a ponte `postMessage` tem uma condição permissiva para origem `null`; a restauração de backup pode gravar parcialmente; a biblioteca aceita MIME `image/*` de forma ampla.
5. **Mapas:** a restauração de tileset perde o perfil e o autotiling de água é limitado.
6. **Godot:** há um adaptador funcional em nível inicial de catálogo, inventário e crafting, mas não integração completa de gameplay.
7. **CI:** há automação relevante, mas smoke test estrutural não equivale a teste funcional e a coordenação dos workflows deve ser verificada.

**Rastreabilidade dos IDs entre o relatório e a Skill de segurança:** relatório SEC-001 corresponde à Skill SEC-001; relatório SEC-003 (uso de `postMessage` com `*`) corresponde à Skill SEC-002; relatório DB-005 (importação não transacional) corresponde à Skill SEC-003. O SEC-002 deste relatório não possui correspondência direta e se sobrepõe parcialmente aos SEC-001 e SEC-002 da Skill. Os identificadores originais foram preservados, sem renumeração.

**Status:** AUDITORIA FORENSE ESTÁTICA CONCLUÍDA COM LIMITES EXPLÍCITOS.  
**Correções aplicadas:** nenhuma.  
**Homologação de produção:** não realizada.  
**Preservação dos arquivos originais:** mantida.

A conclusão mais importante é evitar reconstruir o sistema sem necessidade. O caminho seguro é preservar o que já funciona, corrigir as falhas comprovadas em pequenas etapas e exigir testes objetivos antes de declarar cada módulo concluído.
