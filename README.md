# Modelo preditivo Para Obesidade
Este projeto faz parte da avaliação do curso de ciência de dados pela [Coderhouse](https://www.coderhouse.com/br/?pipe_source=google&pipe_medium=cpc&pipe_campaign=9&gad_source=1&gclid=Cj0KCQjwudexBhDKARIsAI-GWYUYzg8dR_WtLGYV_p8_UJTmY69zBdhG3IXT4KzinPfZG7pkEXDvs8gaAhWfEALw_wcB).<br/>
Dataset Utilizado para o projeto: [UC_Irvine_Machine_learning_Repository](https://archive.ics.uci.edu/dataset/544/estimation+of+obesity+levels+based+on+eating+habits+and+physical+condition)

## Introdução

Neste projeto abordamos como a condição física e hábitos alimentares contribuem para a obesidade. Para este projeto, utilizaremos dados de indivíduos do México, Peru e Colômbia. O nosso projeto tenta responder às seguintes perguntas: 

 
- Influência do vício em cigarro na saúde
- Qual é a propensão de jovens à obesidade em comparação com os idosos?
- Influência da tecnologia e do meio de transporte no sobrepeso 
- Metas mínimas para manter a qualidade de vida (atividade física, alimentação, consumo de bebidas, etc)
- Quais fatores mais contribuem para o desenvolvimento da obesidade (por exemplo, histórico familiar, consumo de alimentos calóricos, ou hábitos de transporte)?
- Identificar padrões de comportamento similares em relação à alimentação, atividade física, uso de tecnologia, nível de obesidade 



## Data Wrangling
Este dataset é formado por 17 colunas,e não contém valores nulos. Como o foco de nosso trabalho é utilizar um modelo preditivo de classificação, utilizaremos a variável **NObeyesdad** como ***target**.*

| Nome | Descrição |Resposta | Tipo |
| --- | --- | --- | --- |
Gender | Gênero | Masculino / Feminino |object
Age | Idade | Anos |float
Height | Altura  | metros |float64
Weight | Peso (em quilogramas) | kilogramas |float64
family_history_with_overweight | Possui um familiar que sofre ou sofreu com sobrepeso? | Sim / Não | object
FAVC | Você consome alimentos com alta calorias frequentemente? | Sim / Não| object
FCVC | Você costuma comer vegetais em suas refeições? | Nunca / Às vezes / Sempre | float
NCP | Quantas refeições principais você come por dia? | Entre 1 e 2 /  Três / Mais de três | float
CAEC | Você come alguma comida entre as refeições? | No / Às vezes / Frequentemente / Sempre | object
SMOKE | Você fuma? | Sim / Não | object
CH2O | Quanta água você bebe diariamente? | Menos de um litro / Entre 1L e 2L / Mais de 2L | float
SCC | Você monitora as calorias que você come diariamente? | Sim / Não | object 
FAF | Com que frequência você faz atividade física? | Eu não faço / 1 ou 2 dias / 2 ou 4 dias / 4 ou 5 dias | float
TUE |Quanto tempo você gasta em aparelhos tecnológicos como celulares, videogames, televisão, computador e outros? | 0-2 horas / 3-5 horas / Mais de 5 horas | float
CALC | Com que frequência você bebe álcool? | Eu não bebo / Às vezes / Frequentemente / Sempre | object
MTRANS | Qual meio de transporte você costuma usar? | Automóvel / Motocicleta / Bicicleta / Transporte público / Caminhada | object
NObeyesdad | Nível de obesidade | Abaixo do peso / Normal / Sobrepeso  I / Sobrepeso II / Obesidade I / Obesidade II / Obesidade III | object

Para conseguirmos construir um modelo preditivo e, ao mesmo tempo, manter uma versão limpa dos dados, dividimos o dataset em dois. No primeiro dataset, chamado de df1, fizemos a transformação dos dados qualitativos em quantitativos, e preservamos a integridade do segundo dataset, chamado de df2. Com a transformação, o dataset df1 ficou da seguinte forma:

| Nome | Tipo | Resposta |
| --- | --- | --- | 
| Smoker | Binary | 0 / 1 | 
| Alcohol | Int | 0 / 1 / 2 /3 |
| Food Bt Meals | Int | 0 / 1 / 2 /3 |
| Mobility | Int | 0 / 0 / 0.5 / 1 / 1 | 
| Obesity F | Binary | 0 / 1 | 
| Bad Food | Binary | 0 / 1 |
| Calories Control | Binary | 0 / 1 |

Como se pode perceber, foram feitas algumas alterações bem interessantes no dataset df1. Primeiro, mudamos alguns nomes para que houvesse um melhor entendimento do que cada coluna significa. Segundo, criamos uma escala de 0 a 1 para a variável "Mobility", onde 0 indica nenhuma mobilidade e 1 representa esforço físico no translado.

## Análise de Dados
Nesta etapa, realizamos algumas explorações analíticas por meio dos dados e obtivemos os seguintes insights:
- **Relação entre Altura, Peso e Gênero:** <br/>
Ao analisarmos os dados, podemos perceber que, quando comparados, os homens apresentam uma relação entre altura e peso maior do que as mulheres.<br/>

- **Proporção de Indivíduos com Histórico Familiar por Nível de Obesidade**:<br/>
Indivíduos com alto grau de sobrepeso e obesidade tendem a ter histórico familiar de sobrepeso. Com essa informação, podemos deduzir que a relação das pessoas com hábitos alimentares e cuidados físicos pode ter uma origem social, com a perpetuação de padrões existentes em seu círculo social.
.<br/>

- **Matriz de Correlação entre Variáveis Contínuas**<br/>Com a matriz de correlação, obtivemos os seguintes resultados:

    - Correlação positiva (0,5) entre altura e peso: Ao utilizarmos a fórmula do IMC (Índice de Massa Corporal), que é calculado como peso (kg) / altura (m)², observamos que ambas as variáveis estão relacionadas.

    - Correlação moderada (0,3) entre consumo de alimentos não saudáveis ("bad food") e peso: Isso indica que o hábito de consumir alimentos de baixa qualidade nutricional tende a influenciar o peso.

    - Correlação moderada (0,3) entre atividade física e altura: Uma possível hipótese é a necessidade de um maior gasto calórico conforme a altura aumenta. Isso sugeriria que pessoas mais altas tendem a ter um consumo calórico maior do que pessoas mais baixas.

- **Quantidade de Indivíduos por Nível de Obesidade - Gênero**<br/>
Ao avaliar a quantidade de indivíduos por nível de obesidade e gênero, constatamos que homens e mulheres apresentam valores muito próximos. No entanto, há uma exceção nos casos de obesidade tipo II e tipo III: enquanto os homens predominam na obesidade tipo II, as mulheres apresentam maior frequência na obesidade tipo III.<br/>

- **Distribuição de Frequência de Atividade Física**<br/>
Com essa análise, identificamos que, quanto maior o número de dias em que os indivíduos realizam atividade física, menor a propensão ao desenvolvimento de sobrepeso e obesidade. Essa análise refere-se aos dias úteis, considerando que muitas pessoas frequentam academias, por exemplo, antes ou após o trabalho.<br/>
- **Distribuições de variáveis qualitativas:**<br/>
 Ao realizarmos uma análise univariada das variáveis qualitativas, obtivemos os seguintes resultados:
    - **Histórico familiar com sobrepeso**: A maioria dos participantes tem histórico familiar de sobrepeso, totalizando 1.722.
    - **Frequência de consumo de comidas hipercalóricas**: A maior parte dos participantes consome comidas hipercalóricas, totalizando 1.844.
    - **Frequência de consumo de vegetais**: Entre os participantes, 1.985 responderam que consomem vegetais sempre ou às vezes.
    - **Número de refeições principais**: A maioria dos participantes, totalizando 1.446, afirmou fazer até três refeições por dia.
    - **Consumo de alimentos entre refeições**: 1.761 participantes relataram consumir alimentos entre as refeições.
    - **Fumante**: A maioria dos participantes afirmou que não fuma, totalizando 2.043.
    - **Consumo de água diariamente**: A maioria dos participantes consome entre 1L e 2L de água por dia, totalizando 1.107, o dobro do segundo maior grupo, com 502
    - **Monitoramento de consumo calórico**: 1.991 participantes afirmaram monitorar seu consumo calórico.
    - **Frequência de atividade física**: Entre os participantes, 1.473 relataram não praticar atividade física ou praticá-la entre uma e duas vezes por semana.
    - **Tempo de uso de dispositivos tecnológicos**: 1.844 participantes afirmaram passar entre duas e cinco horas utilizando dispositivos tecnológicos.
    - **Consumo de álcool**: Entre os participantes, 1.380 relataram consumir álcool com baixa frequência.
    - **Transporte usado**: A maior parte dos participantes afirmou utilizar transporte público, totalizando 1.558.
- **PCA**: Ao analisarmos o gráfico do PCA, podemos observar que, ao dividirmos a distribuição dos dados em dois agrupamentos, conseguimos explicar 43% dos dados analisados.

## Modelo Preditivo
### Ajustes dos Dados e Escolha do Modelo
Para a criação do nosso modelo preditivo, primeiro foi necessário realizar ajustes nos dados. Criamos um dataframe com as variáveis qualitativas ajustadas utilizando a função get_dummies. Posteriormente, adicionamos as variáveis quantitativas, também ajustadas. Como estamos trabalhando com um modelo preditivo supervisionado, foi necessário separar a variável target do conjunto de treinamento.

Para o nosso projeto, dividimos o dataset na proporção 80/20, sendo 80% dos dados destinados ao treinamento e 20% para o teste. Escolhemos quatro algoritmos de classificação para o nosso modelo: Regressão Logística, Árvore de Decisão, Floresta Aleatória e Support Vector Machine (SVM).

### Métricas de Avaliação do Modelo
Após o treinamento do modelo, foi necessário avaliar seu desempenho para identificar possíveis ajustes que poderiam melhorar sua performance. Dividimos a avaliação em duas partes: uma análise simples e outra utilizando um algoritmo de ajuste de hiperparâmetros.

#### Avaliação Simples
Para realizar uma avaliação preliminar do desempenho dos modelos, utilizamos a matriz de confusão para determinar a precisão e a acurácia de cada um.

Ao analisarmos os modelos, concluímos que a Floresta Aleatória apresentou o melhor desempenho para o nosso projeto. Apesar de a Regressão Logística e a Árvore de Decisão terem um recall e um F1-score muito altos, alguns fatores nos levaram a não escolher esses modelos:

- O primeiro fator é que, apesar de ser um algoritmo muito eficiente, a Regressão Logística retorna apenas valores binários, o que não é ideal para o nosso caso.

- O segundo fator é que, assim como a Regressão Logística, os valores de F1-score e recall da Árvore de Decisão estão muito próximos de 100%. Isso indica que o modelo pode estar superajustado e, portanto, pode não ser capaz de generalizar corretamente as predições quando novos dados forem adicionados.

### Avaliação por Hiperparâmetros
Para a avaliação por hiperparâmetros, utilizamos o GridSearch. Ao analisarmos os parâmetros dos modelos de Floresta Aleatória, Support Vector Machine e Árvore de Decisão, chegamos aos seguintes resultados:

- **Árvore de Decisão**:
    - criterion: entropy
    - max_depth: 5
    - max_leaf_nodes: 14
    - splitter: best
    - random_state: 42 (padrão)
    - Score obtido: 0,87
- **Floresta Aleatória**:
    - criterion: entropy
    - max_depth: 6
    - max_leaf_nodes: 14
    - n_estimators: 100
    - random_state: 42 (padrão)
    - Score obtido: 0,88

- **Support Vector Machine**:
    - C: 5
    - kernel: linear
    - Score obtido: 0,97

### Avaliação Cruzada
Na etapa final do nosso projeto, realizamos uma validação cruzada utilizando os parâmetros com melhor desempenho no GridSearch. O método escolhido para essa validação foi o K-Fold.<br/>
Com a avaliação cruzada, concluímos que o melhor algoritmo continua sendo a Floresta Aleatória, com 87% de acurácia. O pior resultado foi o do modelo SVM, com 98% de acurácia, o que indica um superajuste, reduzindo a capacidade de generalização do modelo.<br/>
Por fim, para permitir o uso futuro do modelo para predição, salvamos o arquivo em pickle com o nome modelo_treinado.


## Autores do projeto:

João Silva [Linkedin](https://www.linkedin.com/in/joaonatadasilva)<br/>
Hugo Lima [Linkedin](https://www.linkedin.com/in/hugorodrigueslima/)

