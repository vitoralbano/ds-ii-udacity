# ERD (Entity Relationship Diagram)
![ERD](erd.png)

# 8. Quiz: Relacionamento entre chaves primárias e estrangeiras
### 1. Tente puxar todos os dados da tabela accounts, e todos os dados da tabela orders.
```sql
SELECT *
FROM accounts
	JOIN orders
    ON orders.account_id = accounts.id
    
```

### 2. Tente puxar standard_qty, gloss_qty e poster_qty da tabela orders, e o site e o primary_poc da tabela accounts.
```sql
SELECT accounts.website, 
    accounts.primary_poc, 
    orders.standard_qty, 
    orders.gloss_qty, 
    orders.poster_qty
FROM accounts
JOIN orders
    ON orders.account_id = accounts.id
```    

# 11. Quiz: JOINS (parte 01)
### 1. Forneça uma tabela com todos os web_events associados com o name (nome) de conta do Walmart. Deve haver três colunas. Tenha certeza de incluir a primary_poc, o horário do evento e o channel (canal) para cada evento. Além disso, você pode escolher adicionar uma quarta coluna para garantir que apenas eventos do Walmart sejam escolhidos.

```sql
SELECT ac.name, 
    ac.primary_poc,
    event.occurred_at,
    event.channel
FROM web_events event
JOIN accounts ac
    ON event.account_id = ac.id
WHERE LOWER(ac.name) LIKE 'walmart';
```

### 2. Forneça uma tabela que dê a region (região) para cada sales_rep (representante de vendas) junto de suas respectivas accounts (contas). Sua tabela final deve incluir três colunas: o nome da região, o nome do representante de vendas e o nome da conta. Organize as contas alfabeticamente (A-Z) de acordo com os nomes das contas.

```sql
SELECT region.name AS region_name,
    rep.name AS rep_name,
    ac.name AS ac_name
FROM region
JOIN sales_reps rep
    ON rep.region_id = region.id
JOIN accounts ac
    ON ac.sales_rep_id = rep.id
ORDER BY ac.name;
    
```

### 3. Forneça o nome de cada região de cada pedido, bem como o nome da conta e o preço da unidade que pagaram (total_amt_usd/total) para o pedido. Sua tabela final deve ter 3 colunas: nome da região, nome da conta e preço da unidade. Algumas contas tem 0 como total, então eu dividi por (total + 0.01) para assegurar que não dividiríamos por zero.

```sql
SELECT
    region.name AS region_name,
    ac.name AS account_name,
    (orders.total_amt_usd / (orders.total + 0.01)) AS unit_price
FROM orders
JOIN accounts ac
    ON ac.id = orders.account_id
JOIN sales_reps rep
    ON rep.id = ac.sales_rep_id
JOIN region
    ON region.id = rep.region_id
   
```

# 19 . Quiz: Última verificação
### 1. Forneça uma tabela que dê a region (região) para cada sales_rep (representante de vendas) junto de suas respectivas accounts (contas). Desta vez apenas para a região Midwest. Sua tabela final deve incluir três colunas: o nome da região, o nome do representante de vendas e o nome da conta. Organize as contas alfabeticamente (A-Z) de acordo com os nomes das contas.

```sql
SELECT region.name region_name,
	rep.name rep_name,
    ac.name account_name
FROM sales_reps rep
JOIN region 
	ON rep.region_id = region.id
	AND region.name = 'Midwest'
JOIN accounts ac
	ON ac.sales_rep_id = rep.id
ORDER BY ac.name;
```

### 2. Forneça uma tabela que dê a region (região) para cada sales_rep (representante de vendas) junto de suas respectivas accounts (contas). Desta vez apenas para contas onde o representante de vendas tem um primeiro nome começando com S e na região Midwest. Sua tabela final deve incluir três colunas: o nome da região, o nome do representante de vendas e o nome da conta. Organize as contas alfabeticamente (A-Z) de acordo com os nomes das contas. 

