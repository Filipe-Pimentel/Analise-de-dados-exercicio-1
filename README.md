# Analise-de-dados-exercicio-1
Lab dio analise 1

1️⃣ Esquema Conceitual (Modelo ER)

Entidades:

Conta

id_conta (PK)

tipo_conta (ENUM: PF, PJ) — uma conta não pode ser os dois tipos

nome_razao

cpf_cnpj

email

telefone

Pagamento (uma conta pode ter várias formas)

id_pagamento (PK)

id_conta (FK)

tipo_pagamento (ex: Cartão Crédito, Débito, Boleto, Pix)

detalhes (JSON ou texto)

Entrega

id_entrega (PK)

id_conta (FK)

endereco

status (ex: “pendente”, “enviado”, “entregue”)

codigo_rastreio

Exemplo em SQL
CREATE TABLE Conta (
    id_conta INT AUTO_INCREMENT PRIMARY KEY,
    tipo_conta ENUM('PF', 'PJ') NOT NULL,
    nome_razao VARCHAR(255) NOT NULL,
    cpf_cnpj VARCHAR(20) NOT NULL UNIQUE,
    email VARCHAR(255),
    telefone VARCHAR(50)
);

CREATE TABLE Pagamento (
    id_pagamento INT AUTO_INCREMENT PRIMARY KEY,
    id_conta INT NOT NULL,
    tipo_pagamento VARCHAR(50) NOT NULL,
    detalhes TEXT,
    FOREIGN KEY (id_conta) REFERENCES Conta(id_conta)
);

CREATE TABLE Entrega (
    id_entrega INT AUTO_INCREMENT PRIMARY KEY,
    id_conta INT NOT NULL,
    endereco VARCHAR(255) NOT NULL,
    status ENUM('pendente','enviado','entregue','cancelado') DEFAULT 'pendente',
    codigo_rastreio VARCHAR(100),
    FOREIGN KEY (id_conta) REFERENCES Conta(id_conta)
);

2️⃣ Estrutura do Repositório
/seu-repositorio
│
├── esquema.sql        # Script SQL com as tabelas
├── modelo-er.png      # (opcional) imagem do modelo ER
└── README.md

-------

# Desafio: Modelo Conceitual com Cliente PF/PJ, Pagamento e Entrega

Este projeto foi desenvolvido como parte de um desafio de modelagem de banco de dados.

## 📌 Contexto
O objetivo do desafio é **refinar um modelo conceitual** para contemplar:
- Cliente PF e PJ (uma conta pode ser PF ou PJ, mas não ambos)
- Múltiplas formas de pagamento por cliente
- Entregas com status e código de rastreio

## 🗂️ Estrutura do Projeto
- `esquema.sql` – Script SQL para criar as tabelas
- `modelo-er.png` – Diagrama ER (opcional)
- `README.md` – Descrição do projeto

## 📝 Modelo Conceitual
**Entidades principais:**
- Conta (PF ou PJ)
- Pagamento (N formas para 1 conta)
- Entrega (status + rastreio)

## 🚀 Como usar
1. Clone este repositório:
   ```bash
   git clone https://github.com/seuusuario/seu-repositorio.git
Execute o script esquema.sql no seu banco de dados MySQL/MariaDB/PostgreSQL (ajuste tipos se necessário).

🧩 Tecnologias
SQL (MySQL/MariaDB)

GitHub

👤 Autor
Desenvolvido por Filipe Pimentel
