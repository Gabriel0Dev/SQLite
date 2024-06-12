# Manipulando SQL

## Criando uma tabela

Para criar uma tabela, escreveremos o seguinte código:

```sql
CREATE TABLE filmes (
id INT,
nome TEXT,
ano DATE,
imdb DECIMAL
);
```

Neste exemplo, iremos criar uma tabela chamada **filmes** onde haverá quatro colunas distintas denominadas:

- **id**: que recebe o tipo de dado **INT**.
- **nome**: que recebe o tipo de dado **TEXT**.
- **ano**: que recebe o tipo de dado **DATE**.
- **imdb**: que recebe o tipo de dado **DECIMAL**.

## Inserindo valores

Para inserir valores na tabela **filmes**, escreveremos o seguinte código:

### Inserindo valores em ordem de coluna:

```sql
INSERT INTO filmes
VALUES (1, 'Defiance', '2008-12-31', 7.1);
```

### Inserção de dados por nome:

```sql
INSERT INTO filmes (nome, imdb)
VALUES ('Toy Story 4', 10.0);

INSERT INTO filmes (id, nome)
VALUES (3, 'A Volta dos que Não Foram.');
```

Neste exemplo, utilizando o comando **SELECT * FROM filmes**, retornará os seguintes dados:

| ID   | Nome                       | Ano        | IMDB |
| ---- | -------------------------- | ---------- | ---- |
| 1    | Defiance                   | 2008-12-31 | 7.1  |
| null | Toy Story 4                | null       | 10.0 |
| 3    | A Volta dos que Não Foram. | null       | null |

## Criando novas colunas

Para criar novas colunas na tabela **filmes**, escreveremos o seguinte código:

### Criando uma coluna de gênero para a tabela filmes:

```sql
ALTER TABLE filmes
ADD genero TEXT;
```

Neste código, ao utilizar o comando **SELECT * FROM filmes**, retornará os seguintes dados:

| ID   | Nome                       | Ano        | IMDB | Gênero |
| ---- | -------------------------- | ---------- | ---- | ------ |
| 1    | Defiance                   | 2008-12-31 | 7.1  |        |
| null | Toy Story 4                | null       | 10.0 | null   |
| 3    | A Volta dos que Não Foram. | null       | null | null   |

## Alterando dados da tabela

Alguns dados foram inseridos erroneamente na tabela e, em algumas ocasiões, estão faltando dados. Para resolver esse problema, utilizaremos o **UPDATE**.

### Atualizando dados do filme Defiance:

```sql
UPDATE filmes
SET genero = 'Ação'
WHERE id = 1;
```

### Atualizando dados do filme Toy Story 4:

```sql
UPDATE filmes
SET id = 2, ano = '2019-06-11', imdb = 7.7, genero = 'Animação'
WHERE nome = 'Toy Story 4';
```

Neste código, ao utilizar o comando **SELECT * FROM filmes**, retornará os seguintes dados:

| ID  | Nome                       | Ano        | IMDB | Gênero   |
| --- | -------------------------- | ---------- | ---- | -------- |
| 1   | Defiance                   | 2008-12-31 | 7.1  | Ação     |
| 2   | Toy Story 4                | 2019-06-11 | 7.7  | Animação |
| 3   | A Volta dos que Não Foram. | null       | null | null     |

## Deletando valores da tabela

Acidentalmente adicionamos um filme que não existe em nosso banco de dados. Por conta disso, iremos removê-lo da nossa tabela utilizando **DELETE**.

```sql
DELETE FROM filmes
WHERE id = 3;
```

Após utilizarmos esse código, ao utilizar o comando **SELECT * FROM filmes**, retornará os seguintes dados:

| ID  | Nome        | Ano        | IMDB | Gênero   |
| --- | ----------- | ---------- | ---- | -------- |
| 1   | Defiance    | 2008-12-31 | 7.1  | Ação     |
| 2   | Toy Story 4 | 2019-06-11 | 7.7  | Animação |

# Queries

Para esta etapa eu criei uma tabela com 90 filmes para melhor exemplificar estes atributos.

## Operador `AND`

O operador `AND` permite combinar várias condições. Para que um registro seja incluído no conjunto de resultados, ele deve atender a todas as condições unidas pelo `AND`.

```sql
SELECT nome FROM filmes 
WHERE imdb > 8.9 AND id < 30;
```

