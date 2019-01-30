# COUNT
> Conta as linhas com valores não nulos.
```sql
SELECT COUNT (*) FROM column
```
# Quiz: SUM

### 1. Encontre a quantidade total de papel poster_qty pedida na tabela orders.
```sql 
SELECT SUM(poster_qty)
FROM orders;
```
### 2. Encontre a quantidade total de papel standard_qty pedida na tabela orders.
```sql
SELECT SUM(standard_qty)
FROM orders;
```
### 3. Encontre a quantidade total de vendas em dólares usando total_amt_usd na tabela orders.
```sql
SELECT SUM(total_amt_usd)
FROM orders;
```

### 4. Encontre a quantia total gasta em papel standard_amt_usd e gloss_amt_usd para cada pedido na tabela de pedidos. Isso deve dar uma quantia em dólares para cada pedido na tabela.
```sql
SELECT id,
    (standard_amt_usd + gloss_amt_usd) total_standard_gloss
FROM orders;
```

### 5. Encontre a standard_amt_usd por unidade de papel standard_qty. Sua solução deve usar tanto uma agregação quanto um operador matemático.
```sql
SELECT SUM(standard_amt_usd) / SUM(standard_qty) standard_price_per_unit
FROM orders;
```