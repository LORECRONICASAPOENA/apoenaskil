# Arquivo de conversa — governança documental da auditoria de segurança

**Data:** 2026-11-02  
**Projeto:** Apoena Game Creator  
**Tipo:** registro histórico e decisão de organização documental  
**Cobertura:** PARCIAL — baseado no conteúdo disponível nesta conversa e no dossiê histórico já armazenado.

## Sequência e conteúdo preservado

1. O histórico de auditoria de segurança da V4.1 foi recuperado por um dossiê fornecido pelo autor. O documento de origem declarou que o link compartilhado não expôs o texto, que anexos ZIP não foram integralmente extraídos e que cinco arquivos individuais foram examinados.
2. O dossiê registrou o contexto operacional: aplicação local em Windows, uso por equipe, compartilhamento via GitHub, GitHub Actions habilitado e distribuição por ZIP. A exigência de aprovação independente foi informada como ausente; proteção da branch main permaneceu desconhecida.
3. O dossiê identificou pontos de atenção em bridge entre janelas, protocolo da biblioteca, importação de backup, autenticidade do backup, validação de imagens e integridade de pacotes. Todos foram classificados como achados estáticos preliminares, sem exploração demonstrada.
4. A V4.2 Security Hardening foi apresentada como plano proposto, sem código, commit de correção ou release comprovados.
5. Em conversas posteriores, o autor reiterou a necessidade de preservar decisões, relatórios de erro do Actions e histórico de evolução do Game Creator.
6. O autor também definiu a evolução do produto para uma plataforma única com Estúdio 3D, Estúdio Pixel Art 2D e editor de mapas 2.5D, sem exclusão de funcionalidades existentes sem auditoria.
7. Foram registradas decisões de planejamento online: mundo híbrido, Android e PC e meta inicial de teste de 20–50 jogadores simultâneos. Isso é requisito de planejamento, não capacidade implementada.
8. Nesta conversa, foi proposta a separação entre dois repositórios:
   - **Apoena Skill:** memória central, histórico, decisões, conhecimento, proveniência e documentação transversal dos projetos.
   - **GameCreator:** documentação técnica operacional do editor, auditorias, achados, evidências, correções, testes, arquitetura e changelog técnico.
9. A regra foi aceita como padrão de organização: não duplicar no GameCreator a história narrativa, administrativa ou a memória geral. Registrar ali apenas decisões que afetam tecnicamente o editor.
10. O autor reforçou que não se deve declarar gravação, auditoria integral, correção ou validação sem evidência real.

## Decisão documental vigente

**Apoena Skill é a memória central do ecossistema Apoena. GameCreator é a documentação técnica do produto/editor.**

A separação não significa isolamento: GameCreator pode apontar para registros centrais do Apoena Skill quando a proveniência ou o histórico amplo forem necessários. O repositório técnico deve manter cópias operacionais de evidências e relatórios necessários para manutenção, sem reproduzir a memória geral.

## Estrutura documental adotada

Apoena Skill:
- apoena/docs/game-creator/ — conhecimento técnico contextual e ligações para documentação do produto.
- apoena/docs/game-creator/conversation-archive/ — registros de conversa, decisões e proveniência.
- apoena/docs/game-creator/security-audit/ — dossiês e recuperação histórica de auditorias.
- apoena/skills/apoena-gamecreator-engineering/SKILL.md — instruções reutilizáveis de engenharia.

GameCreator:
- docs/security/ — auditoria técnica, achados, plano de correção, evidências, backup/recuperação, segurança do GitHub e changelog de segurança.
- Código-fonte permanece nas pastas de implementação; documentos não substituem testes nem commits de código.

## Limites e pendências

- Não é transcrição literal integral de todos os turnos.
- O link original e anexos não recuperados continuam como lacunas.
- Os achados SEC-001 a SEC-007 precisam ser revalidados no commit atual do GameCreator.
- Nenhuma correção de segurança é declarada aplicada por este registro.
- Não houve cópia de código-fonte para Apoena Skill.