Resultado da tabela:
| Filmes          |
| --------------- |
| 12 Angry Men    |
| The Dark Knight |
| The Godfather   |

## Clausula `AS`

Colunas ou tabelas podem ser renomeadas usando a cláusula `AS`. Isso permite que colunas ou tabelas recebam nomes específicos no conjunto de resultados retornado. A consulta fornecida retornará um conjunto de resultados onde a coluna nome será renomeada para `titulo_filme`.

```sql
SELECT nome AS 'titulo_filme'
FROM filmes;
```

| titulo_filme           |
| ---------------------- |
| 12 Angry Men           |
| American History X     |
| City of God            |
| Fight Club             |
| Forrest Gump           |
| **Todos os filmes...** |

## Operador `OR`

O operador `OR` permite combinar várias condições. Registros que atendem a qualquer uma das condições unidas pelo `OR` são incluídos no conjunto de resultados. A consulta fornecida selecionará filmes cujo ano seja '1999' ou '2023'.

```sql
SELECT nome FROM filmes 
WHERE ano = '1999' OR ano = '2023';
```

## Wildcard `%`

O caractere wildcard `%` pode ser usado em um padrão com o operador `LIKE` para corresponder a zero ou mais caracteres não especificados. A consulta fornecida selecionará qualquer filme que comece com "The", seguido por zero ou mais caracteres quaisquer.

```sql
SELECT nome FROM movies
WHERE nome LIKE 'The%';
```

## Wildcard `_`

O curinga `_` pode ser usado em um padrão com o operador `LIKE` para corresponder a qualquer caractere único não especificado. A consulta fornecida encontrará qualquer filme que comece com um único caractere, seguido por "ove".

```sql
SELECT nome FROM movies
WHERE nome LIKE '_ove';
```

## Cláusula ORDER BY

A cláusula `ORDER BY` pode ser usada para ordenar o conjunto de resultados por uma coluna específica, seja alfabeticamente ou numericamente. Pode ser ordenada de duas maneiras:

- DESC é uma palavra-chave usada para ordenar os resultados em ordem decrescente.
- ASC é uma palavra-chave usada para ordenar os resultados em ordem crescente (padrão).

```sql
SELECT * FROM filmes
ORDER BY ano DESC;
```

## Operador `LIKE`

O operador `LIKE` pode ser usado dentro de uma cláusula `WHERE` para corresponder a um padrão especificado. A consulta fornecida encontrará qualquer filme que comece com "Star" em seu título.

```sql
SELECT nome FROM filmes
WHERE nome LIKE 'Star%';
```

## Cláusula DISTINCT

Valores únicos de uma coluna podem ser selecionados usando uma consulta `DISTINCT`. Para uma tabela `filmes` com cinco linhas nas quais a coluna `nome` contém 12 Angry Men, American History X, City of God, Fight Club, Forrest Gump a consulta fornecida retornaria:
- 12 Angry Men
- American History X
- City of God
- Fight Club
- Forrest Gump

```sql
SELECT DISTINCT nome FROM filmes;
```

## Operador `BETWEEN`

O operador `BETWEEN` pode ser usado para filtrar por um intervalo de valores. O intervalo de valores pode ser de texto, números ou dados de data. A consulta fornecida encontrará qualquer filme produzido entre os anos de 1980 e 1990, inclusive.

```sql
SELECT * FROM filmes
WHERE ano BETWEEN '1980-01-01' AND '1990-12-31';
```

## Cláusula `LIMIT`

A cláusula `LIMIT` é usada para restringir, ou limitar, um conjunto de resultados ao número especificado de linhas. A consulta fornecida limitará o conjunto de resultados a 5 linhas.

```sql
SELECT * FROM filmes LIMIT 5;
```

## Valores `NULL`

Os valores das colunas podem ser `NULL`, ou seja, não ter nenhum valor. Esses registros podem ser correspondidos (ou não) usando os operadores `IS NULL` e `IS NOT NULL` em combinação com a cláusula `WHERE`. A consulta fornecida encontrará todos os filmes onde o ano tem um valor ou não é `NULL`.

```sql
SELECT ano FROM filmes
WHERE ano IS NOT NULL;
```

## Cláusula `WHERE`

A cláusula `WHERE` é usada para filtrar registros (linhas) que correspondam a uma condição específica. A consulta fornecida selecionará todos os nomes dos filmes onde o ano é igual a 2017.

```sql
SELECT nome FROM filmes
WHERE ano = '2017-01-01';
```
