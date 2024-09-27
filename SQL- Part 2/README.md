# Atividades

# **1. Explorando os dados da tabela de clientes** 

## **1.1. Query 1** 


```sql
SELECT id, idade, sexo, dependentes FROM clientes;
```

## **1.2. Query 2** 


```sql
SELECT id, valor_transacoes_12m FROM clientes WHERE escolaridade = 'mestrado' and sexo = 'F';
```

## **1.3. Query 3** 


```sql
SELECT sexo, AVG(idade) AS "media_idade_por_sexo" FROM clientes GROUP BY sexo;
```

# **2. Inserindo novos dados** 


```sql
SELECT * FROM clientes;
```

# **3. Criando e trabalhando com partições** 

## 3.1. Query 5 


```sql
CREATE EXTERNAL TABLE clientes_part(
  id BIGINT, 
  idade BIGINT, 
  dependentes BIGINT, 
  escolaridade STRING, 
  tipo_cartao STRING, 
  limite_credito DOUBLE, 
  valor_transacoes_12m DOUBLE, 
  qtd_transacoes_12m BIGINT) 
  PARTITIONED BY (sexo string)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
WITH SERDEPROPERTIES ('separatorChar' = ',', 'quoteChar' = '"', 'escapeChar' = '\\')
STORED AS TEXTFILE
LOCATION 's3://bucket-nathalies-partitioned/'
```

```sql
MSCK REPAIR TABLE clientes_part;
```

```sql
select * from clientes_part where sexo = 'F';
````

## 3.2. Query 6

```sql
SELECT id, idade, limite_credito FROM clientes_part WHERE sexo = 'M' ORDER BY limite_credito DESC;
```

# **4. Adicionando colunas**

## 4.1. Query 7

```sql
ALTER TABLE clientes ADD COLUMNS (estado string)
```

Verifique a adicão da nova coluna e envie o resultado da Query 7:

```sql
SELECT * from clientes
```
