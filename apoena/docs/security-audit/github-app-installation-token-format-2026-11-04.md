# Auditoria de compatibilidade — novos tokens GitHub App (ghs_)

**Data da auditoria:** 2026-11-04  
**Escopo:** 11 repositórios acessíveis da organização LORECRONICASAPOENA; 20 workflows GitHub Actions; arquivos de autenticação/configuração identificados por árvore de repositórios.  
**Resultado:** COMPATIBILIDADE ESTÁTICA SEM INCOMPATIBILIDADE DETECTADA NOS ARQUIVOS INSPECIONADOS. Nenhum código foi alterado.

## 1. Mudança oficial do GitHub

Fontes primárias:
- https://github.blog/changelog/2026-10-02-stateless-github-app-installation-tokens-rolled-out/
- https://github.blog/changelog/2026-05-15-github-app-installation-tokens-per-request-override-header/
- https://cli.github.com/manual/gh_help_environment
- https://cli.github.com/manual/gh_auth_login
- https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/use-github-cli
- https://docs.github.com/en/rest/quickstart

O rollout de tokens stateless foi concluído em 2026-10-02. Novos tokens de instalação de GitHub App são emitidos no formato JWT `ghs_APPID_JWT`, prefixo `ghs_`, aproximadamente 520 caracteres e dois pontos. O token anterior era opaco e curto (~40 caracteres). Permissões, escopo de repositórios, expiração de uma hora e endpoint REST de criação permanecem iguais.

O cabeçalho temporário `X-GitHub-Stateless-S2S-Token` será descontinuado em 2026-11-30. Ele serve apenas para forçar o formato em chamadas `POST /app/installations/:installation_id/access_tokens` durante testes; não é necessário para workflows que apenas recebem `github.token`. Não adicionar esse cabeçalho aos workflows Apoena.

## 2. Repositórios e workflows examinados

Foram consultados os metadados e árvores dos 11 repositórios, todos com branch padrão `main`:

1. `projeto-apoena-studio-maker-ia`
2. `JOGO-APOENA-AGAR-`
3. `que-projeto-e-esse`
4. `runner`
5. `GameCreator`
6. `APOENA-AI-HUB-IA`
7. `ApoenaBrowser`
8. `ApoenaBrowser-Updates`
9. `Apoena-pixel-art-html`
10. `apoenaskil`
11. `CEREBRO-AMIGO-APOENA`

Foram lidos 20 arquivos de workflow:

- **GameCreator (2):** `.github/workflows/pixel-art.yml` (blob `41f20c523a1a8c70635ce4f4e711428c15f6b5a3`); `.github/workflows/publicar-creator-unificado.yml` (blob `d35c00c709d9ef0779e71c5175464041be67841e`).
- **Apoena Pixel Art HTML (2):** `.github/workflows/validar-godot.yml` (blob `48b818fca12a25a6b95040d1592c56b71ec5e2b4`); `.github/workflows/validar-pixel-art-windows.yml` (blob `5c4d312c4334afd57a84a0bc816d692026544103`).
- **JOGO APOENA AGAR (10):** `apk-android-pc-apoena.yml`, `atualizar-godot-runner.yml`, `capturas-visuais.yml`, `godot.yml`, `inventario-exploracao.yml`, `mapa01-agar.yml`, `pacote-godot.yml`, `personagens-3d-runner.yml`, `selva-torres-windows.yml`, `validar-atualizacoes-pc.yml`.
- **Studio Maker IA (1):** `.github/workflows/quality.yml`.
- **ApoenaBrowser (3):** `compilar-plugin.yml`, `importar-fonte.yml`, `publicar-canal-atualizacoes.yml`.
- **ApoenaBrowser-Updates (1):** `publicar-manifesto.yml`.
- **que-projeto-e-esse (1):** `godot-check.yml`.

Os repositórios `runner`, `APOENA-AI-HUB-IA`, `apoenaskil` e `CEREBRO-AMIGO-APOENA` foram inspecionados por suas árvores/arquivos de entrada; são, neste estado consultado, documentação, skills, manifests ou material de continuidade, sem workflow de Actions que gere installation tokens.

## 3. Usos reais de tokens encontrados

### 3.1 ApoenaBrowser

Arquivo `.github/workflows/publicar-canal-atualizacoes.yml`, blob `51031c98c3bfcae6345063975ad4e20cf4281cfb`:
- Define `GH_TOKEN: ${{ github.token }}`.
- Usa GitHub CLI em `gh release download`.
- `actions/checkout@v4` mantém credenciais para o `git push` do manifesto.
- Não cria installation token manualmente; não valida comprimento, não corta token e não armazena token em coluna/campo próprio.

### 3.2 ApoenaBrowser-Updates

