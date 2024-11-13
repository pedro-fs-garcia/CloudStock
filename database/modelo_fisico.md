## Criação do banco de dados
```sql
-- Tabela Produto
CREATE TABLE Produto (
    id_produto INT PRIMARY KEY,
    nome VARCHAR(100),
    descricao TEXT,
    quantidade_estoque INT,
    preco_medio_venda DECIMAL(10, 2),
    preco_medio_custo DECIMAL(10, 2)
);

-- Tabela Usuario
CREATE TABLE Usuario (
    id_usuario INT PRIMARY KEY,
    nome VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    senha_hash TEXT,
    nivel_acesso INT
);

-- Tabela Categoria
CREATE TABLE Categoria (
    id_categoria INT PRIMARY KEY,
    nome VARCHAR(100),
    descricao TEXT
);

-- Tabela Fornecedor
CREATE TABLE Fornecedor (
    id_fornecedor INT PRIMARY KEY,
    nome VARCHAR(100),
    contato VARCHAR(100),
    email VARCHAR(100),
    telefone VARCHAR(20)
);

-- Tabela Entrada de Estoque
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

-- Tabela Saída de Estoque
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

-- Tabela Movimentações
CREATE TABLE Movimentacoes (
    id_movimentacao INT PRIMARY KEY,
    id_entrada_estoque INT,
    id_saida_estoque INT,
    FOREIGN KEY (id_entrada_estoque) REFERENCES Entrada_de_estoque (id_entrada),
    FOREIGN KEY (id_saida_estoque) REFERENCES Saida_de_estoque (id_saida)
);

-- Tabela Inventário
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

-- Tabela de relacionamento pertence_a
CREATE TABLE pertence_a (
    id_produto INT,
    id_categoria INT,
    PRIMARY KEY (id_produto, id_categoria),
    FOREIGN KEY (id_produto) REFERENCES Produto (id_produto),
    FOREIGN KEY (id_categoria) REFERENCES Categoria (id_categoria)
);

-- Tabela de relacionamento fornece
CREATE TABLE fornece (
    id_produto INT,
    id_fornecedor INT,
    PRIMARY KEY (id_produto, id_fornecedor),
    FOREIGN KEY (id_produto) REFERENCES Produto (id_produto),
    FOREIGN KEY (id_fornecedor) REFERENCES Fornecedor (id_fornecedor)
);
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