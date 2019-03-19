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

# Comandos úteis para avaliação programática
## DataFrame.[**`.head(n)`**](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.head.html#pandas.DataFrame.head): As primeiras `n` linhas do DataFrame 
## DataFrame.[**`.tail(n)`**](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.tail.html#pandas.DataFrame.tail): As últimas `n` linhas do DataFrame
## DataFrame.[**`.sample(n)`**](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sample.html#pandas.DataFrame.sample): Um exemplo aleatório de um eixo do Objeto
## DataFrame.[**`.info()`**](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.info.html#pandas.DataFrame.info): Resumo conciso do DataFrame
## DataFrame.[**`.describe()`**](): Estatísticas descritivas resumidas
## DataFrame.[**`.loc()`**](): Acessar um grupo de linhas e colunas por meio de labels ou lista booleana
```python
df = pd.DataFrame([[1, 2], [4, 5], [7, 8]],
      index=['cobra', 'viper', 'sidewinder'],
      columns=['max_speed', 'shield'])
df
```

|[index]           | max_speed | shield  |
| :---      | :---:     | :---:   |
|cobra      |        1  | 2       |
|viper      |        4  | 5       |
|sidewinder |        7  | 8       |

### Single label
```python 
df.loc['viper']

max_speed    4
shield       5
Name: viper, dtype: int64
```

### Lista de labels (Note using [[]] returns a DataFrame)
```python
df.loc[['viper', 'sidewinder']]

            max_speed  shield
viper               4       5
sidewinder          7       8
```
### Seleção de intervalos com labels para linha e uma única coluna. As mentioned above, note that both the start and stop of the slice are included.
```python
df.loc['cobra':'viper', 'max_speed']

cobra    1
viper    4
Name: max_speed, dtype: int64
```
> Vídeo explicativo do canal ['Data School'](https://www.youtube.com/watch?v=xvpNA7bC8cs)
>
> [Mais exemplos na documentação `.loc`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.loc.html#pandas.DataFrame.loc)


## DataFrame.[**`.iloc()`**](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.iloc.html#pandas.DataFrame.iloc): Seleção baseada no index como notação de lista
## DataFrame.[**`.duplicated()`**](): Revela as linhas duplicadas.
## Series.[**`.value_counts()`**](): Contagem de valores únicos
## [**bracket notation with/without indexing**]()

> Pandas API reference: https://pandas.pydata.org/pandas-docs/stable/api.html
Dados arrumados (Tidy data) é uma forma padrão de mapear o sentido/significado de um dataset em sua estrutura. Para um dataset ser bagunçado ou arrumado, depende em como suas linhas, colunas e tabelas são combinadas com as observações, variáveis e tipos. 

Um **dataset arrumado**:

1. Cada **variável** forma uma **coluna**
2. Cada **observação** forma uma **linha**
3. Cada tipo de **unidade de observação** forma uma **tabela**

> ### Original source
> Tidy data is a standard way of mapping the meaning of a dataset to its structure. A dataset is **messy** or **tidy** depending on how rows, columns and tables are matched up with observations, variables and types. 
> In **tidy data**:
> 1. Each **variable** forms a **column**
> 2. Each **observation** forms a **row**
> 3. Each type of **observational unit** forms a **table**
>
> More at informal [Tidy data paper](https://cran.r-project.org/web/packages/tidyr/vignettes/tidy-data.html)
>

