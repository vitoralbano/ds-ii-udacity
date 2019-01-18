# 19 - Quiz

## 1. Escreva uma consulta que retorna os 10 primeiros pedidos na tabela orders. Inclua id, occurred_at e total_amt_usd.

```sql
SELECT id, occurred_at, total_amt_usd
FROM orders
```

## 2. Escreva uma consulta para retornar os top 5 pedidos ordenados pelo maior total_amt_usd. Inclua id, account_id e total_amt_usd

```sql
SELECT id, account_id, total_amt_usd
FROM orders
ORDER BY total_amt_usd DESC
LIMIT 5
```

## 3. Escreva uma consulta para retornar os últimos 20 pedidos ordenados pelo menor total. Inclua id, account_id e total.

```sql
SELECT id, account_id, total
FROM orders
ORDER BY total 
LIMIT 20
```