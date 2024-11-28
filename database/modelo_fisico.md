## Criação do banco de dados
```sql
CREATE DATABASE CloudStock;

USE CloudStock;

CREATE TABLE Produto (
    id_produto INT PRIMARY KEY,
    nome VARCHAR(100),
    descricao TEXT,
    quantidade_estoque INT,
    preco_medio_venda DECIMAL(10, 2),
    preco_medio_custo DECIMAL(10, 2)
);

CREATE TABLE Usuario (
    id_usuario INT PRIMARY KEY,
    nome VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    senha_hash TEXT,
    nivel_acesso INT
);

CREATE TABLE Categoria (
    id_categoria INT PRIMARY KEY,
    nome VARCHAR(100),
    descricao TEXT
);

CREATE TABLE Fornecedor (
    id_fornecedor INT PRIMARY KEY,
    nome VARCHAR(100),
    contato VARCHAR(100),
    email VARCHAR(100),
    telefone VARCHAR(20)
);

CREATE TABLE Entrada_de_estoque (
    id_entrada INT PRIMARY KEY,
    data_entrada DATE,
    quantidade INT,
    preco_unitario DECIMAL(10, 2),
    id_usuario INT,
    id_produto INT,
    FOREIGN KEY (id_usuario) REFERENCES Usuario (id_usuario),
    FOREIGN KEY (id_produto) REFERENCES Produto (id_produto)
);

CREATE TABLE Saida_de_estoque (
    id_saida INT PRIMARY KEY,
    quantidade INT,
    data_saida DATE,
    preco_unitario DECIMAL(10, 2),
    id_usuario INT,
    id_produto INT,
    FOREIGN KEY (id_usuario) REFERENCES Usuario (id_usuario),
    FOREIGN KEY (id_produto) REFERENCES Produto (id_produto)
);

CREATE TABLE Movimentacoes (
    id_movimentacao INT PRIMARY KEY,
    id_entrada_estoque INT,
    id_saida_estoque INT,
    FOREIGN KEY (id_entrada_estoque) REFERENCES Entrada_de_estoque (id_entrada),
    FOREIGN KEY (id_saida_estoque) REFERENCES Saida_de_estoque (id_saida)
);

CREATE TABLE Inventario (
    id_inventario INT PRIMARY KEY,
    nome VARCHAR(100),
    descricao TEXT,
    data_criacao DATE,
    id_usuario INT,
    id_movimentacao INT,
    FOREIGN KEY (id_usuario) REFERENCES Usuario (id_usuario),
    FOREIGN KEY (id_movimentacao) REFERENCES Movimentacoes (id_movimentacao)
);

CREATE TABLE pertence_a (
    id_produto INT,
    id_categoria INT,
    PRIMARY KEY (id_produto, id_categoria),
    FOREIGN KEY (id_produto) REFERENCES Produto (id_produto),
    FOREIGN KEY (id_categoria) REFERENCES Categoria (id_categoria)
);

CREATE TABLE fornece (
    id_produto INT,
    id_fornecedor INT,
    PRIMARY KEY (id_produto, id_fornecedor),
    FOREIGN KEY (id_produto) REFERENCES Produto (id_produto),
    FOREIGN KEY (id_fornecedor) REFERENCES Fornecedor (id_fornecedor)
);
```

## inserção de dados no banco de dados

