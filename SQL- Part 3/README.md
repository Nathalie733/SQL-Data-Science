# **1. Selecionando dados**

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

## 1.1 Query 1 

```sql 
SELECT * from transacoes
```
## 1.2 Query 2 

```sql 
SELECT id_cliente , valor, id_loja AS nome_loja FROM transacoes;
```
## 1.3 Query 3

```sql 
SELECT DISTINCT  id_loja AS nome_loja FROM transacoes;
```
# 2. Ordenando e limitando dados

## 2.1 Query 4

```sql 
SELECT id_cliente, valor FROM transacoes ORDER BY valor DESC LIMIT 2;
```
