# Manifesto de extração — Game Creator / 2026-11-02

**Status global:** PARCIAL — registro documental, não transcrição integral certificada.  
**Repositório:** apoenalore/apoenaskil  
**Projeto documentado:** apoenalore/GameCreator  
**Versão histórica examinada:** V4.1  
**Commit de referência histórica:** 0bd916157d9bfab6c6c9b121c26050f94918cf80  
**Data do evento:** 2026-11-02; horários individuais somente quando preservados nas fontes.

## Fontes disponíveis e cobertura

| Fonte | Conteúdo | Cobertura / limite |
|---|---|---|
| Dossiê fornecido pelo autor sobre “Analisar segurança do repositório” | Cronologia, contexto operacional, cinco arquivos examinados, achados preliminares | Fonte secundária fornecida pelo autor; declara 24 turnos, link compartilhado sem texto recuperável e recuperação parcial |
| Histórico compartilhado do projeto historiaegeografia disponível no contexto | Decisões de arquitetura, auditoria organizacional, online, integração 2D/3D/2.5D e política de backup | Contexto compartilhado e checkpoints; não equivale à exportação integral de todas as conversas |
| Mensagens desta conversa de 2026-11-02 | Regra de separação Apoena Skill/GameCreator e estrutura documental proposta | Conteúdo direto disponível nesta conversa |
| Repositório GameCreator | Referência de código e documentação técnica | O commit V4.1 indicado é histórico; não prova que seja o HEAD atual |

## Materiais e anexos

- GameCreator-main (1).zip e Apoena-GameCreator-V4.1.zip: conteúdo interno não integralmente recuperado na conversa de origem.
- 1000066266.jpg e 1000066265.jpg: anexos mencionados; não reanalisados visualmente de forma independente no dossiê.
- Cinco arquivos-fonte descritos como examinados: index.html, asset-library.js, creator-bridge.js, library-backup.js e tileset-check.js.
- Não declarar auditoria dos 76 arquivos de runtime.
- Não declarar que binários, IndexedDB, assets locais ou backups do computador foram copiados para GitHub.

## Achados e classificação

- SEC-001 a SEC-007 permanecem históricos/preliminares e precisam ser revalidados no SHA atual.
- Não houve exploração demonstrada, teste dinâmico, incidente confirmado, teste de ransomware ou restauração comprovada.
- A V4.2 Security Hardening é proposta, não versão implementada.
- A PR #12 do GameCreator é documental no último estado observado; consultar seu estado atual antes de afirmar merge.

## Regras de preservação

1. Não apagar registros históricos quando uma conclusão mudar; acrescentar correção com fonte, data e commit.
2. Distinguir declaração do autor, evidência observada, hipótese, proposta e implementação verificada.
3. Manter o histórico acessível somente na medida em que as fontes realmente o disponibilizem.
4. Não preencher mensagens ausentes com reconstrução imaginada.
5. Para novas conversas, registrar data/hora, origem, cobertura, anexos, decisões, pendências e links para commits/PRs.
6. Apoena Skill é o arquivo central de conhecimento e proveniência; GameCreator recebe apenas documentação técnica operacional pertinente ao código/editor.
