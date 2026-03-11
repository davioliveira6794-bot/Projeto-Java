# 🚀 RecrutaTech — Recrutamento Inteligente e Ágil

**Projeto Integrador | Técnico de Informática para Internet — SENAI Ariquemes 2026**

Autores: Davi Oliveira Silva • Géssica Reis Nery • Emily Lorrainne • Isaac Ruiz

---

## 📁 Estrutura do Projeto

```
recrutatech/
├── backend/          ← Spring Boot 3 + Maven (Java 17)
└── frontend/         ← Angular 17 + SCSS
```

---

## 🗄️ Modelagem de Dados

```
┌─────────────┐     ┌──────────────┐     ┌────────────┐
│   Usuario   │     │     Vaga     │     │ Candidato  │
│─────────────│     │──────────────│     │────────────│
│ id          │     │ id           │     │ id         │
│ nome        │     │ titulo       │     │ nome       │
│ email       │◄────│ criadoPor(FK)│     │ email      │
│ senha       │     │ area         │     │ telefone   │
│ role        │     │ nivel        │     │ linkedin   │
│ ativo       │     │ modalidade   │     │ habilidades│
└─────────────┘     │ localizacao  │     └────────────┘
                    │ status       │           │
                    │ requisitos[] │           │
                    └──────────────┘           │
                           │                  │
                    ┌──────▼──────────────────▼┐
                    │       Candidatura         │
                    │───────────────────────────│
                    │ id                        │
                    │ candidato_id (FK)          │
                    │ vaga_id (FK)               │
                    │ status                    │
                    │ scoreIA (0-100)            │
                    │ inscritoEm                │
                    └────────────┬──────────────┘
                                 │
                    ┌────────────▼──────────────┐
                    │        Entrevista          │
                    │───────────────────────────│
                    │ id                        │
                    │ candidatura_id (FK)        │
                    │ entrevistador_id (FK)      │
                    │ dataHora                  │
                    │ tipo (ONLINE/PRESENCIAL..) │
                    │ nota (1-10)               │
                    │ feedback                  │
                    │ realizada                 │
                    └───────────────────────────┘
```

### Fluxo de StatusCandidatura:
```
INSCRITO → TRIAGEM (IA) → ENTREVISTA → TECNICO → OFERTA → APROVADO
                                                         ↘ REPROVADO
```

---

## ⚙️ Nível de Complexidade

| Camada | Tecnologias | Nível |
|--------|-------------|-------|
| Backend | Spring Boot 3, Spring Security, JWT, JPA/Hibernate | ⭐⭐⭐⭐ Avançado |
| Banco | PostgreSQL, relacionamentos N:N, Enums | ⭐⭐⭐ Intermediário |
| Frontend | Angular 17, Serviços HTTP, Guards, Interceptors | ⭐⭐⭐⭐ Avançado |
| Design | SCSS customizado, dark theme, design system | ⭐⭐⭐⭐ Avançado |
| IA Simulada | Score automático por match de habilidades | ⭐⭐⭐ Intermediário |

---

## 🔧 Como Rodar

### Pré-requisitos
- Java 17+
- Maven 3.8+
- Node.js 18+
- PostgreSQL 14+

### Backend

```bash
# 1. Criar banco de dados
psql -U postgres -c "CREATE DATABASE recrutatech;"

# 2. Entrar na pasta
cd backend

# 3. Compilar e rodar
mvn spring-boot:run
```

**A API ficará disponível em:** `http://localhost:8080`

### Frontend

```bash
# 1. Entrar na pasta
cd frontend

# 2. Instalar dependências
npm install

# 3. Rodar em modo dev
npm start
```

**O app ficará disponível em:** `http://localhost:4200`

---

## 🔌 Endpoints da API REST

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| POST   | `/api/auth/login` | Autenticação JWT |
| GET    | `/api/vagas` | Listar todas as vagas |
| POST   | `/api/vagas` | Criar nova vaga |
| PUT    | `/api/vagas/{id}` | Atualizar vaga |
| DELETE | `/api/vagas/{id}` | Excluir vaga |
| GET    | `/api/candidatos` | Listar candidatos |
| POST   | `/api/candidatos` | Cadastrar candidato |
| POST   | `/api/candidaturas/inscrever` | Inscrever candidato em vaga |
| PATCH  | `/api/candidaturas/{id}/status` | Avançar no funil |
| POST   | `/api/entrevistas` | Agendar entrevista |
| GET    | `/api/dashboard` | KPIs e métricas |

---

## 🔐 Autenticação

Todas as rotas (exceto `/api/auth/login`) exigem token JWT no header:
```
Authorization: Bearer <token>
```

---

## 🎨 Design System

- **Tema:** Dark corporativo com accent azul elétrico
- **Fontes:** Syne (display) + DM Sans (corpo)
- **Cores principais:** `#0d0f14` (fundo), `#4f8ef7` (accent), `#22c55e` (sucesso)
- **Componentes:** Cards, Badges, Tabelas, Modais, Score bars

