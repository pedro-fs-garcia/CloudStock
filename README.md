# CloudStock
![CloudStock logo](/docs/cloudstock.png)


# Definição do problema:
- Dificuldade em gerenciar estoques de forma remota
# Objetivo:
- Migração do sistema de gestão de estoque de uma empresa para a nuvem 
- Garantir acesso remoto e em tempo real às informações de estoque
- Modernizar o processo de gestão de estoque
# Produto
Aplicação web para gestão de estoque em nuvem, com acesso remoto em tempo real.
# Requisitos Funcionais:
## 1 - Dashboard Principal:
- visão geral do estoque: gráficos e métricas
- Indicadores de desempenho: níveis de estoque, valor total do inventário, alertas de produtos críticos
## 2 - Gestão de produtos
- Visualização de Produtos: Tela para visualizar todos os produtos no estoque com opções de filtragem e busca.
- Adicionar Produtos: Formulário para adicionar novos produtos ao estoque, incluindo detalhes como nome, categoria, preço e fornecedor.
- Editar Produtos: Opção para atualizar informações dos produtos existentes.
- Excluir Produtos: Funcionalidade para remover produtos do estoque quando necessário.
## 3 - Controles de entrada e saída
- Registro de Movimentações: Tela para registrar entradas e saídas de produtos, com a capacidade de adicionar detalhes sobre cada movimentação.
- Histórico de Movimentações: Visualização do histórico de movimentações para acompanhamento e auditoria.
## 4 - Acompanhamento em tempo real:
- Sincronização do inventário com as movimentações do cliente em tempo real
- Intervalos de atualização de 5 a 10 minutos
- Importação automatizada das informações já existentes do estoque
- Implementação de uma API básica para sincronização e importação de dados, com funcionalidades adicionais sendo desenvolvidas após o lançamento.
## 4 - Relatórios e análises
- Geração de Relatórios: Criação de relatórios detalhados sobre o estado do estoque, incluindo entradas, saídas, e níveis de estoque.
- Análises de Dados: Ferramentas para analisar tendências e padrões de estoque, como relatórios de produtos mais vendidos e sazonalidade.
- Análise Histórica: Utilização de dados históricos para prever a demanda futura com base em padrões passados.
- Modelos Estatísticos: Aplicação de modelos estatísticos para antecipar variações sazonais e tendências de mercado.
## 5 - Acesso remoto multiusuário
- Gerenciamento de Usuários: Controle de login de diferentes usuários com diferentes níveis de permissão.
- Permissões de Acesso: Definição de permissões específicas para cada tipo de usuário (Editor, Supervisor, Gerente, Administrador).
## 6 - Controle de Acesso e Pagamento
- Modelo Freemium: Acesso limitado para empresas não pagantes (1 inventário e 5 usuários) e acesso completo para empresas pagantes.
- Gerenciamento de Assinaturas: Implementação de um sistema de pagamento para gerenciar assinaturas e acesso às funcionalidades premium.
## 7 - Inventário Personalizável
- Banco de Dados Flexível: Permitir aos usuários a criação e personalização de tabelas e colunas conforme suas necessidades.
- Começar com um conjunto fixo de colunas e tabelas padrão, deixando a personalização para uma fase futura.
- Colunas sugeridas: 
    - ID do produto
    - nome
    - categoria
    - quantidade em estoque
    - preço de custo
    - preço de venda
    - fornecedor
    - data de entrada
    - data de validade
    - localização no armazém.

# Requisitos não funcionais:
- Escalabilidade
- Segurança: criptografia de dados e autenticação de usuários
- Desempenho
- Usabilidade

# Tecnologias Utilizadas:
- SpringBoot
- Bootstrap
# Protótipo Figma


# Cronograma inicial:
- Sprint 1:
    - Planejamento detalhado e design da arquitetura
    - Desenvolvimento inicial do backend (CRUD de produtos, autenticação)
    - Configuração do banco de dados e integração inicial
- Sprint 2:
    - Desenvolvimento do dashboard simplificado
    - Implementação básica do controle de entradas e saídas
    - configuração do sistema de pagamento
- Sprint 3:
    - Implementação do acompanhamento em tempo real (versão somplificada): sincronização básica com o inventário em tempo real
    - Desenvolvimento da interface de usuário para funcionalidades essenciais
    - Testes unitários e de integração contínuos
- Sprint 4:
    - Finalização de funcionalidades críticas e correção de bugs
    - Preparação e execução da implementação

