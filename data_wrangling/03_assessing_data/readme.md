# Avaliação dos dados (Assessing data)

# Dimensões de qualidade de dados

As **dimensões de qualidade de dados**, que podem variar por autor, servem como um auxílio no processo avaliação e também limpeza dos dados. Apesar de suas variações, as quatro dimensões abaixo cobrem as principais:

## Integridade (Completeness)
Estão presentes todos os registros e colunas necessárias? Há registros faltando? Há linha específicas, colunas ou células faltando? 

## Validade (Validity)
Os registros presentes são válidos, eles conformam a um esquema definido? Um esquema é um conjunto definido de regras para os dados. Regras que podem representar restrições do mundo real (ex: Altura negativa é impossível) e restrições da tabela (ex: Chave única de identificação).

## Acuracidade (Accuracy)
Dados incorretos, são dados errados porém válidos. Respeitam as restrições do esquema, mas não representam a realidade. (ex: Medidas que não condizem com o fato representado, mais ou menos pesado, etc).

## Consistência (Consistency)
Dados formatados de forma não padronizada. Dados diferentes representando a mesma informação. (ex: Variações de uso, como sigla de estados e nome do estado na mesma coluna)

> # Comandos úteis para avaliação programática
> * [**`.head([n])`**](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.head.html#pandas.DataFrame.head): As primeiras `n` linhas do DataFrame 
> * [**`.tail([n])`**](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.tail.html#pandas.DataFrame.tail): As últimas `n` linhas do DataFrame
> * [**`.sample([n])`**](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sample.html#pandas.DataFrame.sample): Um exemplo aleatório de um eixo do Objeto
> * [**`.info()`**](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.info.html#pandas.DataFrame.info): Resumo conciso do DataFrame
> * [**`.describe()`**](): 
> * [**`.value_counts()`**]():
> * [**`.loc()`**]():
> * [**`.iloc()`**]():
> * [**bracket notation with/without indexing**]()
>
> Pandas API reference: https://pandas.pydata.org/pandas-docs/stable/api.html