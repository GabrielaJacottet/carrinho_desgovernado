# Carrinho Desgovernado: instruções para o Claude

## Economize tokens (regra principal)
- Não leia arquivos inteiros sem necessidade: use grep e leia só os trechos que vai mudar. `src/modeldata.js` e `index.html` são enormes e gerados, então nunca leia esses dois.
- Prefira edições pequenas e pontuais, sem reescrever arquivos.
- Gere screenshots/imagens só quando for indispensável para checar o visual.
- Respostas curtas: diga o que mudou, sem recapitular o processo.
- Não gere desenhos conceituais sem o usuário pedir.

## Como o projeto funciona
- Edite só em `src/` e rode `python3 tools/build.py` para gerar `index.html`.
- `src/sim.js` é determinística e roda no anfitrião. Os clientes recebem o estado empacotado (`packGame`) via presença da sala, que tem limite de cerca de 4KB, então mantenha o pacote abaixo de uns 2.9KB. Confira com `node tools/simtest.js src/sim.js`.
- Renderização 3D: motor próprio em `src/mini3d.js`. Primitivas com nome `@modelo` vêm de `src/modeldata.js`, e `hasModel()` diz se o modelo carregou.
- Sem WebGL, o jogo cai automaticamente no renderizador 2D antigo, que fica em `src/template.html`.
- Idioma da interface: português do Brasil.
