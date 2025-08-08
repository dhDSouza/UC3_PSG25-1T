# 📚 Aula 8: Consultas em Múltiplas Tabelas

## 🎯 Objetivo da Aula

Aprender a realizar **consultas que envolvem múltiplas tabelas** apenas com condições WHERE, combinando dados de diferentes tabelas de forma eficiente.

---

## 🧠 Revisão Rápida: Relacionamento entre Tabelas

Em bancos de dados relacionais, as tabelas estão conectadas através de **chaves**:
- **Chave primária (PK)**: Identificador único em uma tabela
- **Chave estrangeira (FK)**: Referência a uma chave primária em outra tabela

---

## 🔗 Consultando Múltiplas Tabelas com WHERE

Podemos relacionar tabelas especificando a condição de relacionamento no WHERE:

```sql
SELECT tabela1.coluna, tabela2.coluna
FROM tabela1, tabela2
WHERE tabela1.chave = tabela2.chave;
```

📌 **Exemplo prático**:
```sql
SELECT clientes.nome, produtos.nome
FROM clientes, produtos
WHERE clientes.id = 5 AND produtos.preco > 1000;
```

---

## 🔍 Tipos de Relacionamentos

### 1. Relacionamento 1:1 (Um para Um)

```sql
SELECT tabela1.*, tabela2.*
FROM tabela1, tabela2
WHERE tabela1.id = tabela2.id_tabela1;
```

### 2. Relacionamento 1:N (Um para Muitos)

```sql
SELECT tabela_pai.*, tabela_filho.*
FROM tabela_pai, tabela_filho
WHERE tabela_pai.id = tabela_filho.id_pai;
```

### 3. Relacionamento N:M (Muitos para Muitos)

```sql
SELECT tabela1.*, tabela2.*
FROM tabela1, tabela2, tabela_intermediaria
WHERE tabela1.id = tabela_intermediaria.id_tabela1
AND tabela2.id = tabela_intermediaria.id_tabela2;
```

---

## 🛠️ Técnicas Avançadas

### 1. Aliases para tabelas (AS)

```sql
SELECT c.nome, p.nome
FROM clientes AS c, produtos AS p
WHERE c.cidade = 'São Paulo' AND p.preco > 500;
```

### 2. Filtros adicionais

```sql
SELECT c.nome, p.nome
FROM clientes c, produtos p
WHERE c.idade > 30 
AND p.categoria = 'Games'
AND p.preco < 1000;
```

### 3. Ordenação combinada

```sql
SELECT c.nome, p.nome, p.preco
FROM clientes c, produtos p
WHERE c.cidade = p.categoria -- Exemplo fictício
ORDER BY c.nome ASC, p.preco DESC;
```

---

## ⚠️ Cuidados Importantes

1. **Produto cartesiano**: Sem WHERE, você combina TODAS as linhas de ambas tabelas!
   - Tabela A com 10 linhas + Tabela B com 20 linhas = 200 linhas no resultado!

2. **Desempenho**: Consultas em múltiplas tabelas podem ser pesadas - sempre filtre o máximo possível.

3. **Clareza**: Use aliases e nomeie as colunas explicitamente (tabela.coluna) para evitar ambiguidades.

---

## 🚀 Exemplos Práticos

Usando nosso banco de dados atual (clientes e produtos):

1. Mostre os nomes dos clientes e produtos onde o preço do produto é maior que 1000

```sql
SELECT c.nome AS cliente, p.nome AS produto
FROM clientes c, produtos p
WHERE p.preco > 1000;
```

2. Liste clientes de Porto Alegre com produtos que contenham "Notebook" no nome

```sql
SELECT c.nome AS cliente, p.nome AS produto
FROM clientes c, produtos p
WHERE c.cidade = 'Porto Alegre'
AND p.nome LIKE '%Notebook%';
```

3. Combine clientes de São Paulo com produtos da categoria Informática, ordenando por preço decrescente

```sql
SELECT c.nome AS cliente, p.nome AS produto, p.preco
FROM clientes c, produtos p
WHERE c.cidade = 'São Paulo'
AND p.categoria = 'Informática'
ORDER BY p.preco DESC;
```

---

## 📌 Conclusão

Consultas em múltiplas tabelas sem JOIN são:
- Poderosas para combinar dados relacionados
- Exigem cuidado para evitar produtos cartesianos
- Úteis quando você precisa de combinações específicas
- A base para entender os JOINs que veremos depois!

> [!TIP]
> Prática é essencial - experimente criar suas próprias combinações!
