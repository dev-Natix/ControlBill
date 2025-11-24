# 💳 ControlBill — Controle Financeiro Pessoal

Aplicação web simples para controle financeiro pessoal, com autenticação de usuários, lançamentos de receitas e despesas, limite mensal de gastos e interface responsiva.

---

## 🧰 Tecnologias

- PHP 8+
- MySQL / MariaDB (XAMPP)
- PDO + Prepared Statements
- HTML5 + CSS3 (responsivo)
- JavaScript (validação básica no front-end)

---

## 🗂 Estrutura de pastas

```text
controlbill/
├── config/
│   ├── config.php        # Configurações gerais (DB, BASE_URL, sessão)
│   └── db.php            # Conexão PDO com MySQL
├── includes/
│   ├── auth.php          # Autenticação, sessão, funções de usuário
│   ├── flash.php         # Mensagens de feedback (sucesso/erro)
│   ├── header.php        # Cabeçalho HTML + inclusão de CSS/JS
│   ├── navbar.php        # Menu de navegação
│   └── footer.php        # Rodapé
├── public/
│   ├── index.php         # Redireciona para login/dashboard
│   ├── login.php         # Tela de login
│   ├── logout.php        # Logout
│   ├── register.php      # Cadastro de usuário
│   ├── dashboard.php     # Resumo financeiro (saldo, limites)
│   ├── transactions_list.php   # Lista e filtro de lançamentos
│   ├── transactions_form.php   # Form de criação/edição de lançamentos
│   ├── transaction_save.php    # Processa insert/update
│   ├── transaction_delete.php  # Exclui lançamentos
│   ├── css/
│   │   └── style.css     # Estilos globais e responsivos
│   └── js/
│       └── validation.js # Validação simples de formulários
└── sql/
    └── schema.sql        # Script de criação do banco e tabelas
🗄 Banco de dados

Banco: controlbill

Tabela users

id (INT, PK, AI)

name (VARCHAR)

email (VARCHAR, único)

password_hash (VARCHAR)

monthly_limit (DECIMAL) — limite mensal de despesas

created_at (TIMESTAMP)

Tabela transactions

id (INT, PK, AI)

user_id (INT, FK → users.id)

type (ENUM: receita | despesa)

category (VARCHAR)

description (VARCHAR)

amount (DECIMAL)

date (DATE)

status (ENUM: pago | pendente)

created_at (TIMESTAMP)

O script sql/schema.sql contém o CREATE DATABASE, USE e os CREATE TABLE.

✨ Funcionalidades

✅ Cadastro de usuário com limite mensal de despesas

✅ Login e logout com sessões em PHP

✅ Área restrita protegida por require_login()

✅ CRUD completo de lançamentos financeiros (receitas e despesas)

✅ Filtro de lançamentos por mês

✅ Resumo financeiro no dashboard:

Total de receitas

Total de despesas

Saldo atual

Barra de progresso do limite mensal

✅ Validação no front-end (JS) e back-end (PHP)

✅ Feedback visual de ações (sucesso/erro) com flash messages

✅ Estilo responsivo com paleta:

#092327, #0B5351, #00A9A5, #4E8098, #90C2E7

📏 Requisitos do projeto (enunciado) — Checklist

 Estrutura completa com HTML e CSS responsivo

 Cadastro, edição e exclusão de dados (CRUD) usando PHP e MySQL

 Autenticação de usuários (login/logout) e proteção de área restrita

 Uso de sessões em PHP para controle de acesso e dados do usuário

 Formulários com validação no front-end (HTML/JS) e back-end (PHP)

 Organização por módulos/arquivos separados (camadas)

 Uso de PDO com Prepared Statements para MySQL

 Feedback visual para ações (sucesso, erro, mensagens)

 Regras de negócio (limite mensal de despesa, bloqueio data futura como “pago”, valores > 0)

 Documentação interna (comentários) e externa (este README)

🚀 Como rodar (XAMPP)

Copie a pasta controlbill para dentro de htdocs do XAMPP.

Inicie Apache e MySQL no painel do XAMPP.

Abra o phpMyAdmin e execute o script:

Em sql/schema.sql (ou cole o conteúdo na aba SQL).

Ajuste, se necessário, as configurações em config/config.php:

define('DB_HOST', '127.0.0.1');
define('DB_NAME', 'controlbill');
define('DB_USER', 'root');
define('DB_PASS', '');
define('BASE_URL', '/controlbill/public');


Acesse no navegador:

http://localhost/controlbill/public/


Clique em Registrar, crie um usuário e depois faça login.

🧠 Regras de negócio implementadas

Despesas/receitas não podem ter valor menor ou igual a zero.

Não é permitido marcar uma transação com data futura como pago.

Para despesas:

A soma das despesas do mês não pode ultrapassar o monthly_limit do usuário;

Se ultrapassar, o sistema bloqueia o lançamento e exibe mensagem de erro.

🧩 Possíveis melhorias futuras

Categorias pré-cadastradas por tipo (receita/despesa)

Relatórios gráficos por período

Exportação para CSV/Excel

Edição do limite mensal na própria interface do usuário