```sql
SELECT region.name region_name,
	rep.name rep_name,
    ac.name account_name
FROM sales_reps rep
JOIN region 
	ON rep.region_id = region.id
	AND region.name = 'Midwest'
    AND rep.name LIKE 'S%'
JOIN accounts ac
	ON ac.sales_rep_id = rep.id
ORDER BY ac.name;
```

### 3. Forneça uma tabela que dê a region (região) para cada sales_rep (representante de vendas) junto de suas respectivas accounts (contas). Desta vez apenas para contas onde o representante de vendas tem um sobrenome começando com K e na região Midwest. Sua tabela final deve incluir três colunas: o nome da região, o nome do representante de vendas e o nome da conta. Organize as contas alfabeticamente (A-Z) de acordo com os nomes das contas. 

```sql
SELECT region.name region_name,
	rep.name rep_name,
    ac.name account_name
FROM sales_reps rep
JOIN region 
	ON rep.region_id = region.id
	AND region.name = 'Midwest'
    AND rep.name LIKE 'K%'
JOIN accounts ac
	ON ac.sales_rep_id = rep.id
ORDER BY ac.name;
```

### 4. Forneça o nome de cada região de cada pedido, bem como o nome da conta e o preço da unidade que pagaram (total_amt_usd/total) para o pedido. No entanto, você deve fornecer os resultados apenas se a standard order quantity (quantidade de pedido de padrão) exceder 100. Sua tabela final deve ter 3 colunas: nome da região, nome da conta e preço da unidade. A fim de evitar uma divisão por zero erro, adicionar .01 ao denominador aqui é útil total_amt_usd/(total+0.01). 


```sql
SELECT region.name region_name,
    ac.name account_name,
    orders.total_amt_usd / (orders.total + 0.01) unit_price
FROM orders
JOIN accounts ac
	ON orders.account_id = ac.id
    AND orders.standard_qty > 100
JOIN sales_reps rep
	ON ac.sales_rep_id = rep.id
JOIN region 
	ON rep.region_id = region.id;
```

### 5. Forneça o nome de cada região de cada pedido, bem como o nome da conta e o preço da unidade que pagaram (total_amt_usd/total) para o pedido. Contudo, você deve fornecer os resultados apenas se a standard order quantity (quantidade de pedido de padrão) exceder 100 e a poster order quantity (quantidade de pedido de pôster) exceder 50. Sua tabela final deve ter 3 colunas: nome da região, nome da conta e preço da unidade. Classifique pelo menor unit price (preço de unidade) primeiro. A fim de evitar uma divisão por zero erro, adicionar .01 ao denominador aqui é útil total_amt_usd/(total+0.01). 

```sql
SELECT region.name region_name,
    ac.name account_name,
    orders.total_amt_usd / (orders.total + 0.01) unit_price
FROM orders
JOIN accounts ac
    ON orders.account_id = ac.id
    AND orders.standard_qty > 100
    AND orders.poster_qty > 50
JOIN sales_reps rep
    ON ac.sales_rep_id = rep.id
JOIN region 
    ON rep.region_id = region.id;
```

### 6. Forneça o nome de cada região de cada pedido, bem como o nome da conta e o preço da unidade que pagaram (total_amt_usd/total) para o pedido. Contudo, você deve fornecer os resultados apenas se a standard order quantity (quantidade de pedido de padrão) exceder 100 e a poster order quantity (quantidade de pedido de pôster) exceder 50. Sua tabela final deve ter 3 colunas: nome da região, nome da conta e preço da unidade. Classifique pelo maior unit price (preço de unidade) primeiro. A fim de evitar uma divisão por zero erro, adicionar .01 ao denominador aqui é útil total_amt_usd/(total+0.01). 

```sql
SELECT region.name region_name,
    ac.name account_name,
    orders.total_amt_usd / (orders.total + 0.01) unit_price
FROM orders
JOIN accounts ac
	ON orders.account_id = ac.id
    AND orders.standard_qty > 100
    AND orders.poster_qty > 50
JOIN sales_reps rep
	ON ac.sales_rep_id = rep.id
JOIN region 
	ON rep.region_id = region.id
ORDER BY unit_price DESC;  
```

