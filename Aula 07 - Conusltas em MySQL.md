# 📚 Aula 7: Consultas em MySQL


## 🎯 Objetivo da Aula

Aprender a realizar **consultas mais elaboradas** em MySQL, **filtrando, ordenando e limitando** resultados para buscar informações específicas do banco de dados.

---

## 🧠 Revisão Rápida

Antes de avançarmos, lembre-se:

```sql
SELECT * FROM tabela;
```

Isso retorna **todos os registros** e **todas as colunas**, mas raramente é o ideal em sistemas reais.

---

## 🔑 Selecionando Colunas Específicas

Podemos buscar apenas as colunas necessárias:

```sql
SELECT nome, email FROM usuarios;
```

📌 **Por quê?** Menos dados → consultas mais rápidas e seguras.

---

## 🎯 Filtrando Dados com `WHERE`

Permite buscar registros que atendem a uma condição:

```sql
SELECT * FROM produtos
WHERE preco > 100;
```

### Operadores comuns:

* `=` (igual)
* `!=` ou `<>` (diferente)
* `>` `<` `>=` `<=`
* `BETWEEN valor1 AND valor2`
* `IN (valor1, valor2, ...)`
* `LIKE` (buscas com curingas `%` e `_`)
* `IS NULL` / `IS NOT NULL`

📌 **Exemplo prático**:

```sql
SELECT nome FROM clientes
WHERE cidade = 'São Paulo' AND idade BETWEEN 18 AND 30;
```

---

## 🔍 Pesquisando com `LIKE`

Útil para buscas parciais:

```sql
SELECT nome FROM produtos
WHERE nome LIKE 'C%'; -- começa com C

SELECT nome FROM produtos
WHERE nome LIKE '%fone%'; -- contém "fone"
```

---

## 🧮 Ordenando Resultados com `ORDER BY`

Permite organizar os resultados:

```sql
SELECT nome, preco FROM produtos
ORDER BY preco ASC; -- crescente

SELECT nome, preco FROM produtos
ORDER BY preco DESC; -- decrescente
```

📌 Dá para ordenar por múltiplas colunas:

```sql
ORDER BY categoria ASC, preco DESC;
```

---

## 🔝 Limitando Resultados com `LIMIT`

Para retornar apenas X registros:

```sql
SELECT * FROM usuarios
LIMIT 5;
```

Paginação:

```sql
SELECT * FROM usuarios
LIMIT 10 OFFSET 20; -- pula 20, pega 10
```

---

## 📊 Eliminando Duplicados com `DISTINCT`

Se quiser valores únicos:

```sql
SELECT DISTINCT cidade FROM clientes;
```

---

## ⚡ Desafios Práticos

1. Liste os nomes e preços dos produtos que custam mais de 200, ordenados do maior para o menor.
2. Mostre apenas as cidades únicas dos clientes cadastrados.
3. Liste os nomes dos produtos que contêm "game" no nome.
4. Mostre os 3 produtos mais baratos.
5. Liste os nomes dos clientes que moram em "Porto Alegre" ou "Canoas".
6. Liste o nome e a cidade dos clientes que moram em Canoas.
7. Mostre todos os clientes com idade entre 30 e 40 anos.
8. Liste o nome e preço dos produtos que contenham "Note" no nome.
9. Mostre todos os clientes que moram em São Paulo, Porto Alegre ou Curitiba.
10. Liste todos os produtos da categoria Games, ordenados do mais caro para o mais barato.
11. Mostre apenas os 5 primeiros produtos mais caros da tabela.
12. Liste os 3 clientes mais jovens (nome, idade e cidade).
13. Mostre os produtos com preço menor que 100 reais.
14. Liste nome e categoria dos produtos que custam mais de 1000 reais e sejam da categoria Informática ou Eletrônicos.
15. Mostre apenas as cidades distintas onde há clientes cadastrados.
16. Liste todos os clientes que não moram em São Paulo.
17. Mostre todos os produtos cujo preço não esteja entre 200 e 800 reais.
