# Direção visual do jogo Apoena — Anime 2,5D estilizado

**Decisão refinada pelo criador em 04/11/2026.** Esta especificação é a referência visual do jogo; não substitui as regras próprias do mangá.

## Identidade artística
Anime 2D estilizado, limpo, expressivo e colorido, com acabamento profissional de jogo. O criador prefere anime menos detalhista, não semirrealismo cinematográfico carregado.

- Cel shading/sombras suaves em blocos, contornos controlados e cores vibrantes.
- Personagens com expressões legíveis, proporções anime e detalhes seletivos.
- Cenários ricos em composição, arquitetura, vegetação, água e relevo, mas com superfícies simplificadas.
- Objetos e monstros com volumes claros, paleta harmoniosa e silhueta reconhecível.
- Priorizar detalhe de design, não microtextura.

## Evitar
Semirrealismo pesado, aparência fotográfica, excesso de textura em pele/tecido/cabelo, pontilhismo, dithering, ruído visual, excesso de ornamentos, bandeiras, logos, brasões e textos aleatórios.

## Apresentação 2,5D
O mundo é composto por imagens e sprites 2D de alta qualidade. Profundidade por perspectiva coerente, escala, camadas, ordenação Y, oclusão, paralaxe, sombras e iluminação 2D. Não exigir modelagem 3D.

Câmera oblíqua/isométrica fixa é a recomendação inicial. Rotação em passos de 90 graus não está aprovada.

## Consistência dos assets
Personagens, casas das quatro tribos, monstros, árvores, florestas, rios, cachoeiras, pedras, pontes e objetos devem compartilhar perspectiva, escala, paleta, direção de luz e nível de estilização. Manter alpha real nos PNGs quando necessário, pivôs e pontos de apoio adequados e metadados de colisão/oclusão quando aplicável.

## GameCreator — capacidades planejadas
Importação e recorte de imagens, biblioteca de assets, composição de mapas por camadas, ordenação Y/oclusão, escala e pivôs, colisões, iluminação/sombras 2D, pré-visualização da câmera e exportação para Godot. Isso é requisito planejado, não funcionalidade já validada.
