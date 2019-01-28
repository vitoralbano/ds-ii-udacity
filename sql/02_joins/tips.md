# COUNT
Doesn't count cells with null values;
```sql
SELECT COUNT(phone) FROM user
// 5
SELECT COUNT(*) FROM user
// 8
```

# AVG 
As `COUNT`, `AVG` doesn't count null cells.

# Agregations

> TIP!
>
> **To remember**: Always that one column wouldn't be in a agregation should be in `GROUP BY` statement
> 
> **Lembrete**: Qualquer coluna que não estiver em uma agregação deve aparecer na declaração `GROUP BY`.

## HAVING

> `HAVING` is used to make 'clean' filters on aggregated consults
>
> `HAVING` é utilizado para criar filtros em consultas agregadas
```sql
SELECT account_id, 
    SUM(total_amt_usd) sum_total_usd
    FROM orders
GROUP BY 1
HAVING SUM(total_amt_usd) >= 250000
```

# DATE

## DATE_TRUNC
