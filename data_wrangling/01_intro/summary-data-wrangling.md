# Resumo

<!-- GASSES CLEAN > DECOTE Define Code Test -->
# Gather (Coleta)
* Os passos de coleta variam de acordo com a fonte de dados e formato

# Assess (Avaliação)
## Pontos a serem avaliados 
* **Qualidade:** Dados sujos, com problemas, não padronizados
* **Organização:** Uma estrutura desorganizada dificulta o processo de análise. 
Assim, é importante que:
    1. Cada **coluna** represente uma **variável**
    2. Cada **linha** represente uma **observação**
    3. Cada **tabela** represente uma **unidade observacional**

## Tipos de avaliação
1. Avaliação visual por meio de uma aplicação. [Excel, Google Sheets, ...]
2. Avaliação por meio de programação. Utilizar, por exemplo, métodos como `head`, `tail` e `info` do Pandas.

# Clean (Limpeza)
## Tipos de limpeza
* **Manual** (recomendado apenas para ocorrências pontuais)
* **Programação** Identificação, tratamento e limpeza por meio de código

## Limpeza por meio de programação
1. **Definir:** Uma lista de tarefas de limpeza. Uma boa prática de instruções para uma futura reprodução e leitura da análise
2. **Codificar/Programar:** Converter a lista de tarefas de limpeza em código
3. **Testar:** Testar a limpeza do conjunto de dados com programação ou a utilização de recursos visuais

## Cópias originais
Uma boa prática é sempre fazer uma cópia original dos trechos originais dos dados antes de limpa-los

# Reavaliar e iterar
Após a limpeza, é importante uma reavaliação dos passos de **_data wrangling_** para certificar que se algo foi esquecido ou que possa ser melhorado.

# Armazenar
Se necessário, para um uso futuro, armazene o resultado alcançado
