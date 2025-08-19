# 👾 Retro Games Database Challenge

![Retro Games Database Challenge]("./Images/Retro_Games_Database_Challenge.png")

## 👥 Organização da Turma

* A turma será dividida em **4 grupos de 5 pessoas**.
* Cada grupo participará de um **campeonato de jogos retrô do Super Nintendo (SNES)**, com 5 títulos clássicos:

  * **Street Fighter II**
  * **Ultimate Mortal Kombat 3**
  * **Killer Instinct**
  * **Super Mario Kart**
  * **Bomberman 5**

Cada grupo indicará **um jogador por jogo**. Todas as partidas devem acontecer durante a aula.

---

## 🧩 Objetivo da Atividade

Ao final da aula, cada grupo deverá:

1. Criar um **banco de dados** para registrar as informações do campeonato.
2. Montar as **tabelas necessárias** para organizar os dados (grupos, jogadores, jogos, partidas, pontuações…).
3. Registrar os resultados de **todas as partidas disputadas**.
4. Realizar **consultas SQL** para analisar e apresentar os dados.

---

## 📁 Tabelas que devem ser criadas

O banco de dados precisa conter:

* **Grupos participantes** (nome do grupo, número de integrantes…)
* **Jogadores**, vinculados ao grupo
* **Jogos retrô** disponíveis
* **Resultados das partidas**, contendo:

  * Qual jogador jogou
  * Qual jogo foi disputado
  * A pontuação/resultado obtido (ex: vitórias, pontos ou ranking da partida)
  * A data da partida

---

## 📈 Diagrama de Entidade e Relacionamento (DER)

Utilizando a ferramenta de modelagem do `MySQL Workbench` deve ser realizado o **DER** do banco de dados.

## 🔍 Consultas obrigatórias

Depois de inserir os dados no banco, cada grupo deverá criar consultas para responder:

### 🧑‍🤝‍🧑 1. **Quais são os jogadores e a qual grupo cada um pertence?**

➡️ Relacione o nome dos jogadores com seus respectivos grupos.

---

### 🎮 2. **Quais partidas foram jogadas, com jogador, jogo e pontuação?**

➡️ Liste todas as partidas realizadas, mostrando:

* Nome do jogador
* Nome do jogo retrô
* Pontuação obtida

---

### ➕ 3. **Qual é a soma total de pontos de cada grupo?**

➡️ Para cada grupo:

* Liste os jogadores vinculados a ele
* Some os pontos conquistados nas partidas

---

### 🥇 4. **Quem teve a maior pontuação em cada jogo?**

➡️ Para cada jogo (ex: Street Fighter II, Mario Kart…), descubra:

* Qual foi a maior pontuação registrada
* Quem foi o jogador que conseguiu essa pontuação

---

### 📊 5. **Qual é a média de pontuação de cada grupo?**

➡️ Para cada grupo, calcule a **média das pontuações** de todos os seus jogadores.

---

### 📉 6. **Qual foi a menor e a maior pontuação de cada grupo?**

➡️ Para cada grupo:

* Verifique a **menor pontuação feita em qualquer jogo**
* E a **maior pontuação registrada**

---

### 💡 7. **Monte uma consulta que mostre o **ranking final dos grupos**, ordenado da maior para a menor pontuação total.**
