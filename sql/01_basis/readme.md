# 19. Quiz: ORDER BY [parte 01]

### 1. Escreva uma consulta que retorna os 10 primeiros pedidos na tabela orders. Inclua id, occurred_at e total_amt_usd.

```sql
SELECT id, occurred_at, total_amt_usd
FROM orders;
```

### 2. Escreva uma consulta para retornar os top 5 pedidos ordenados pelo maior total_amt_usd. Inclua id, account_id e total_amt_usd

```sql
SELECT id, account_id, total_amt_usd
FROM orders
ORDER BY total_amt_usd DESC
LIMIT 5;
```

### 3. Escreva uma consulta para retornar os últimos 20 pedidos ordenados pelo menor total. Inclua id, account_id e total.

```sql
SELECT id, account_id, total
FROM orders
ORDER BY total 
LIMIT 20;
```

# 22. Quiz: ORDER BY [parte 02]
### 1. Escreva uma consulta que retorna as primeiras 5 linhas de orders, ordenadas do mais novo ao mais antigo, e com ordenação pelo maior total_amt_usd para cada data listada. Você vai perceber que cada uma dessas datas aparece como se fosse única por causa do elemento de tempo. Ao aprender sobre truncar datas (nas próximas aulas), você conseguirá ver essa pergunta de acordo com dia, mês ou ano. 

```sql
SELECT id, account_id, occurred_at, total_amt_usd
FROM orders
ORDER BY occurred_at DESC, total_amt_usd DESC
LIMIT 5;
```

### 2. Escreva uma consulta que retorna as primeiras 10 linhas de orders, ordenadas do mais antigo ao mais novo, mas com o menor total_amt_usd para cada data listada primeiro para cada data. Você vai perceber que cada uma dessas datas aparece como se fosse única por causa do elemento de tempo. Ao aprender sobre truncar datas (nas próximas aulas), você conseguirá ver essa pergunta de acordo com dia, mês ou ano. 

```sql
SELECT id, account_id, occurred_at, total_amt_usd
FROM orders
ORDER BY occurred_at, total_amt_usd
LIMIT 10;
```

# 25. Quiz: WHERE
### 1. Puxe as primeiras 5 linhas e todas as colunas da tabela orders que possuem uma quantia em dólares de gloss_amt_usd maior que ou igual a 1000

```sql
SELECT *
FROM orders
WHERE gloss_amt_usd >= 1000
LIMIT 5;
```

## 2. Puxe as primeiras 10 linhas e todas as colunas da tabela orders que possuem uma total_amt_usd menor que 500.

```sql
SELECT *
FROM orders
WHERE total_amt_usd < 500
LIMIT 10;
```

# 28. Quiz: WHERE com dados não numéricos
### 1. Filtre a tabela de contas para incluir o name(nome) da empresa, o website o ponto inicial de contato (primary_poc) para Exxon Mobil na tabela accounts.

```sql
SELECT name, website, primary_poc
FROM accounts
WHERE name = 'Exxon Mobil';
```
> A String deve ser identificada com aspas simples

# 31. Operações aritméticas
### 1. Crie uma coluna que divida a standard_amt_usd pela standard_qty para encontrar o preço por unidade para papel padrão em cada pedido. Limite os resultados para os 10 primeiros pedidos e inclua os campos id e account_id.

```sql
SELECT 
    id, 
    account_id, 
    standard_amt_usd, 
    standard_qty,
    standard_amt_usd / standard_qty AS unit_price
FROM orders
LIMIT 10;
```
> O apelido não é no formato String

### 2. Escreva uma consulta que encontra a percentagem de receita que vem de papel pôster para cada pedido. Você vai precisar usar apenas as colunas que terminam com _usd. (Tente fazer isso sem usar a coluna de total). Inclua os campos id e account_id. OBSERVAÇÃO - você receberá um erro com a solução correta para essa pergunta. Este erro ocorre pois acontece uma divisão por zero. Você vai aprender como chegar a uma solução sem um erro para essa consulta quando você aprender sobre declarações CASE em uma seção, mais a frente. Por enquanto, você pode só adicionar algum valor muito pequeno ao seu denominador como uma solução alternativa. 

```sql
SELECT 
    id, 
    account_id, 
    standard_amt_usd, 
    gloss_amt_usd,
    poster_amt_usd
    standard_qty,  
    poster_amt_usd / (standard_amt_usd + gloss_amt_usd + poster_amt_usd + 0.00001) AS poster_per
  
FROM orders
LIMIT 10;
```
# 35. Quiz: LIKE
Use a tabela accounts para descobrir

