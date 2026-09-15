# graficosUX

Análise exploratória de respostas sobre adoção de animais, perfil dos participantes e contexto de moradia. O projeto reúne os dados brutos, notebooks em Python, visualizações e um visualizador dos prompts usados com a IA.

## Arquivos principais

- [`animal.csv`](animal.csv): base de respostas utilizada nas análises. O arquivo é separado por `;` e foi lido com codificação `latin-1`.
- [`Perfis.ipynb`](Perfis.ipynb): notebook com o fluxo de limpeza, normalização, criação dos perfis e gráficos.
- [`../teste.ipynb`](../teste.ipynb): versão alternativa do notebook, localizada na pasta raiz do workspace.
- [`index.html`](index.html): visualizador interativo do histórico de prompts e respostas da IA.
- [`copilot_all_prompts_2026-09-15T22-40-58.json`](copilot_all_prompts_2026-09-15T22-40-58.json): exportação do log usado pelo visualizador.

## Como reproduzir as análises

1. Abra `Perfis.ipynb` no VS Code com a extensão Jupyter instalada.
2. Selecione um ambiente Python com `pandas`, `numpy` e `matplotlib` instalados.
3. Execute as células em ordem.

O tratamento realizado pelo notebook inclui:

- leitura da base e remoção de colunas que não entram na análise;
- conversão da idade para número e preenchimento de valores ausentes pela mediana;
- preenchimento de categorias vazias como `Não informado`;
- transformação das respostas categóricas com one-hot encoding;
- padronização z-score das variáveis codificadas;
- agrupamento de respostas para comparar perfis, experiência de adoção e tipo de moradia.

## Análises e insights

### Perfil geral

O notebook encontrou 28 respostas válidas. A separação automática por uma pergunta categórica escolheu a pergunta de gênero, formando os grupos `Masculino` (15 pessoas, idade média de 29,6 anos) e `Femenino` (13 pessoas, idade média de 27,5 anos). Em ambos os grupos, as respostas mais frequentes indicam apartamento, moradia com familiares, presença de animais e experiência anterior de adoção.

Essa divisão serve para descrever a amostra, mas não deve ser interpretada como uma explicação de comportamento. A escolha do grupo é automática e depende das respostas disponíveis na base.

### Experiência com adoção

- `Adotante experiente`: 20 pessoas, idade média de 28,4 anos; 75% têm animais.
- `Interessado sem experiência`: 4 pessoas, idade média de 23 anos; 50% têm animais.
- `Sem interesse`: 4 pessoas, idade média de 35 anos; 25% têm animais.

O principal sinal é que a experiência com adoção concentra a maior parte da amostra e aparece associada, neste conjunto de respostas, a uma maior proporção de pessoas com animais. Como os grupos têm tamanhos diferentes e os dados são observacionais, isso é uma associação descritiva, não uma relação de causa e efeito.

### Comportamento e resgate

- 18 pessoas declararam ter animais de estimação e 10 não têm.
- 20 já adotaram um animal, 4 têm interesse mas nunca tentaram e 4 não têm interesse.
- Apenas 1 pessoa declarou que resgata, cuida ou encaminha animais; 23 responderam que não e 4 não informaram.

O cruzamento sugere que a base representa principalmente adotantes ou potenciais adotantes, e não pessoas atuantes em resgate. Por isso, conclusões sobre necessidades de protetores devem ser tratadas como lacuna de pesquisa, não como resultado consolidado.

### Moradia e presença de animais

- `Apartamento`: 17 pessoas; 9 têm animais (52,9%).
- `Casa com quintal`: 9 pessoas; todas têm animais (100%).
- `Casa sem quintal`: 2 pessoas; nenhuma tem animais (0%).

Entre casa com pátio e apartamento, foi observada uma diferença de 47,1 pontos percentuais na proporção de pessoas com animais. O resultado é um bom ponto de partida para investigar restrições de espaço e critérios de adoção, mas o grupo de casa sem pátio tem somente 2 pessoas e a amostra não é suficiente para generalizar o achado.

## Como abrir o log da conversa com a IA

O histórico exportado está em [`copilot_all_prompts_2026-09-15T22-40-58.json`](copilot_all_prompts_2026-09-15T22-40-58.json) e pode ser visualizado pelo [`index.html`](index.html).

1. Abra `index.html` no navegador. No VS Code, use **Open with Default Browser** ou clique duas vezes no arquivo pelo Explorador de Arquivos.
2. Clique em **Carregar Arquivo JSON**.
3. Selecione `copilot_all_prompts_2026-09-15T22-40-58.json` na mesma pasta.
4. Use a busca para localizar perguntas sobre insights, gráficos ou interpretação dos dados.
5. Deixe ativado o filtro **Ocultar telemetria interna (Ghost/NES)** para mostrar apenas as interações da conversa.

O visualizador permite navegar pelos turnos, ler as respostas formatadas em Markdown e copiar uma versão limpa em Markdown. Ele funciona localmente no navegador e não altera o arquivo JSON.

## Limitações

- A análise usa apenas 28 respostas e pode não representar a população estudada.
- As categorias dependem da forma como cada participante respondeu ao questionário.
- Percentuais de grupos pequenos podem variar muito com poucas respostas adicionais.
- Os insights devem orientar novas perguntas e decisões de UX, não substituir uma validação com uma amostra maior.
