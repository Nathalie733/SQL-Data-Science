# 1.

```sql
CREATE EXTERNAL TABLE transacoes(
id_cliente BIGINT,
id_transacao BIGINT,
valor FLOAT,
id_loja STRING)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
WITH SERDEPROPERTIES ('separatorChar' = ',', 'quoteChar' = '"', 'escapeChar' = '\\')
STORED AS TEXTFILE
LOCATION 's3://bucket-transacoes/'
```

# 2. 
## 2.1 Query 1 

```sql 
SELECT *
FROM transacoes
WHERE valor > 30 AND id_loja = 'magalu';
```

## 2.2 Query 2 

```sql 
SELECT *
FROM transacoes
WHERE valor > 30 OR id_loja = 'magalu';
```

## 2.3 Query 3

```sql 
SELECT *
FROM transacoes
WHERE id_loja IN ('magalu','subway') AND valor > 10;
```

## 2.4 Query 4

```sql 
SELECT *
FROM transacoes
WHERE valor BETWEEN 60.0 AND 1000.0;
```

# 3. 

## 3.1 Query 5 

```sql 
SELECT * 
FROM transacoes 
WHERE id_loja LIKE 'mag%'
```

## 3.2 Query 6

```sql 
SELECT * 
FROM transacoes 
WHERE id_loja LIKE '%sh%'
```

# 4. 

## 4.1 Query 7 

```sql 
SELECT id_cliente, id_loja, valor,
CASE
    WHEN valor > 1000 THEN 'Compra com alto valor'
    WHEN valor < 1000 THEN 'Compra com baixo valor'
END 
AS classeValor, 
CASE
    WHEN id_loja IN ('giraffas','subway')  THEN 'alimentacao'
    WHEN id_loja IN ('magalu','extra') THEN 'variedade'
    WHEN id_loja IN ('postoshell','seveneleven') THEN '24horas'
    ELSE 'outros'
END 
AS tipo_compra
FROM transacoes;
```
