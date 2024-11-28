# Modelo lógico
```uml
@startuml
entity Produto {
    id_produto : int
    nome : varchar
    descricao : varchar
    preco : decimal
    quantidade_estoque : int
    id_categoria : int
    id_fornecedor : int
}

entity Categoria {
    id_categoria : int
    nome : varchar
    descricao : varchar
}

entity Fornecedor {
    id_fornecedor : int
    nome : varchar
    contato : varchar
    email : varchar
    telefone : varchar
}

entity Usuario {
    id_usuario : int
    nome : varchar
    email : varchar
    senha_hash : varchar
    nivel_acesso : varchar
}

entity Entrada_Estoque {
    id_entrada : int
    quantidade : int
    data_entrada : date
    id_produto : int
    id_usuario : int
    id_fornecedor : int
}

entity Saida_Estoque {
    id_saida : int
    quantidade : int
    data_saida : date
    id_produto : int
    id_usuario : int
}

entity Ordem_Compra {
    id_ordem_compra : int
    quantidade : int
    data_compra : date
    status : varchar
    id_produto : int
    id_fornecedor : int
}

entity Ordem_Venda {
    id_ordem_venda : int
    quantidade : int
    data_venda : date
    id_produto : int
    id_usuario : int
}

Produto }|--|| Categoria
Produto }|--|| Fornecedor
Entrada_Estoque }|--|| Produto
Entrada_Estoque }|--|| Usuario
Entrada_Estoque }|--|| Fornecedor
Saida_Estoque }|--|| Produto
Saida_Estoque }|--|| Usuario
Ordem_Compra }|--|| Produto
Ordem_Compra }|--|| Fornecedor
Ordem_Venda }|--|| Produto
Ordem_Venda }|--|| Usuario

@enduml
```