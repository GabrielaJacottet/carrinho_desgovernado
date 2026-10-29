# Carrinho Desgovernado

Jogo co-op em 3D, feito para jogar com a família no computador e no celular.
Um jogador é o **carrinho de supermercado**, que desce a ladeira quase sem freio. Os outros **correm atrás das compras** e arremessam tudo dentro do cesto. O caixa só libera quando a lista estiver completa.

## Como jogar
- Abra o `index.html` no navegador (Chrome, Edge, Safari ou Firefox atualizados).
- **Modo sozinho:** funciona em qualquer lugar. A tecla `Q` alterna entre ser o carrinho e ser quem corre.
- **Modo online (sala com código):** só funciona quando o jogo está publicado como artefato no claude.ai, porque usa o recurso de salas de lá.

### Controles
| Quem | Teclado | Celular |
|---|---|---|
| Quem corre | WASD/setas para correr, Espaço/E para ação (pegar, arremessar, colocar no carrinho) | Joystick à esquerda, botão **Ação** |
| Carrinho | WASD para andar, Espaço para frear, **Shift para turbo**, F para pular, R para buzinar, E para pegar da prateleira ou chacoalhar | Joystick, botões **Turbo**, Freio, Pulo, Buzina, Pegar |
| Câmera | `+` / `-` ou rodinha do mouse | Botões `+` e `−` |

## Fases
Mercadinho do Seu Juca, Hortifruti, Congelados, Festa infantil, Atacadão e Black Friday.
Cada fase tem uma missão especial: troca na padaria, depósito com dois botões ou prateleira alta. Também tem catástrofes (apagão, estouro de bichos, terremoto, sprinklers), ladrões, bônus e música que fica tensa nos últimos 15 segundos.

## Estrutura
```
index.html              jogo pronto (arquivo único, gerado)
src/template.html       interface, HUD, controles, sons, música, rede
src/sim.js              simulação do jogo (mapas, regras, NPCs, ladrões, eventos)
src/mini3d.js           motor WebGL próprio (sem bibliotecas)
src/models3d.js         modelos procedurais e montagem dos modelos importados
src/r3d.js              cenário 3D, câmera e desenho de cada quadro
src/modeldata.js        modelos 3D compactados (gerado por tools/build_models.py)
tools/build.py          junta src/ em index.html
tools/build_models.py   converte os pacotes de modelos (GLB/OBJ/FBX) em src/modeldata.js
tools/conv.py           leitores de GLB, OBJ e FBX binário
tools/simtest.js        teste da simulação sem navegador: node tools/simtest.js src/sim.js
```

### Gerar de novo
```bash
python3 tools/build.py                 # depois de editar algo em src/
python3 tools/build_models.py          # só se trocar os modelos (precisa da pasta assets/, ver abaixo)
```

## Créditos dos modelos
- [Kenney](https://kenney.nl): Food Kit, Furniture Pack e Mini Characters (CC0)
- [Quaternius](https://quaternius.com): Farm Animals (CC0)
- Pacote "Supermercado" (estante gôndola, freezer, ovos, café, suco, sabonete, leite). **Licença a confirmar antes de publicar.**

Os pacotes originais não estão no repositório. Para gerar os modelos de novo, extraia cada .zip em `assets/<nome-do-zip>/`, com os mesmos nomes de pasta usados em `tools/build_models.py`.
