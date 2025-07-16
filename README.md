# 📘 ORiem Banking Web App – Blueprint Documentation

## 📌 Overview

**ORiem** is a secure, modern, and scalable banking platform designed for customers and administrators to manage digital banking operations with ease, safety, and efficiency.

### 🎯 Goals

- Enable customers to perform banking operations online.
- Provide admins with tools to monitor users, transactions, and loans.
- Ensure security, compliance, and performance at scale.
- Modularize codebase and workflows for maintainability and expansion.

---

## ⚙️ Tech Stack

| Layer        | Technology                            |
|--------------|----------------------------------------|
| Frontend     | React + Vite + i18next                 |
| Backend      | FastAPI (Python) + PyJWT + SQLModel    |
| Database     | Supabase (PostgreSQL) + Row-level Security |
| Auth         | JWT + 2FA (OTP) + RBAC + Device Logging|
| DevOps       | Docker + GitHub Actions + UptimeRobot  |
| Hosting      | Vercel (Frontend), Railway/Render (Backend) |
| CI/CD        | GitHub Workflows + Supabase backups    |
| Monitoring   | Sentry + PostHog (optional)            |

---

## 🧱 Architecture

```txt
React (Vite)
   ↓ REST
FastAPI (Python)
   ↓ ORM
Supabase (PostgreSQL)
```

- Secure RESTful APIs
- Modular services and routes (User, Accounts, Loans, Admin)
- JWT + Refresh tokens
- RBAC + Middleware-based permissions
- 2FA + Rate limiting + Device/session tracking

---

## 📂 Project Structure

```
orbanking/
├── frontend/                 # React app (Vite)
│   └── i18n/                 # Language files
├── backend/                  # FastAPI backend
│   ├── routes/
│   ├── services/
│   ├── models/
│   └── middleware/
├── database/                 # SQL schema & seeders
├── docker/                   # Dockerfiles + Compose
├── tests/                    # Pytest + Cypress
├── .github/workflows/        # CI/CD pipeline
├── changelog.md
├── README.md
└── .env.example
```

---

## 🧩 Core Modules & Status

| Module               | Status       |
|----------------------|--------------|
| User/Auth            | ✅ Completed |
| Accounts/Transactions| 🟡 In Progress |
| Loans                | 🔴 Planned   |
| Admin Dashboard      | 🟡 In Progress |
| Audit & Logs         | ✅ Completed |
| Notifications        | 🔴 Planned   |

---

## 🔐 Security & Compliance

- HTTPS (TLS 1.3)
- AES-256 encrypted fields (e.g., KYC docs)
- JWT auth with refresh & device metadata
- Rate limiting via FastAPI middleware
- 2FA (TOTP via OTP provider API)
- Session logging per device/IP
- Audit trails on user/admin actions
- Compliance with CBN, NDPR/GDPR, PCI DSS

---

## 🗃️ Database Schema

### Tables
- `users` – Basic profile, email, hashed password
- `accounts` – Savings/Current, balances, timestamps
- `transactions` – Transfers, deposits, withdrawals
- `loans` – Loan details & status
- `loan_repayments` – Schedules, due dates
- `audit_logs` – Admin/customer activities
- `admins` – Special access rights
- `role_permissions` – RBAC matrix
- `notifications` – System messages
- `sessions` – Logged-in devices

---

## 🔌 API Blueprint (Sample Endpoints)

### Auth
```http
POST   /auth/register
POST   /auth/login
POST   /auth/verify-2fa
POST   /auth/refresh-token
POST   /auth/forgot-password
POST   /auth/logout
```

### Accounts
```http
POST   /accounts/
GET    /accounts/{id}
GET    /accounts/{id}/transactions
POST   /accounts/transfer
```

### Transactions
```http
GET    /transactions/{user_id}
GET    /transactions/{id}/receipt
```

### Loans
```http
POST   /loans/apply
PUT    /loans/{id}/approve
GET    /loans/{user_id}
GET    /loans/{id}/repayments
```

### Admin
```http
GET    /admin/users
GET    /admin/logs
POST   /admin/roles
GET    /admin/branches
```

---

## 🧪 Testing Strategy

- **Frontend**:
  - Unit: Jest + React Testing Library
  - E2E: Cypress with mock API
- **Backend**:
  - Unit: Pytest + TestClient
  - Mocking: Faker + Dependency Injection
- **CI/CD**:
  - GitHub Actions for lint, test, build
  - Auto-deploy on `main` to Vercel/Railway

---

## 🚀 Deployment Strategy

| Component | Tool      | Notes                               |
|-----------|-----------|--------------------------------------|
| Frontend  | Vercel    | Auto deploy on push to `main`        |
| Backend   | Railway   | Auto-deploy from GitHub              |
| Database  | Supabase  | Daily backups, row-level security    |
| CI/CD     | GitHub    | Run `ci.yml` for build + test matrix |

### `.env.example`
```env
DATABASE_URL=
JWT_SECRET=
OTP_API_KEY=
SUPABASE_ANON_KEY=
SUPABASE_SERVICE_KEY=
```

---

## 📈 Monitoring & Observability

- **Uptime**: UptimeRobot + Slack alerts
- **Logging**: Console + Sentry (backend)
- **Crash Reports**: Sentry or Logtail
- **Analytics**: PostHog or Google Analytics
- **Downtime fallback**: Show offline page (PWA)

---

## 📄 Legal & Support Pages

- ✅ `Privacy Policy`
- ✅ `Terms & Conditions`
- ✅ `Security Notice`
- ✅ `Support Contact` (Live chat, ticketing)
- ✅ `Accessibility & WCAG`

---

## 🧭 Future Roadmap

| Feature                    | Status   |
|----------------------------|----------|
| ✅ Biometric login         | Done     |
| ✅ Multi-currency wallet   | Done     |
| ⏳ USSD channel integration| Planned  |
| ⏳ Virtual debit cards     | Planned  |
| ⏳ In-app support inbox    | Planned  |
| ⏳ Credit bureau API sync  | Planned  |
| ⏳ AI fraud pattern alerts | Planned  |

---

## 📦 Optional Tools

| Tool         | Purpose                      |
|--------------|------------------------------|
| Sentry       | Error tracking               |
| PostHog      | Product analytics            |
| Clerk/Auth0  | Auth-as-a-service (optional) |
| Stripe       | Virtual card APIs            |
| Langfuse     | Observability for LLMs       |

---

## 🧑‍💻 Developer Setup

```bash
git clone https://github.com/oriem-org/orbanking-webapp.git
cd orbanking-webapp
cp .env.example .env

# Backend
cd backend
uvicorn app.main:app --reload

# Frontend
cd ../frontend
npm install
npm run dev
```

---

## 📬 Contact & Contribution

- GitHub: [github.com/oriem-org](#)
- Contact: dev@oriem.finance
- License: MIT
- Contributions: PRs welcome with proper testing & descriptions

---

## 📌 Versioning & Changelog

```
Current Version: v1.0.0

## [1.0.0] – 2025-07-16
### Added
- Auth module with 2FA
- Accounts & transaction endpoints
- Admin user management
- CI/CD via GitHub Actions
```
