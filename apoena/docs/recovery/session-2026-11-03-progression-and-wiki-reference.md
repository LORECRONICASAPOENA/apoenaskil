# Recuperação de conversa — referências de progressão e sistemas de jogo para Apoena

**Data:** 2026-11-03  
**Projeto:** Apoena / jogo AGAR  
**Tipo de registro:** derivado do conteúdo visível da conversa; não é transcrição integral  
**Cobertura:** parcial, restrita à mensagem com referências e à resposta de adaptação  
**Status:** estudo de design; nenhuma mecânica foi implementada ou declarada cânone  
**Origem:** pedido do autor para aproveitar o que for útil das referências, convertendo para o universo Apoena

## 1. Pedido do autor

O autor forneceu páginas de uma wiki de jogo e um texto de referência sobre progressão, XP, classificação, equipamentos e crescimento de personagem, com a instrução:

> VAMOS APLICAR OQ SERVIR MUDANDO PARA O UNIVERSO APOENA

Ao final, levantou a proposta de que cada nível exija **30% mais experiência que o nível anterior**:

> VAMOS IMAGINAR QUE A CADA NIVEL PRECISA DE +30% DE EXPERICENCIA DO NIVEL AANTERIOR ENTENDE?

A ideia da progressão de +30% foi expressamente apresentada pelo autor. A quantidade inicial de XP por nível, arredondamento, nível máximo da conta e recompensas ainda não foram definidos pelo autor.

## 2. Fontes externas fornecidas pelo autor

Estas URLs foram fornecidas na conversa como material de referência. O registro preserva os endereços; não declara que todos os detalhes atuais dessas páginas foram verificados:

- [EXP Potion Calculator](https://wiki.gla.com.br/EXP_Potion_Calculator)
- [Alianças](https://wiki.gla.com.br/Alian%C3%A7as)
- [Colosseum](https://wiki.gla.com.br/Colosseum)
- [Noland Tales](https://wiki.gla.com.br/Noland_Tales)
- [Items — Equipment](https://wiki.gla.com.br/Items#Equipment)

O autor também incluiu uma explicação de referência sobre League of Legends. Ela menciona, entre outros pontos: XP de conta obtida por partidas e missões; duração de partidas influenciando XP em PvP; bônus de primeira vitória a cada 20 horas; partidas contra bots como alternativa de progressão inicial; impulsionadores; requisitos de conta para ranqueadas; partidas de posicionamento; tiers/divisões; PDL; e MMR. Essas informações foram fornecidas pelo autor como material de comparação, não como regras a copiar para Apoena.

## 3. Conteúdo de design apresentado na mensagem

### XP e nível de conta
- XP pode ser obtida por partidas, missões e ações específicas.
- A duração da partida pode influenciar o ganho de XP em alguns modos.
- A mensagem de referência cita bônus de primeira vitória, bots e impulsionadores.
- A experiência acumulada pode liberar recursos e modos.

### Classificação competitiva
A referência de LoL descreve requisitos de acesso, posicionamento, tiers e divisões, pontos de liga e MMR oculto. Não foi decidido que Apoena usará nível 30, 16 campeões, Ferro–Desafiante, divisões IV–I, séries de promoção ou PDL.

### Progressão do personagem
A mensagem distingue:
- XP por monstros, missões, exploração e ações;
- marcos narrativos (*milestones*) em que a progressão vem da conclusão de um arco;
- progressão vertical por atributos;
- progressão horizontal por habilidades, talentos ou árvores;
- acesso a equipamentos com requisitos de nível.

### Curvas de XP citadas
A mensagem descreve três famílias:
1. Linear: XP cresce por uma quantidade fixa ou relação simples com o nível.
2. Exponencial/potência: XP cresce mais rapidamente nos níveis altos.
3. Tabela manual: valores definidos e balanceados por nível.

O ponto específico levantado pelo autor foi o aumento de 30% em relação ao custo de XP do nível anterior.

## 4. Formalização matemática — interpretação da proposta

Seja (X_n) o custo de XP para avançar do nível (n) ao próximo. A interpretação direta da proposta de +30% é:

\[
X_{n+1}=1{,}30\times X_n
\]

O primeiro custo (X_1) continua **indefinido**. Valores precisam ser arredondados de modo consistente para XP inteira; regra de arredondamento também não foi definida.

**Exemplo ilustrativo da resposta do assistente, não aprovado como parâmetro do autor:** usando (X_1=500), os primeiros custos aproximados seriam 500, 650, 845, 1.099, 1.428, 1.856, 2.413, 3.137, 4.079 e 5.302 XP. A escolha de 500 XP foi apenas um exemplo para visualizar a curva; não é decisão final.

A resposta anterior observou que uma curva composta de +30% fica exigente em níveis altos e que a taxa de XP das missões deve ser calibrada. Essa observação é análise de design, não especificação fechada.

## 5. Adaptações propostas para Apoena — ideias ainda não aprovadas

As adaptações abaixo foram sugeridas pelo assistente para converter os conceitos das referências em sistemas com identidade Apoena. Devem continuar rotuladas como propostas até decisão do autor.

### Calculadora de EXP / poções
- Mostrar XP atual, XP exigida para o próximo nível e quanto falta.
- Se houver poções de XP, calcular o efeito ou a quantidade necessária.
- Não presumir que a fórmula da página de referência corresponde ao jogo Apoena.

### Alianças
- Possível sistema de grupos/cooperativas com contribuição coletiva.
- Ideias de benefícios: melhorias de instalações, treinamento, pesquisa ou missões em grupo.
- Os nomes, recursos e benefícios devem ser adaptados ao universo Apoena, sem copiar literalmente a estrutura da referência.

### Coliseu / Arena de Agar
- Possível sequência de desafios contra IA, com etapas e recompensas por marcos.
- Chefes, desafios em equipe e checkpoints são possibilidades de design, não requisitos já aprovados.
- A identidade visual e a lore devem permanecer próprias de Agar.

### Noland Tales / exploração
- Possível inspiração para exploração de ruínas, enigmas, armadilhas, tesouros e descobertas.
- Adaptar a Agar, Pandora e Arkana somente quando compatível com o mapa e a história definidos pelo autor.

### Equipamentos
- A forja de Apoena pode organizar armas, armaduras, escudos, acessórios e consumíveis.
- Itens podem ter requisitos de nível e alterar atributos, desde que sejam balanceados e compatíveis com as regras do jogo.
- A proposta não define ainda lista final, preços, slots ou fórmulas de atributo.

## 6. Separação de progressões sugerida na resposta

O assistente recomendou tratar como sistemas distintos:
- **Nível permanente da conta:** progresso entre sessões.
- **Nível do personagem durante uma partida:** progresso temporário e reiniciado conforme as regras de partida já discutidas.
- **Classificação competitiva:** resultado em partidas ranqueadas, se esse modo for aprovado.

Essa separação é recomendação de organização de sistemas. Não registra uma decisão nova do autor nem substitui a progressão de partida já discutida.

## 7. Estado e limites

- O autor pediu para aproveitar o que servir e adaptar ao universo Apoena.
- O autor explicitou a ideia de +30% de XP por nível consecutivo.
- O valor inicial de XP, limites, desbloqueios, recompensas, modo ranqueado e curva da progressão temporária permanecem em aberto.
- A resposta do assistente incluiu sugestões; não houve confirmação subsequente de que todas foram aceitas.
- Nenhum código, cena, configuração, cânone narrativo ou repositório do jogo foi alterado nesta etapa.
- Este documento não substitui as fontes externas nem uma futura especificação de design aprovada.
