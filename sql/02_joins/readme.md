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