### 7. Quais são os diferentes channels (canais) usados pela account id 1001? Sua tabela final deve ter apenas 2 colunas: account name e os diferentes channels. Você pode experimentar SELECT DISTINCT para restringir os resultados a apenas valores únicos.

```sql
SELECT DISTINCT ac.name,
	 event.channel
FROM accounts ac
JOIN web_events event
	ON event.account_id = ac.id
    AND ac.id = 1001;
```

### 8. Encontre todos os pedidos feitos em 2015. Sua tabela final deve ter 4 colunas: occurred_at, account name, order total e order total_amt_usd.

```sql
SELECT orders.occurred_at,
	ac.name account_name,
    orders.total,
    orders.total_amt_usd
FROM orders
JOIN accounts ac
    ON orders.account_id = ac.id
    AND orders.occurred_at BETWEEN '2015-01-01' AND '2016-01-01'
ORDER BY orders.occurred_at DESC;
```


# 11. Quiz: MIN, MAX e AVG

### 1. Quando foi feito o primeiro de todos os pedidos? Você só precisa retornar a data.
```sql
SELECT MIN(orders.occurred_at)
FROM orders;

-- 2013-12-04T04:22:44.000Z
```

### 2. Tente executar a mesma consulta da pergunta 1, sem usar a função de agregação. 
```sql
SELECT occurred_at
FROM orders
ORDER BY occurred_at 
LIMIT 1;

-- 2013-12-04T04:22:44.000Z
```

### 3. Quando ocorreu o web_event mais recente (o último)?
```sql
SELECT MAX(occurred_at)
FROM web_events;

-- 2017-01-01T23:51:09.000Z
```

### 4. Tente executar o resultado da consulta anterior sem usar uma função de agregação.
```sql
SELECT occurred_at
FROM web_events
ORDER BY occurred_at DESC
LIMIT 1;

-- 2017-01-01T23:51:09.000Z
```

### 5. Encontre a quantia média (AVERAGE) gasta por pedido em cada tipo de papel, bem como a quantidade média de cada tipo de papel comprado por pedido. Sua resposta final deve ter 6 valores - uma para cada tipo de papel para o número médio de vendas, bem como a quantia média.
```sql
SELECT AVG(standard_qty) avg_standard_qty,
    AVG(gloss_qty) avg_gloss_qty,
    AVG(poster_qty) avg_poster_qty,
    AVG(standard_amt_usd) avg_standard_amt_usd,
    AVG(gloss_amt_usd) avg_gloss_amt_usd,
    AVG(poster_amt_usd) avg_poster_amt_usd
FROM orders;
```

### 6. Pelo vídeo você pode estar interessado(a) em calcular a MEDIANA. Embora isso seja mais avançado do que o que vimos até aqui, tente descobrir - qual é a MEDIANA de total_usd gasta em todos os pedidos?
```sql
-- total rows: 6912
SELECT id, total_amt_usd
FROM 
    (SELECT id, total_amt_usd
    FROM orders
    ORDER BY total_amt_usd
    LIMIT 6912 / 2) half_sorted
ORDER BY total_amt_usd DESC 
LIMIT 2;
```

# 14 Quiz: GROUP BY

### 1. Qual account (conta), por nome, fez o primeiro pedido de todos? Sua solução deve ter o nome da conta e a data do pedido.

```sql
SELECT ac.name,
    MIN(ord.occurred_at) occurred_at
FROM accounts ac
JOIN orders ord
    ON ord.account_id = ac.id
GROUP BY ac.name
LIMIT 1;
```

### 2. Encontre o total de vendas em usd para cada conta. Você deve incluir duas colunas - o total de vendas para os pedidos de cada empresa em usd e o nome da empresa.

```sql
SELECT ac.name,
	SUM(ord.total_amt_usd) total_usd
FROM orders ord
JOIN accounts ac
	ON ac.id = ord.account_id
GROUP BY ac.name;
```

