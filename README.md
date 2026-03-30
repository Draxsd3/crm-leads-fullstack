# CRM Leads — Plataforma Comercial Full Stack

> CRM completo para times comerciais: pipeline visual, gestão de leads,
> agenda de reuniões, KYC e relatórios com exportação PDF e Excel.

![React](https://img.shields.io/badge/React-18-61DAFB?style=flat-square&logo=react&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-18+-339933?style=flat-square&logo=nodedotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express-4-000000?style=flat-square&logo=express&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-Mongoose-47A248?style=flat-square&logo=mongodb&logoColor=white)
![MUI](https://img.shields.io/badge/MUI-v5-007FFF?style=flat-square&logo=mui&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-Auth-000000?style=flat-square&logo=jsonwebtokens&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

---

## Sobre o Projeto

O **CRM Leads** foi desenvolvido para simular um ambiente real de operação
comercial — desde a prospecção até o fechamento — com controle de acesso
por perfil, integrações externas e exportação de relatórios operacionais.

O foco técnico foi construir uma arquitetura em camadas limpa e escalável,
com autenticação stateless por JWT, RBAC completo, consulta de CNPJ com
fallback automático de provedores e geração de documentos direto pelo backend.

---

## Arquitetura
```
CRM-FullStack/
├── backend/
│   ├── config/           # variáveis e conexão
│   ├── controllers/      # lógica de requisição
│   ├── middlewares/      # auth, RBAC, validação
│   ├── models/           # schemas Mongoose
│   ├── routes/           # mapeamento de endpoints
│   ├── services/         # regras de negócio
│   ├── database/         # setup e seed do MongoDB
│   └── server.js
└── frontend/
    └── src/
        ├── components/
        ├── contexts/     # AuthContext, NotificationContext
        ├── pages/
        ├── services/     # cliente HTTP
        └── utils/
```

**Fluxo de autenticação:**
```
POST /api/users/login  →  JWT gerado  →  Header Authorization  →  Middleware RBAC  →  Rota protegida
```

---

## Funcionalidades

| Módulo | Funcionalidades |
|---|---|
| **Auth** | Login JWT, proteção de rotas, controle por perfil (RBAC) |
| **Leads & Empresas** | CRUD completo, busca por CNPJ com preenchimento automático |
| **Pipeline** | Funil de vendas com drag and drop entre etapas |
| **KYC** | Histórico de movimentações e dados cadastrais por empresa |
| **Agenda** | Gestão de reuniões com visualização em calendário |
| **Relatórios** | Filtros avançados, exportação em PDF e Excel |
| **Usuários** | Cadastro, upload de foto de perfil, troca de senha |

---

## Perfis de Acesso (RBAC)

| Perfil | Permissões |
|---|---|
| `ADM` | Acesso total, gestão de usuários |
| `SDR` | Prospecção, cadastro de leads |
| `Closer` | Pipeline, reuniões, fechamento |
| `Supervisor` | Relatórios e dashboards completos |

---

## Stack Tecnológica

### Backend
- **Node.js 18+** com **Express 4**
- **Mongoose** — modelagem ODM para MongoDB
- **JWT + bcryptjs** — autenticação stateless e hash de senhas
- **express-validator** — validação de entrada
- **Helmet + CORS + Morgan** — segurança e logging HTTP
- **PDFKit + ExcelJS** — geração de relatórios
- **Multer** — upload de imagem de perfil

### Frontend
- **React 18** com **Material UI v5**
- **React Router DOM** — roteamento protegido por perfil
- **@hello-pangea/dnd** — drag and drop no pipeline
- **React Big Calendar** — visualização de agenda
- **Chart.js** — gráficos de conversão e dashboard
- **Formik + Yup** — formulários com validação
- **Axios** — cliente HTTP com interceptors

### Banco de Dados
- **MongoDB** com Mongoose
- Scripts organizados em `backend/database/` (setup + seed)

### Integrações Externas
- **BrasilAPI** — consulta de CNPJ
- **ReceitaWS** — fallback automático em caso de indisponibilidade

---

## Como Executar Localmente

### Pré-requisitos
- Node.js 18+
- MongoDB local ou Atlas

### 1. Clone o repositório
```bash
git clone https://github.com/Draxsd3/crm-fullstack
cd CRM-FullStack
```

### 2. Configure o backend
```bash
cd backend
npm install
cp .env.example .env   # Linux/macOS
# copy .env.example .env  (Windows)
```

Variáveis principais em `backend/.env`:
```
MONGODB_URI=
JWT_SECRET=
PORT=5000
ALLOWED_ORIGINS=http://localhost:3000
```

### 3. Prepare o banco
```bash
npm run db:setup:seed   # setup + seed
npm run db:reset        # reset completo (opcional)
```

### 4. Inicie o backend
```bash
npm run dev
# API disponível em http://localhost:5000/api
```

### 5. Configure e inicie o frontend
```bash
cd ../frontend
npm install
npm start
# App disponível em http://localhost:3000
```

---

## Credenciais de Demonstração

| Perfil | E-mail | Senha |
|---|---|---|
| ADM | `admin@crmleads.com` | `Admin@2024` |
| SDR | `renan@crmleads.com` | `Renan@2004` |
| Closer | `maria@crmleads.com` | `Maria@2024` |
| Supervisor | `carlos@crmleads.com` | `Carlos@2024` |

---

## Endpoints Principais
```
POST   /api/users/login
GET    /api/users/me
PUT    /api/users/profile

GET    /api/companies
POST   /api/companies
GET    /api/companies/cnpj/:cnpj

GET    /api/pipeline
POST   /api/pipeline/update-status

GET    /api/meetings
POST   /api/meetings

GET    /api/reports/full
```

---

## Diferenciais Técnicos

- Arquitetura em camadas: `routes → controllers → services → models`
- RBAC granular com 4 perfis e middlewares independentes
- Consulta de CNPJ com fallback automático entre dois provedores
- Geração de PDF e Excel diretamente no backend sem dependências de terceiros
- Drag and drop nativo no pipeline sem bibliotecas pesadas
- Interceptors Axios centralizados para token, erros e notificações

---

## Roadmap

- [ ] Testes automatizados (Jest + Supertest no backend)
- [ ] CI/CD com GitHub Actions
- [ ] Auditoria de atividades por usuário
- [ ] Dashboard com KPIs avançados por etapa do funil

---

## Licença

MIT License. Consulte `LICENSE` para detalhes.
