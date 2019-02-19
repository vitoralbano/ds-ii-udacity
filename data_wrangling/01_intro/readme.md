# Introdução a Data Wrangling

Composto pelas etapas de Coleta, Avaliação e Limpeza, o Data Wrangling é importante para que os dados estejam organizados, preparados e limpos para que se dê início a sua análise.

## 1. Gather (Coleta)
Carregar os dados de forma automatizada de forma que minimize ao máximo o trabalho de quem possa vir a executar sua análise é uma boa prática.
> Acessando os dados programaticamente, seja buscando-os na web ou extraindo de um arquivo zip

Após a configuração e carregamento dos dados se da início a próxima etapa, a de avaliação (assess) dos dados.

## 2. Assess (Avaliação)
A Avaliação consiste em identificar a qualidade dos dados e sua organização. Dados de baixa de qualidade são sujos e dados de desordenados estão bagunçados.
A qualidade dos dados é uma percepção ou avaliação de possíveis adequações dos dados para que atendam ao propósito de determinado contexto/aplicação. Em outras palavras, não há regras rigorosas para a qualidade dos dados. Um conjunto de dados pode apresentar uma alta qualidade para um determinado contexto, mas baixa qualidade para outro.

Nesta etapa é importante a identificação, por exemplo: 
* falta de dados como valores nulos;
* dados inválidos, valores negativos em contextos não aplicaveis (ex: altura, peso, distância, etc);
* dados imprecisos, valores que não representam a realidade que supostamente os dados deveriam representar;
* dados inconsistentes, diferentes tipos de unidades para uma mesma coluna (ex: metros, centímetros, polegadas, etc)
* organização dos dados;

## 3. Clean (Limpeza)
Melhorar a qualidade dos dados não é o mesmo de altera-los, o que é uma fraude, essa transformação dos dados consiste em:
* cada variável seja uma coluna;
* cada observação seja uma linha;
* cada unidade de observação seja uma tabela;

O processo de limpeza por meio de programação pode ser dividido em três etapas, **definir**, **código** e **testar**;
### 1. Definir
Definir por escrito um plano de limpeza, explicitando tarefas de limpeza. Estas tarefas irão auxiliar em um segundo momento as pessoas que ver a análise e ou reproduzi-la.

### 2. Código
Implementar as tarefas definidas em código e executa-las.

### 3. Testar
Certificar que as adaptações da limpeza funcionaram.

# Wrangling x EDA x ETL
> **EDA** (Exploratory Data Analysis): 
Uma abordagem de análise que foca na identificação de padrões gerais nos dados, e na identificação de **_outliers_** e características dos dados que podem não ter sido antecipadas.

## Data Wrangling 
Se trata da coleta dos pedaços certos dos dados, a avaliação de sua qualidade e estrutura e, depois, iterar os seus dados para limpa-los. Essas avaliações e operações de limpeza, no entanto, não deixam a análise ou modelo melhor. O objetivo é torná-las possíveis, ou seja, funcionais.

## EDA (Exploratory Data Analysis)
Consiste na exploração dos dados de modo a **maximizar o potencial** de nossas análises, visualizações e modelos. Durante a exploração, visualizações simples são frequentemente usadas para resumir as principais características de seus dados. A partir disso você pode tratar pontos como **_outliers_** e criar recursos novos e mais descritivos dos dados existentes, também conhecidos como [**_feature engineering_**](https://en.wikipedia.org/wiki/Feature_engineering). Ou detectar e remover **_outliers_** para que seu modelo se adeque melhor.

## ETL (Extract-transform-load)
O **ETL** difere do **data wrangling** de três maneiras:
1. Os usuários são diferentes
2. Os dados são diferentes
3. os casos de utilização são diferentes

> [Data wrangling x ETL - What's the difference?](https://tdwi.org/articles/2017/02/10/data-wrangling-and-etl-differences.aspx)