```sql
INSERT INTO Produto (id_produto, nome, descricao, quantidade_estoque, preco_medio_venda, preco_medio_custo)
VALUES 
(1, 'Notebook Dell Inspiron', 'Notebook com 16GB de RAM e 512GB SSD', 15, 4500.00, 3500.00),
(2, 'Mouse Logitech', 'Mouse sem fio com conexão Bluetooth', 50, 120.00, 80.00),
(3, 'Teclado Mecânico', 'Teclado mecânico com switches Cherry MX Blue', 30, 250.00, 180.00);

INSERT INTO Usuario (id_usuario, nome, email, senha_hash, nivel_acesso)
VALUES 
(1, 'Admin', 'admin@cloudstock.com', 'hashsenha123', 3),
(2, 'Carlos Silva', 'carlos.silva@cloudstock.com', 'hashsenha456', 2),
(3, 'Maria Oliveira', 'maria.oliveira@cloudstock.com', 'hashsenha789', 1);

INSERT INTO Categoria (id_categoria, nome, descricao)
VALUES 
(1, 'Eletrônicos', 'Produtos eletrônicos em geral'),
(2, 'Acessórios', 'Acessórios para computadores e dispositivos'),
(3, 'Periféricos', 'Dispositivos como teclados, mouses e fones de ouvido');

INSERT INTO Fornecedor (id_fornecedor, nome, contato, email, telefone)
VALUES 
(1, 'TechDistribuidora', 'João Costa', 'joao@techdistribuidora.com', '11987654321'),
(2, 'MegaFornecedor', 'Ana Paula', 'ana@megafornecedor.com', '21987654321'),
(3, 'EletrônicosBrasil', 'Lucas Mendes', 'lucas@eletronicosbrasil.com', '31987654321');

INSERT INTO Entrada_de_estoque (id_entrada, data_entrada, quantidade, preco_unitario, id_usuario, id_produto)
VALUES 
(1, '2024-10-10', 20, 100.00, 1, 2),
(2, '2024-10-15', 10, 450.00, 2, 3),
(3, '2024-10-20', 5, 4000.00, 1, 1);

INSERT INTO Saida_de_estoque (id_saida, quantidade, data_saida, preco_unitario, id_usuario, id_produto)
VALUES 
(1, 3, '2024-10-25', 120.00, 3, 2),
(2, 1, '2024-10-30', 4500.00, 2, 1),
(3, 2, '2024-10-28', 250.00, 1, 3);

INSERT INTO Movimentacoes (id_movimentacao, id_entrada_estoque, id_saida_estoque)
VALUES 
(1, 1, 1),
(2, 2, 3),
(3, 3, 2);

INSERT INTO Inventario (id_inventario, nome, descricao, data_criacao, id_usuario, id_movimentacao)
VALUES 
(1, 'Inventário Outubro', 'Controle de estoque para Outubro', '2024-10-31', 1, 1),
(2, 'Inventário Especial', 'Controle especial para Black Friday', '2024-11-01', 2, 2);

INSERT INTO pertence_a (id_produto, id_categoria)
VALUES 
(1, 1), -- Produto 1 pertence à categoria Eletrônicos
(2, 2), -- Produto 2 pertence à categoria Acessórios
(3, 3); -- Produto 3 pertence à categoria Periféricos

INSERT INTO fornece (id_produto, id_fornecedor)
VALUES 
(1, 1), -- Produto 1 fornecido pelo Fornecedor 1
(2, 2), -- Produto 2 fornecido pelo Fornecedor 2
(3, 3); -- Produto 3 fornecido pelo Fornecedor 3

SELECT p.nome AS produto, c.nome AS categoria 
FROM Produto p
JOIN pertence_a pa ON p.id_produto = pa.id_produto
JOIN Categoria c ON pa.id_categoria = c.id_categoria;

SELECT p.nome AS produto, f.nome AS fornecedor 
FROM Produto p
JOIN fornece fo ON p.id_produto = fo.id_produto
JOIN Fornecedor f ON fo.id_fornecedor = f.id_fornecedor;

```


# DML
## Seleciona produtos com menos de 10 unidades
```sql
SELECT * 
FROM Produto 
WHERE quantidade_estoque < 10;
```

## Listar os fornecedores em ordem alfabética
```sql
SELECT * 
FROM Fornecedor 
ORDER BY nome ASC;
```

## Agrupar as vendas realizadas e calcular a receita total de cada produto.
```sql
SELECT id_produto, 
       SUM(preco_unitario * quantidade) AS receita_total 
FROM Saida_de_estoque 
GROUP BY id_produto;
```

## Listar todos os produtos e suas categorias
```sql
SELECT Produto.nome AS nome_produto, 
       Categoria.nome AS nome_categoria 
FROM Produto 
JOIN pertence_a ON Produto.id_produto = pertence_a.id_produto 
JOIN Categoria ON pertence_a.id_categoria = Categoria.id_categoria;
```

## Listar os produtos que pertencem a uma lista de categorias específicas (Ex.: Eletrônicos e Roupas)
```sql
SELECT nome 
FROM Produto 
WHERE id_produto IN ( 
    SELECT id_produto 
    FROM pertence_a 
    WHERE id_categoria IN (125, 287)
);
```

## Listar todos os produtos que não foram fornecidos por um fornecedor específico.
```sql
SELECT nome 
FROM Produto 
WHERE id_produto NOT IN (
    SELECT id_produto 
    FROM fornece 
    WHERE id_fornecedor = 1  -- ID de exemplo do fornecedor
);
```

## Buscar fornecedores cujo nome contenha "Tech"
```sql
SELECT * 
FROM Fornecedor 
WHERE nome LIKE '%Tech%';
```