### 3. Por meio de qual channel (canal) ocorreu o web_event mais recente, qual account (conta) estava associada a esse web_event? Sua consulta deve retornar apenas três valores - date (data), channel (canal) e account name (nome da conta).

```sql
SELECT MAX(ev.occurred_at) occurred_at,
	ev.channel,
	ac.name
FROM web_events ev
JOIN accounts ac
	ON ac.id = ev.account_id
GROUP BY ev.channel, ac.name
ORDER BY occurred_at DESC
LIMIT 1
    
```

### 4. Encontre o número total de vezes em que cada tipo de channel (canal) dos web_events foram usados. Sua tabela final deve ter duas colunas - o channel (canal) e o número de vez que o canal foi usado.

```sql
SELECT ev.channel,
	COUNT(*) freq
FROM web_events ev
GROUP BY ev.channel
ORDER BY freq;
```

### 5. Quem foi o primary contact (contato inicial) associado ao primeiro web_event? 

```sql
SELECT ac.primary_poc
FROM web_events ev
JOIN accounts ac
    ON ac.id = ev.account_id
ORDER BY ev.occurred_at
LIMIT 1

-- Leana Hawker
```

### 6. Qual foi o menor pedido feito por cada conta em termos de total usd (total em dólares)? Dê apenas duas colunas - o name (nome) da conta e o total usd (total em dólares). Ordene da menor quantia em dólares à maior.

```sql
SELECT ac.name,
    MIN(ord.total_amt_usd) total_usd
FROM orders ord
JOIN accounts ac
    ON ac.id = ord.account_id
GROUP BY ac.name
ORDER BY total_usd;
```

### 7. Encontre o número de sales reps (representantes de vendas) em cada região. Sua tabela final deve ter duas colunas - a region (região) e o número de sales_reps (representantes de vendas). Ordene do menor número de representantes ao maior.

```sql
SELECT reg.name,
    COUNT(sr.region_id)
FROM sales_reps sr
JOIN region reg
    ON reg.id = sr.region_id
GROUP BY reg.name;
```
![ERD](erd.png)

# 17. Quiz: GROUP BY [parte 02]

### 1. Para cada conta, determine a quantidade média de papel que eles pediram em seus pedidos. Seu resultado deve ter quatro colunas - uma para o nome da conta e uma para a quantidade média comprada para cada um dos tipos de papel para cada conta. 

```sql
SELECT ac.name,
	AVG(ord.standard_qty) avg_standard,
    AVG(ord.poster_qty) avg_poster,
    AVG(ord.gloss_qty) avg_gloss
FROM orders ord
JOIN accounts ac
	ON ac.id = ord.account_id
GROUP BY ac.name
ORDER BY ac.name;
```

### 2. Para cada conta, determine o valor gasto em média por pedido em cada tipo de papel. Seu resultado deve ter quatro colunas - uma para o nome da conta e uma para a quantia média gasta em casa tipo de papel. 

```sql
SELECT ac.name,
	AVG(ord.standard_amt_usd) avg_standard,
    AVG(ord.poster_amt_usd) avg_poster,
    AVG(ord.gloss_amt_usd) avg_gloss
FROM orders ord
JOIN accounts ac
	ON ac.id = ord.account_id
GROUP BY ac.name
ORDER BY ac.name;
```

### 3. Determine o número de vezes que um channel (canal) em particular foi usado na tabela web_events para cada sales rep (representante de vendas). Sua tabela final deve ter três colunas - o name of the sales rep (nome do representante de vendas), o channel (canal) e o número de ocorrências. Ordene sua tabela com o maior número de ocorrências vindo primeiro.

```sql
SELECT sr.name,
    ev.channel,
    COUNT(ev.*) channel_count
FROM web_events ev
JOIN accounts ac
    ON ac.id = ev.account_id
JOIN sales_reps sr
    ON sr.id = ac.sales_rep_id
GROUP BY ev.channel, sr.name;
```

