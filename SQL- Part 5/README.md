## **1. Criação da tabela** 


```sql
CREATE EXTERNAL TABLE IF NOT EXISTS default.heartattack (
  `age` int,
  `sex` int,
  `cp` int,
  `trtbps` int,
  `chol` int,
  `fbs` int,
  `restecg` int,
  `thalachh` int,
  `exng` int,
  `oldpeak` double,
  `slp` int,
  `caa` int,
  `thall` int,
  `output` int 
)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe'
WITH SERDEPROPERTIES (
  'serialization.format' = ',',
  'field.delim' = ','
) LOCATION 's3://heart-attack-<seu-nome>-ebac/'
TBLPROPERTIES ('has_encrypted_data'='false');
```

## **2. Função COUNT e GROUP BY** 

### **2.1. Query 1** 

```sql
SELECT * FROM heartattack limit 10;
```

### **2.2. Query 2** 

```sql
SELECT COUNT(age) AS QUANTIDADE_LINHAS
FROM heartattack
```

### **2.3. Query 3** 


```sql
SELECT COUNT(age) AS QUANTIDADE, 
CASE
WHEN output =1 THEN ' more chance of heart attack'
ELSE 'less chance of heart attack'
END AS output
FROM heartattack
GROUP BY output;
```

## **3.Funções MIN/MAX/SUM/AVG**

### 3.1 Query 4


```sql
SELECT MAX(age), MIN(age), AVG(age), output  
FROM heartattack
GROUP BY output
```

### 3.2 Query 5


```sql
SELECT MAX(age), MIN(age), AVG(age), output ,sex
FROM heartattack
GROUP BY output, sex;
```
## 4. Função HAVING

### 4.1. Query 6

```sql
SELECT COUNT(output), output, sex 
FROM heartattack
GROUP BY output, sex
having COUNT(output) > 25
```
