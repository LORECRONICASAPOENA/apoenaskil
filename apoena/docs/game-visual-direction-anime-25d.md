# Direção visual do jogo Apoena — Anime 2,5D com assets 2D

Status: direção aprovada pelo criador em 04/11/2026. Orienta Amigo Apoena, Alberto e desenvolvimento futuro do GameCreator. Não afirma que os recursos já estejam implementados.

## Decisão central
O jogo mantém a identidade visual anime de Apoena. A apresentação é 2,5D, mas os elementos artísticos são imagens e sprites 2D de alta qualidade. Não usar pixel art tradicional pontilhada como estilo padrão e não exigir modelagem 3D.

## Câmera e profundidade
- Câmera oblíqua/isométrica fixa como recomendação inicial.
- Rotação a cada 90° não aprovada; requer autorização futura e assets direcionais específicos.
- Profundidade por perspectiva coerente, escala por posição, camadas, ordenação Y, oclusão, paralaxe, sombras e iluminação 2D.

## Direção de arte
- Anime 2D de alta qualidade, ilustração digital limpa, volume e acabamento pintado.
- Formas legíveis, paleta controlada, materiais reconhecíveis e detalhes refinados sem ruído.
- Minimalismo remove poluição visual, não reduz resolução ou qualidade.
- Não adicionar bandeiras, logos, brasões, textos, inscrições ou ornamentos sem necessidade/autorização.
- Preservar arquitetura e paletas das quatro tribos a partir das referências aprovadas.

## Pipeline de assets
Personagens, monstros, casas, árvores, florestas, rios, cachoeiras, pedras, pontes, objetos e efeitos devem ser PNGs/sprites 2D. Quando necessário, usar alpha real. Definir pivô/base, escala, colisão e camada de oclusão. Tilesets devem compartilhar perspectiva, luz, escala e acabamento.

## Responsabilidades esperadas do GameCreator
Planejado: importação e recorte de imagens; biblioteca de assets; composição de mapas por camadas; ordenação Y/oclusão; escala e pivôs; colisões; iluminação e sombras 2D; pré-visualização da câmera; exportação para Godot. Implementar em etapas pequenas após auditoria do estado atual do Creator.

## Separação de estilos
O Prompt Mestre 4.0 do mangá continua válido para a obra narrativa. Para o jogo, esta especificação é a autoridade visual específica. Não misturar automaticamente as regras de reprodução minimalista do mangá com o acabamento dos assets do jogo.

## Escopo desta mudança
Atualização documental das instruções do Amigo Apoena e criação desta especificação. Nenhum código de runtime, cena Godot, asset binário ou funcionalidade do GameCreator foi alterado nesta etapa.