## Consultar fornecedores que não entregaram produtos em um determinado período
```sql
SELECT Fornecedor.nome 
FROM Fornecedor 
WHERE id_fornecedor NOT IN (
    SELECT id_fornecedor 
    FROM Entrada_de_estoque 
    WHERE data_entrada BETWEEN '2024-01-01' AND '2024-12-31'
);
```

## Selecionar as entradas de estoque realizadas entre duas datas
```sql
SELECT * 
FROM Entrada_de_estoque 
WHERE data_entrada BETWEEN '2024-01-01' AND '2024-12-31';
```

## Calcular a média de preço de venda de todos os produtos
```sql
SELECT AVG(preco_medio_venda) AS preco_medio 
FROM Produto;
```

## Contar quantos usuários têm um determinado nível de acesso
```sql
SELECT COUNT(id_usuario) AS total_usuarios 
FROM Usuario 
WHERE nivel_acesso = 1; --nível de acesso de exemplo: 1
```

## Inserir no inventário um conjunto de produtos com base em uma seleção específica
```sql
INSERT INTO Inventario (id_inventario, nome, descricao, data_criacao, id_usuario, id_movimentacao)
SELECT 1, 
       'Inventário Inicial', 
       'Inventário automático', 
       CURRENT_DATE, 
       1, 
       id_movimentacao 
FROM Movimentacoes 
WHERE id_movimentacao BETWEEN 1 AND 10;
```

## Atualizar o estoque de um produto após uma venda
```sql
UPDATE Produto 
SET quantidade_estoque = quantidade_estoque - (
    SELECT quantidade 
    FROM Saida_de_estoque 
    WHERE id_produto = Produto.id_produto AND id_saida = 1 específica
)
WHERE id_produto = 1;
```

## Consultar produtos que estão abaixo de um nível crítico de estoque
```sql
SELECT nome, quantidade_estoque 
FROM Produto 
WHERE quantidade_estoque < 5; 
```

## Listar os 5 produtos mais vendidos
```sql
SELECT id_produto, 
       SUM(quantidade) AS total_vendido 
FROM Saida_de_estoque 
GROUP BY id_produto 
ORDER BY total_vendido DESC 
LIMIT 5;
```

## Registrar uma nova entrada de estoque
```sql
INSERT INTO Entrada_de_estoque (id_entrada, data_entrada, quantidade, preco_unitario, id_usuario, id_produto) 
VALUES (101, '2024-10-20', 50, 15.99, 2, 1);
```

## Excluir um produto que não pertence a nenhuma categoria
```sql
DELETE FROM Produto 
WHERE id_produto NOT IN (
    SELECT id_produto 
    FROM pertence_a
);
```

## Calcular o lucro médio por produto
```sql
SELECT Produto.id_produto, 
       Produto.nome, 
       AVG(Saida_de_estoque.preco_unitario - Entrada_de_estoque.preco_unitario) AS lucro_medio 
FROM Saida_de_estoque 
JOIN Entrada_de_estoque ON Saida_de_estoque.id_produto = Entrada_de_estoque.id_produto 
JOIN Produto ON Produto.id_produto = Saida_de_estoque.id_produto 
GROUP BY Produto.id_produto, Produto.nome;
```

## Consultar inventários com movimentações realizadas por um usuário específico
```sql
SELECT Inventario.nome, Inventario.descricao 
FROM Inventario 
JOIN Movimentacoes ON Inventario.id_movimentacao = Movimentacoes.id_movimentacao 
WHERE Inventario.id_usuario = 3;
```

## Listar categorias e a quantidade de produtos em cada uma
```sql
SELECT Categoria.nome, 
       COUNT(pertence_a.id_produto) AS total_produtos 
FROM Categoria 
LEFT JOIN pertence_a ON Categoria.id_categoria = pertence_a.id_categoria 
GROUP BY Categoria.nome;
```

## Atualizar o preço médio de venda de um produto
```sql
UPDATE Produto 
SET preco_medio_venda = (
    SELECT AVG(preco_unitario) 
    FROM Saida_de_estoque 
    WHERE id_produto = Produto.id_produto
)
WHERE id_produto = 1; -- ID do produto específico
```

## Listar os usuários que realizaram movimentações em mais de um inventário
```sql
SELECT Usuario.nome, 
       COUNT(DISTINCT Inventario.id_inventario) AS inventarios 
FROM Usuario 
JOIN Inventario ON Usuario.id_usuario = Inventario.id_usuario 
GROUP BY Usuario.nome 
HAVING COUNT(DISTINCT Inventario.id_inventario) > 1;
```