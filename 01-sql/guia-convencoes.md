# Guia de Convenções SQL

Adaptação em português do [SQL Style Guide](https://www.sqlstyle.guide/), de
Simon Holywell, publicado sob a licença
[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).

O objetivo é ter um padrão único para nomes, formatação e estrutura de SQL.
Consistência vale mais do que preferência pessoal: escolha uma regra e aplique
em todo o projeto.

> **Neste repositório:** a convenção é usar tabelas no plural
> (`authors`, `books`, `customers`) e colunas no singular. O guia original
> prefere nomes coletivos (`staff`) a plurais; as duas formas são aceitáveis,
> desde que você mantenha a mesma escolha.

---

## Índice

- [1. Princípios gerais](#1-princípios-gerais)
- [2. Nomenclatura](#2-nomenclatura)
- [3. Sintaxe de consultas](#3-sintaxe-de-consultas)
- [4. Sintaxe de criação](#4-sintaxe-de-criação)
- [5. Exemplo completo](#5-exemplo-completo)
- [6. Checklist rápido](#6-checklist-rápido)
- [7. Licença e atribuição](#7-licença-e-atribuição)

---

## 1. Princípios gerais

### Faça

- Use nomes descritivos, únicos e consistentes.
- Use espaçamento e indentação para facilitar a leitura.
- Armazene datas e horas no formato ISO 8601:
  `YYYY-MM-DDTHH:MM:SS.SSSSS`.
- Prefira funções SQL padrão (ANSI) às funções proprietárias, para manter a
  portabilidade.
- Escreva consultas curtas, sem redundâncias como parênteses desnecessários,
  aspas evitáveis ou condições que podem ser deduzidas.
- Comente o que não é óbvio. Prefira `/* ... */`; use `--` quando o comentário
  for de uma linha.

### Evite

- `camelCase` e `PascalCase` em identificadores.
- Prefixos descritivos ou notação húngara, como `tbl_`, `sp_` ou `col_`.
- Plural quando existe um coletivo mais natural (`staff` em vez de
  `employees`).
- Identificadores entre aspas. Se for inevitável, prefira aspas duplas no
  padrão SQL-92.
- Aplicar conceitos de orientação a objetos ao modelo relacional.

---

## 2. Nomenclatura

### Regras gerais

- O nome deve ser único e não pode ser uma palavra reservada.
- Use no máximo 30 bytes (normalmente 30 caracteres).
- Comece com uma letra e não termine com `_`.
- Use apenas letras, números e `_`.
- Não use `__` (underscore duplo).
- Use `_` onde haveria um espaço: `first_name`, `order_date`.
- Evite abreviações, a menos que sejam amplamente conhecidas.
- Use minúsculas; nomes próprios podem ser uma exceção justificada.

### Tabelas

- Prefira um nome coletivo (`staff`, `people`). Plural (`employees`) também é
  aceitável.
- Não use prefixos como `tbl_`.
- Uma tabela não pode ter o mesmo nome de uma de suas colunas, e vice-versa.
- Para tabelas de relacionamento, prefira um nome de domínio em vez de juntar
  os nomes das tabelas. Exemplo: `services` em vez de `cars_mechanics`.

### Colunas

- Use sempre o singular: `customer_name`, `order_date`.
- Evite `id` sozinho quando um nome mais descritivo for possível. Prefira
  `customer_id`, `book_id`.
- Uma coluna não pode ter o mesmo nome da tabela, e vice-versa.
- Use minúsculas.

### Aliases e correlações

- O alias deve ter relação com o objeto ou expressão que representa.
- Uma boa correlação usa as iniciais das palavras do nome:
  `customers` → `c`; `order_details` → `od`.
- Se o alias já estiver em uso, acrescente um número: `c1`, `c2`.
- Escreva sempre `AS`, mesmo quando for opcional.
- Para resultados calculados (`SUM`, `AVG` etc.), use o nome que a coluna
  mereceria no schema: `total_sales`, `average_price`.

### Stored procedures

- O nome deve conter um verbo: `get_customer`, `calculate_total`.
- Não use prefixos como `sp_`.

### Sufixos uniformes

| Sufixo | Uso | Exemplo |
|---|---|---|
| `_id` | identificador único, normalmente chave primária | `customer_id` |
| `_status` | situação ou flag | `order_status` |
| `_total` | total ou soma | `order_total` |
| `_num` | campo numérico | `invoice_num` |
| `_name` | nome | `product_name` |
| `_seq` | sequência contínua | `line_seq` |
| `_date` | data associada ao registro | `created_date` |
| `_tally` | contagem | `item_tally` |
| `_size` | tamanho | `file_size` |
| `_addr` | endereço físico ou lógico | `email_addr` |

---

## 3. Sintaxe de consultas

### Palavras reservadas

- Escreva palavras-chave em **MAIÚSCULAS**: `SELECT`, `FROM`, `WHERE`, `JOIN`.
- Evite abreviações quando existe a forma completa: `COUNT`, não `CNT`.
- Prefira a palavra-chave ANSI quando uma versão proprietária fizer o mesmo.

### Espaços

- Alinhe as palavras-chave raiz para que terminem na mesma coluna, criando uma
  separação visual no meio da consulta.
- Palavras-chave ficam alinhadas à direita; colunas e detalhes ficam à
  esquerda.
- Mantenha espaços antes e depois de `=`.
- Mantenha um espaço depois das vírgulas.

```sql
SELECT c.customer_name,
       c.country,
       o.order_date
  FROM customers AS c
  JOIN orders AS o
    ON o.customer_id = c.customer_id
 WHERE o.order_date >= '2024-01-01'
 ORDER BY o.order_date DESC;
```

### Quebras de linha

- Coloque `AND` e `OR` no início da linha, não no fim.
- Separe consultas com uma nova linha depois do `;`.
- Quebre a linha depois das palavras-chave que iniciam blocos.
- Quebre colunas em grupos lógicos, com uma vírgula no fim da linha anterior.
- Use linhas em branco para separar partes da consulta.

```sql
SELECT customer_id,
       customer_name,
       country
  FROM customers
 WHERE country = 'Brazil'
   AND customer_name LIKE 'A%'
    OR customer_name LIKE 'B%';
```

### Indentação

- Indente cláusulas de join para o lado oposto da separação visual.
- Agrupe joins relacionados com quebras de linha quando necessário.
- Ao usar `JOIN` sozinho, coloque-o antes da separação, não dentro do bloco.
- Alinhe subconsultas à direita da separação.
- Formate a consulta interna com a mesma estrutura da externa.
- Em aninhamentos profundos, coloque o parêntese de fechamento em uma linha
  própria, alinhado ao parêntese de abertura.

```sql
SELECT c.customer_name,
       (
           SELECT COUNT(*)
             FROM orders AS o
            WHERE o.customer_id = c.customer_id
       ) AS total_orders
  FROM customers AS c;
```

### Preferências de forma

- Prefira `BETWEEN` a várias condições `>=` e `<=`.
- Prefira `IN (...)` a várias comparações com `OR`.
- Use `CASE` quando um valor precisar ser interpretado antes de sair do banco.
  `CASE` aninhado é aceitável para lógica complexa.
- Evite `UNION` e tabelas temporárias quando for possível resolver o problema
  melhorando o schema.
- Use `EXISTS` em vez de `COUNT(*) > 0` para testar existência.
- Evite `SELECT *` em código de produção; liste as colunas necessárias.
- Use `IS NULL` e `IS NOT NULL`, nunca `= NULL`.
- Prefira `COALESCE` às funções proprietárias equivalentes.

---

## 4. Sintaxe de criação

### Estrutura geral

- Mantenha o DDL legível para humanos.
- Agrupe as colunas em ordem lógica.
- Indente as definições de coluna com quatro espaços dentro do `CREATE`.

```sql
CREATE TABLE customers (
    CONSTRAINT pk_customers PRIMARY KEY (customer_id),
    customer_id   INTEGER      NOT NULL,
    customer_name VARCHAR(100) NOT NULL,
    country       VARCHAR(60),
    created_at    TIMESTAMP    NOT NULL DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT uq_customers_name UNIQUE (customer_name)
);
```

### Escolha de tipos de dados

- Evite tipos proprietários; prefira tipos portáveis.
- Use `REAL` ou `FLOAT` apenas quando a matemática de ponto flutuante for
  realmente necessária.
- Nos demais casos, prefira `NUMERIC` ou `DECIMAL`, que não sofrem os
  arredondamentos do ponto flutuante.

Tipos portáveis comuns:

| Categoria | Tipos |
|---|---|
| Texto | `CHAR`, `VARCHAR`, `CLOB` |
| Inteiros | `SMALLINT`, `INTEGER`, `BIGINT` |
| Decimais exatos | `DECIMAL`, `NUMERIC`, `DECFLOAT` |
| Ponto flutuante | `REAL`, `FLOAT`, `DOUBLE PRECISION` |
| Datas e horas | `DATE`, `TIME`, `TIMESTAMP` |
| Binários | `BINARY`, `VARBINARY`, `BLOB` |
| Outros | `BOOLEAN`, `INTERVAL`, `XML` |

### Valores padrão

- O valor padrão deve ser compatível com o tipo da coluna.
- Coloque o `DEFAULT` depois do tipo e antes de `NOT NULL`.

```sql
created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
```

### Constraints e chaves

- Toda tabela deve ter pelo menos uma chave.
- Nomeie as constraints, exceto `UNIQUE`, `PRIMARY KEY` e `FOREIGN KEY`, em que
  o nome gerado pelo SGBD pode ser suficiente.
- Escolha chaves com unicidade significativa, tipo estável, valores validáveis
  e estrutura simples. Chaves compostas são permitidas quando necessárias.
- Declare a chave primária logo depois da abertura da tabela.
- Defina constraints específicas de uma coluna logo abaixo dela, alinhadas ao
  nome da coluna.
- Coloque constraints de várias colunas perto delas; se não for possível,
  deixe no fim.
- Coloque constraints da tabela inteira no fim.
- Quando ordenar cláusulas, coloque `ON DELETE` antes de `ON UPDATE`.
- Alinhe aspectos repetidos, como `NOT NULL`, na mesma posição quando for
  prático.

### Validação

- Use `LIKE` ou `SIMILAR TO` para formatos de texto conhecidos.
- Use `CHECK` para limitar faixas numéricas e evitar inserções inválidas.
- Na maioria dos casos, valores numéricos devem ser maiores que zero.
- Mantenha cada `CHECK` em uma cláusula separada para facilitar a depuração.

```sql
CREATE TABLE order_items (
    CONSTRAINT pk_order_items PRIMARY KEY (order_id, product_id),
    order_id   INTEGER NOT NULL,
    product_id INTEGER NOT NULL,
    quantity   INTEGER NOT NULL,
    unit_price NUMERIC(10, 2) NOT NULL,
    CONSTRAINT ck_order_items_quantity CHECK (quantity > 0),
    CONSTRAINT ck_order_items_price    CHECK (unit_price > 0)
);
```

### Designs a evitar

- Forçar orientação a objetos no modelo relacional.
- Separar valor e unidade em colunas diferentes; deixe a unidade clara no nome
  da coluna e use `CHECK` quando necessário.
- Tabelas no modelo Entidade–Atributo–Valor (EAV); se precisar desse tipo de
  dado, use uma solução específica para dados sem schema.
- Dividir um mesmo conjunto de dados em várias tabelas por tempo, localização
  ou outro critério arbitrário; isso obriga `UNION`s desconfortáveis depois.

---

## 5. Exemplo completo

### Antes

```sql
select c.CustomerName,o.OrderDate,sum(od.Quantity) as Total
from Customers c, Orders o, OrderDetails od
where c.CustomerID=o.CustomerID and o.OrderID=od.OrderID
and o.OrderDate>='2024-01-01'
group by c.CustomerName,o.OrderDate
having sum(od.Quantity)>10;
```

Problemas: palavras-chave em minúsculas, `camelCase`, joins implícitos,
falta de espaços, aliases sem `AS`, colunas sem padronização.

### Depois

```sql
SELECT c.customer_name,
       o.order_date,
       SUM(od.quantity) AS total_quantity
  FROM customers AS c
  JOIN orders AS o
    ON o.customer_id = c.customer_id
  JOIN order_details AS od
    ON od.order_id = o.order_id
 WHERE o.order_date >= '2024-01-01'
 GROUP BY c.customer_name,
          o.order_date
HAVING SUM(od.quantity) > 10
 ORDER BY c.customer_name,
          o.order_date;
```

Agora o código está consistente, legível e com joins explícitos.

---

## 6. Checklist rápido

- [ ] Palavras-chave em maiúsculas.
- [ ] Identificadores em `snake_case` e minúsculos.
- [ ] Tabelas com nome coletivo ou plural, sempre igual.
- [ ] Colunas no singular.
- [ ] Chaves com sufixo `_id`.
- [ ] `AS` explícito em todos os aliases.
- [ ] Joins com `ON`, nunca com vírgula no `FROM`.
- [ ] `BETWEEN` e `IN` no lugar de múltiplos `OR`.
- [ ] `CASE` para lógica condicional.
- [ ] `NOT NULL`, `DEFAULT` e `CHECK` onde fazem sentido.
- [ ] Constraints nomeadas.
- [ ] Datas em ISO 8601.
- [ ] Comentários apenas onde o código não se explica.
- [ ] `SELECT *` evitado em produção.
- [ ] Nenhum prefixo húngaro (`tbl_`, `sp_`, `col_`).

---

## 7. Licença e atribuição

- **Original:** [SQL Style Guide](https://www.sqlstyle.guide/), de Simon
  Holywell.
- **Licença:** [Creative Commons Attribution-ShareAlike 4.0
  International](https://creativecommons.org/licenses/by-sa/4.0/).
- Esta adaptação é um resumo em português e também é distribuída sob a mesma
  licença. Consulte o original para a versão completa, a lista de palavras
  reservadas e as traduções disponíveis.