### 1. Todas as empresas cujos nomes começam com 'C'. 

```sql
SELECT id, name
FROM accounts
WHERE name LIKE 'C%';
```

### 2. Todas as empresas que possuem a string 'one' em algum lugar no nome.
```sql
SELECT id, name
FROM accounts
WHERE name LIKE '%one%';
```

### 3. Todas as empresas cujos nomes terminam com 's'.

```sql
SELECT id, name
FROM accounts
WHERE name LIKE '%s';
```

# 38. Quiz: IN
### 1. Use a tabela accounts para encontrar o name, primary_poc e sales_rep_id da conta para Walmart, Target e Nordstrom.

```sql
SELECT name, primary_poc, sales_rep_id
FROM accounts
WHERE name IN ('Walmart', 'Target', 'Nordstrom');
```

### 2. Use a tabela web_events para encontrar todas as informações sobre indivíduos que foram contactados pelo channel organic ou adwords.

```sql
SELECT *
FROM web_events 
WHERE channel IN ('organic', 'adwords');
```

# 41. Quiz: NOT
Podemos puxar todas as linhas que foram excluídas das consultas nos dois tópicos anteriores com o nosso novo operador.

### 1. Use a tabela accounts para encontrar o nome da conta, contato primário e id de representante de vendas para todas as lojas exceto Walmart, Target e Nordstrom.

```sql
SELECT name, primary_poc, sales_rep_id
FROM accounts
WHERE name NOT IN ('Walmart', 'Target', 'Nordstrom');
```

### 2. Use a tabela web_events para encontrar todas as informações sobre indivíduos que foram contactados por quaisquer métodos, exceto os métodos organic ou adwords.

```sql
SELECT *
FROM web_events 
WHERE channel NOT IN ('organic', 'adwords');
```

Use a tabela accounts para descobrir:

### 1. Todas as empresas cujos nomes não começam com 'C'. 
```sql
SELECT id, name
FROM accounts
WHERE name NOT LIKE 'C%';
```
### 2. Todas as empresas que não possuem a string 'one' em nenhum lugar no nome.
```sql
SELECT id, name
FROM accounts
WHERE name NOT LIKE '%one%';
```

### 3. Todas as empresas cujos nomes não terminam com 's'.
```sql
SELECT id, name
FROM accounts
WHERE name NOT LIKE '%s';
```


# 44. Quiz: AND e BETWEEN

### 1. Escreva uma consulta que retorna todos os pedidos nos quais standard_qty é maior que 1000, a poster_qty é 0, e a gloss_qty é 0.
```sql
SELECT * 
FROM orders
WHERE standard_qty > 1000 AND poster_qty = 0 AND gloss_qty = 0;
```

### 2. Usando a tabela accounts encontre todas as empresas cujos nomes não começam com 'C' e terminam com 's'.
```sql
SELECT * 
FROM accounts
WHERE name NOT LIKE 'C%' AND name LIKE '%s';
```

### 3. Use a tabela web_events para encontrar todas as informações sobre indivíduos que foram contactados via organic ou adwords e começaram suas contas em qualquer momento em 2016, do mais recente ao mais antigo.

```sql
SELECT * 
FROM web_events 
WHERE channel IN('organic', 'adwords') 
    AND cast(occurred_at as date) BETWEEN '2016-01-01' AND '2016-12-31'
ORDER BY occurred_at DESC;    
```
> BETWEEN é inclusivo no início e fim do intervalo informado

# 47. Quiz: OR
### 1. Encontre lista de ids de pedidos nos quais gloss_qty or poster_qty são maiores que 4000. Inclua apenas o campo id na tabela resultante.

```sql
SELECT id
FROM orders
WHERE gloss_qty > 4000 OR poster_qty > 4000;
```

### 2. Escreva uma consulta que retorna todos uma lista dos pedidos nos quais standard_qty é zero e ou gloss_qty ou poster_qty é maior que 1000.

```sql
SELECT *
FROM orders
WHERE standard_qty = 0
    AND (gloss_qty > 1000 or poster_qty > 1000);
```

### 3. Encontre todos os nomes de empresas que começam com um 'C' ou 'W', e o contato primário contém 'ana' or 'Ana', mas não contém 'eana'.

```sql
SELECT name
FROM accounts
WHERE (name LIKE 'C%' OR name LIKE 'W%')
    AND LOWER(primary_poc) LIKE '%ana%'
    AND LOWER(primary_poc) NOT LIKE '%eana%';
```