# 🛠️ Aula: Modificando Tabelas no MySQL com `ALTER TABLE`

## 🎯 Objetivos da Aula

* Entender o comando **ALTER TABLE** no MySQL.
* Aprender a **adicionar, modificar e excluir** colunas.
* Saber **renomear tabelas** e **colunas**.
* Compreender quando usar essas alterações no ciclo de vida do banco de dados.

---

## 🧠 Introdução

Em um banco de dados relacional, muitas vezes precisamos **ajustar a estrutura** das tabelas para acomodar novas necessidades do sistema.
Com o comando **`ALTER TABLE`**, conseguimos **alterar a estrutura da tabela sem perder os dados já existentes**.

> [!WARNING]
> Sempre faça backup antes de alterar tabelas em produção!

---

## ➕ Adicionando uma Coluna

Se quisermos **incluir um novo campo**, usamos `ADD COLUMN`.

### 📝 Exemplo:

```sql
ALTER TABLE clientes
ADD COLUMN telefone VARCHAR(20);
```

📌 **Explicação:**

* A tabela `clientes` agora possui a coluna `telefone`.
* `VARCHAR(20)` define o tipo e o tamanho do campo.

---

## ✏️ Modificando uma Coluna

Para alterar **tipo de dado**, **tamanho** ou **restrições** de uma coluna, usamos `MODIFY COLUMN`.

### 📝 Exemplo:

```sql
ALTER TABLE clientes
MODIFY COLUMN telefone VARCHAR(30) NOT NULL;
```

📌 **Explicação:**

* A coluna `telefone` agora suporta até 30 caracteres.
* `NOT NULL` torna obrigatório preencher esse campo.

---

## 🔄 Renomeando uma Coluna

Para **mudar o nome** de uma coluna existente, usamos `CHANGE COLUMN`.

### 📝 Exemplo:

```sql
ALTER TABLE clientes
CHANGE COLUMN telefone celular VARCHAR(30);
```

📌 **Explicação:**

* `telefone` foi renomeado para `celular`.
* É necessário informar novamente o **tipo da coluna** (mesmo que não mude).

---

## 🏷️ Renomeando uma Tabela

Podemos renomear a tabela inteira com `RENAME`.

### 📝 Exemplo:

```sql
RENAME TABLE clientes TO usuarios;
```

📌 **Explicação:**

* A tabela `clientes` agora se chama `usuarios`.
* Todos os dados são mantidos.

---

## ❌ Deletando uma Coluna

Para remover um campo que não será mais utilizado:

### 📝 Exemplo:

```sql
ALTER TABLE usuarios
DROP COLUMN celular;
```

📌 **Explicação:**

* Remove a coluna `celular` da tabela `usuarios`.
* ⚠️ **Os dados dessa coluna são perdidos permanentemente.**

---

## 🗑️ Deletando uma Tabela Inteira

Quando a tabela não é mais necessária:

### 📝 Exemplo:

```sql
DROP TABLE usuarios;
```

📌 **Explicação:**

* Exclui completamente a tabela `usuarios` e todos os dados.
  
> [!IMPORTANT]
> ⚠️ CUIDADO
>  **Esta operação é irreversível!**

---

## 🧭 Quando Usar?

* 👨‍💻 **Durante manutenção** de sistemas.
* 🔄 **Migração** para novas versões do software.
* 🔧 Ajustes em requisitos do cliente.

---

## 📝 Exercícios Práticos

1. Crie uma tabela `produtos` com campos `id`, `nome`, `preco`.
2. Adicione uma coluna `estoque` (tipo INT).
3. Altere a coluna `preco` para ter duas casas decimais (`DECIMAL(10,2)`).
4. Renomeie a coluna `nome` para `descricao`.
5. Exclua a coluna `estoque`.
6. Renomeie a tabela `produtos` para `itens`.
7. Finalmente, delete a tabela `itens`.
