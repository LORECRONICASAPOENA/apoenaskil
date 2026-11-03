# Backup — Integração do Criador Modular no Pixel Art (GameCreator)

**Registro:** 2026-11-03  
**Projeto:** Apoena / GameCreator  
**Estado:** requisito registrado; integração visual ainda não validada no computador do usuário.

## Intenção original do usuário

O usuário pediu que o novo gerador/criador de personagens fosse integrado e testado e, especificamente, que ficasse no lugar do editor que atualmente aparece em Pixel Art. A expectativa visual, esclarecida após o resultado frustrante, é que o criador novo apareça na própria área de edição, sobre/substituindo o personagem/editor antigo que está visível, sem exigir que o usuário navegue até outro arquivo, abra outra janela ou faça etapas técnicas para encontrar o protótipo.

## Falha de comunicação e de execução

Foi respondido que a integração havia sido feita, mas a captura enviada pelo usuário mostrou a interface antiga ainda aberta. A orientação posterior para trocar branch e reabrir um HTML local transferiu ao usuário o trabalho de localizar a implementação e não resolveu a necessidade. Não considerar integração concluída só porque uma branch/PR ou arquivo de protótipo existe.

## Requisito funcional/visual obrigatório

1. Manter a navegação e o contexto atuais do GameCreator.
2. Dentro da aba Pixel Art, renderizar o Criador Modular diretamente no espaço de trabalho do editor antigo — no mesmo painel/área onde aparece o personagem/editor atual.
3. O novo criador deve ser a interface efetivamente carregada e utilizável, não apenas uma rota, protótipo separado, iframe com caminho quebrado ou página que existe sem estar conectada ao fluxo.
4. Não deixar o editor antigo sobreposto, atrás, nem como conteúdo principal. Se houver necessidade de preservar funcionalidades antigas, mantê-las fora da área principal ou como fallback explicitamente indicado, não como a visualização padrão.
5. Verificar caminho relativo de assets e scripts, inicialização, tamanho responsivo do painel e compatibilidade com execução local file:// e com o modo de servidor/build usado pelo projeto.
6. A integração precisa estar visível no primeiro acesso à aba Pixel Art, sem pedir ao usuário para selecionar uma branch, localizar arquivo ou fazer setup manual específico.
7. Preservar as abas de Objetos/Mapas e os demais fluxos existentes, sem regressões.

## Critérios de aceitação (antes de declarar pronto)

- [ ] Abrir o GameCreator na entrada habitual e ir à aba Pixel Art.
- [ ] O criador modular aparece no painel do editor antigo, no lugar da interface/personagem anterior.
- [ ] Controles de criação e edição respondem; console sem erros críticos; nenhum recurso com URL/path 404.
- [ ] Testado no mesmo modo de execução que o usuário usa, incluindo a abertura local mostrada na captura.
- [ ] Conferir que a área de Pixel Art não diminui/reflow de forma inesperada e que o criador não aparece em uma janela separada.
- [ ] Captura de tela ou evidência de teste documentada.
- [ ] Informar honestamente o que foi implementado e o que ainda depende de teste do usuário.

## Contramedidas para próximos trabalhos

- Antes de editar, abrir o repositório e rastrear a página de entrada, o componente/painel da aba Pixel Art e o editor atual.
- Não assumir que integrar significa adicionar iframe ou criar página independente. Confirmar o destino no fluxo existente.
- Fazer inspeção do código e diff; executar checks/build disponíveis e verificar caminhos/assets.
- Manter um checklist de validação visual e funcional.
- Não declarar feito sem testar a entrada real usada pelo usuário. Se não houver execução local disponível, marcar como implementação pendente de validação, não como concluída.
- Quando o usuário disser que não funciona, priorizar diagnóstico da tela e do código/branch conectados, sem simplesmente repassar etapas de atualização para o usuário.

## Referência da conversa

O usuário esclareceu: “mais pq vc não colocou ele pra aparece em cima desse cara não entendi nada”. Isso define o alvo de integração: o novo criador precisa aparecer exatamente no lugar/área do editor antigo visível.