### 4. Determine o número de vezes que um channel (canal) em particular foi usado na tabela web_events para cada region (região). Sua tabela final deve ter três colunas - o region name (nome da região), o channel (canal) e o número de ocorrências. Ordene sua tabela com o maior número de ocorrências vindo primeiro.

```sql
SELECT reg.name,
    ev.channel,
    COUNT(ev.channel) counter
FROM web_events ev
JOIN accounts ac
    ON ac.id = ev.account_id
JOIN sales_reps sr
    ON sr.id = ac.sales_rep_id
JOIN region reg
    ON reg.id = sr.region_id
GROUP BY ev.channel, reg.name
ORDER BY counter DESC;
```

![ERD](erd.png)

# 20. Quiz: DISTINCT

### 1. Use DISTINCT para testar se você tem quaisquer contas associadas com mais de uma região.

```sql
SELECT DISTINCT ac.id,
	ac.name account_name,
    reg.name region_name
FROM accounts ac
JOIN sales_reps sr
    ON sr.id = ac.sales_rep_id
JOIN region reg
    ON reg.id = sr.region_id
ORDER BY account_name;

```


### 2. Algum dos sales reps (representantes de vendas) trabalhou em mais de uma conta?

```sql
SELECT DISTINCT sr.name rep_name,
    ac.name account_name
FROM sales_reps sr
JOIN accounts ac
    ON ac.sales_rep_id = sr.id;

```

# 23. Quiz: HAVING
### 1. Quantos sales reps (representantes de vendas) possuem mais de 5 contas gerenciadas por eles?

```sql
SELECT sr.name,
    COUNT(*) count_sr
FROM sales_reps sr
JOIN accounts ac
    ON ac.sales_rep_id = sr.id
GROUP BY sr.name
HAVING COUNT(*) > 5
ORDER BY count_sr;

-- 34 results
```

### 2. Quantas accounts (contas) possuem mais de 20 pedidos?

```sql
SELECT ac.name,
    COUNT(*) counter
FROM orders ord
JOIN accounts ac
    ON ac.id = ord.account_id
GROUP BY ac.name
HAVING COUNT(*) > 20
ORDER BY counter;
    
-- 120 results
```

### 3. Qual conta tem mais pedidos?

```sql
SELECT ac.name,
	COUNT(*) counter
FROM orders ord
JOIN accounts ac
	ON ac.id = ord.account_id
GROUP BY ac.name
ORDER BY counter DESC
LIMIT 1;

-- Leucadia National	71
```

### 4. Quantas contas gastaram mais do que 30.000 dólares, no total, em todos os pedidos?

```sql
SELECT ac.name,
	SUM(ord.total_amt_usd) total_usd
FROM orders ord
JOIN accounts ac
	ON ac.id = ord.account_id
GROUP BY ac.name
HAVING SUM(ord.total_amt_usd) > 30000
ORDER BY total_usd;

-- 204 results
```

### 5. Quantas contas gastaram menos que 1.000 dólares, no total, em todos os pedidos?

```sql
SELECT ac.id,
	ac.name ac_name,
    SUM(ord.total_amt_usd) total_usd
FROM orders ord
JOIN accounts ac
	ON ac.id = ord.account_id
GROUP BY ac.id, ac.name
HAVING SUM(total_amt_usd) < 1000
ORDER BY total_usd;

-- 3 results
```

### 6. Qual conta gastou mais conosco?

```sql
SELECT ac.name,
	SUM(ord.total_amt_usd) total_usd
FROM orders ord
JOIN accounts ac
	ON ac.id = ord.account_id
GROUP BY ac.name
ORDER BY total_usd DESC
LIMIT 1;

-- EOG Resources	382873.30
```

### 7. Qual conta menos gastou conosco?

```sql
SELECT ac.name,
	SUM(ord.total_amt_usd) total_usd
FROM orders ord
JOIN accounts ac
	ON ac.id = ord.account_id
GROUP BY ac.name
ORDER BY total_usd
LIMIT 1;

-- Nike	390.25
```

### 8. Quais contas usaram o facebook como um channel (canal) para contactar clientes mais de 6 vezes?

