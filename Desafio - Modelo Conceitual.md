# 🧠 **Desafio – Criação de Modelo Conceitual (DER)**

📌 **Cenário:**

Uma clínica realiza **atendimentos** entre **pacientes** e **médicos**.
Cada **paciente** pode realizar vários atendimentos com diferentes **médicos**, e cada **médico** pode atender diversos **pacientes**.
Durante cada **atendimento**, são registrados a **data** e o **diagnóstico**.

---

### 🎯 **Objetivo do exercício:**

Com base no cenário acima:

#### a) Identifique as **entidades** presentes.

#### b) Aponte os **atributos relevantes** de cada entidade.

#### c) Modele o(s) **relacionamento(s)** entre as entidades, destacando:

* Nome do relacionamento
* Cardinalidades *(1:1, 1:N, N:N)*
* Atributos do relacionamento

---

💡 **Dica para o DER:**

* Use **nomes significativos** para os relacionamentos (ex: “Realiza”, “Atende” etc).
* Lembre-se de que **atributos como data e diagnóstico**, neste caso, pertencem ao relacionamento (pois são específicos do atendimento e não do médico ou paciente).
* Considere se há necessidade de uma **`entidade associativa` *(tabela de relação N:N)*** para representar esse relacionamento de forma mais clara.
