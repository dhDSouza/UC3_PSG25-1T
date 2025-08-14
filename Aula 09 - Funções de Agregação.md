# 📚 Aula 9: Funções de Agregação em SQL

## 🎯 Objetivo da Aula

Aprender a usar **funções de agregação** para realizar cálculos em conjuntos de dados, agrupar resultados e filtrar grupos com condições especiais.

---

## 🧠 Conceitos Fundamentais

### O que são Funções de Agregação?

São funções que realizam cálculos em um conjunto de valores e retornam um único valor resumido.

### Por que usamos?

- Calcular métricas importantes
- Identificar padrões nos dados
- Tomar decisões baseadas em dados agregados

---

## 📊 Principais Funções de Agregação

### 1. COUNT() - Contar registros

```sql
-- Conta todos os clientes
SELECT COUNT(*) AS total_clientes FROM clientes;

-- Conta clientes de Porto Alegre
SELECT COUNT(*) FROM clientes WHERE cidade = 'Porto Alegre';
```

### 2. SUM() - Soma de valores

```sql
-- Soma total gasto em todas as compras
SELECT SUM(preco * quantidade) AS total_vendas
FROM compras co, produtos p
WHERE co.produto_id = p.id;
```

### 3. AVG() - Média de valores

```sql
-- Preço médio dos produtos
SELECT AVG(preco) AS preco_medio FROM produtos;

-- Média de idade dos clientes
SELECT AVG(idade) FROM clientes;
```

### 4. MAX() - Valor máximo

```sql
-- Produto mais caro
SELECT MAX(preco) FROM produtos;

-- Data da última compra
SELECT MAX(data_compra) FROM compras;
```

### 5. MIN() - Valor mínimo

```sql
-- Produto mais barato
SELECT MIN(preco) FROM produtos;

-- Menor quantidade comprada
SELECT MIN(quantidade) FROM compras;
```

---

## 🔍 GROUP BY - Agrupando Resultados

Permite agrupar linhas que têm os mesmos valores em colunas especificadas.

```sql
SELECT categoria, COUNT(*) AS qtd_produtos
FROM produtos
GROUP BY categoria;
```

📌 **Exemplo prático**: Vendas por categoria

```sql
SELECT p.categoria, SUM(p.preco * co.quantidade) AS total_vendido
FROM produtos p, compras co
WHERE p.id = co.produto_id
GROUP BY p.categoria;
```

⚠️ **Regra importante**: Todas as colunas no SELECT devem estar no GROUP BY ou em funções de agregação.

---

## 📝 HAVING - Filtrando Grupos

O WHERE filtra linhas, o HAVING filtra grupos.

```sql
SELECT cidade, COUNT(*) AS qtd_clientes
FROM clientes
GROUP BY cidade
HAVING COUNT(*) > 5;  -- Só cidades com mais de 5 clientes
```

📌 **Exemplo avançado**:

```sql
SELECT p.categoria, 
       AVG(p.preco) AS preco_medio,
       SUM(co.quantidade) AS unidades_vendidas
FROM produtos p, compras co
WHERE p.id = co.produto_id
GROUP BY p.categoria
HAVING AVG(p.preco) > 500 AND SUM(co.quantidade) > 10;
```

---

## 🛠️ Técnicas Avançadas

### 1. Múltiplos níveis de agregação

```sql
SELECT 
    c.cidade,
    p.categoria,
    COUNT(*) AS qtd_compras,
    SUM(p.preco * co.quantidade) AS total_vendido
FROM clientes c, compras co, produtos p
WHERE c.id = co.cliente_id AND p.id = co.produto_id
GROUP BY c.cidade, p.categoria;
```

### 2. Ordenando resultados agregados

```sql
SELECT p.nome, SUM(co.quantidade) AS total_vendido
FROM produtos p, compras co
WHERE p.id = co.produto_id
GROUP BY p.nome
ORDER BY total_vendido DESC
LIMIT 5;  -- Top 5 produtos mais vendidos
```

### 3. Agregação condicional

```sql
SELECT 
    c.cidade,
    SUM(CASE WHEN p.categoria = 'Eletrônicos' THEN 1 ELSE 0 END) AS qtd_eletronicos,
    SUM(CASE WHEN p.categoria = 'Informática' THEN 1 ELSE 0 END) AS qtd_informatica
FROM clientes c, compras co, produtos p
WHERE c.id = co.cliente_id AND p.id = co.produto_id
GROUP BY c.cidade;
```

---

## ⚠️ Armadilhas Comuns

1. **Esquecer do GROUP BY**: Usar colunas não agregadas sem agrupamento causa erro.
2. **Confundir WHERE e HAVING**:
   - WHERE filtra antes da agregação
   - HAVING filtra depois da agregação
3. **Desempenho**: Agregações em grandes tabelas podem ser lentas.

---

## 🚀 Exemplos Práticos com Nosso Banco

### 1. Média de preço por categoria

```sql
SELECT categoria, AVG(preco) AS preco_medio
FROM produtos
GROUP BY categoria
ORDER BY preco_medio DESC;
```

### 2. Total gasto por cliente

```sql
SELECT c.nome, SUM(p.preco * co.quantidade) AS total_gasto
FROM clientes c, compras co, produtos p
WHERE c.id = co.cliente_id AND p.id = co.produto_id
GROUP BY c.nome
ORDER BY total_gasto DESC;
```

### 3. Produtos que venderam mais unidades

```sql
SELECT p.nome, SUM(co.quantidade) AS total_unidades
FROM produtos p, compras co
WHERE p.id = co.produto_id
GROUP BY p.nome
HAVING SUM(co.quantidade) > 50
ORDER BY total_unidades DESC;
```

### 4. As 3 cidades com maior volume de compras

```sql
SELECT c.cidade, SUM(p.preco * co.quantidade) AS volume_compras
FROM clientes c, compras co, produtos p
WHERE c.id = co.cliente_id AND p.id = co.produto_id
GROUP BY c.cidade
ORDER BY volume_compras DESC
LIMIT 3;
```

### 5. Clientes que compram acima da média

```sql
SELECT c.nome, SUM(p.preco * co.quantidade) AS total_gasto
FROM clientes c, compras co, produtos p
WHERE c.id = co.cliente_id AND p.id = co.produto_id
GROUP BY c.nome
HAVING SUM(p.preco * co.quantidade) > (
    SELECT AVG(p.preco * co.quantidade)
    FROM compras co, produtos p
    WHERE p.id = co.produto_id
);
```

---

## 🏋️ Exercícios

1. Conte quantos produtos existem em cada categoria.
2. Calcule o valor total em estoque (preço × quantidade) por categoria.
3. Liste as 5 cidades com mais clientes.
4. Mostre os produtos que nunca foram comprados.
5. Calcule a média de idade dos clientes por cidade.
6. Liste os clientes que gastaram mais de R$ 5000 no total.
7. Calcule o ticket médio (valor médio) por compra.
8. Liste as categorias com vendas médias superiores a R$ 1000.
9. Mostre a diferença entre o produto mais caro e o mais barato em cada categoria.
