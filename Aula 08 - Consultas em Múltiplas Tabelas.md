# 📚 Aula 8: Consultas em Múltiplas Tabelas

## 🎯 Objetivo da Aula

Aprender a realizar **consultas que envolvem múltiplas tabelas** apenas com condições `WHERE`, combinando dados de tabelas relacionadas de forma eficiente.

---

## 🧠 Revisão Rápida: Relacionamento entre Tabelas

Em bancos de dados relacionais, as tabelas estão conectadas através de **chaves**:

* **Chave primária (PK)**: Identificador único em uma tabela.
* **Chave estrangeira (FK)**: Referência a uma chave primária em outra tabela.

No nosso caso:

* **clientes.id** é PK da tabela `clientes`.
* **produtos.id** é PK da tabela `produtos`.
* **compras.cliente_id** é FK que aponta para `clientes.id`.
* **compras.produto_id** é FK que aponta para `produtos.id`.

---

## 🔗 Consultando Múltiplas Tabelas com WHERE

Podemos relacionar tabelas especificando a condição de relacionamento diretamente no `WHERE`:

```sql
SELECT tabela1.coluna, tabela2.coluna
FROM tabela1, tabela2
WHERE tabela1.chave = tabela2.chave;
```

📌 **Exemplo prático com nosso banco**:

```sql
SELECT c.nome AS cliente, p.nome AS produto
FROM clientes c, compras co, produtos p
WHERE c.id = co.cliente_id
  AND p.id = co.produto_id
  AND p.preco > 1000;
```

---

## 🔍 Tipos de Relacionamentos no Nosso Banco

### 1. Relacionamento 1:N (Um para Muitos)

Um cliente pode ter várias compras.

```sql
SELECT c.nome, co.id, co.data_compra
FROM clientes c, compras co
WHERE c.id = co.cliente_id;
```

### 2. Relacionamento N:M (Muitos para Muitos)

Um cliente pode comprar muitos produtos e um produto pode ser comprado por vários clientes.
A tabela `compras` faz essa ligação.

```sql
SELECT c.nome, p.nome, co.quantidade
FROM clientes c, compras co, produtos p
WHERE c.id = co.cliente_id
  AND p.id = co.produto_id;
```

---

## 🛠️ Técnicas Úteis

### 1. Aliases para Tabelas

Deixam a consulta mais curta e legível:

```sql
SELECT c.nome, p.nome
FROM clientes AS c, compras AS co, produtos AS p
WHERE c.id = co.cliente_id
  AND p.id = co.produto_id
  AND c.cidade = 'São Paulo'
  AND p.preco > 500;
```

### 2. Filtros Adicionais

Podemos combinar condições de múltiplas tabelas:

```sql
SELECT c.nome, p.nome
FROM clientes c, compras co, produtos p
WHERE c.id = co.cliente_id
  AND p.id = co.produto_id
  AND c.idade > 30
  AND p.categoria = 'Games'
  AND p.preco < 1000;
```

### 3. Ordenação Combinada

Ordenar usando colunas de tabelas diferentes:

```sql
SELECT c.nome, p.nome, p.preco
FROM clientes c, compras co, produtos p
WHERE c.id = co.cliente_id
  AND p.id = co.produto_id
ORDER BY c.nome ASC, p.preco DESC;
```

---

## ⚠️ Cuidados Importantes

1. **Produto cartesiano**: sem `WHERE` de ligação, todas as linhas de ambas tabelas são combinadas.   
   Exemplo: 10 clientes × 20 produtos = 200 combinações.
   
<div align="center">
    <img src="https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExZW45djFydm85Z3dpN3ZnaTQwbHZtZHZuanllaDlycWx1ZnJ1NXk1MiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/xUPGcjUQcWclgK94ti/giphy.gif" alt="Você está demitido">
    <p>
        Fonte: <em><a href="https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExZW45djFydm85Z3dpN3ZnaTQwbHZtZHZuanllaDlycWx1ZnJ1NXk1MiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/xUPGcjUQcWclgK94ti/giphy.gif" target="_blank">https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExZW45djFydm85Z3dpN3ZnaTQwbHZtZHZuanllaDlycWx1ZnJ1NXk1MiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/xUPGcjUQcWclgK94ti/giphy.gif</a></em>
    </p>
</div>  

2. **Desempenho**: sempre use filtros para reduzir resultados desnecessários.

3. **Clareza**: use aliases (`c`, `p`, `co`) e prefixe as colunas (`tabela.coluna`) para evitar ambiguidades.

---

## 🚀 Exemplos Práticos com Nosso Banco

### 1. Clientes que compraram produtos acima de R$ 1000

```sql
SELECT c.nome AS cliente, p.nome AS produto, p.preco
FROM clientes c, compras co, produtos p
WHERE c.id = co.cliente_id
  AND p.id = co.produto_id
  AND p.preco > 1000;
```

### 2. Clientes de Porto Alegre que compraram "Notebook"

```sql
SELECT c.nome AS cliente, p.nome AS produto
FROM clientes c, compras co, produtos p
WHERE c.id = co.cliente_id
  AND p.id = co.produto_id
  AND c.cidade = 'Porto Alegre'
  AND p.nome LIKE '%Notebook%';
```

### 3. Clientes de São Paulo com produtos de Informática, ordenados por preço decrescente

```sql
SELECT c.nome AS cliente, p.nome AS produto, p.preco
FROM clientes c, compras co, produtos p
WHERE c.id = co.cliente_id
  AND p.id = co.produto_id
  AND c.cidade = 'São Paulo'
  AND p.categoria = 'Informática'
ORDER BY p.preco DESC;
```

---

## 🏋️ Exercícios

1. Liste o nome dos clientes e os produtos que eles compraram.
2. Mostre os clientes que compraram mais de 1 unidade de qualquer produto.
3. Liste os produtos da categoria "Eletrônicos" comprados por clientes de Canoas.
4. Mostre os clientes que compraram "Gamepad 54".
5. Liste todos os clientes que já compraram "Notebook".
6. Mostre os nomes dos clientes e os preços dos produtos comprados acima de R$ 1500.
7. Liste clientes de Salvador que compraram produtos da categoria "Informática".
8. Mostre todos os produtos que o cliente "Ana Fernandes" já comprou.
9. Liste todos os clientes que compraram produtos cujo nome começa com "Camiseta".
10. Mostre todos os clientes e produtos comprados em fevereiro de 2025.
