<div align="center">

<img src="https://cdn-icons-png.flaticon.com/512/4299/4299956.png" alt="DAO JDBC Logo" width="110" />

# 🗃️ Demo DAO JDBC — Padrão DAO com Java + MySQL

**Implementação completa do padrão de projeto DAO (Data Access Object) em Java,**
**utilizando JDBC para comunicação direta com banco de dados MySQL.**

<br>

![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![JDBC](https://img.shields.io/badge/JDBC-Conexão%20Nativa-007396?style=for-the-badge&logo=java&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![DAO Pattern](https://img.shields.io/badge/Padrão-DAO-8B0000?style=for-the-badge)
![OOP](https://img.shields.io/badge/Paradigma-OOP-blueviolet?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completo-brightgreen?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

</div>

---

## 📚 Tabela de Conteúdos

> Navegue rapidamente pelas seções do projeto.

| # | Seção |
|:-:|:------|
| 1 | [📖 Sobre o Projeto](#-sobre-o-projeto) |
| 2 | [🏛️ O Padrão DAO](#️-o-padrão-dao) |
| 3 | [✨ Funcionalidades (CRUD)](#-funcionalidades-crud) |
| 4 | [🛠️ Pilha de Tecnologias](#️-pilha-de-tecnologias) |
| 5 | [📦 Arquitetura e Pacotes](#-arquitetura-e-pacotes) |
| 6 | [🗃️ Banco de Dados](#️-banco-de-dados) |
| 7 | [📂 Estrutura do Projeto](#-estrutura-do-projeto) |
| 8 | [🚀 Como Executar](#-como-executar) |
| 9 | [🤝 Como Contribuir](#-como-contribuir) |
| 10 | [👨‍💻 Autor](#-autor) |
| 11 | [📄 Licença](#-licença) |

---

## 📖 Sobre o Projeto

> **Demo DAO JDBC** é uma implementação prática e completa do padrão de projeto **DAO (Data Access Object)** em Java puro, utilizando **JDBC** para interagir diretamente com um banco de dados **MySQL** — sem o uso de ORMs como Hibernate ou JPA.

O projeto consiste em um sistema de gerenciamento de **Vendedores** e **Departamentos**, demonstrando como organizar a camada de persistência de dados de forma limpa, desacoplada e reutilizável, separando completamente o acesso a dados da lógica de negócio.

---

## 🏛️ O Padrão DAO

> O **Data Access Object (DAO)** é um padrão de projeto estrutural que isola a camada de acesso a dados do restante da aplicação, permitindo que a lógica de negócio seja independente do banco de dados utilizado.

```
┌─────────────────────────────────────────────────────┐
│                   APPLICATION LAYER                  │
│           Program.java / Classes Demo               │
└──────────────────────┬──────────────────────────────┘
                       │ usa
┌──────────────────────▼──────────────────────────────┐
│                  DAO INTERFACES                      │
│         SellerDao          DepartmentDao             │
└──────────┬───────────────────────┬──────────────────┘
           │ implementa            │ implementa
┌──────────▼──────────┐ ┌─────────▼──────────────────┐
│  SellerDaoJDBC      │ │  DepartmentDaoJDBC          │
│  (SQL + ResultSet)  │ │  (SQL + ResultSet)          │
└──────────┬──────────┘ └─────────┬──────────────────┘
           │                      │
┌──────────▼──────────────────────▼──────────────────┐
│                 DB (Utility Class)                  │
│         Gerencia Connection, PreparedStatement      │
└─────────────────────────┬──────────────────────────┘
                          │
┌─────────────────────────▼──────────────────────────┐
│               MySQL Database                        │
│         coursejdbc · seller · department            │
└────────────────────────────────────────────────────┘
```

### 🔑 Benefícios do Padrão DAO

| Benefício | Descrição |
|:----------|:----------|
| 🧩 **Desacoplamento** | A lógica de negócio não conhece detalhes de SQL ou JDBC. |
| 🔄 **Substituição** | Trocar MySQL por PostgreSQL exige alterar apenas a implementação DAO. |
| 🧪 **Testabilidade** | Interfaces DAO permitem mockar dependências de banco nos testes. |
| 📐 **Responsabilidade Única** | Cada classe tem uma função clara e bem definida. |

---

## ✨ Funcionalidades (CRUD)

### 👤 Seller (Vendedor)

| Operação | Método | Descrição |
|:---------|:------:|:----------|
| 🔍 **Buscar por ID** | `findById(Integer id)` | Retorna um vendedor pelo seu identificador único. |
| 📋 **Buscar Todos** | `findAll()` | Retorna a lista completa de todos os vendedores. |
| 🏢 **Buscar por Departamento** | `findByDepartment(Department dep)` | Retorna todos os vendedores de um departamento específico. |
| ➕ **Inserir** | `insert(Seller obj)` | Cadastra um novo vendedor no banco de dados. |
| ✏️ **Atualizar** | `update(Seller obj)` | Atualiza os dados de um vendedor existente. |
| 🗑️ **Deletar** | `deleteById(Integer id)` | Remove um vendedor pelo seu ID. |

### 🏢 Department (Departamento)

| Operação | Método | Descrição |
|:---------|:------:|:----------|
| 🔍 **Buscar por ID** | `findById(Integer id)` | Retorna um departamento pelo seu identificador. |
| 📋 **Buscar Todos** | `findAll()` | Retorna a lista completa de todos os departamentos. |
| ➕ **Inserir** | `insert(Department obj)` | Cadastra um novo departamento. |
| ✏️ **Atualizar** | `update(Department obj)` | Atualiza os dados de um departamento. |
| 🗑️ **Deletar** | `deleteById(Integer id)` | Remove um departamento pelo seu ID. |

---

## 🛠️ Pilha de Tecnologias

| Tecnologia | Função no Projeto |
|:-----------|:------------------|
| **Java** | Linguagem principal — toda a lógica de negócio e padrões de projeto. |
| **JDBC** | API Java para comunicação nativa com o banco de dados MySQL (sem ORM). |
| **MySQL** | Banco de dados relacional para persistência dos dados de Vendedores e Departamentos. |
| **MySQL Connector/J** | Driver JDBC para estabelecer a conexão Java ↔ MySQL. |
| **Eclipse IDE** | IDE utilizada no desenvolvimento (arquivos `.classpath` e `.project` incluídos). |

---

## 📦 Arquitetura e Pacotes

> O projeto segue uma organização em pacotes com separação clara de responsabilidades.

| Pacote | Classe | Responsabilidade |
|:-------|:------:|:-----------------|
| `model.entities` | `Seller.java` | Entidade Vendedor com atributos: nome, email, salário, data de nascimento e departamento. |
| `model.entities` | `Department.java` | Entidade Departamento com atributos: id e nome. |
| `model.dao` | `SellerDao.java` | **Interface** que define o contrato CRUD para Vendedores. |
| `model.dao` | `DepartmentDao.java` | **Interface** que define o contrato CRUD para Departamentos. |
| `model.dao.impl` | `SellerDaoJDBC.java` | **Implementação** concreta do SellerDao usando JDBC e SQL. |
| `model.dao.impl` | `DepartmentDaoJDBC.java` | **Implementação** concreta do DepartmentDao usando JDBC e SQL. |
| `db` | `DB.java` | Classe utilitária para abertura/fechamento de `Connection`, `Statement` e `ResultSet`. |
| `db` | `DbException.java` | Exceção customizada para erros de banco de dados (runtime). |
| `db` | `DbIntegrityException.java` | Exceção para violações de integridade referencial (FK constraints). |
| `application` | `DaoFactory.java` | **Factory** para instanciar os DAOs — desacopla a criação das implementações. |
| `application` | `Program.java` | Classe de demonstração com exemplos de uso de todas as operações CRUD. |

---

## 🗃️ Banco de Dados

### ⚙️ Configuração — `db.properties`

```properties
# ─────────────────────────────────────────
# Configuração de Conexão com MySQL
# ─────────────────────────────────────────
dburl=jdbc:mysql://localhost:3306/coursejdbc
user=seu_usuario
password=sua_senha
useSSL=false
```

> ⚠️ **Nunca** versione o `db.properties` com credenciais reais. Adicione-o ao `.gitignore` em projetos de produção.

---

### 📄 Script SQL — `database.sql`

```sql
-- ─────────────────────────────────────────
-- Criação do Banco de Dados
-- ─────────────────────────────────────────
CREATE DATABASE IF NOT EXISTS coursejdbc;
USE coursejdbc;

-- ─────────────────────────────────────────
-- Tabela: Department
-- ─────────────────────────────────────────
CREATE TABLE department (
    Id   INT         NOT NULL AUTO_INCREMENT,
    Name VARCHAR(60) NULL,
    PRIMARY KEY (Id)
);

-- ─────────────────────────────────────────
-- Tabela: Seller (referencia Department)
-- ─────────────────────────────────────────
CREATE TABLE seller (
    Id           INT          NOT NULL AUTO_INCREMENT,
    Name         VARCHAR(60)  NOT NULL,
    Email        VARCHAR(100) NOT NULL,
    BirthDate    DATETIME     NOT NULL,
    BaseSalary   DOUBLE       NOT NULL,
    DepartmentId INT          NOT NULL,
    PRIMARY KEY (Id),
    FOREIGN KEY (DepartmentId) REFERENCES department (Id)
);

-- ─────────────────────────────────────────
-- Dados de Exemplo
-- ─────────────────────────────────────────
INSERT INTO department (Name) VALUES
    ('Computers'), ('Electronics'), ('Fashion'), ('Books');

INSERT INTO seller (Name, Email, BirthDate, BaseSalary, DepartmentId) VALUES
    ('Bob Brown',    'bob@gmail.com',    '1998-04-21 00:00:00', 1000.0, 1),
    ('Maria Pink',  'maria@gmail.com',  '1979-10-31 00:00:00', 3500.0, 1),
    ('Alex Grey',   'alex@gmail.com',   '1988-01-15 00:00:00', 2200.0, 2),
    ('Ana Lima',    'ana@gmail.com',    '1995-09-13 00:00:00', 1700.5, 4),
    ('John White',  'john@gmail.com',   '1991-11-21 00:00:00', 3000.0, 4);
```

### 📊 Relacionamento das Entidades

```
┌──────────────────┐         ┌─────────────────────────────┐
│    department    │         │           seller             │
│──────────────────│         │─────────────────────────────│
│ Id          PK   │◄────────│ DepartmentId       FK       │
│ Name             │  1   N  │ Id                 PK       │
└──────────────────┘         │ Name                        │
                             │ Email                       │
                             │ BirthDate                   │
                             │ BaseSalary                  │
                             └─────────────────────────────┘
```

---

## 📂 Estrutura do Projeto

```plaintext
demo_dao_jdbc/
│
├── 📄 database.sql                            # 🗃️  Script de criação do BD e dados de exemplo
├── 📄 db.properties                           # ⚙️  Credenciais de conexão MySQL ← NÃO versionar
├── 📄 .classpath                              # ⚙️  Configuração do classpath (Eclipse)
├── 📄 .project                                # ⚙️  Configuração do projeto (Eclipse)
│
└── 📁 src/
    ├── 📁 model/
    │   ├── 📁 entities/
    │   │   ├── 📄 Department.java             # 🏛️  Entidade Departamento
    │   │   └── 📄 Seller.java                 # 🏛️  Entidade Vendedor
    │   │
    │   └── 📁 dao/
    │       ├── 📄 DepartmentDao.java          # 📋 Interface DAO — Departamento
    │       ├── 📄 SellerDao.java              # 📋 Interface DAO — Vendedor
    │       │
    │       └── 📁 impl/
    │           ├── 📄 DepartmentDaoJDBC.java  # ⚙️  Implementação JDBC — Departamento ← CORE
    │           └── 📄 SellerDaoJDBC.java      # ⚙️  Implementação JDBC — Vendedor ← CORE
    │
    ├── 📁 db/
    │   ├── 📄 DB.java                         # 🔌 Utilitário de conexão JDBC
    │   ├── 📄 DbException.java                # 🚨 Exceção de banco de dados
    │   └── 📄 DbIntegrityException.java       # 🚨 Exceção de integridade referencial
    │
    └── 📁 application/
        ├── 📄 DaoFactory.java                 # 🏭 Factory de instâncias DAO
        └── 📄 Program.java                    # ▶️  Demonstração de todas as operações CRUD
```

---

## 🚀 Como Executar

### 📋 Pré-requisitos

| Requisito | Detalhe |
|:----------|:--------|
| **JDK** | Versão **11 ou superior** instalada e configurada no `PATH`. |
| **MySQL Server** | Versão **8.x** rodando localmente (porta padrão `3306`). |
| **MySQL Connector/J** | Driver JDBC adicionado ao classpath do projeto. |
| **Eclipse IDE** | Recomendado — arquivos de configuração já incluídos no repositório. |
| **Git** | Para clonar o repositório. |

---

### 🔧 Passo a Passo

**1. Clone o repositório:**

```bash
git clone https://github.com/VictorHJesusSantiago/demo_dao_jdbc.git
cd demo_dao_jdbc
```

**2. Crie o banco de dados e as tabelas:**

```bash
mysql -u root -p < database.sql
```

**3. Configure as credenciais no `db.properties`:**

```properties
dburl=jdbc:mysql://localhost:3306/coursejdbc
user=root
password=sua_senha_aqui
useSSL=false
```

**4. Abra no Eclipse IDE:**

```
File → Import → Existing Projects into Workspace
→ Selecione a pasta 'demo_dao_jdbc'
→ Finish
```

**5. Adicione o MySQL Connector/J ao Build Path:**

```
Clique direito no projeto → Build Path → Add External Archives
→ Selecione o arquivo mysql-connector-j-X.X.X.jar
```

**6. Execute o programa:**

```
Clique direito em src/application/Program.java
→ Run As → Java Application
```

---

### 🖥️ Exemplo de Saída no Console

```
=== TEST 1: findById ===
Seller{id=3, name=Alex Grey, email=alex@gmail.com, ...}

=== TEST 2: findByDepartment ===
Seller{id=1, name=Bob Brown, email=bob@gmail.com, ...}
Seller{id=2, name=Maria Pink, email=maria@gmail.com, ...}

=== TEST 3: findAll ===
[lista completa de vendedores]

=== TEST 4: Seller insert ===
Inserted! New id = 6

=== TEST 5: Seller update ===
Update completed!

=== TEST 6: Seller delete ===
Done! Deleted!
```

---

## 🤝 Como Contribuir

> Contribuições são muito bem-vindas! Siga as etapas abaixo para colaborar de forma organizada.

| Passo | Ação | Comando |
|:-----:|:-----|:--------|
| 1️⃣ | **Fork** | Crie um fork do repositório para a sua conta. | — |
| 2️⃣ | **Branch** | Crie sua feature branch a partir da `main`. | `git checkout -b feature/NovaFeature` |
| 3️⃣ | **Commit** | Salve as alterações com mensagem clara e semântica. | `git commit -m 'feat: Adiciona NovaFeature'` |
| 4️⃣ | **Push** | Envie a branch para o repositório remoto. | `git push origin feature/NovaFeature` |
| 5️⃣ | **Pull Request** | Abra um PR detalhando as mudanças realizadas. | — |

<div align="center">

<br>

**Se este projeto foi útil para os seus estudos, deixe uma estrela ⭐️ no repositório!**

</div>

---

## 👨‍💻 Autor

<div align="center">

<br>

**Victor H. J. Santiago**

<br>

[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/VictorHJesusSantiago)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/victor-henrique-de-jesus-santiago/)

</div>

---

## 📄 Licença

<div align="center">

Este projeto está distribuído sob a **Licença MIT**.
Consulte o arquivo [`LICENSE`](./LICENSE) no repositório para mais informações.

![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

</div>

---

<div align="center">

*Feito com 🗃️ e Java por **Victor H. J. Santiago***

</div>
