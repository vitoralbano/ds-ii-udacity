# 1. Quiz: Subqueries

### 1. Encontre o número de eventos que ocorre a cada dia e em cada canal.
### 2. Crie uma subconsulta que simplesmente forneça todos os dados de sua primeira consulta
### 3. Encontre o número médio de evento de cada canal. 

```sql
SELECT channel,
    AVG(events_count) AS avg_count
FROM
    (SELECT channel,
        DATE_TRUNC('day', occurred_at) AS day,
        COUNT(*) events_count
    FROM web_events
    GROUP BY 1,2) sub
GROUP BY 1
ORDER BY avg_count DESC;
```

# 7. Quiz: Subqueries (parte 02)

### 1. Encontre os pedidos que occorreram no mesmo mês e ano que o primeiro pedido e, então, puxe a média para cada tipo de papel `qty` deste mês e a soma do total em USD.

```sql
SELECT AVG(standard_qty) avg_standard,
    AVG(gloss_qty) avg_gloss,
    AVG(poster_qty) avg_poster,
    SUM(total_amt_usd) total_usd
FROM orders
WHERE DATE_TRUNC('month', occurred_at) = 
    (SELECT DATE_TRUNC('month', MIN(occurred_at)) date_month
    FROM orders);

```

# 9. Quiz: Addicted in subqueries

### 1. Dê o name (nome) do(a) sales_rep (representante de vendas) em cada region (região) com a maior quantia de vendas em total_amt_usd (quantia total em dólares).

```sql
SELECT 
    rep_total.rep_name,
    reg_max.region_name,
    reg_max.total_usd
FROM 
    (SELECT 
        reg_total.region_name,
        MAX(reg_total.total_usd) total_usd
    FROM 
        (SELECT 
            sr.name rep_name,
            reg.name region_name,
            SUM(ord.total_amt_usd) total_usd
        FROM sales_reps sr
        JOIN accounts ac ON ac.sales_rep_id = sr.id
        JOIN orders ord ON ord.account_id = ac.id
        JOIN region reg ON reg.id = sr.region_id
        GROUP BY sr.name, reg.name) reg_total

    GROUP BY reg_total.region_name) reg_max

JOIN 
    (SELECT 
            sr.name rep_name,
            reg.name region_name,
            SUM(ord.total_amt_usd) total_usd
        FROM sales_reps sr
        JOIN accounts ac ON ac.sales_rep_id = sr.id
        JOIN orders ord ON ord.account_id = ac.id
        JOIN region reg ON reg.id = sr.region_id
        GROUP BY sr.name, reg.name) rep_total
ON 
    rep_total.total_usd = reg_max.total_usd

ORDER BY reg_max.total_usd DESC
```

### 2. Em relação à região com mais vendas(sum) em total_amt_usd, quantos pedidos no total(count) foram feitos? 

```sql
SELECT 
    rep_total.rep_name,
    reg_max.region_name,
    reg_max.order_count,
    reg_max.total_usd
FROM 
    (SELECT 
        reg_total.region_name,
        SUM(reg_total.order_count) order_count,
        MAX(reg_total.total_usd) total_usd
    FROM 
        (SELECT 
            sr.name rep_name,
            reg.name region_name,
            COUNT(*) order_count,
            SUM(ord.total_amt_usd) total_usd
        FROM sales_reps sr
        JOIN accounts ac ON ac.sales_rep_id = sr.id
        JOIN orders ord ON ord.account_id = ac.id
        JOIN region reg ON reg.id = sr.region_id
        GROUP BY sr.name, reg.name) reg_total

    GROUP BY reg_total.region_name) reg_max

JOIN 
    (SELECT 
            sr.name rep_name,
            reg.name region_name,
            SUM(ord.total_amt_usd) total_usd
        FROM sales_reps sr
        JOIN accounts ac ON ac.sales_rep_id = sr.id
        JOIN orders ord ON ord.account_id = ac.id
        JOIN region reg ON reg.id = sr.region_id
        GROUP BY sr.name, reg.name) rep_total
ON 
    rep_total.total_usd = reg_max.total_usd

ORDER BY reg_max.total_usd DESC
```

### 3. Em relação ao name/nome da conta que mais comprou (no total em toda a sua existência enquanto cliente) o papel standard_qty, quantas contas tinham uma quantidade total ainda maior de compras? 

```sql

```

### 4. Em relação ao cliente que mais gastou (no total durante sua existência enquanto cliente) total_amt_usd, quantos web_events ele teve para cada canal?

```sql

```

### 5. Qual é a média de quantia gasta durante durante a existência como cliente em termos de total_amt_usd para as 10 contas que mais gastaram?

```sql

```

### 6. Qual é a média de gasto durante sua existência como cliente em termos de total_amt_usd para apenas as empresas que gastaram mais que a média de todos os pedidos.

```sql

```