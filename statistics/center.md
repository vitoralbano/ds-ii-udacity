<a id="tendencia-central"></a>
# Medidas de tendência central
Há três medidas de tendência central:
1. [`Média` - *Mean*](#media)
2. [`Mediana` - *Median*](#mediana)
3. [`Moda` - *Mode*](#excecoes)

<a id="media"></a>
# Média - *Mean*
Frequentemente chamada de **valor esperado** na matemática. Calcula-se a média adicionando todos os nossos valores e dividindo o resultado pelo número de valores do conjunto de dados.

<a id="mediana"></a>
# Mediana - *Median*
A **mediana** divide o conjunto de dados de forma que 50% dos valores sejam menores e os outros 50%, maiores.

## Mediana para valores ímpares
Para um conjunto de dados com uma quantidade **ímpar** (*odd*), a **mediana** é simplesmente o número no meio do conjunto. 

Ex: Em  um conjunto de 5 valores, a terceira posição é a mediana. 
[1, 2, **3**, 4, 5]

## Mediana para valores pares
Em um conjunto de dados com um número **par** (*even*) de observações, a **mediana** é a **média de dos dois valores do meio**.

Ex: [1, 2, 3, **4, 6**, 8, 9, 10]
* [4, 6] = (4 + 6) / 2
* 10 / 2 = **5**

Mediana = 5

## Média ou Mediana
Para usar a média ou mediana para descrever o conjunto de dados é preciso analisar a **forma** do conjunto de dados e a existência de **exceções** (*outliers*).

<a id="Moda"></a>
# Moda - *Mode*
A **moda** é o valor mais frequente observado no conjunto de dados.

Podem existir varias modas para um conjunto de dados em particular ou nenhuma moda.

## Sem moda
Se todas as observações do conjunto de dados possuem a mesma frequência, não há moda. 

Ex: 1, 1, 2, 2, 3, 3, 4, 4

## Muitas modas
Se dois (ou mais) números compartilham o valor máximo de frequência, então há mais de uma moda.

Ex: 1, 2, **3, 3, 3**, 4, 5, **6, 6, 6**, 7, 8, 9

`[3, 6]` representam a moda do conjunto pois aparecem com a mesma frequência, três vezes, enquanto que os demais aparecem apenas uma vez.