# Backup técnico — recuperação CI do GameCreator / PR #14

**Estado:** IMPLEMENTADO E VALIDADO NO PR; ainda não integrado à `main` do GameCreator.  
**Registro:** 2026-11-03.  
**Fonte:** [apoenalore/GameCreator](https://github.com/apoenalore/GameCreator), PR [#14](https://github.com/apoenalore/GameCreator/pull/14).  
**Branch de origem:** `feat/apoena-modular-character-creator-integration`.  
**Commit de código validado:** `03382b02e74e2b39da0924bd0ff72ddacdf27e5a`.  
**Registro técnico de erros:** commit `16b477fcdc5550b292dad2f35e08bacc42b6ca17` na branch de origem.  
**GitHub Actions:** [run #41565001752](https://github.com/apoenalore/GameCreator/actions/runs/41565001752), evento `pull_request`, concluído `success` em 2026-11-03T02:17:55Z.

## O que este snapshot preserva

Cópia textual dos seis arquivos do GameCreator diretamente envolvidos nas correções e na validação da integração do Criador Modular:

| Caminho original no GameCreator | Caminho neste snapshot | Git blob SHA de origem |
|---|---|---|
| `.github/workflows/pixel-art.yml` | `source/.github/workflows/pixel-art.yml` | `395cb70d1363c392e08eae032194a55ca86533cf` |
| `pixel-art/personagens.js` | `source/pixel-art/personagens.js` | `f09267f5701d6908f55659e5774c6a276dbc656f` |
| `pixel-art/ponte-creator.js` | `source/pixel-art/ponte-creator.js` | `a045a226648e274033c9846c3a2235f3ea9e6e96` |
| `shared/asset-library.js` | `source/shared/asset-library.js` | `7027820e2c55298a73fa6467f72dceee15eb790a` |
| `tests/creator-bridge.test.cjs` | `source/tests/creator-bridge.test.cjs` | `75fd45c42cc7889a53f3cf0638dd78d3bf76a051` |
| `tests/personagens-browser.html` | `source/tests/personagens-browser.html` | `9b5e9b8272f0e2d59186606f62e0d840b95906e4` |

Os Git blob SHAs da cópia conferem com os da origem; os arquivos foram copiados sem transformação.

## Causa e correções registradas

1. O workflow era acionado por `push` e `pull_request` para o mesmo branch, compartilhando um grupo de concorrência que cancelava os jobs duplicados. O gatilho `push` foi limitado à branch `main`; branches de trabalho seguem validadas pelo evento da PR.
2. Um run intermediário falhou no teste funcional do navegador ao aguardar a conclusão das ações assíncronas do editor. O hook de teste passou a sinalizar o estado ocioso somente quando o contador de operações pendentes chega a zero.
3. O limite de manifesto da ponte com o Creator foi ajustado para aceitar o manifesto de pixel art maior, com cobertura do contrato em `tests/creator-bridge.test.cjs`.
4. O teste funcional usa um host em memória para a ponte da biblioteca. A persistência IndexedDB real foi verificada separadamente no mesmo workflow pelo teste dedicado da biblioteca.

## Validação observada

O run #41565001752 passou build nativo, smoke test do navegador, sintaxe JavaScript, teste de modelo do Criador Modular, teste funcional no navegador, exportação pixel-perfect, encaixe de tilesets, biblioteca/IndexedDB, backup/restauração, catálogo e contrato Godot, integração, manifesto do atualizador, hidrologia/erosão, runtime Godot 4 e preservação dos módulos. O teste opcional de sintaxe Python foi ignorado porque o runner não tinha Python instalado.

## Limites

- Este é um snapshot parcial de código para continuidade técnica; não é uma cópia integral do GameCreator.
- A PR #14 continua aberta em draft; o resultado não representa integração na `main`.
- A validação do editor/contratos não prova que os assets exportados já sejam consumidos pelo runtime do jogo.
- Este snapshot no GitHub não substitui uma cópia independente/offline nem um teste de restauração.
- Não contém saves do usuário, credenciais, dados locais do runner ou dependências instaladas.

