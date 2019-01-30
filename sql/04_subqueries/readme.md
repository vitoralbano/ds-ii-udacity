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