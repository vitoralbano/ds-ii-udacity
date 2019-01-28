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
Date functions documentation at
<https://www.postgresql.org/docs/9.1/functions-datetime.html>


# CASE
1. Sempre vai na cláusula `SELECT`.

2. `CASE` deve incluir os seguintes componentes: `WHEN`, `THEN` e `END`. `ELSE` é um componente opcional para casos que não atendem a nenhuma das condições `CASE` anteriores.

3. Você pode fazer qualquer declaração condicional usando um operador condicional (como [`WHERE`](https://community.modeanalytics.com/sql/tutorial/sql-where/)) entre `WHEN` e `THEN`. Isso inclui fazer strings de várias declarações condicionais usando `AND` e `OR`.

4. Você pode incluir várias declarações `WHERE`, bem como uma declaração `ELSE` novamente, para lidar com quaisquer condições ainda não acessadas.

## Exemplo
```sql
SELECT	account_id,
    CASE WHEN standard_qty = 0 
        OR standard_qty IS NULL
    THEN 0
    ELSE standard_amt_usd / standard_qty 
    END AS unit_price
FROM orders
LIMIT 10;
```