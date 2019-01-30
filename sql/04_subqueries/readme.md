# 1. Quiz: Subquerie

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