Arquivo `.github/workflows/publicar-manifesto.yml`, blob `447c7496149fc2e15492edae9044033eeebfe001`:
- Define `GH_TOKEN: ${{ github.token }}`.
- Usa GitHub CLI em `gh release download`.
- `actions/checkout@v4` mantém credenciais para o `git push`.
- Não cria installation token manualmente; não valida comprimento, não corta token e não armazena token em campo de tamanho fixo.

A documentação oficial do GitHub CLI recomenda precisamente disponibilizar `github.token` pela variável `GH_TOKEN` em workflows. O CLI consome a variável como credencial, sem o workflow impor um comprimento.

### 3.3 Demais workflows

- Workflows do GameCreator, Pixel Art, JOGO AGAR, Studio Maker e Lore Engine usam `actions/checkout@v4` ou `@v5`; alguns publicam commits por `git push` usando as credenciais configuradas pelo checkout.
- Nenhum dos 20 workflows examinados contém `actions/create-github-app-token`, chamada ao endpoint de criação de installation token, validação de 40 caracteres, regex legada de token, truncamento, coluna de banco para token ou cabeçalho temporário de override.
- Os workflows de validação do Pixel Art usam `persist-credentials: false`; não deixam a credencial de checkout configurada no Git após a ação.
- O Studio Maker IA usa autenticação de sessão própria por HMAC em `lib/auth.ts`; esse token de cookie local não é GitHub App installation token. O `.env.example` contém chaves de provedores de IA e senha de acesso da aplicação, sem credencial GitHub.
- Os manifests e scripts do ApoenaBrowser geram links/manifestos e hashes SHA-256 de APK; não tratam tokens GitHub.

## 4. Verificação das ações oficiais de checkout e GitHub CLI

Foram consultados os fontes oficiais `actions/checkout/v4/src/git-auth-helper.ts` e `actions/checkout/v5/src/git-auth-helper.ts`. O helper codifica o par `x-access-token:<token>` em Base64 para configurar o cabeçalho de autenticação do Git; não foi encontrada validação que exija 40 caracteres. Os dois workflows de publicação que usam `GH_TOKEN` seguem o padrão documentado pelo GitHub CLI.

Observação de protocolo: se uma integração futura fizer chamadas REST diretamente com o JWT stateless, deve usar `Authorization: Bearer` conforme a documentação do GitHub para JWT; não reutilizar exemplos antigos de `Authorization: token` para JWT. O GitHub CLI cuida da autenticação em seus próprios comandos.

## 5. Buscas e limitações

- Busca de código por `ghs_`, `GITHUB_TOKEN`, `github.token`, `create-github-app-token`, `token.length`, `40 characters` e `X-GitHub-Stateless-S2S-Token` retornou zero itens; a API marcou os resultados com `incomplete_results=true`. Portanto, esse resultado não foi tratado como prova de ausência global.
- A conclusão baseia-se na leitura dos 20 workflows, arquivos de autenticação/configuração e scripts de release identificados nas árvores. Não foi feita extração integral de todos os bundles, dependências ou cada arquivo-fonte dos repositórios maiores.
- Não foi possível inspecionar valores de secrets, configurações internas de instalações de GitHub Apps, credenciais locais do GitHub Desktop nem o código interno do conector GitHub do ChatGPT. Nenhum segredo foi solicitado, lido ou registrado.
- Não foi executada CI porque nenhum código ou workflow foi alterado; não há novo run a declarar como aprovado.

## 6. Decisão e ações

**Decisão técnica:** não modificar código nem workflows nesta etapa. Não há incompatibilidade demonstrada nos arquivos inspecionados. Atualizar versões de actions, adicionar regex ou introduzir o cabeçalho temporário sem evidência criaria mudança desnecessária.

Manter:
- `GH_TOKEN: ${{ github.token }}` para GitHub CLI em Actions.
- `actions/checkout` para Git e publicação quando as permissões de workflow forem suficientes.
- Permissões mínimas declaradas por workflow.

Se um serviço Apoena passar a criar installation tokens por conta própria:
1. Tratar o token como string opaca; nunca exigir exatamente 40 caracteres.
2. Aceitar pelo menos 520 caracteres em armazenamento e transporte; evitar limite fixo pequeno.
3. Não truncar Authorization headers; verificar proxy/gateway e redaction de logs.
4. Preferir não decodificar/validar o JWT; se a validação de formato for inevitável, seguir a regex atualizada indicada pelo changelog oficial.
5. Testar os formatos stateless e clássico enquanto o cabeçalho temporário ainda estiver disponível; remover o cabeçalho antes de 2026-11-30.

**Estado final:** AUDITORIA ESTÁTICA CONCLUÍDA PARA O ESCOPO LISTADO; SEM CORREÇÃO DE CÓDIGO NECESSÁRIA; COBERTURA DE CÓDIGO-FONTE COMPLETO NÃO CERTIFICADA.
