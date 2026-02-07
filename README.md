# Projeto Conceitual de Banco de Dados  
## Sistema de Ordem de Serviço – Oficina Mecânica

## Descrição
Este projeto apresenta a modelagem conceitual de um banco de dados, utilizando o padrão **EER (Enhanced Entity-Relationship)**, para um **sistema de controle e gerenciamento de ordens de serviço em uma oficina mecânica**.

O esquema foi desenvolvido a partir de uma narrativa proposta pela **DIO (Digital Innovation One)**, com o objetivo de identificar corretamente entidades, atributos, relacionamentos e cardinalidades, aplicando boas práticas de modelagem de dados.

O diagrama conceitual foi elaborado no **MySQL Workbench 8.0 Community Edition**.

---

## Objetivo
Criar um esquema conceitual EER capaz de representar:
- O cadastro de clientes e seus veículos;
- A abertura e o gerenciamento de ordens de serviço;
- A associação de equipes e mecânicos à execução dos serviços;
- O cálculo de valores com base em serviços prestados e peças utilizadas;
- A organização e integridade das informações do sistema.

---

## Ferramentas Utilizadas
- MySQL Workbench 8.0 CE  
- Modelo EER (Enhanced Entity-Relationship)  
- GitHub para versionamento e entrega do projeto  

---

## Visão Geral do Modelo
O modelo conceitual foi estruturado respeitando:
- Normalização até a **3ª Forma Normal (3FN)**;
- Uso adequado de **chaves primárias (PK)** e **chaves estrangeiras (FK)**;
- Resolução correta de relacionamentos **N:M** por meio de tabelas associativas;
- Separação entre dados cadastrais e dados transacionais;
- Manutenção de valores históricos para evitar inconsistências futuras.

---

## Entidades Principais

### Cliente
Armazena os dados dos clientes da oficina.
- idCliente (PK)
- Nome
- Endereço
- CPF_CNPJ (armazenado apenas com dígitos, sem pontuação)
- Telefone

### Veículo
Representa os veículos pertencentes aos clientes.
- idVeiculo (PK)
- Placa (única)
- Marca
- Modelo
- Ano
- Cor
- idCliente (FK)

### Ordem de Serviço (OS)
Controla os serviços executados em um veículo.
- idOrdemServico (PK)
- Número
- Data de Emissão
- Data de Conclusão
- Status
- Valor Total
- idVeiculo (FK)
- idEquipe (FK)

### Equipe
Agrupa os mecânicos responsáveis pela execução das ordens de serviço.
- idEquipe (PK)
- Nome da Equipe

### Mecânico
Armazena os dados dos mecânicos da oficina.
- idMecanico (PK)
- Nome
- Endereço
- Especialidade
- idEquipe (FK)

### Serviço
Tabela de referência dos serviços prestados.
- idServico (PK)
- Descrição
- Valor da Mão de Obra

### Peça
Tabela de referência das peças utilizadas.
- idPeca (PK)
- Descrição
- Valor Unitário

---

## Tabelas Associativas

### OS_Servico
Relaciona ordens de serviço aos serviços executados.
- idOrdemServico (PK, FK)
- idServico (PK, FK)
- Quantidade
- Valor Praticado (valor do serviço no momento da execução)

### OS_Peca
Relaciona ordens de serviço às peças utilizadas.
- idOrdemServico (PK, FK)
- idPeca (PK, FK)
- Quantidade
- Valor Unitário (valor da peça no momento da execução)

---

## Relacionamentos e Cardinalidades
- Cliente – Veículo: **1:N**
- Veículo – Ordem de Serviço: **1:N**
- Equipe – Mecânico: **1:N**
- Equipe – Ordem de Serviço: **1:N**
- Ordem de Serviço – Serviço: **N:M**
- Ordem de Serviço – Peça: **N:M**

---

## Decisões de Projeto
- O campo **CPF_CNPJ** armazena apenas números, facilitando validações e padronização.
- O atributo **Valor Total** da Ordem de Serviço é armazenado para otimizar consultas, apesar de ser um valor derivado.
- Os valores de serviços e peças são registrados nas tabelas associativas para manter histórico, mesmo que os preços de referência sejam alterados futuramente.
- O atributo **Ano** do veículo foi definido como `VARCHAR(4)` devido a limitações do MySQL Workbench com o tipo `YEAR`.

Todas as decisões não explicitamente definidas na narrativa foram assumidas com base em boas práticas de modelagem de dados e estão documentadas neste arquivo.

---

## Diagrama Conceitual
O diagrama EER completo está disponível neste repositório em formato `.png`, conforme solicitado no desafio.

---

## Conclusão
O modelo conceitual desenvolvido atende integralmente à narrativa proposta, aplicando corretamente os conceitos de modelagem de dados, relacionamentos, cardinalidades e normalização, estando adequado para avaliação no contexto da DIO.
