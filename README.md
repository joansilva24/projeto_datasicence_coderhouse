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



## Modelo preditivo




## Autores do projeto:

João Silva [Linkedin](https://www.linkedin.com/in/joaonatadasilva)<br/>
Hugo Lima [Linkedin](https://www.linkedin.com/in/hugorodrigueslima/)