```sql
SELECT ac.name,
	COUNT(*) counter
FROM web_events ev
JOIN accounts ac
	ON ac.id = ev.account_id
    AND ev.channel = 'facebook'
GROUP BY ac.name
HAVING COUNT(*) > 6
ORDER BY counter;

-- 46 results
```

### 9. Qual conta usou mais o facebook como um channel (canal)? 

```sql
SELECT ac.name,
	COUNT(*) counter
FROM web_events ev
JOIN accounts ac
	ON ac.id = ev.account_id
    AND ev.channel = 'facebook'
GROUP BY ac.name
ORDER BY counter DESC
LIMIT 1;

-- Gilead Sciences	16
```

### 10. Qual foi o canal usado mais frequentemente pela maioria das contas?

```sql
SELECT ac.id, 
    ac.name,
    ev.channel,
    COUNT(*) counter
FROM web_events ev
JOIN accounts ac
    ON ac.id = ev.account_id
GROUP BY ac.id, ac.name, ev.channel
ORDER BY counter DESC
LIMIT 10;
-- 1509 results
```

![ERD](erd.png)

# 27. Quiz: Funções DATE

### 1. Encontre as vendas em termos de dólares no total para todos os pedidos a cada ano, ordenados do maior ao menor. Você notou quaisquer tendências nos totais das vendas anuais?

```sql
SELECT DATE_TRUNC('year', ord.occurred_at),
	SUM(ord.total_amt_usd)
FROM orders ord
GROUP BY 1
ORDER BY 1;

-- As vendas apresentam crescimento anualmente
```

### 2. Em qual mês Parch & Posey teve mais vendas em termos de total de dólares? Todos os meses são uniformemente representados pelo conjunto de dados?

```sql
SELECT DATE_PART('month', ord.occurred_at) as month,
	SUM(ord.total_amt_usd) total_usd
FROM orders ord
GROUP BY 1
ORDER BY 2 DESC
LIMIT 1;

-- 12	3129411.98
```

Todos os meses são uniformemente representados pelo conjunto de dados?
```sql
SELECT DATE_PART('month', ord.occurred_at),
    SUM(ord.total_amt_usd) total
FROM orders ord
GROUP BY 1
ORDER BY 1;

-- No they aren't uniform. The last quarter shows a good profit rise
```

### 3. Em qual ano Parch & Posey teve mais vendas em termos de número total de pedidos? Todos os anos são uniformemente representados pelo conjunto de dados?

```sql
SELECT DATE_PART('year', ord.occurred_at),
	COUNT(*)
FROM orders ord
GROUP BY 1
ORDER BY 1;

-- The year with the greatest amount of orders was 2016
-- 2013	99
-- 2014	1306
-- 2015	1725
-- 2016	3757
-- 2017	25
```

### 4. Em qual mês Parch & Posey teve mais vendas em termos de número total de pedidos? Todos os meses são uniformemente representados pelo conjunto de dados?

```sql
SELECT DATE_PART('month', ord.occurred_at),
	COUNT(*)
FROM orders ord
GROUP BY 1
ORDER BY 1;

-- As expected and was shown on profit query, the last quarter shows a rise on amount of orders
-- 1	458
-- 2	409
-- 3	482
-- 4	472
-- 5	518
-- 6	527
-- 7	571
-- 8	603
-- 9	602
-- 10	675
-- 11	713
-- 12	882
```

### 5. Em qual mês de qual ano Walmart gastou mais em gloss paper em termos de dólares?

```sql
SELECT DATE_TRUNC('month', ord.occurred_at) AS date,
	SUM(ord.gloss_amt_usd)
FROM orders ord
JOIN accounts ac 
	ON ac.id = ord.account_id
GROUP BY 1
ORDER BY 2 DESC
LIMIT 1;

-- The answer is December from 2016

-- 2016-12-01T00:00:00.000Z	506825.83
```

