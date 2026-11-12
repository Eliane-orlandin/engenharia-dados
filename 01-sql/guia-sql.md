# Guia de SQL

Guia de referência rápida baseado na ementa do tutorial de SQL da W3Schools.
Os resumos e exemplos foram escritos em português; não são cópia do material
original.

- **Ementa:** [w3schools.com/sql](https://www.w3schools.com/sql/)
- **Playground:** [Tryit Editor](https://www.w3schools.com/sql/trysql.asp?filename=trysql_select_all)

## Como usar este guia

1. Use o índice abaixo para ir direto ao assunto.
2. Cada tópico tem uma explicação curta, a sintaxe e um exemplo.
3. Os exemplos usam o banco de demonstração do W3Schools, então podem ser
   colados direto no playground.
4. A sintaxe varia entre SGBDs. Onde houver diferença, há uma nota de
   **dialetos** (MySQL, PostgreSQL, SQL Server, SQLite).
5. Comandos `INSERT`, `UPDATE`, `DELETE` e DDL alteram os dados do playground;
   recarregar a página restaura o banco original.

## Banco de exemplo

O playground do W3Schools usa estas tabelas:

| Tabela | Colunas principais |
|---|---|
| `Customers` | `CustomerID`, `CustomerName`, `ContactName`, `Address`, `City`, `PostalCode`, `Country` |
| `Categories` | `CategoryID`, `CategoryName`, `Description` |
| `Employees` | `EmployeeID`, `LastName`, `FirstName`, `BirthDate`, `Notes` |
| `OrderDetails` | `OrderDetailID`, `OrderID`, `ProductID`, `Quantity` |
| `Orders` | `OrderID`, `CustomerID`, `EmployeeID`, `OrderDate`, `ShipperID` |
| `Products` | `ProductID`, `ProductName`, `SupplierID`, `CategoryID`, `Unit`, `Price` |
| `Shippers` | `ShipperID`, `ShipperName`, `Phone` |
| `Suppliers` | `SupplierID`, `SupplierName`, `ContactName`, `Address`, `City`, `PostalCode`, `Country`, `Phone` |

---

## Índice

### Fundamentos
- [Introdução](#introdução)
- [Sintaxe](#sintaxe)
- [Comentários](#comentários)
- [Operadores](#operadores)

### Consultas
- [SELECT](#select)
- [SELECT DISTINCT](#select-distinct)
- [WHERE](#where)
- [ORDER BY](#order-by)
- [AND](#and)
- [OR](#or)
- [NOT](#not)
- [LIMIT e TOP](#limit-e-top)
- [LIKE](#like)
- [Wildcards](#wildcards)
- [IN](#in)
- [BETWEEN](#between)
- [Aliases](#aliases)
- [CASE](#case)
- [Valores NULL](#valores-null)
- [Funções de NULL](#funções-de-null)
- [Funções de agregação](#funções-de-agregação)
- [MIN](#min)
- [MAX](#max)
- [COUNT](#count)
- [SUM](#sum)
- [AVG](#avg)
- [GROUP BY](#group-by)
- [HAVING](#having)

### Junções e conjuntos
- [JOINs](#joins)
- [INNER JOIN](#inner-join)
- [LEFT JOIN](#left-join)
- [RIGHT JOIN](#right-join)
- [FULL JOIN](#full-join)
- [SELF JOIN](#self-join)
- [UNION](#union)
- [UNION ALL](#union-all)
- [EXISTS](#exists)
- [ANY](#any)
- [ALL](#all)

### Alteração de dados
- [INSERT INTO](#insert-into)
- [INSERT INTO SELECT](#insert-into-select)
- [UPDATE](#update)
- [DELETE](#delete)
- [SELECT INTO](#select-into)

### Estrutura do banco
- [CREATE DATABASE](#create-database)
- [DROP DATABASE](#drop-database)
- [BACKUP DATABASE](#backup-database)
- [CREATE TABLE](#create-table)
- [DROP TABLE](#drop-table)
- [ALTER TABLE](#alter-table)
- [Constraints](#constraints)
- [NOT NULL](#not-null)
- [UNIQUE](#unique)
- [PRIMARY KEY](#primary-key)
- [FOREIGN KEY](#foreign-key)
- [CHECK](#check)
- [DEFAULT](#default)
- [CREATE INDEX](#create-index)
- [AUTO INCREMENT](#auto-increment)
- [Datas](#datas)
- [VIEWS](#views)
- [Stored Procedures](#stored-procedures)

### Segurança e operação
- [SQL Injection](#sql-injection)
- [Parâmetros](#parâmetros)
- [Prepared Statements](#prepared-statements)
- [Hosting](#hosting)

---

## Fundamentos

### Introdução

**O que é:** SQL (Structured Query Language) é a linguagem usada para consultar
e manipular dados em bancos relacionais.

Com SQL é possível:

- consultar dados (`SELECT`);
- inserir, alterar e excluir registros (`INSERT`, `UPDATE`, `DELETE`);
- criar e alterar estruturas (`CREATE`, `ALTER`, `DROP`);
- controlar permissões e transações.

**Sintaxe**
```sql
SELECT coluna
FROM tabela
WHERE condição;
```

**Exemplos de SGBDs:** MySQL, PostgreSQL, SQL Server, Oracle, SQLite.

> **Dialetos:** o núcleo do SQL é padronizado, mas cada SGBD tem funções e
> detalhes próprios. Este guia indica as diferenças mais comuns.

---

### Sintaxe

**O que faz:** define a estrutura de um comando SQL.

Regras gerais:

- palavras-chave não diferenciam maiúsculas de minúsculas (`SELECT` = `select`);
- comandos terminam com ponto e vírgula (`;`);
- textos usam aspas simples (`'texto'`);
- nomes com espaço ou palavra reservada usam aspas duplas ou backticks,
  dependendo do SGBD.

**Sintaxe**
```sql
SELECT coluna1, coluna2
FROM tabela
WHERE condição
ORDER BY coluna1;
```

**Exemplo**
```sql
SELECT CustomerName, Country
FROM Customers
WHERE Country = 'Brazil';
```

---

### Comentários

**O que faz:** ignora trechos do código, útil para documentar.

**Sintaxe**
```sql
-- comentário de uma linha

/*
comentário
de várias linhas
*/
```

**Exemplo**
```sql
-- Retorna apenas clientes do Brasil
SELECT CustomerName
FROM Customers
WHERE Country = 'Brazil';
```

---

### Operadores

**O que fazem:** permitem comparar valores e combinar condições.

| Tipo | Operadores |
|---|---|
| Aritméticos | `+`, `-`, `*`, `/`, `%` |
| Comparação | `=`, `<>` ou `!=`, `>`, `<`, `>=`, `<=` |
| Lógicos | `AND`, `OR`, `NOT` |
| Intervalo | `BETWEEN ... AND ...` |
| Lista | `IN (...)` |
| Texto | `LIKE`, `NOT LIKE` |
| Nulo | `IS NULL`, `IS NOT NULL` |

**Exemplo**
```sql
SELECT ProductName, Price
FROM Products
WHERE Price > 20 AND CategoryID = 1;
```

> **Dialetos:** `%` é o resto da divisão na maioria dos SGBDs; `!=` e `<>` são
> equivalentes.

---

## Consultas

### SELECT

**O que faz:** seleciona colunas de uma ou mais tabelas.

**Sintaxe**
```sql
SELECT coluna1, coluna2
FROM tabela;
```

**Exemplo**
```sql
SELECT CustomerName, City
FROM Customers;
```

**Notas**
- `SELECT *` retorna todas as colunas.
- É possível usar expressões: `SELECT Price * 1.1 AS PrecoComTaxa FROM Products;`
- A ordem das colunas no resultado segue a ordem escrita no `SELECT`.

---

### SELECT DISTINCT

**O que faz:** retorna apenas valores únicos, removendo linhas duplicadas.

**Sintaxe**
```sql
SELECT DISTINCT coluna
FROM tabela;
```

**Exemplo**
```sql
SELECT DISTINCT Country
FROM Customers;
```

**Notas**
- Com várias colunas, a combinação delas é comparada.
- `DISTINCT` vale para todas as colunas do `SELECT`.

---

### WHERE

**O que faz:** filtra as linhas antes de retornar o resultado.

**Sintaxe**
```sql
SELECT coluna
FROM tabela
WHERE condição;
```

**Exemplo**
```sql
SELECT CustomerName
FROM Customers
WHERE Country = 'Mexico';
```

**Notas**
- Textos ficam entre aspas simples; números não.
- Use `AND`/`OR` para combinar condições.
- `WHERE` filtra linhas; `HAVING` filtra grupos.

---

### ORDER BY

**O que faz:** ordena o resultado por uma ou mais colunas.

**Sintaxe**
```sql
SELECT coluna
FROM tabela
ORDER BY coluna [ASC | DESC];
```

**Exemplo**
```sql
SELECT ProductName, Price
FROM Products
ORDER BY Price DESC;
```

**Notas**
- `ASC` é o padrão (crescente).
- É possível ordenar por várias colunas: `ORDER BY Country, City;`
- Também aceita posição ou alias: `ORDER BY 2 DESC;`

---

### AND

**O que faz:** exige que **todas** as condições sejam verdadeiras.

**Sintaxe**
```sql
SELECT coluna
FROM tabela
WHERE condição1 AND condição2;
```

**Exemplo**
```sql
SELECT CustomerName
FROM Customers
WHERE Country = 'Germany' AND City = 'Berlin';
```

---

### OR

**O que faz:** exige que **pelo menos uma** condição seja verdadeira.

**Sintaxe**
```sql
SELECT coluna
FROM tabela
WHERE condição1 OR condição2;
```

**Exemplo**
```sql
SELECT CustomerName
FROM Customers
WHERE Country = 'Germany' OR Country = 'Spain';
```

**Notas**
- Use parênteses para deixar a precedência explícita:
  `WHERE (A OR B) AND C`.

---

### NOT

**O que faz:** inverte uma condição.

**Sintaxe**
```sql
SELECT coluna
FROM tabela
WHERE NOT condição;
```

**Exemplo**
```sql
SELECT CustomerName
FROM Customers
WHERE NOT Country = 'Germany';
```

**Variações**
```sql
WHERE NOT LIKE '%A%'
WHERE NOT IN (1, 2, 3)
WHERE NOT BETWEEN 10 AND 20
WHERE NOT EXISTS (SELECT ...)
```

---

### LIMIT e TOP

**O que faz:** limita a quantidade de linhas retornadas.

**Sintaxe**
```sql
-- MySQL, PostgreSQL, SQLite
SELECT coluna
FROM tabela
LIMIT 10;

-- SQL Server
SELECT TOP 10 coluna
FROM tabela;
```

**Exemplo**
```sql
SELECT CustomerName
FROM Customers
LIMIT 5;
```

> **Dialetos:** Oracle usa `FETCH FIRST 5 ROWS ONLY`. SQL Server usa `TOP`.
> No MySQL, `LIMIT 5, 10` significa “pular 5 e retornar 10”.

---

### LIKE

**O que faz:** procura um padrão em textos.

**Sintaxe**
```sql
SELECT coluna
FROM tabela
WHERE coluna LIKE 'padrão';
```

**Exemplo**
```sql
SELECT CustomerName
FROM Customers
WHERE CustomerName LIKE 'A%';
```

**Curingas comuns**
- `%` representa zero ou mais caracteres.
- `_` representa exatamente um caractere.

> **Dialetos:** a comparação pode ser case-sensitive dependendo do SGBD e da
> collation. No MySQL, `LIKE` geralmente ignora maiúsculas/minúsculas.

---

### Wildcards

**O que fazem:** complementam o `LIKE`.

| Curinga | Significado | Exemplo |
|---|---|---|
| `%` | zero ou mais caracteres | `'A%'` |
| `_` | um caractere | `'_o%'` |
| `[]` | um caractere da lista | `'[ABC]%'` (SQL Server) |
| `[^]` | um caractere fora da lista | `'[^ABC]%'` (SQL Server) |
| `-` | intervalo | `'[A-C]%'` (SQL Server) |

**Exemplo**
```sql
SELECT CustomerName
FROM Customers
WHERE CustomerName LIKE '_a%';
```

> **Dialetos:** `[]`, `[^]` e `-` são específicos do SQL Server/Access. Em
> outros SGBDs, use `SIMILAR TO` ou expressões regulares quando disponíveis.

---

### IN

**O que faz:** verifica se um valor está em uma lista.

**Sintaxe**
```sql
SELECT coluna
FROM tabela
WHERE coluna IN (valor1, valor2, ...);
```

**Exemplo**
```sql
SELECT CustomerName
FROM Customers
WHERE Country IN ('Germany', 'France', 'UK');
```

**Notas**
- `IN` também aceita uma subconsulta:
  `WHERE CustomerID IN (SELECT CustomerID FROM Orders);`
- `NOT IN` faz o oposto.

---

### BETWEEN

**O que faz:** verifica se um valor está em um intervalo **inclusivo**.

**Sintaxe**
```sql
SELECT coluna
FROM tabela
WHERE coluna BETWEEN valor1 AND valor2;
```

**Exemplo**
```sql
SELECT ProductName, Price
FROM Products
WHERE Price BETWEEN 10 AND 20;
```

**Notas**
- Funciona com números, textos e datas.
- `NOT BETWEEN` exclui o intervalo.

> **Dialetos:** em datas, cuidado com a hora. `BETWEEN '2024-01-01' AND
> '2024-12-31'` pode excluir registros de 31/12 se houver componente de hora.

---

### Aliases

**O que faz:** dá um nome temporário a uma coluna ou tabela no resultado.

**Sintaxe**
```sql
SELECT coluna AS alias
FROM tabela AS t;
```

**Exemplo**
```sql
SELECT CustomerName AS Cliente, City AS Cidade
FROM Customers AS c;
```

**Notas**
- `AS` é opcional, mas deixa o código mais legível.
- Aliases com espaço precisam de aspas: `AS "Nome do Cliente"`.
- Aliases de tabela são úteis em joins.

---

### CASE

**O que faz:** cria uma lógica condicional dentro da consulta, semelhante a
`if/else`.

**Sintaxe**
```sql
SELECT
    coluna,
    CASE
        WHEN condição1 THEN resultado1
        WHEN condição2 THEN resultado2
        ELSE resultado_padrão
    END AS alias
FROM tabela;
```

**Exemplo**
```sql
SELECT
    ProductName,
    Price,
    CASE
        WHEN Price < 20 THEN 'Barato'
        WHEN Price < 50 THEN 'Médio'
        ELSE 'Caro'
    END AS Faixa
FROM Products;
```

**Notas**
- `ELSE` é opcional; sem ele, casos não cobertos retornam `NULL`.
- Existe também a forma simples: `CASE coluna WHEN valor THEN resultado END`.

---

### Valores NULL

**O que faz:** `NULL` representa ausência de valor; não é zero nem texto vazio.

**Sintaxe**
```sql
WHERE coluna IS NULL
WHERE coluna IS NOT NULL
```

**Exemplo**
```sql
SELECT CustomerName
FROM Customers
WHERE PostalCode IS NULL;
```

**Notas**
- Use `IS NULL`, nunca `= NULL`.
- Comparações com `NULL` retornam desconhecido, não verdadeiro.
- `COUNT(coluna)` ignora `NULL`; `COUNT(*)` conta todas as linhas.

---

### Funções de NULL

**O que fazem:** substituem `NULL` por um valor padrão.

**Sintaxe**
```sql
COALESCE(coluna, valor_padrão)
```

**Exemplo**
```sql
SELECT CustomerName, COALESCE(PostalCode, 'Sem CEP') AS CEP
FROM Customers;
```

**Equivalentes por dialeto**
- `COALESCE` — padrão SQL, funciona na maioria dos SGBDs.
- `IFNULL(a, b)` — MySQL e SQLite.
- `ISNULL(a, b)` — SQL Server.
- `NVL(a, b)` — Oracle.
- `NULLIF(a, b)` — retorna `NULL` se `a = b`.

---

### Funções de agregação

**O que fazem:** resumem várias linhas em um único valor.

Principais funções:

| Função | Retorno |
|---|---|
| `MIN` | menor valor |
| `MAX` | maior valor |
| `COUNT` | quantidade de linhas |
| `SUM` | soma |
| `AVG` | média |

**Exemplo**
```sql
SELECT COUNT(*) AS TotalClientes
FROM Customers;
```

**Notas**
- Podem ser combinadas com `GROUP BY`.
- `WHERE` filtra antes da agregação; `HAVING` filtra depois.

---

### MIN

**O que faz:** retorna o menor valor de uma coluna.

**Sintaxe**
```sql
SELECT MIN(coluna) FROM tabela;
```

**Exemplo**
```sql
SELECT MIN(Price) AS MenorPreco
FROM Products;
```

**Notas**
- Ignora `NULL`.
- Funciona com números, textos e datas.

---

### MAX

**O que faz:** retorna o maior valor de uma coluna.

**Sintaxe**
```sql
SELECT MAX(coluna) FROM tabela;
```

**Exemplo**
```sql
SELECT MAX(Price) AS MaiorPreco
FROM Products;
```

---

### COUNT

**O que faz:** conta linhas ou valores não nulos.

**Sintaxe**
```sql
SELECT COUNT(*) FROM tabela;
SELECT COUNT(coluna) FROM tabela;
SELECT COUNT(DISTINCT coluna) FROM tabela;
```

**Exemplo**
```sql
SELECT COUNT(*) AS TotalPedidos
FROM Orders;
```

**Notas**
- `COUNT(*)` conta todas as linhas.
- `COUNT(coluna)` ignora `NULL`.
- `COUNT(DISTINCT coluna)` conta valores únicos.

---

### SUM

**O que faz:** soma os valores de uma coluna numérica.

**Sintaxe**
```sql
SELECT SUM(coluna) FROM tabela;
```

**Exemplo**
```sql
SELECT SUM(Quantity) AS TotalItens
FROM OrderDetails;
```

**Notas**
- Ignora `NULL`.
- Use `GROUP BY` para somar por categoria.

---

### AVG

**O que faz:** calcula a média dos valores de uma coluna numérica.

**Sintaxe**
```sql
SELECT AVG(coluna) FROM tabela;
```

**Exemplo**
```sql
SELECT AVG(Price) AS PrecoMedio
FROM Products;
```

**Notas**
- Ignora `NULL`.
- Para média por grupo, combine com `GROUP BY`.

---

### GROUP BY

**O que faz:** agrupa linhas com valores iguais para aplicar agregações.

**Sintaxe**
```sql
SELECT coluna, COUNT(*)
FROM tabela
GROUP BY coluna;
```

**Exemplo**
```sql
SELECT Country, COUNT(*) AS Total
FROM Customers
GROUP BY Country;
```

**Notas**
- Toda coluna do `SELECT` que não está em uma agregação deve estar no
  `GROUP BY` (na maioria dos SGBDs).
- Pode agrupar por várias colunas: `GROUP BY Country, City;`

---

### HAVING

**O que faz:** filtra grupos depois da agregação.

**Sintaxe**
```sql
SELECT coluna, COUNT(*)
FROM tabela
GROUP BY coluna
HAVING condição;
```

**Exemplo**
```sql
SELECT Country, COUNT(*) AS Total
FROM Customers
GROUP BY Country
HAVING COUNT(*) > 5;
```

**Notas**
- `WHERE` filtra linhas antes do agrupamento.
- `HAVING` filtra grupos depois do agrupamento.
- `HAVING` pode usar funções de agregação; `WHERE` não.

---

## Junções e conjuntos

### JOINs

**O que fazem:** combinam linhas de duas ou mais tabelas com base em uma
condição.

**Sintaxe**
```sql
SELECT a.coluna, b.coluna
FROM tabela_a AS a
JOIN tabela_b AS b
  ON a.chave = b.chave;
```

Tipos principais:

| Tipo | Retorna |
|---|---|
| `INNER JOIN` | apenas correspondências |
| `LEFT JOIN` | tudo da esquerda + correspondências |
| `RIGHT JOIN` | tudo da direita + correspondências |
| `FULL JOIN` | tudo dos dois lados |

**Exemplo**
```sql
SELECT o.OrderID, c.CustomerName
FROM Orders AS o
INNER JOIN Customers AS c
  ON o.CustomerID = c.CustomerID;
```

---

### INNER JOIN

**O que faz:** retorna apenas as linhas que têm correspondência nas duas
tabelas.

**Sintaxe**
```sql
SELECT colunas
FROM tabela_a
INNER JOIN tabela_b
  ON tabela_a.chave = tabela_b.chave;
```

**Exemplo**
```sql
SELECT o.OrderID, c.CustomerName
FROM Orders AS o
INNER JOIN Customers AS c
  ON o.CustomerID = c.CustomerID;
```

**Notas**
- `JOIN` sozinho equivale a `INNER JOIN`.
- Linhas sem correspondência ficam de fora.

---

### LEFT JOIN

**O que faz:** retorna todas as linhas da tabela da esquerda e as
correspondências da direita.

**Sintaxe**
```sql
SELECT colunas
FROM tabela_a
LEFT JOIN tabela_b
  ON tabela_a.chave = tabela_b.chave;
```

**Exemplo**
```sql
SELECT c.CustomerName, o.OrderID
FROM Customers AS c
LEFT JOIN Orders AS o
  ON c.CustomerID = o.CustomerID;
```

**Notas**
- Quando não há correspondência, as colunas da direita vêm como `NULL`.
- Útil para encontrar registros órfãos: `WHERE o.OrderID IS NULL`.

---

### RIGHT JOIN

**O que faz:** retorna todas as linhas da tabela da direita e as
correspondências da esquerda.

**Sintaxe**
```sql
SELECT colunas
FROM tabela_a
RIGHT JOIN tabela_b
  ON tabela_a.chave = tabela_b.chave;
```

**Exemplo**
```sql
SELECT c.CustomerName, o.OrderID
FROM Orders AS o
RIGHT JOIN Customers AS c
  ON o.CustomerID = c.CustomerID;
```

> **Dialetos:** SQLite só passou a suportar `RIGHT JOIN` na versão 3.39.
> Em SGBDs antigos, inverta a ordem e use `LEFT JOIN`.

---

### FULL JOIN

**O que faz:** retorna todas as linhas das duas tabelas, com `NULL` onde não
há correspondência.

**Sintaxe**
```sql
SELECT colunas
FROM tabela_a
FULL OUTER JOIN tabela_b
  ON tabela_a.chave = tabela_b.chave;
```

**Exemplo**
```sql
SELECT c.CustomerName, o.OrderID
FROM Customers AS c
FULL OUTER JOIN Orders AS o
  ON c.CustomerID = o.CustomerID;
```

> **Dialetos:** MySQL não suporta `FULL OUTER JOIN`; emule com
> `LEFT JOIN ... UNION ... RIGHT JOIN`.

---

### SELF JOIN

**O que faz:** junta uma tabela com ela mesma. Útil para comparar linhas da
mesma tabela.

**Sintaxe**
```sql
SELECT a.coluna, b.coluna
FROM tabela AS a
JOIN tabela AS b
  ON a.chave = b.chave;
```

**Exemplo**
```sql
SELECT
    a.CustomerName AS Cliente1,
    b.CustomerName AS Cliente2,
    a.City
FROM Customers AS a
JOIN Customers AS b
  ON a.City = b.City
 AND a.CustomerID < b.CustomerID;
```

**Notas**
- É obrigatório usar aliases diferentes para a mesma tabela.
- A condição extra `a.CustomerID < b.CustomerID` evita pares repetidos e a
  comparação de uma linha com ela mesma.

---

### UNION

**O que faz:** combina o resultado de duas consultas, removendo duplicatas.

**Sintaxe**
```sql
SELECT coluna FROM tabela_a
UNION
SELECT coluna FROM tabela_b;
```

**Exemplo**
```sql
SELECT City FROM Customers
UNION
SELECT City FROM Suppliers;
```

**Notas**
- As consultas precisam ter a mesma quantidade de colunas e tipos compatíveis.
- A ordem final não é garantida sem `ORDER BY`.
- `UNION` remove duplicatas; `UNION ALL` as mantém.

---

### UNION ALL

**O que faz:** combina resultados mantendo as duplicatas.

**Sintaxe**
```sql
SELECT coluna FROM tabela_a
UNION ALL
SELECT coluna FROM tabela_b;
```

**Exemplo**
```sql
SELECT City FROM Customers
UNION ALL
SELECT City FROM Suppliers;
```

**Notas**
- Costuma ser mais rápido que `UNION`, por não remover duplicatas.
- Use quando as duplicatas são esperadas ou não importam.

---

### EXISTS

**O que faz:** verifica se uma subconsulta retorna pelo menos uma linha.

**Sintaxe**
```sql
SELECT coluna
FROM tabela
WHERE EXISTS (subconsulta);
```

**Exemplo**
```sql
SELECT SupplierName
FROM Suppliers
WHERE EXISTS (
    SELECT 1
    FROM Products
    WHERE Products.SupplierID = Suppliers.SupplierID
      AND Price < 20
);
```

**Notas**
- `NOT EXISTS` faz o oposto.
- Costuma ser mais eficiente que `IN` em subconsultas grandes.

---

### ANY

**O que faz:** compara um valor com **qualquer** valor retornado por uma
subconsulta.

**Sintaxe**
```sql
SELECT coluna
FROM tabela
WHERE coluna > ANY (subconsulta);
```

**Exemplo**
```sql
SELECT ProductName
FROM Products
WHERE ProductID = ANY (
    SELECT ProductID
    FROM OrderDetails
    WHERE Quantity > 10
);
```

> **Dialetos:** MySQL e PostgreSQL suportam `ANY`/`SOME`. SQLite não suporta
> `ANY`; use `IN` ou `EXISTS`.

---

### ALL

**O que faz:** compara um valor com **todos** os valores retornados por uma
subconsulta.

**Sintaxe**
```sql
SELECT coluna
FROM tabela
WHERE coluna > ALL (subconsulta);
```

**Exemplo**
```sql
SELECT ProductName
FROM Products
WHERE Price > ALL (
    SELECT Price
    FROM Products
    WHERE CategoryID = 1
);
```

> **Dialetos:** assim como `ANY`, `ALL` não é suportado pelo SQLite.

---

## Alteração de dados

### INSERT INTO

**O que faz:** insere novas linhas em uma tabela.

**Sintaxe**
```sql
INSERT INTO tabela (coluna1, coluna2)
VALUES (valor1, valor2);
```

**Exemplo**
```sql
INSERT INTO Customers (CustomerName, ContactName, City, Country)
VALUES ('João Silva', 'João Silva', 'São Paulo', 'Brazil');
```

**Notas**
- As colunas e os valores precisam estar na mesma ordem.
- É possível inserir várias linhas de uma vez:
  `VALUES (...), (...), (...);`
- Colunas omitidas recebem `NULL` ou o valor `DEFAULT`.

---

### INSERT INTO SELECT

**O que faz:** insere o resultado de uma consulta em outra tabela.

**Sintaxe**
```sql
INSERT INTO tabela_destino (coluna1, coluna2)
SELECT coluna1, coluna2
FROM tabela_origem
WHERE condição;
```

**Exemplo**
```sql
INSERT INTO Customers (CustomerName, City, Country)
SELECT SupplierName, City, Country
FROM Suppliers
WHERE Country = 'Brazil';
```

**Notas**
- A quantidade e os tipos das colunas precisam ser compatíveis.
- A tabela de destino precisa existir.

---

### UPDATE

**O que faz:** altera valores de linhas existentes.

**Sintaxe**
```sql
UPDATE tabela
SET coluna1 = valor1, coluna2 = valor2
WHERE condição;
```

**Exemplo**
```sql
UPDATE Customers
SET ContactName = 'João da Silva'
WHERE CustomerID = 1;
```

**Notas**
- **Sempre** use `WHERE`. Sem ele, todas as linhas são alteradas.
- Faça um `SELECT` com o mesmo `WHERE` antes de atualizar, para conferir.

---

### DELETE

**O que faz:** remove linhas de uma tabela.

**Sintaxe**
```sql
DELETE FROM tabela
WHERE condição;
```

**Exemplo**
```sql
DELETE FROM Customers
WHERE CustomerName = 'João Silva';
```

**Notas**
- **Sempre** use `WHERE`. Sem ele, a tabela fica vazia.
- `DELETE` remove linhas; `DROP TABLE` remove a tabela inteira.
- `TRUNCATE TABLE` esvazia a tabela de forma mais rápida em alguns SGBDs.

---

### SELECT INTO

**O que faz:** cria uma nova tabela a partir do resultado de uma consulta.

**Sintaxe**
```sql
SELECT colunas
INTO nova_tabela
FROM tabela_origem
WHERE condição;
```

**Exemplo**
```sql
SELECT *
INTO CustomersBackup
FROM Customers;
```

> **Dialetos:** `SELECT INTO` é do SQL Server. Em PostgreSQL, MySQL e SQLite,
> use `CREATE TABLE nova_tabela AS SELECT ...;`

---

## Estrutura do banco

### CREATE DATABASE

**O que faz:** cria um novo banco de dados.

**Sintaxe**
```sql
CREATE DATABASE nome_do_banco;
```

**Exemplo**
```sql
CREATE DATABASE estudos;
```

> **Dialetos:** no SQLite, o banco é um arquivo; não existe `CREATE DATABASE`.
> No PostgreSQL, o comando é `CREATE DATABASE`; no MySQL, igual.

---

### DROP DATABASE

**O que faz:** apaga um banco de dados inteiro.

**Sintaxe**
```sql
DROP DATABASE nome_do_banco;
```

**Exemplo**
```sql
DROP DATABASE estudos;
```

**Notas**
- Operação irreversível.
- Alguns SGBDs exigem que o banco não esteja em uso.

---

### BACKUP DATABASE

**O que faz:** cria uma cópia de segurança do banco.

**Sintaxe**
```sql
-- SQL Server
BACKUP DATABASE nome_do_banco
TO DISK = 'caminho\arquivo.bak';
```

**Exemplo**
```sql
BACKUP DATABASE estudos
TO DISK = 'D:\backups\estudos.bak';
```

> **Dialetos:** o comando varia muito. PostgreSQL usa `pg_dump`, MySQL usa
> `mysqldump`, SQLite usa `.backup` ou copiar o arquivo.

---

### CREATE TABLE

**O que faz:** cria uma tabela com colunas e tipos.

**Sintaxe**
```sql
CREATE TABLE nome (
    coluna1 tipo [restrições],
    coluna2 tipo [restrições]
);
```

**Exemplo**
```sql
CREATE TABLE Persons (
    PersonID  INT          PRIMARY KEY,
    LastName  VARCHAR(100) NOT NULL,
    FirstName VARCHAR(100),
    City      VARCHAR(60)
);
```

**Tipos comuns**
- `INT` / `INTEGER` — números inteiros.
- `DECIMAL(p, s)` / `NUMERIC(p, s)` — números com casas decimais.
- `VARCHAR(n)` — texto de tamanho variável.
- `TEXT` — texto longo.
- `DATE`, `DATETIME`, `TIMESTAMP` — datas e horas.
- `BOOLEAN` — verdadeiro/falso (varia por SGBD).

---

### DROP TABLE

**O que faz:** apaga uma tabela e seus dados.

**Sintaxe**
```sql
DROP TABLE nome;
DROP TABLE IF EXISTS nome;
```

**Exemplo**
```sql
DROP TABLE IF EXISTS Persons;
```

**Notas**
- Irreversível.
- `IF EXISTS` evita erro quando a tabela não existe (suporte varia).

---

### ALTER TABLE

**O que faz:** altera a estrutura de uma tabela existente.

**Sintaxe**
```sql
-- adicionar coluna
ALTER TABLE tabela ADD coluna tipo;

-- remover coluna
ALTER TABLE tabela DROP COLUMN coluna;

-- renomear tabela
ALTER TABLE tabela RENAME TO novo_nome;
```

**Exemplo**
```sql
ALTER TABLE Persons ADD Email VARCHAR(150);
```

> **Dialetos:** para alterar o tipo de uma coluna, SQL Server usa
> `ALTER COLUMN`, MySQL usa `MODIFY COLUMN` e PostgreSQL usa
> `ALTER COLUMN ... TYPE`.

---

### Constraints

**O que fazem:** regras aplicadas às colunas para garantir a integridade dos
dados.

Principais restrições:

| Restrição | Garante |
|---|---|
| `NOT NULL` | valor obrigatório |
| `UNIQUE` | valores únicos |
| `PRIMARY KEY` | identificador único e não nulo |
| `FOREIGN KEY` | referência válida a outra tabela |
| `CHECK` | condição válida |
| `DEFAULT` | valor padrão |

**Exemplo**
```sql
CREATE TABLE Persons (
    PersonID INT PRIMARY KEY,
    LastName VARCHAR(100) NOT NULL,
    Email    VARCHAR(150) UNIQUE,
    Age      INT CHECK (Age >= 0)
);
```

---

### NOT NULL

**O que faz:** impede que a coluna receba `NULL`.

**Sintaxe**
```sql
coluna tipo NOT NULL
```

**Exemplo**
```sql
CREATE TABLE Persons (
    PersonID INT PRIMARY KEY,
    LastName VARCHAR(100) NOT NULL
);
```

---

### UNIQUE

**O que faz:** garante que todos os valores da coluna sejam diferentes.

**Sintaxe**
```sql
coluna tipo UNIQUE
```

**Exemplo**
```sql
CREATE TABLE Persons (
    PersonID INT PRIMARY KEY,
    Email    VARCHAR(150) UNIQUE
);
```

**Notas**
- `UNIQUE` aceita `NULL` em alguns SGBDs (e pode permitir mais de um `NULL`).
- Uma tabela pode ter várias colunas `UNIQUE`, mas apenas uma `PRIMARY KEY`.

---

### PRIMARY KEY

**O que faz:** identifica cada linha de forma única; implica `NOT NULL` e
`UNIQUE`.

**Sintaxe**
```sql
coluna tipo PRIMARY KEY
```

**Exemplo**
```sql
CREATE TABLE Persons (
    PersonID INT PRIMARY KEY,
    LastName VARCHAR(100) NOT NULL
);
```

**Notas**
- Cada tabela deve ter uma chave primária.
- Pode ser composta: `PRIMARY KEY (coluna1, coluna2)`.

---

### FOREIGN KEY

**O que faz:** garante que um valor exista como chave em outra tabela.

**Sintaxe**
```sql
CONSTRAINT nome_fk
FOREIGN KEY (coluna)
REFERENCES outra_tabela (coluna)
```

**Exemplo**
```sql
CREATE TABLE Orders (
    OrderID    INT PRIMARY KEY,
    CustomerID INT,
    CONSTRAINT fk_orders_customer
        FOREIGN KEY (CustomerID)
        REFERENCES Customers (CustomerID)
);
```

**Notas**
- Impede referências a registros inexistentes.
- `ON DELETE CASCADE` remove os filhos quando o pai é apagado.
- Nem todo SGBD aplica a FK por padrão; no SQLite, ative com
  `PRAGMA foreign_keys = ON;`.

---

### CHECK

**O que faz:** valida uma condição antes de inserir ou atualizar.

**Sintaxe**
```sql
coluna tipo CHECK (condição)
```

**Exemplo**
```sql
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    Price     DECIMAL(10, 2) CHECK (Price >= 0)
);
```

**Notas**
- A condição precisa ser verdadeira para o registro ser aceito.
- `CHECK` com subconsultas não é suportado por todos os SGBDs.

---

### DEFAULT

**O que faz:** define um valor padrão quando a coluna não é informada.

**Sintaxe**
```sql
coluna tipo DEFAULT valor
```

**Exemplo**
```sql
CREATE TABLE Orders (
    OrderID   INT PRIMARY KEY,
    OrderDate DATE DEFAULT CURRENT_DATE,
    Status    VARCHAR(20) DEFAULT 'pendente'
);
```

**Notas**
- O valor padrão só é usado quando a coluna é omitida no `INSERT`.
- `DEFAULT` não substitui `NULL` explícito.

---

### CREATE INDEX

**O que faz:** cria um índice para acelerar consultas em uma coluna.

**Sintaxe**
```sql
CREATE INDEX nome_do_indice
ON tabela (coluna);
```

**Exemplo**
```sql
CREATE INDEX idx_customers_country
ON Customers (Country);
```

**Notas**
- Índices aceleram leituras, mas deixam inserções e atualizações mais lentas.
- Índice único: `CREATE UNIQUE INDEX ...`
- `DROP INDEX nome_do_indice;` remove o índice.

---

### AUTO INCREMENT

**O que faz:** gera automaticamente um número sequencial para a coluna.

**Sintaxe por dialeto**
```sql
-- MySQL
id INT AUTO_INCREMENT PRIMARY KEY

-- SQL Server
id INT IDENTITY(1,1) PRIMARY KEY

-- PostgreSQL
id SERIAL PRIMARY KEY

-- SQLite
id INTEGER PRIMARY KEY AUTOINCREMENT
```

**Exemplo**
```sql
CREATE TABLE Persons (
    PersonID INTEGER PRIMARY KEY AUTOINCREMENT,
    LastName VARCHAR(100) NOT NULL
);
```

> **Dialetos:** a sintaxe muda bastante. Em PostgreSQL moderno, também é
> possível usar `GENERATED ALWAYS AS IDENTITY`.

---

### Datas

**O que fazem:** armazenam e manipulam datas e horas.

**Tipos comuns**
- `DATE` — apenas data.
- `DATETIME` — data e hora.
- `TIMESTAMP` — data e hora, normalmente com fuso.
- `TIME` — apenas hora.

**Exemplo**
```sql
SELECT OrderID, OrderDate
FROM Orders
WHERE OrderDate >= '2024-01-01';
```

**Funções por dialeto**
| Objetivo | MySQL | PostgreSQL | SQL Server | SQLite |
|---|---|---|---|---|
| data/hora atual | `NOW()` | `NOW()` | `GETDATE()` | `datetime('now')` |
| data atual | `CURDATE()` | `CURRENT_DATE` | `CAST(GETDATE() AS DATE)` | `date('now')` |
| somar dias | `DATE_ADD(d, INTERVAL 1 DAY)` | `d + INTERVAL '1 day'` | `DATEADD(day, 1, d)` | `date(d, '+1 day')` |

**Notas**
- Use o formato `YYYY-MM-DD` para evitar ambiguidade.
- Comparar datas com strings funciona na maioria dos SGBDs, mas cuidado com
  hora e fuso.

---

### VIEWS

**O que faz:** cria uma “tabela virtual” a partir de uma consulta salva.

**Sintaxe**
```sql
CREATE VIEW nome_da_view AS
SELECT colunas
FROM tabela
WHERE condição;
```

**Exemplo**
```sql
CREATE VIEW ClientesBrasil AS
SELECT CustomerName, City
FROM Customers
WHERE Country = 'Brazil';
```

**Uso**
```sql
SELECT * FROM ClientesBrasil;
```

**Notas**
- A view não armazena dados; ela executa a consulta sempre que é acessada.
- `CREATE OR REPLACE VIEW` atualiza a definição (suporte varia).
- `DROP VIEW nome_da_view;` remove a view.
- Views com joins e agregações podem não ser atualizáveis.

---

### Stored Procedures

**O que faz:** salva um bloco de SQL no banco para ser executado depois.

**Sintaxe**
```sql
-- MySQL
CREATE PROCEDURE nome_procedure()
BEGIN
    SELECT * FROM Customers;
END;
```

**Exemplo**
```sql
-- MySQL
CREATE PROCEDURE ListarClientes()
BEGIN
    SELECT CustomerName, Country
    FROM Customers;
END;

CALL ListarClientes();
```

**Notas**
- SQL Server usa `CREATE PROCEDURE ... AS ...` e `EXEC`.
- PostgreSQL usa `CREATE PROCEDURE` ou `CREATE FUNCTION` com `LANGUAGE plpgsql`.
- SQLite não tem stored procedures.
- Procedures podem receber parâmetros e conter lógica de controle.

---

## Segurança e operação

### SQL Injection

**O que é:** uma falha em que dados do usuário são concatenados diretamente
no SQL, permitindo que comandos maliciosos sejam executados.

**Exemplo vulnerável**
```sql
-- Não faça isto: o valor entra direto na consulta
SELECT *
FROM Customers
WHERE CustomerName = 'valor_digitado';
```

Se o valor for `' OR '1'='1`, a condição passa a ser sempre verdadeira.

**Como evitar**
- Use **prepared statements** com parâmetros.
- Valide e limite os dados de entrada.
- Aplique o princípio do menor privilégio no usuário do banco.
- Nunca concatene texto do usuário em comandos SQL.

---

### Parâmetros

**O que fazem:** separam o comando SQL dos valores, evitando injeção.

**Sintaxe por driver**
```text
?        -- SQLite, MySQL (alguns drivers)
$1       -- PostgreSQL
@p1      -- SQL Server
:name    -- Oracle e alguns drivers Python
```

**Exemplo conceitual**
```sql
SELECT *
FROM Customers
WHERE Country = ?;
```

**Notas**
- O valor é enviado separadamente da consulta.
- O banco trata o valor como dado, não como código.

---

### Prepared Statements

**O que fazem:** pré-compilam a consulta e executam com parâmetros.

**Exemplo em Python (SQLite)**
```python
import sqlite3

conn = sqlite3.connect("banco.db")
cursor = conn.cursor()

cursor.execute(
    "SELECT * FROM Customers WHERE Country = ?",
    ("Brazil",),
)
for linha in cursor.fetchall():
    print(linha)
```

**Notas**
- A consulta é compilada uma vez e pode ser executada várias vezes.
- É a forma recomendada de receber dados externos.
- A sintaxe do placeholder varia conforme o driver.

---

### Hosting

**O que é:** onde o banco de dados fica hospedado.

Opções comuns:

- **Serviço gerenciado** — o provedor cuida de backup, atualização e
  disponibilidade (ex.: RDS, Cloud SQL, Azure SQL).
- **VPS ou servidor próprio** — mais controle, mais manutenção.
- **Local** — ideal para estudo e desenvolvimento.

Pontos de atenção:

- backup e restauração;
- segurança e controle de acesso;
- custo e escalabilidade;
- latência e localização dos dados;
- conformidade com LGPD.

---

## Fontes

- Ementa e playground: [W3Schools — SQL Tutorial](https://www.w3schools.com/sql/)
- Material de estudo original: PDFs locais em `documentos/` (DataCamp).
