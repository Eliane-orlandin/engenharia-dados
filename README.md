# 🚀 Estudos em Engenharia de Dados

Repositório dedicado à organização de estudos, anotações, scripts, exercícios práticos e projetos da trilha de **Engenharia de Dados**.

---

## 🗺️ Trilha de Estudos

### 1. [SQL](./01-sql)
- [ ] Consultas básicas (`SELECT`, `WHERE`, `ORDER BY`, `GROUP BY`, `HAVING`)
- [ ] Joins (`INNER`, `LEFT`, `RIGHT`, `FULL`, `CROSS`)
- [ ] Subqueries e CTEs (`WITH`)
- [ ] Window Functions (`ROW_NUMBER`, `RANK`, `DENSE_RANK`, `LEAD`, `LAG`, `OVER`)
- [ ] Funções de agregação, data e manipulação de strings
- [ ] Views, Procedures e Triggers

### 2. [Bancos de Dados](./02-bancos-de-dados)
- **Conceitos & Arquitetura**
  - [ ] Modelagem Relacional (Conceitual, Lógica e Física)
  - [ ] Normalização (1FN, 2FN, 3FN, BCNF)
  - [ ] Índices (B-Tree, Hash, Índices Compostos, Clusterizados vs. Não-Clusterizados) e Otimização de Queries
- **SGBDs**
  - [ ] PostgreSQL
  - [ ] MySQL
  - [ ] SQL Server

### 3. [Python para Engenharia de Dados](./03-python)
- [ ] Estruturas de Dados (Listas, Tuplas, Dicionários, Sets, Comprehensions)
- [ ] Programação Orientada a Objetos (Classes, Herança, Polimorfismo, Encapsulamento)
- [ ] Análise e Transformação com **Pandas**
- [ ] Manipulação de Arquivos (**CSV**, **JSON** e **Parquet**)
- [ ] Consumo de APIs REST (`requests`, paginação, autenticação, tratamento de erros)

### 4. [ETL e ELT](./04-etl-e-elt)
- **Conceitos de Ingestão, Extração, Transformação e Carga**
- **Ferramentas de Orquestração e Pipelines:**
  - [ ] Apache Airflow (DAGs, Operators, Hooks, Sensors, TaskFlow API)
  - [ ] Databricks Workflows
  - [ ] Azure Data Factory (ADF)
  - [ ] AWS Glue

### 5. [Big Data](./05-big-data)
- [ ] Processamento Distribuído (Conceitos de Cluster, Driver, Executors, Shuffling)
- [ ] Apache Spark & **PySpark** (RDDs, DataFrames, Spark SQL, Catalyst Optimizer)
- [ ] Estratégias de Particionamento e Bucketing

### 6. [Data Warehouse, Data Lake e Lakehouse](./06-data-warehouse-e-data-lake)
- **Arquitetura e Modelagem Dimensional**
  - [ ] Data Warehouse vs. Data Lake vs. Data Lakehouse (Arquitetura Medallion: Bronze, Silver, Gold)
  - [ ] Star Schema e Snowflake Schema
  - [ ] Tabelas Fato e Dimensão (SCD - Slowly Changing Dimensions)
- **Ferramentas & Plataformas**
  - [ ] Databricks
  - [ ] Snowflake
  - [ ] Google BigQuery
  - [ ] Amazon Redshift
  - [ ] Azure Synapse Analytics

### 7. [Cloud Computing](./07-cloud)
- **Microsoft Azure**
  - [ ] Azure Storage (Blob Storage, Data Lake Storage Gen2 - ADLS)
  - [ ] Azure Data Factory
  - [ ] Azure Databricks
- **Amazon Web Services (AWS)**
  - [ ] Amazon S3
  - [ ] AWS Glue (Data Catalog, Jobs, Crawlers)
  - [ ] Amazon Athena
  - [ ] Amazon Redshift

### 8. [Docker](./08-docker)
- [ ] Conceitos de Containers, Imagens, Volumes e Redes
- [ ] Criação de `Dockerfile`
- [ ] Orquestração local de múltiplos serviços com `Docker Compose` (ex.: Postgres + Airflow + Spark)

---

## 📂 Estrutura de Pastas

```text
├── 01-sql/
│   ├── consultas/
│   └── exercicios/
├── 02-bancos-de-dados/
│   ├── indices-e-normalizacao/
│   ├── modelagem-relacional/
│   ├── mysql/
│   ├── postgresql/
│   └── sql-server/
├── 03-python/
│   ├── consumo-apis/
│   ├── estruturas-de-dados/
│   ├── manipulacao-arquivos/
│   ├── pandas/
│   └── poo/
├── 04-etl-e-elt/
│   ├── apache-airflow/
│   ├── aws-glue/
│   ├── azure-data-factory/
│   └── databricks-workflows/
├── 05-big-data/
│   ├── apache-spark-pyspark/
│   ├── particionamento/
│   └── processamento-distribuido/
├── 06-data-warehouse-e-data-lake/
│   ├── azure-synapse/
│   ├── bigquery/
│   ├── conceitos-e-modelagem/
│   ├── databricks/
│   ├── redshift/
│   └── snowflake/
├── 07-cloud/
│   ├── aws/
│   │   ├── athena/
│   │   ├── glue/
│   │   ├── redshift/
│   │   └── s3/
│   └── azure/
│       ├── data-factory/
│       ├── databricks/
│       └── storage/
├── 08-docker/
│   ├── containers/
│   ├── docker-compose/
│   └── dockerfile/
└── projetos/
```

---

## 🛠️ Como Utilizar este Repositório

1. Cada módulo possui sua própria pasta numerada seguindo a ordem sugerida de estudos.
2. Scripts práticos, notebooks e anotações em Markdown ficam organizados dentro de seus respectivos subtópicos.
3. Projetos integrando múltiplas ferramentas (ex.: ingestão via Python + orquestração Airflow + armazenamento Cloud/DW containerizado em Docker) ficam em [`projetos/`](./projetos).