# 31. Quiz: CASE
### 1. Gostaríamos de entender três níveis diferentes de clientes com base na quantia associada às suas compras. O ramo superior inclui qualquer um com um Lifetime Value (vendas totais de todos os pedidos) maior que 200.000 dólares. O segundo ramo está entre 200.000 e 100.000 dólares. O ramo mais baixo é qualquer um abaixo de 100.000 dólares. Forneça uma tabela que inclui o nível associado a cada conta. Você deve fornecer o account name (nome da conta), as total sales of all orders (vendas totais de todos os pedidos) para o cliente e o nível. Ordene com os clientes que mais gastam sendo listados primeiro.

```sql
SELECT ac.name,
    SUM(ord.total_amt_usd) total_usd,
    CASE WHEN SUM(ord.total_amt_usd) > 200000 THEN 'Top'
        WHEN SUM(ord.total_amt_usd) > 100000 THEN 'Middle'
        ELSE 'Low'
    END AS class
FROM orders ord
JOIN accounts ac ON ac.id = ord.account_id
GROUP BY ac.name
ORDER BY 2 DESC;
```

### 2. Gostaríamos de fazer um cálculo similar antes, mas queremos obter a quantia total gasta por clientes somente em 2016 e 2017. Mantenha os mesmos níveis da pergunta anterior. Ordene com os clientes que mais gastam sendo listados primeiro.

```sql
SELECT ac.name,
    SUM(ord.total_amt_usd) total_usd,
    CASE WHEN SUM(ord.total_amt_usd) > 200000 THEN 'Top'
    WHEN SUM(ord.total_amt_usd) > 100000 THEN 'Middle'
    ELSE 'Low'
    END AS class
FROM orders ord
JOIN accounts ac ON ac.id = ord.account_id
WHERE ord.occurred_at BETWEEN '2016-01-01' AND '2017-12-31'
GROUP BY ac.name
ORDER BY 2 DESC;
```

### 3. Gostaríamos de identificar os sales reps (representantes de vendas) com melhor desempenho, que são os representantes associados a mais de 200 pedidos. Crie uma tabela com o sales rep name (nome de representante), o número total de pedidos e uma coluna com top ou not dependendo se eles possuem ou não mais de 200 pedidos, respectivamente. Coloque os top vendedores primeiro em sua tabela final.

```sql
SELECT sr.name,
    COUNT(*) as counter,
    CASE WHEN COUNT(*) > 200 THEN 'Top'
        ELSE 'Not'
    END AS class
FROM orders ord
JOIN accounts ac ON ac.id = ord.account_id
JOIN sales_reps sr ON sr.id = ac.sales_rep_id
GROUP BY sr.name
ORDER BY 2 DESC;
```

### 4. A anterior não considerava o meio, nem a quantia em dólares associada com essas vendas. A gestão decide que eles querem ver essas características representadas também. Gostaríamos de identificar os sales reps (representantes de vendas) com melhor desempenho, que são os representantes associados a mais de 200 pedidos ou mais de 750000 em vendas, no total. O grupo do meio contém qualquer representante com mais de 150 pedidos ou 500000 em vendas. Crie uma tabela com o sales rep name (nome de representante), o número total de pedidos, vendas totais em todos os pedidos e uma coluna com top (alto), middle (meio) ou low (baixo) dependendo desses critérios. Coloque as pessoas com mais vendas com base nas quantias em dólares de vendas no final de sua tabela. Você pode ver alguns vendedores chateados por esse critério!

```sql
SELECT sr.name,
    COUNT(*) counter,
    SUM(ord.total_amt_usd) total_usd,
    CASE WHEN COUNT(*) > 200 OR SUM(ord.total_amt_usd) > 750000 THEN 'Top'
        WHEN COUNT(*) > 150 OR SUM(ord.total_amt_usd) > 50000 THEN 'Middle'
        ELSE 'Low'
    END AS class
FROM orders ord
JOIN accounts ac ON ac.id = ord.account_id
JOIN sales_reps sr ON sr.id = ac.sales_rep_id
GROUP BY sr.name
ORDER BY 3 DESC;
```