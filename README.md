# 🎮 PixelPlay – Sistema de Vendas de Games

> Um mini banco de dados SQL para gerenciar **jogos, clientes e vendas** da loja fictícia **PixelPlay**.  
> Projeto criado para praticar comandos SQL no **phpMyAdmin** ou **MySQL Workbench**.

---

## 🚀 Funcionalidades Principais

✅ Cadastro e gerenciamento de **Games**  
✅ Registro de **Clientes** e seus dados de contato  
✅ Histórico de **Vendas** com datas e relacionamentos automáticos  
✅ Suporte a **ON DELETE CASCADE** (remoção automática de vendas ao excluir cliente ou game)  
✅ Consultas para **análise de dados e correções rápidas**

---

## 🧱 Estrutura do Banco

O banco é composto por três tabelas interligadas:

| Tabela | Descrição |
|--------|------------|
| **Game** | Armazena informações dos jogos (nome, plataforma, gênero e ano) |
| **Cliente** | Guarda os dados dos clientes (nome, e-mail e telefone) |
| **Venda** | Registra cada compra, conectando cliente e game |

Diagrama simplificado:
Cliente 1─∞ Venda ∞─1 Game

---

## ⚙️ Criação do Banco e Tabelas

```sql
CREATE DATABASE PixelPlay;

CREATE TABLE Game (
    id_game INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    plataforma VARCHAR(50),
    genero VARCHAR(50),
    ano_lancamento INT
);

CREATE TABLE Cliente (
    id_cliente INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100),
    email VARCHAR(100),
    telefone VARCHAR(20)
);

CREATE TABLE Venda (
    id_venda INT AUTO_INCREMENT PRIMARY KEY,
    id_cliente INT,
    id_game INT,
    data_venda DATE,
    FOREIGN KEY (id_cliente) REFERENCES Cliente(id_cliente) ON DELETE CASCADE,
    FOREIGN KEY (id_game) REFERENCES Game(id_game) ON DELETE CASCADE
);

## 🎮 Inserindo Dados Iniciais

Jogos, clientes e vendas já pré-cadastrados para testes:

-- Inserção de jogos
INSERT INTO Game (nome, plataforma, genero, ano_lancamento) VALUES
('Elden Ring', 'PC', 'RPG', 2022),
('FIFA 23', 'PS5', 'Esporte', 2022),
('Minecraft', 'PC', 'Sandbox', 2011),
('Zelda: Breath of the Wild', 'Switch', 'Aventura', 2017),
('Cyberpunk 2077', 'PC', 'RPG', 2020);

-- Inserção de clientes
INSERT INTO Cliente (nome, email, telefone) VALUES
('Ana Souza', 'ana@gmail.com', 11988887777),
('Gabrielly Alves', 'gaby@hotmail.com', 11977778888),
('Evellyn Lima', 'evy@gmail.com', 11966665555),
('Leandro Silva', 'leandro@yahoo.com', 11955554444),
('Matheus Fonseca', 'matheus@gmail.com', 11944443333),
('João Cancio', 'joao@gmail.com', 11933332222),
('Caio Martins', 'caio@hotmail.com', 11922221111),
('Moisés Fonseca', 'moises@gmail.com', 11911110000),
('Kelly Cristina', 'kelly@gmail.com', 11900009999),
('James Kaindé', 'james@yahoo.com', 11888887777);

-- Inserção de vendas
INSERT INTO Venda (id_cliente, id_game, data_venda) VALUES
(1, 1, '2025-10-01'),
(3, 3, '2025-10-05'),
(5, 2, '2025-10-10'),
(2, 4, '2025-10-12'),
(4, 5, '2025-09-30');

# 🔍 Consultas Úteis
Objetivo	Comando SQL
Ver todos os games	SELECT * FROM Game;
Clientes com Gmail	SELECT * FROM Cliente WHERE email LIKE '%gmail.com';
Vendas em outubro	SELECT * FROM Venda WHERE data_venda BETWEEN '2025-10-01' AND '2025-10-31';
RPGs em estoque	SELECT * FROM Game WHERE genero = 'RPG' ORDER BY nome ASC;

# 🔧 Atualizações e Correções
-- Corrigir telefone de um cliente
UPDATE Cliente
SET telefone = '11999998888'
WHERE nome = 'Ana Souza';

-- Corrigir ano de lançamento de um game
UPDATE Game
SET ano_lancamento = 2023
WHERE nome = 'Cyberpunk 2077';

# 🧹 Limpeza e Exclusões
-- Remover game do catálogo
DELETE FROM Game WHERE nome = 'FIFA 23';

-- Excluir vendas com mais de 30 dias
DELETE FROM Venda WHERE data_venda < CURDATE() - INTERVAL 30 DAY;


