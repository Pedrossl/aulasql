
# Comandos SQL - Exemplos Práticos

## 🧱 Estruturação do Banco de Dados

```sql
-- Criar banco de dados
CREATE DATABASE IF NOT EXISTS jogos_bons;

-- Usar banco
USE jogos_bons;

-- Criar tabelas
CREATE TABLE IF NOT EXISTS categoria (
  id INT PRIMARY KEY AUTO_INCREMENT,
  nome VARCHAR(45) NOT NULL
);

CREATE TABLE IF NOT EXISTS jogo (
  id INT PRIMARY KEY AUTO_INCREMENT,
  nome VARCHAR(45) NOT NULL,
  qtd INT NOT NULL,
  categoria_id INT NOT NULL,
  FOREIGN KEY (categoria_id) REFERENCES categoria(id)
);

CREATE TABLE IF NOT EXISTS funcionario (
  id INT PRIMARY KEY AUTO_INCREMENT,
  nome VARCHAR(40) NOT NULL,
  telefone VARCHAR(20) NOT NULL UNIQUE
);

CREATE TABLE IF NOT EXISTS cliente (
  id INT PRIMARY KEY AUTO_INCREMENT,
  nome VARCHAR(40) NOT NULL,
  cpf VARCHAR(20) NOT NULL UNIQUE
);

CREATE TABLE IF NOT EXISTS venda (
  id INT PRIMARY KEY AUTO_INCREMENT,
  cliente_id INT NOT NULL,
  jogo_id INT NOT NULL,
  funcionario_id INT NOT NULL,
  qtd INT DEFAULT 1,
  FOREIGN KEY (cliente_id) REFERENCES cliente(id),
  FOREIGN KEY (jogo_id) REFERENCES jogo(id),
  FOREIGN KEY (funcionario_id) REFERENCES funcionario(id)
);
```

## ➕ Inserção de Dados

```sql
-- Categorias
INSERT INTO categoria (nome) VALUES ('Terror'), ('Ação'), ('Aventura'), ('Estratégia'), ('RPG'), ('Puzzle'), ('MOBA');

-- Jogos
INSERT INTO jogo (nome, qtd, categoria_id) VALUES
('Bloodborne', 8, 1),
('God of War', 12, 2),
('Zelda: Breath of the Wild', 7, 3),
('Civilization VI', 5, 4),
('Elden Ring', 10, 5),
('Portal 2', 6, 6),
('League of Legends', 15, 7);

-- Funcionários
INSERT INTO funcionario (nome, telefone) VALUES
('Carlos Mendes', '+55(11)91234-5678'),
('Ana Paula', '+55(21)99876-5432'),
('Rodrigo Lima', '+55(31)98765-4321');

-- Clientes
INSERT INTO cliente (nome, cpf) VALUES
('João Silva', '12345678900'),
('Maria Oliveira', '98765432100'),
('Fernanda Souza', '45678912300');

-- Vendas
INSERT INTO venda (cliente_id, jogo_id, funcionario_id) VALUES
(1, 1, 1),
(2, 2, 2),
(3, 3, 3),
(1, 4, 2),
(2, 5, 1);
```

## 🔍 Comandos SELECT

```sql
-- Jogos com estoque < 10
SELECT * FROM jogo WHERE qtd < 10;

-- Funcionários com nome específico
SELECT * FROM funcionario WHERE nome = 'Ana Paula';

-- Vendas por funcionário
SELECT * FROM venda WHERE funcionario_id = 1;

-- Cliente por CPF
SELECT * FROM cliente WHERE cpf = '12345678900';

-- Clientes com ID > 1
SELECT * FROM cliente WHERE id > 1;
```

## 🛠️ Comandos UPDATE

```sql
-- Atualizar quantidade de jogo
UPDATE jogo SET qtd = 20 WHERE nome = 'Portal 2';

-- Atualizar nome do cliente
UPDATE cliente SET nome = 'João Pedro Silva' WHERE id = 1;

-- Atualizar telefone
UPDATE funcionario SET telefone = '+55(11)90000-0000' WHERE nome = 'Carlos Mendes';

-- Atualizar nome da categoria
UPDATE categoria SET nome = 'Ação e Aventura' WHERE id = 2;
```

## 🗑️ Comandos DELETE

```sql
-- Excluir venda
DELETE FROM venda WHERE id = 3;

-- Excluir jogos com estoque zerado
DELETE FROM jogo WHERE qtd = 0;

-- Excluir cliente por CPF
DELETE FROM cliente WHERE cpf = '45678912300';

-- Excluir funcionário por ID
DELETE FROM funcionario WHERE id = 2;

-- Excluir funcionário por nome
DELETE FROM funcionario WHERE nome = 'João';
```
