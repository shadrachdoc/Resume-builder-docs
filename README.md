# Resume Builder Platform - Complete Project Plan

## 📋 Table of Contents
1. [Project Overview](#project-overview)
2. [Tech Stack](#tech-stack)
3. [Repository Structure](#repository-structure)
4. [Infrastructure Architecture](#infrastructure-architecture)
5. [Database Schema](#database-schema)
6. [Kubernetes Architecture](#kubernetes-architecture)
7. [Deployment Strategy](#deployment-strategy)
8. [Development Workflow](#development-workflow)
9. [Testing Strategy](#testing-strategy)
10. [Security Architecture](#security-architecture)
11. [Implementation Phases](#implementation-phases)
12. [Timeline & Milestones](#timeline--milestones)

---

## 🎯 Project Overview

### Vision
A modern, responsive resume builder and job application tracker with payment integration. Mobile-first design with dark mode support.

### Core Modules
1. **Resume Builder** - Create, customize, and export professional resumes
2. **Job Tracker** - Kanban-style job application management
3. **Payment System** - Subscription-based monetization (Phase 2)

### Key Features
- 🎨 Modern, colorful, playful UI
- 📱 Separate mobile views (not just responsive)
- 🌙 Dark mode from day 1
- 🔒 Enterprise-grade security (2FA, encryption, GDPR)
- ♾️ Highly customizable resume templates
- 💳 Freemium model with premium tiers

---

## 🛠️ Tech Stack

### Backend
- **Language:** PHP 8.2+
- **Framework:** Laravel 11
- **Database:** PostgreSQL 15
- **Cache/Queue:** Redis 7
- **Authentication:** Laravel Sanctum
- **PDF Generation:** DOMPDF
- **Testing:** PHPUnit, PHPStan

### Frontend
- **Language:** TypeScript
- **Framework:** React 18
- **Build Tool:** Vite
- **Styling:** Tailwind CSS
- **State Management:** Zustand
- **API Client:** Axios
- **Query Management:** TanStack Query
- **Drag & Drop:** @dnd-kit
- **Testing:** Vitest, React Testing Library, Playwright

### DevOps & Infrastructure
- **Version Control:** Git, GitHub
- **CI/CD:** GitHub Actions
- **GitOps:** ArgoCD
- **Container:** Docker
- **Orchestration:** Kubernetes (Docker Desktop → AWS EKS/Azure AKS)
- **Package Manager:** Helm
- **IaC (Phase 3):** Terraform
- **Monitoring (Future):** Prometheus, Grafana

### Payment (Phase 2)
- **Gateway:** Stripe
- **Webhooks:** Laravel Queue

### Third-party Integrations (Phase 2+)
- Google OAuth
- LinkedIn OAuth
- SendGrid (Email)
- AWS S3 (File storage)

---

## 📁 Repository Structure

### Total Repositories: 4

```
1. resume-builder-backend/
   - Laravel API
   - Database migrations
   - Business logic
   - API documentation

2. resume-builder-frontend/
   - React application
   - UI components
   - State management
   - Client-side routing

3. resume-builder-infrastructure/
   - Kubernetes manifests
   - Helm charts
   - ArgoCD configurations
   - Docker Compose files
   - Terraform scripts (Phase 3)

4. resume-builder-docs/
   - User documentation
   - API documentation
   - Architecture diagrams
   - Setup guides
   - Deployment procedures
```

### Repository Details

#### 1. Backend Repository
```
resume-builder-backend/
├── .github/
│   └── workflows/
│       ├── ci.yml                 # Run tests, linting
│       ├── build.yml              # Build Docker image
│       └── deploy.yml             # Trigger ArgoCD
├── app/
│   ├── Http/
│   │   ├── Controllers/
│   │   │   └── Api/
│   │   │       └── V1/
│   │   │           ├── AuthController.php
│   │   │           ├── ResumeController.php
│   │   │           ├── JobApplicationController.php
│   │   │           ├── PaymentController.php
│   │   │           └── DashboardController.php
│   │   ├── Middleware/
│   │   │   ├── CheckPlanLimit.php
│   │   │   └── VerifyTwoFactor.php
│   │   └── Requests/
│   ├── Models/
│   │   ├── User.php
│   │   ├── Resume.php
│   │   ├── JobApplication.php
│   │   ├── Subscription.php
│   │   └── Payment.php
│   ├── Services/
│   │   ├── ResumeService.php
│   │   ├── PdfExportService.php
│   │   ├── StripeService.php
│   │   └── EncryptionService.php
│   ├── Policies/
│   └── Jobs/
│       ├── SendWelcomeEmail.php
│       └── GenerateResumePDF.php
├── database/
│   ├── migrations/
│   ├── seeders/
│   └── factories/
├── routes/
│   └── api.php
├── tests/
│   ├── Feature/
│   └── Unit/
├── docker/
│   ├── Dockerfile
│   └── php.ini
├── .env.example
├── composer.json
└── README.md
```

#### 2. Frontend Repository
```
resume-builder-frontend/
├── .github/
│   └── workflows/
│       ├── ci.yml
│       ├── build.yml
│       └── deploy.yml
├── public/
├── src/
│   ├── api/
│   │   ├── axios.ts
│   │   ├── auth.ts
│   │   ├── resumes.ts
│   │   ├── jobs.ts
│   │   └── payments.ts
│   ├── components/
│   │   ├── common/
│   │   │   ├── Button.tsx
│   │   │   ├── Input.tsx
│   │   │   ├── Card.tsx
│   │   │   ├── Navbar.tsx
│   │   │   └── LoadingSpinner.tsx
│   │   ├── resume/
│   │   │   ├── ResumeBuilder/
│   │   │   ├── TemplateSelector/
│   │   │   ├── ResumePreview/
│   │   │   └── CustomizationPanel/
│   │   ├── jobs/
│   │   │   ├── KanbanBoard/
│   │   │   ├── JobCard/
│   │   │   ├── JobModal/
│   │   │   └── ListView/ (Mobile)
│   │   └── payment/
│   │       ├── PricingTable/
│   │       ├── CheckoutForm/
│   │       └── SubscriptionDashboard/
│   ├── pages/
│   │   ├── auth/
│   │   │   ├── Login.tsx
│   │   │   └── Register.tsx
│   │   ├── Dashboard.tsx
│   │   ├── Resumes.tsx
│   │   ├── ResumeEditor.tsx
│   │   ├── JobTracker.tsx
│   │   ├── Pricing.tsx
│   │   └── Settings.tsx
│   ├── stores/
│   │   ├── authStore.ts
│   │   ├── resumeStore.ts
│   │   └── themeStore.ts
│   ├── hooks/
│   │   ├── useAuth.ts
│   │   ├── useFeatureAccess.ts
│   │   └── useMediaQuery.ts
│   ├── types/
│   │   └── index.ts
│   ├── utils/
│   │   └── cn.ts
│   ├── styles/
│   │   └── index.css
│   ├── App.tsx
│   └── main.tsx
├── e2e/
│   └── tests/
├── docker/
│   └── Dockerfile
├── .env.example
├── package.json
├── tailwind.config.js
├── vite.config.ts
└── README.md
```

#### 3. Infrastructure Repository
```
resume-builder-infrastructure/
├── docker-compose/
│   ├── development.yml           # Local development
│   └── README.md
├── kubernetes/
│   ├── base/                     # Base K8s manifests
│   │   ├── namespace.yaml
│   │   ├── backend/
│   │   │   ├── deployment.yaml
│   │   │   ├── service.yaml
│   │   │   └── configmap.yaml
│   │   ├── frontend/
│   │   │   ├── deployment.yaml
│   │   │   └── service.yaml
│   │   ├── database/
│   │   │   ├── statefulset.yaml
│   │   │   ├── service.yaml
│   │   │   └── pvc.yaml
│   │   └── redis/
│   │       ├── deployment.yaml
│   │       └── service.yaml
│   └── overlays/
│       ├── local/                # Docker Desktop K8s
│       ├── staging/
│       └── production/
├── helm/
│   └── resume-builder/
│       ├── Chart.yaml
│       ├── values.yaml
│       ├── values-local.yaml
│       ├── values-staging.yaml
│       ├── values-production.yaml
│       └── templates/
│           ├── backend/
│           ├── frontend/
│           ├── database/
│           ├── redis/
│           └── ingress.yaml
├── argocd/
│   ├── applications/
│   │   ├── backend.yaml
│   │   ├── frontend.yaml
│   │   └── database.yaml
│   └── projects/
│       └── resume-builder.yaml
├── terraform/                    # Phase 3
│   ├── aws/
│   │   ├── eks/
│   │   ├── rds/
│   │   └── vpc/
│   └── azure/
│       ├── aks/
│       └── postgresql/
└── README.md
```

#### 4. Documentation Repository
```
resume-builder-docs/
├── architecture/
│   ├── overview.md
│   ├── database-design.md
│   ├── api-design.md
│   └── infrastructure.md
├── guides/
│   ├── setup/
│   │   ├── local-development.md
│   │   ├── docker-setup.md
│   │   └── k8s-setup.md
│   ├── deployment/
│   │   ├── local-deployment.md
│   │   ├── staging-deployment.md
│   │   └── production-deployment.md
│   └── development/
│       ├── coding-standards.md
│       ├── git-workflow.md
│       └── testing.md
├── api/
│   └── openapi.yaml
├── user-manual/
│   ├── getting-started.md
│   ├── resume-builder.md
│   └── job-tracker.md
└── README.md
```

---

## 🏗️ Infrastructure Architecture

### Phase 1: Local Development (Docker Desktop K8s)

```
┌────────────────────────────────────────────────────────────────────┐
│                         YOUR LAPTOP                                 │
│                                                                     │
│  ┌──────────────────────────────────────────────────────────────┐ │
│  │              Docker Desktop with Kubernetes                   │ │
│  │                                                                │ │
│  │  ┌─────────────────────────────────────────────────────────┐ │ │
│  │  │  Namespace: resume-builder-dev                          │ │ │
│  │  │                                                          │ │ │
│  │  │  ┌────────────────┐  ┌────────────────┐               │ │ │
│  │  │  │ Backend Pod    │  │ Frontend Pod   │               │ │ │
│  │  │  │ Laravel:8000   │  │ React:5173     │               │ │ │
│  │  │  │ Replicas: 1    │  │ Replicas: 1    │               │ │ │
│  │  │  └───────┬────────┘  └────────────────┘               │ │ │
│  │  │          │                                              │ │ │
│  │  │  ┌───────▼──────────┐  ┌────────────────┐            │ │ │
│  │  │  │ PostgreSQL       │  │ Redis          │            │ │ │
│  │  │  │ StatefulSet      │  │ Deployment     │            │ │ │
│  │  │  │ PVC: 10Gi        │  │ Memory: 512Mi  │            │ │ │
│  │  │  └──────────────────┘  └────────────────┘            │ │ │
│  │  │                                                          │ │ │
│  │  │  ┌────────────────────────────────────────┐           │ │ │
│  │  │  │ Services                                │           │ │ │
│  │  │  │ - backend-service (ClusterIP)          │           │ │ │
│  │  │  │ - frontend-service (NodePort:30080)    │           │ │ │
│  │  │  │ - postgres-service (ClusterIP)         │           │ │ │
│  │  │  │ - redis-service (ClusterIP)            │           │ │ │
│  │  │  └────────────────────────────────────────┘           │ │ │
│  │  └─────────────────────────────────────────────────────────┘ │ │
│  │                                                                │ │
│  │  ┌─────────────────────────────────────────────────────────┐ │ │
│  │  │  Namespace: argocd                                      │ │ │
│  │  │  - ArgoCD Server                                        │ │ │
│  │  │  - Application Controller                               │ │ │
│  │  │  - Repo Server                                          │ │ │
│  │  └─────────────────────────────────────────────────────────┘ │ │
│  └──────────────────────────────────────────────────────────────┘ │
│                                                                     │
│  Access URLs:                                                      │
│  - Frontend: http://localhost:30080                                │
│  - Backend API: http://localhost:30000/api                         │
│  - ArgoCD UI: http://localhost:30081                               │
└────────────────────────────────────────────────────────────────────┘
                              ▲
                              │
                        Git Push/Pull
                              │
┌─────────────────────────────┴──────────────────────────────────────┐
│                          GitHub                                     │
│                                                                     │
│  ┌────────────────┐  ┌─────────────────┐  ┌──────────────────┐   │
│  │ Backend Repo   │  │ Frontend Repo   │  │ Infra Repo       │   │
│  │ (Laravel)      │  │ (React)         │  │ (K8s/Helm)       │   │
│  └────────┬───────┘  └────────┬────────┘  └────────┬─────────┘   │
│           │                    │                     │              │
│  ┌────────▼────────────────────▼─────────────────────▼──────────┐ │
│  │              GitHub Actions (CI/CD)                           │ │
│  │  - Run Tests                                                  │ │
│  │  - Build Docker Images                                        │ │
│  │  - Push to GitHub Container Registry                          │ │
│  │  - Update Helm values                                         │ │
│  │  - Trigger ArgoCD Sync                                        │ │
│  └───────────────────────────────────────────────────────────────┘ │
│                                                                     │
│  ┌───────────────────────────────────────────────────────────────┐ │
│  │              GitHub Container Registry (GHCR)                 │ │
│  │  - resume-builder-backend:latest                              │ │
│  │  - resume-builder-frontend:latest                             │ │
│  └───────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────────┘
```

### Phase 2: Cloud Production (AWS EKS / Azure AKS)

```
┌─────────────────────────────────────────────────────────────────────┐
│                    Cloud Provider (AWS/Azure)                        │
│                                                                      │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │                  Managed Kubernetes (EKS/AKS)                  │ │
│  │                                                                 │ │
│  │  ┌────────────────────────────────────────────────────────┐   │ │
│  │  │ Ingress Controller (nginx-ingress)                     │   │ │
│  │  │ + Load Balancer + SSL/TLS (Let's Encrypt)             │   │ │
│  │  │ - resume-builder.com                                   │   │ │
│  │  │ - api.resume-builder.com                               │   │ │
│  │  └──────────────────────┬─────────────────────────────────┘   │ │
│  │                         │                                      │ │
│  │  ┌──────────────────────▼─────────────────────┐              │ │
│  │  │ Namespace: resume-builder-production       │              │ │
│  │  │                                             │              │ │
│  │  │  ┌────────────────────────────────────┐   │              │ │
│  │  │  │ Backend Deployment                 │   │              │ │
│  │  │  │ Replicas: 3 (Auto-scaling 3-10)    │   │              │ │
│  │  │  │ Resources:                          │   │              │ │
│  │  │  │   CPU: 500m - 1000m                │   │              │ │
│  │  │  │   Memory: 512Mi - 1Gi              │   │              │ │
│  │  │  └────────────────────────────────────┘   │              │ │
│  │  │                                             │              │ │
│  │  │  ┌────────────────────────────────────┐   │              │ │
│  │  │  │ Frontend Deployment                │   │              │ │
│  │  │  │ Replicas: 2                        │   │              │ │
│  │  │  │ Resources:                          │   │              │ │
│  │  │  │   CPU: 200m - 500m                 │   │              │ │
│  │  │  │   Memory: 256Mi - 512Mi            │   │              │ │
│  │  │  └────────────────────────────────────┘   │              │ │
│  │  │                                             │              │ │
│  │  │  ┌────────────────────────────────────┐   │              │ │
│  │  │  │ Redis Deployment                   │   │              │ │
│  │  │  │ Or ElastiCache (AWS)               │   │              │ │
│  │  │  │ Or Azure Cache for Redis           │   │              │ │
│  │  │  └────────────────────────────────────┘   │              │ │
│  │  └─────────────────────────────────────────────┘              │ │
│  │                                                                 │ │
│  │  ┌──────────────────────────────────────────────────────────┐ │ │
│  │  │ Namespace: argocd                                        │ │ │
│  │  │ - ArgoCD for GitOps                                      │ │ │
│  │  └──────────────────────────────────────────────────────────┘ │ │
│  └─────────────────────────────────────────────────────────────────┘│
│                                                                      │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │              Managed Database (RDS/Azure Database)             │ │
│  │  PostgreSQL 15                                                 │ │
│  │  - Multi-AZ deployment                                         │ │
│  │  - Automated backups                                           │ │
│  │  - Read replicas                                               │ │
│  └────────────────────────────────────────────────────────────────┘ │
│                                                                      │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │              Object Storage (S3/Azure Blob)                    │ │
│  │  - Resume PDFs                                                 │ │
│  │  - User uploads                                                │ │
│  │  - Template assets                                             │ │
│  └────────────────────────────────────────────────────────────────┘ │
│                                                                      │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │              Monitoring & Logging                              │ │
│  │  - CloudWatch/Azure Monitor                                    │ │
│  │  - Prometheus + Grafana                                        │ │
│  │  - ELK Stack (Future)                                          │ │
│  └────────────────────────────────────────────────────────────────┘ │
└──────────────────────────────────────────────────────────────────────┘
```

---

## 🗄️ Database Schema

### Entity Relationship Diagram

```
┌─────────────────────────────────────────────────────────────────────┐
│                                                                      │
│  ┌─────────────┐                                                    │
│  │   users     │                                                    │
│  ├─────────────┤                                                    │
│  │ id          │◄───────────────┐                                  │
│  │ name        │                 │                                  │
│  │ email       │                 │                                  │
│  │ password    │                 │                                  │
│  │ email_ver..│                 │                                  │
│  │ current_p..│───┐             │                                  │
│  │ trial_end..│   │             │                                  │
│  │ is_premium │   │             │                                  │
│  │ two_factor..│   │             │                                  │
│  │ two_factor..│   │             │                                  │
│  │ created_at │   │             │                                  │
│  │ updated_at │   │             │                                  │
│  └─────────────┘   │             │                                  │
│         │           │             │                                  │
│         │           │             │                                  │
│  ┌──────▼──────┐   │     ┌───────▼───────────┐                    │
│  │  resumes    │   │     │ job_applications  │                    │
│  ├─────────────┤   │     ├───────────────────┤                    │
│  │ id          │   │     │ id                │                    │
│  │ user_id     │───┘     │ user_id           │                    │
│  │ title       │         │ resume_id         │─────┐              │
│  │ template_id │───┐     │ company_name      │     │              │
│  │ personal_..│   │     │ position          │     │              │
│  │ sections    │   │     │ location          │     │              │
│  │ styling     │   │     │ status            │     │              │
│  │ is_active   │   │     │ job_url           │     │              │
│  │ created_at  │   │     │ salary_min        │     │              │
│  │ updated_at  │   │     │ salary_max        │     │              │
│  │ deleted_at  │   │     │ currency          │     │              │
│  └─────────────┘   │     │ applied_date      │     │              │
│         ▲           │     │ deadline          │     │              │
│         │           │     │ priority          │     │              │
│         │           │     │ job_description   │     │              │
│         │           │     │ notes             │     │              │
│         └───────────┼─────│ column_order      │     │              │
│                     │     │ company_logo      │     │              │
│                     │     │ created_at        │     │              │
│  ┌─────────────────┐│     │ updated_at        │     │              │
│  │resume_templates ││     │ deleted_at        │     │              │
│  ├─────────────────┤│     └───────────────────┘     │              │
│  │ id              ││              │                 │              │
│  │ name            ││              │                 │              │
│  │ slug            ││     ┌────────▼──────────┐      │              │
│  │ description     ││     │interview_rounds   │      │              │
│  │ preview_image   ││     ├───────────────────┤      │              │
│  │ default_styling ││     │ id                │      │              │
│  │ is_premium      ││     │ job_application_id│      │              │
│  │ is_active       ││     │ round_name        │      │              │
│  │ created_at      ││     │ scheduled_at      │      │              │
│  │ updated_at      ││     │ feedback          │      │              │
│  └─────────────────┘│     │ status            │      │              │
│                     │     │ interviewer_name  │      │              │
│                     │     │ meeting_link      │      │              │
│                     │     │ created_at        │      │              │
│                     │     │ updated_at        │      │              │
│                     │     └───────────────────┘      │              │
│                     │                                │              │
│  ┌──────────────────▼──┐                            │              │
│  │subscription_plans   │                            │              │
│  ├─────────────────────┤                            │              │
│  │ id                  │                            │              │
│  │ name                │                            │              │
│  │ slug                │                            │              │
│  │ price               │                            │              │
│  │ billing_cycle       │                            │              │
│  │ features (JSON)     │                            │              │
│  │ limits (JSON)       │                            │              │
│  │ is_active           │                            │              │
│  │ created_at          │                            │              │
│  │ updated_at          │                            │              │
│  └─────────────────────┘                            │              │
│         │                                            │              │
│         │                                            │              │
│  ┌──────▼──────────┐                                │              │
│  │ subscriptions   │                                │              │
│  ├─────────────────┤                                │              │
│  │ id              │                                │              │
│  │ user_id         │────────────────────────────────┘              │
│  │ plan_id         │                                               │
│  │ status          │                                               │
│  │ starts_at       │                                               │
│  │ ends_at         │                                               │
│  │ trial_ends_at   │                                               │
│  │ cancelled_at    │                                               │
│  │ created_at      │                                               │
│  │ updated_at      │                                               │
│  └─────────────────┘                                               │
│         │                                                           │
│         │                                                           │
│  ┌──────▼──────────┐                                               │
│  │   payments      │                                               │
│  ├─────────────────┤                                               │
│  │ id              │                                               │
│  │ user_id         │                                               │
│  │ subscription_id │                                               │
│  │ amount          │                                               │
│  │ currency        │                                               │
│  │ status          │                                               │
│  │ payment_method  │                                               │
│  │ stripe_payment_id                                               │
│  │ stripe_invoice_id                                               │
│  │ paid_at         │                                               │
│  │ created_at      │                                               │
│  │ updated_at      │                                               │
│  └─────────────────┘                                               │
│                                                                     │
│  ┌──────────────────┐                                              │
│  │ usage_tracking   │                                              │
│  ├──────────────────┤                                              │
│  │ id               │                                              │
│  │ user_id          │                                              │
│  │ feature          │ (resumes_created, pdf_exports, etc.)        │
│  │ count            │                                              │
│  │ period           │ (YYYY-MM)                                   │
│  │ reset_at         │                                              │
│  │ created_at       │                                              │
│  │ updated_at       │                                              │
│  └──────────────────┘                                              │
│                                                                     │
│  ┌──────────────────┐                                              │
│  │ board_columns    │                                              │
│  ├──────────────────┤                                              │
│  │ id               │                                              │
│  │ user_id          │                                              │
│  │ name             │                                              │
│  │ slug             │                                              │
│  │ order            │                                              │
│  │ color            │                                              │
│  │ created_at       │                                              │
│  │ updated_at       │                                              │
│  └──────────────────┘                                              │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### Table Definitions

#### 1. users
```sql
CREATE TABLE users (
    id BIGSERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    email_verified_at TIMESTAMP,
    current_plan_id BIGINT REFERENCES subscription_plans(id),
    trial_ends_at TIMESTAMP,
    is_premium BOOLEAN DEFAULT FALSE,
    two_factor_secret VARCHAR(255),
    two_factor_enabled BOOLEAN DEFAULT FALSE,
    remember_token VARCHAR(100),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_current_plan ON users(current_plan_id);
```

#### 2. resumes
```sql
CREATE TABLE resumes (
    id BIGSERIAL PRIMARY KEY,
    user_id BIGINT NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    title VARCHAR(255) NOT NULL,
    template_id VARCHAR(100) DEFAULT 'modern',
    personal_info JSONB,
    sections JSONB,
    styling JSONB,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP
);

CREATE INDEX idx_resumes_user_id ON resumes(user_id);
CREATE INDEX idx_resumes_template_id ON resumes(template_id);
CREATE INDEX idx_resumes_deleted_at ON resumes(deleted_at);
```

#### 3. job_applications
```sql
CREATE TABLE job_applications (
    id BIGSERIAL PRIMARY KEY,
    user_id BIGINT NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    resume_id BIGINT REFERENCES resumes(id) ON DELETE SET NULL,
    company_name VARCHAR(255) NOT NULL,
    position VARCHAR(255) NOT NULL,
    location VARCHAR(255),
    status VARCHAR(50) DEFAULT 'wishlist',
    job_url TEXT,
    salary_min DECIMAL(12,2),
    salary_max DECIMAL(12,2),
    currency VARCHAR(3) DEFAULT 'USD',
    applied_date DATE,
    deadline DATE,
    priority VARCHAR(20) DEFAULT 'medium',
    job_description TEXT,
    notes TEXT,
    column_order INTEGER DEFAULT 0,
    company_logo VARCHAR(255),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP
);

CREATE INDEX idx_job_applications_user_id ON job_applications(user_id);
CREATE INDEX idx_job_applications_status ON job_applications(status);
CREATE INDEX idx_job_applications_resume_id ON job_applications(resume_id);
```

#### 4. interview_rounds
```sql
CREATE TABLE interview_rounds (
    id BIGSERIAL PRIMARY KEY,
    job_application_id BIGINT NOT NULL REFERENCES job_applications(id) ON DELETE CASCADE,
    round_name VARCHAR(255) NOT NULL,
    scheduled_at TIMESTAMP,
    feedback TEXT,
    status VARCHAR(50) DEFAULT 'scheduled',
    interviewer_name VARCHAR(255),
    meeting_link TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_interview_rounds_job_id ON interview_rounds(job_application_id);
```

#### 5. resume_templates
```sql
CREATE TABLE resume_templates (
    id BIGSERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    slug VARCHAR(100) UNIQUE NOT NULL,
    description TEXT,
    preview_image VARCHAR(255),
    default_styling JSONB,
    is_premium BOOLEAN DEFAULT FALSE,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_resume_templates_slug ON resume_templates(slug);
CREATE INDEX idx_resume_templates_is_premium ON resume_templates(is_premium);
```

#### 6. subscription_plans
```sql
CREATE TABLE subscription_plans (
    id BIGSERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    slug VARCHAR(50) UNIQUE NOT NULL,
    price DECIMAL(10,2) NOT NULL,
    billing_cycle VARCHAR(20) DEFAULT 'monthly',
    features JSONB,
    limits JSONB,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Example limits JSON:
-- {
--   "max_resumes": 3,
--   "max_templates": 3,
--   "max_jobs": 50,
--   "pdf_exports_per_month": 10,
--   "custom_colors": false,
--   "ai_suggestions": false
-- }
```

#### 7. subscriptions
```sql
CREATE TABLE subscriptions (
    id BIGSERIAL PRIMARY KEY,
    user_id BIGINT NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    plan_id BIGINT NOT NULL REFERENCES subscription_plans(id),
    status VARCHAR(50) DEFAULT 'active',
    starts_at TIMESTAMP NOT NULL,
    ends_at TIMESTAMP,
    trial_ends_at TIMESTAMP,
    cancelled_at TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_subscriptions_user_id ON subscriptions(user_id);
CREATE INDEX idx_subscriptions_status ON subscriptions(status);
```

#### 8. payments
```sql
CREATE TABLE payments (
    id BIGSERIAL PRIMARY KEY,
    user_id BIGINT NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    subscription_id BIGINT REFERENCES subscriptions(id) ON DELETE SET NULL,
    amount DECIMAL(10,2) NOT NULL,
    currency VARCHAR(3) DEFAULT 'USD',
    status VARCHAR(50) DEFAULT 'pending',
    payment_method VARCHAR(50),
    stripe_payment_id VARCHAR(255),
    stripe_invoice_id VARCHAR(255),
    paid_at TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_payments_user_id ON payments(user_id);
CREATE INDEX idx_payments_stripe_payment_id ON payments(stripe_payment_id);
```

#### 9. usage_tracking
```sql
CREATE TABLE usage_tracking (
    id BIGSERIAL PRIMARY KEY,
    user_id BIGINT NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    feature VARCHAR(100) NOT NULL,
    count INTEGER DEFAULT 0,
    period VARCHAR(7) NOT NULL,
    reset_at TIMESTAMP NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(user_id, feature, period)
);

CREATE INDEX idx_usage_tracking_user_period ON usage_tracking(user_id, period);
```

#### 10. board_columns
```sql
CREATE TABLE board_columns (
    id BIGSERIAL PRIMARY KEY,
    user_id BIGINT NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    name VARCHAR(100) NOT NULL,
    slug VARCHAR(100) UNIQUE NOT NULL,
    order INTEGER DEFAULT 0,
    color VARCHAR(7) DEFAULT '#6B7280',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_board_columns_user_id ON board_columns(user_id);
```

---

## ☸️ Kubernetes Architecture

### Namespaces

#### Total Namespaces: 4

```yaml
1. resume-builder-dev       # Local development
2. resume-builder-staging   # Staging environment (Future)
3. resume-builder-production # Production (Phase 3)
4. argocd                   # ArgoCD GitOps controller
```

### Namespace: resume-builder-dev

#### Resources Breakdown

```
resume-builder-dev/
│
├── Deployments (4)
│   ├── backend-deployment
│   │   ├── Replicas: 1
│   │   ├── Image: ghcr.io/username/resume-builder-backend:latest
│   │   ├── Resources:
│   │   │   ├── Requests: CPU 200m, Memory 256Mi
│   │   │   └── Limits: CPU 500m, Memory 512Mi
│   │   ├── Env Variables:
│   │   │   ├── DB_HOST: postgres-service
│   │   │   ├── REDIS_HOST: redis-service
│   │   │   └── APP_ENV: local
│   │   └── Ports: 8000
│   │
│   ├── frontend-deployment
│   │   ├── Replicas: 1
│   │   ├── Image: ghcr.io/username/resume-builder-frontend:latest
│   │   ├── Resources:
│   │   │   ├── Requests: CPU 100m, Memory 128Mi
│   │   │   └── Limits: CPU 200m, Memory 256Mi
│   │   └── Ports: 80
│   │
│   ├── redis-deployment
│   │   ├── Replicas: 1
│   │   ├── Image: redis:7-alpine
│   │   ├── Resources:
│   │   │   ├── Requests: CPU 100m, Memory 256Mi
│   │   │   └── Limits: CPU 200m, Memory 512Mi
│   │   └── Ports: 6379
│   │
│   └── (PostgreSQL as StatefulSet - see below)
│
├── StatefulSets (1)
│   └── postgres-statefulset
│       ├── Replicas: 1
│       ├── Image: postgres:15-alpine
│       ├── Resources:
│       │   ├── Requests: CPU 200m, Memory 512Mi
│       │   └── Limits: CPU 500m, Memory 1Gi
│       ├── Ports: 5432
│       └── Volume: postgres-pvc (10Gi)
│
├── Services (4)
│   ├── backend-service
│   │   ├── Type: ClusterIP
│   │   ├── Port: 8000
│   │   └── Selector: app=backend
│   │
│   ├── frontend-service
│   │   ├── Type: NodePort
│   │   ├── Port: 80
│   │   ├── NodePort: 30080
│   │   └── Selector: app=frontend
│   │
│   ├── postgres-service
│   │   ├── Type: ClusterIP
│   │   ├── Port: 5432
│   │   └── Selector: app=postgres
│   │
│   └── redis-service
│       ├── Type: ClusterIP
│       ├── Port: 6379
│       └── Selector: app=redis
│
├── ConfigMaps (2)
│   ├── backend-config
│   │   └── Contains: Non-sensitive config
│   └── frontend-config
│       └── Contains: API URL, environment
│
├── Secrets (2)
│   ├── backend-secrets
│   │   └── Contains: DB password, JWT secret, Stripe keys
│   └── postgres-secrets
│       └── Contains: Postgres password
│
├── PersistentVolumeClaims (1)
│   └── postgres-pvc
│       ├── Size: 10Gi
│       ├── AccessMode: ReadWriteOnce
│       └── StorageClass: hostpath (local)
│
└── HorizontalPodAutoscaler (0 for local, 2 for production)
    └── (Will be added in production phase)
```

### Helm Chart Structure

```yaml
helm/resume-builder/
├── Chart.yaml
├── values.yaml              # Default values
├── values-local.yaml        # Local development overrides
├── values-staging.yaml      # Staging overrides
├── values-production.yaml   # Production overrides
│
└── templates/
    ├── _helpers.tpl         # Template helpers
    │
    ├── namespace.yaml
    │
    ├── backend/
    │   ├── deployment.yaml
    │   ├── service.yaml
    │   ├── configmap.yaml
    │   ├── secret.yaml
    │   └── hpa.yaml         # HorizontalPodAutoscaler
    │
    ├── frontend/
    │   ├── deployment.yaml
    │   ├── service.yaml
    │   ├── configmap.yaml
    │   └── hpa.yaml
    │
    ├── database/
    │   ├── statefulset.yaml
    │   ├── service.yaml
    │   ├── secret.yaml
    │   └── pvc.yaml
    │
    ├── redis/
    │   ├── deployment.yaml
    │   └── service.yaml
    │
    └── ingress.yaml         # For production with domain
```

### Sample Helm Values

```yaml
# values-local.yaml
global:
  environment: local
  domain: localhost

backend:
  replicaCount: 1
  image:
    repository: ghcr.io/username/resume-builder-backend
    tag: latest
    pullPolicy: Always
  resources:
    requests:
      cpu: 200m
      memory: 256Mi
    limits:
      cpu: 500m
      memory: 512Mi
  service:
    type: ClusterIP
    port: 8000
  env:
    APP_ENV: local
    APP_DEBUG: "true"
    DB_HOST: postgres-service
    REDIS_HOST: redis-service

frontend:
  replicaCount: 1
  image:
    repository: ghcr.io/username/resume-builder-frontend
    tag: latest
  resources:
    requests:
      cpu: 100m
      memory: 128Mi
    limits:
      cpu: 200m
      memory: 256Mi
  service:
    type: NodePort
    port: 80
    nodePort: 30080

database:
  enabled: true
  image:
    repository: postgres
    tag: 15-alpine
  resources:
    requests:
      cpu: 200m
      memory: 512Mi
    limits:
      cpu: 500m
      memory: 1Gi
  persistence:
    enabled: true
    size: 10Gi
    storageClass: hostpath

redis:
  enabled: true
  image:
    repository: redis
    tag: 7-alpine
  resources:
    requests:
      cpu: 100m
      memory: 256Mi
```

```yaml
# values-production.yaml
global:
  environment: production
  domain: resume-builder.com

backend:
  replicaCount: 3
  autoscaling:
    enabled: true
    minReplicas: 3
    maxReplicas: 10
    targetCPUUtilizationPercentage: 70
  resources:
    requests:
      cpu: 500m
      memory: 512Mi
    limits:
      cpu: 1000m
      memory: 1Gi
  service:
    type: ClusterIP

frontend:
  replicaCount: 2
  autoscaling:
    enabled: true
    minReplicas: 2
    maxReplicas: 5
  resources:
    requests:
      cpu: 200m
      memory: 256Mi
    limits:
      cpu: 500m
      memory: 512Mi

database:
  enabled: false  # Use managed RDS/Azure Database
  externalHost: resume-builder.xxxx.rds.amazonaws.com

redis:
  enabled: false  # Use ElastiCache/Azure Cache
  externalHost: resume-builder.xxxx.cache.amazonaws.com

ingress:
  enabled: true
  className: nginx
  annotations:
    cert-manager.io/cluster-issuer: letsencrypt-prod
  hosts:
    - host: resume-builder.com
      paths:
        - path: /
          pathType: Prefix
          service: frontend
    - host: api.resume-builder.com
      paths:
        - path: /
          pathType: Prefix
          service: backend
  tls:
    - secretName: resume-builder-tls
      hosts:
        - resume-builder.com
        - api.resume-builder.com
```

---

## 🚀 Deployment Strategy

### Deployment Flow Diagram

```
┌──────────────────────────────────────────────────────────────────┐
│                    Developer Workflow                             │
└──────────────────────────────────────────────────────────────────┘
                              │
                              │ 1. Code & Commit
                              ▼
                    ┌───────────────────┐
                    │   Git Push to     │
                    │   GitHub (main)   │
                    └─────────┬─────────┘
                              │
                              │ 2. Trigger
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                    GitHub Actions CI/CD                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌────────────────┐  ┌────────────────┐  ┌──────────────────┐ │
│  │  Run Tests     │→ │  Build Docker  │→ │  Push to GHCR    │ │
│  │  (PHPUnit,     │  │  Image         │  │  (Container      │ │
│  │   Vitest)      │  │                │  │   Registry)      │ │
│  └────────────────┘  └────────────────┘  └──────────────────┘ │
│                                                    │             │
│                                                    │             │
│  ┌────────────────┐  ┌────────────────────────────▼──────────┐ │
│  │ Update Helm    │← │  Tag: latest, v1.0.0, commit-sha      │ │
│  │ values.yaml    │  └───────────────────────────────────────┘ │
│  └────────┬───────┘                                             │
│           │                                                      │
└───────────┼──────────────────────────────────────────────────────┘
            │
            │ 3. Git Commit (values updated)
            ▼
┌─────────────────────────────────────────────────────────────────┐
│               Infrastructure Repository                          │
│  ┌───────────────────────────────────────────────────────────┐ │
│  │  helm/resume-builder/values.yaml                          │ │
│  │  (Updated with new image tag)                             │ │
│  └───────────────────────────────────────────────────────────┘ │
└──────────────────────────┬──────────────────────────────────────┘
                           │
                           │ 4. ArgoCD detects change
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│                         ArgoCD                                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌──────────────┐  ┌──────────────┐  ┌─────────────────────┐  │
│  │ Detect Git   │→ │ Helm Template│→ │ Apply to Kubernetes │  │
│  │ Changes      │  │ Generation   │  │                     │  │
│  └──────────────┘  └──────────────┘  └─────────────────────┘  │
│                                                                  │
│  Sync Strategy: Auto (or Manual approval for production)        │
│  Self-Heal: Enabled                                             │
│  Prune: Enabled                                                 │
│                                                                  │
└──────────────────────────┬──────────────────────────────────────┘
                           │
                           │ 5. Deploy
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Kubernetes Cluster                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  Rolling Update                                          │  │
│  │  - Backend: 1 pod → 2 pods → kill old → 1 pod           │  │
│  │  - Frontend: Same strategy                               │  │
│  │  - Zero downtime deployment                              │  │
│  └──────────────────────────────────────────────────────────┘  │
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  Health Checks                                           │  │
│  │  - Readiness probe: /api/health                          │  │
│  │  - Liveness probe: /api/ping                             │  │
│  └──────────────────────────────────────────────────────────┘  │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
                           │
                           │ 6. Success/Failure notification
                           ▼
                    ┌──────────────┐
                    │   Slack /    │
                    │   Email      │
                    └──────────────┘
```

### Deployment Commands

#### Local Development Deployment

```bash
# 1. Install ArgoCD
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# 2. Access ArgoCD UI
kubectl port-forward svc/argocd-server -n argocd 8080:443

# 3. Get initial admin password
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

# 4. Install application using Helm
helm install resume-builder ./helm/resume-builder \
  --namespace resume-builder-dev \
  --create-namespace \
  --values ./helm/resume-builder/values-local.yaml

# 5. Create ArgoCD Application
kubectl apply -f argocd/applications/resume-builder-dev.yaml

# 6. Verify deployment
kubectl get pods -n resume-builder-dev
kubectl get svc -n resume-builder-dev

# 7. Access application
# Frontend: http://localhost:30080
# Backend API: http://localhost:30000
```

#### Update Deployment

```bash
# Option 1: Helm upgrade
helm upgrade resume-builder ./helm/resume-builder \
  --namespace resume-builder-dev \
  --values ./helm/resume-builder/values-local.yaml

# Option 2: ArgoCD sync (GitOps way)
# Just push changes to Git, ArgoCD auto-syncs

# Option 3: Manual image update
kubectl set image deployment/backend-deployment \
  backend=ghcr.io/username/resume-builder-backend:v1.0.1 \
  -n resume-builder-dev
```

---

## 🔄 Development Workflow

### Git Workflow (Git Flow)

```
main (production-ready)
  │
  ├── develop (integration branch)
  │     │
  │     ├── feature/resume-builder
  │     ├── feature/job-tracker
  │     ├── feature/payment-integration
  │     │
  │     ├── bugfix/pdf-export-issue
  │     │
  │     └── hotfix/security-patch
  │
  └── release/v1.0.0
```

### Branch Strategy

```
main
├── Protected branch
├── Requires PR approval
├── Auto-deploy to production (Phase 3)
└── Tagged releases (v1.0.0, v1.1.0)

develop
├── Integration branch
├── Auto-deploy to local K8s
├── Continuous integration
└── Merge from feature branches

feature/*
├── Created from develop
├── Naming: feature/module-name
├── PR to develop
└── Delete after merge

bugfix/*
├── Created from develop
├── For non-critical bugs
└── PR to develop

hotfix/*
├── Created from main
├── Critical production fixes
├── PR to both main and develop
└── Immediate deployment
```

### Daily Development Workflow

```
┌─────────────────────────────────────────────────────────────────┐
│                   Daily Workflow (1-2 hours)                     │
└─────────────────────────────────────────────────────────────────┘

Day Start:
  1. Pull latest develop branch
     git checkout develop
     git pull origin develop

  2. Create feature branch
     git checkout -b feature/add-resume-export

  3. Code (45-60 min)
     - Write feature code
     - Write unit tests
     - Test locally

  4. Commit
     git add .
     git commit -m "feat: add PDF export functionality"

  5. Push
     git push origin feature/add-resume-export

  6. Create Pull Request (PR)
     - Add description
     - Link to GitHub Project task
     - Request review (self-review for solo)

  7. Merge to develop
     - GitHub Actions runs tests
     - If pass, merge to develop
     - ArgoCD auto-deploys to local K8s

  8. Verify deployment
     - Check ArgoCD UI
     - Test feature on local K8s
     - Update GitHub Project board

Day End:
  - Update documentation
  - Plan next day's task
```

### Commit Message Convention

```
Format: <type>(<scope>): <subject>

Types:
  - feat: New feature
  - fix: Bug fix
  - docs: Documentation
  - style: Formatting, missing semicolons
  - refactor: Code restructuring
  - test: Adding tests
  - chore: Maintenance

Examples:
  feat(resume): add template customization
  fix(job-tracker): resolve drag-drop issue
  docs(api): update endpoint documentation
  test(auth): add login integration tests
```

---

## 🧪 Testing Strategy

### Testing Pyramid

```
                 ▲
                ╱ ╲
               ╱ E2E╲              10% - 20 tests
              ╱─────╲              Full user journeys
             ╱       ╲             Playwright
            ╱Integration╲          30% - 60 tests
           ╱───────────╲           API + Database
          ╱             ╲          PHPUnit Feature Tests
         ╱      Unit     ╲         60% - 120 tests
        ╱─────────────────╲        Functions, Components
                                   PHPUnit, Vitest
```

### Test Coverage Goals

```
Backend (Laravel):
├── Unit Tests: 70% coverage
├── Feature Tests: 60% coverage
└── Total: 65% minimum

Frontend (React):
├── Component Tests: 60% coverage
├── Integration Tests: 50% coverage
└── Total: 55% minimum

E2E Tests:
└── Critical paths: 100% coverage
    ├── User registration/login
    ├── Resume creation
    ├── PDF export
    ├── Job application tracking
    └── Payment flow (Phase 2)
```

### Test Execution

```bash
# Backend tests
composer test                    # Run all tests
composer test:unit              # Unit tests only
composer test:feature           # Feature tests only
composer test:coverage          # With coverage report

# Frontend tests
npm test                        # Run all tests
npm test:unit                   # Unit tests
npm test:watch                  # Watch mode
npm test:coverage               # Coverage report

# E2E tests
npm run test:e2e               # Playwright tests
npm run test:e2e:ui            # With UI

# CI/CD
# GitHub Actions runs all tests on every push
```

---

## 🔒 Security Architecture

### Security Layers

```
┌─────────────────────────────────────────────────────────────────┐
│                      Security Layers                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Layer 1: Network Security                                      │
│  ├── HTTPS/TLS 1.3 (Let's Encrypt)                             │
│  ├── CORS configuration                                         │
│  ├── Rate limiting (60 req/min per IP)                         │
│  └── DDoS protection (Cloudflare)                              │
│                                                                  │
│  Layer 2: Application Security                                  │
│  ├── Authentication                                             │
│  │   ├── Laravel Sanctum (API tokens)                          │
│  │   ├── Password hashing (bcrypt)                             │
│  │   ├── 2FA (TOTP - Google Authenticator)                     │
│  │   └── Social OAuth (Google, LinkedIn)                       │
│  ├── Authorization                                              │
│  │   ├── Policy-based access control                           │
│  │   ├── Plan-based feature gating                             │
│  │   └── Resource ownership validation                         │
│  └── Input Validation                                           │
│      ├── Request validation (Laravel)                           │
│      ├── XSS prevention                                         │
│      ├── SQL injection prevention (Eloquent ORM)               │
│      └── CSRF protection                                        │
│                                                                  │
│  Layer 3: Data Security                                         │
│  ├── Encryption at Rest                                         │
│  │   ├── Resume data (Laravel encrypted casts)                 │
│  │   ├── Sensitive user data                                   │
│  │   └── Payment information (Stripe handles)                  │
│  ├── Encryption in Transit                                      │
│  │   ├── TLS 1.3                                               │
│  │   └── Secure headers (HSTS, CSP)                            │
│  └── Database Security                                          │
│      ├── PostgreSQL SSL connections                            │
│      ├── Prepared statements                                   │
│      └── Principle of least privilege                          │
│                                                                  │
│  Layer 4: Infrastructure Security                               │
│  ├── Kubernetes                                                 │
│  │   ├── Network policies                                      │
│  │   ├── Pod security policies                                 │
│  │   ├── RBAC (Role-Based Access Control)                     │
│  │   └── Secrets management                                    │
│  ├── Container Security                                         │
│  │   ├── Non-root user                                         │
│  │   ├── Read-only filesystem                                  │
│  │   ├── Minimal base images (Alpine)                          │
│  │   └── Image scanning (Trivy)                                │
│  └── Cloud Security (Phase 3)                                   │
│      ├── VPC isolation                                         │
│      ├── Security groups                                        │
│      └── IAM roles                                              │
│                                                                  │
│  Layer 5: Compliance & Privacy                                  │
│  ├── GDPR Compliance                                            │
│  │   ├── Data export (JSON)                                    │
│  │   ├── Right to deletion                                     │
│  │   ├── Consent management                                    │
│  │   └── Privacy policy                                        │
│  ├── Payment Security (PCI DSS)                                │
│  │   └── Stripe handles card data                              │
│  └── Audit Logging                                              │
│      ├── User actions                                          │
│      ├── Admin actions                                         │
│      └── Security events                                       │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Secrets Management

```
Development (Local):
├── .env files (gitignored)
└── K8s Secrets (base64 encoded)

Production:
├── AWS Secrets Manager / Azure Key Vault
├── Sealed Secrets (Bitnami)
└── External Secrets Operator

Rotation Policy:
├── Database passwords: Every 90 days
├── API keys: Every 180 days
└── TLS certificates: Auto-renewed (Let's Encrypt)
```

---

## 📅 Implementation Phases

### Phase 1: FREE MVP (Months 1-5) - 140 Days

#### Month 1: Foundation (Days 1-28)
**Week 1: Setup**
- Repository creation
- Docker Compose setup
- K8s local deployment
- CI/CD pipeline basic

**Week 2: Authentication**
- User registration/login API
- Email verification
- Frontend auth pages
- Token management

**Week 3: Core Infrastructure**
- Dashboard layout
- Navigation system
- Dark mode implementation
- Mobile responsive foundation

**Week 4: Design System**
- Component library
- Color theme system
- Typography system
- Design documentation

**Deliverables:**
✅ Running local environment
✅ User can register/login
✅ Basic dashboard
✅ Component library ready

---

#### Month 2: Resume Builder (Days 29-56)
**Week 5: Data Structure**
- Resume model & migrations
- Resume API endpoints
- Personal info form
- Data validation

**Week 6: First Template**
- "Modern" template design
- Template rendering
- Live preview
- Basic styling

**Week 7: Resume Sections**
- Work experience
- Education
- Skills
- Projects

**Week 8: Editor UX**
- Section management
- Drag-to-reorder
- Desktop layout
- Mobile wizard view

**Deliverables:**
✅ Create resume
✅ 1 template working
✅ All sections functional
✅ Mobile-friendly editor

---

#### Month 3: Templates & Export (Days 57-84)
**Week 9: More Templates**
- "Minimal" template
- "Creative" template
- Template switcher

**Week 10: Customization**
- Font selection
- Color palettes
- Spacing controls
- Style persistence

**Week 11: PDF Export**
- DOMPDF integration
- PDF styling
- Download functionality
- Preview before export

**Week 12: Resume Management**
- Resume list view
- Duplicate resume
- Delete resume
- Search/filter

**Deliverables:**
✅ 3 templates available
✅ Customization working
✅ PDF export functional
✅ Resume management complete

---

#### Month 4: Job Tracker (Days 85-112)
**Week 13: Foundation**
- Job application model
- CRUD API endpoints
- Job form
- Validation

**Week 14: Kanban Board**
- Board layout
- Drag-and-drop
- Column management
- Status updates

**Week 15: Job Details**
- Job card design
- Detail modal
- Interview tracking
- Notes/deadlines

**Week 16: Mobile View**
- List view layout
- Filters/search
- Swipe gestures
- Mobile-optimized forms

**Deliverables:**
✅ Job tracking working
✅ Kanban functional
✅ Mobile view ready
✅ Interview tracking

---

#### Month 5: Polish & Launch (Days 113-140)
**Week 17: Dashboard**
- Stats/analytics
- Recent activity
- Quick actions
- Widgets

**Week 18: Limits**
- Free tier enforcement
- Usage tracking
- Upgrade prompts
- Limit messaging

**Week 19: Testing**
- Full app testing
- Mobile testing
- Bug fixes
- Performance tuning

**Week 20: Launch**
- Documentation
- User guides
- Deployment
- **🚀 LAUNCH!**

**Deliverables:**
✅ Complete dashboard
✅ Free tier working
✅ All bugs fixed
✅ **PUBLIC LAUNCH**

---

### Phase 2: Payment System (Months 6-7) - 56 Days

#### Month 6: Payments (Days 141-168)
**Week 21: Stripe Integration**
- Stripe account setup
- Subscription plans model
- Payment API
- Webhook handlers

**Week 22: Payment UI**
- Pricing page
- Checkout flow
- Payment form
- Success/failure pages

**Week 23: Feature Gating**
- Plan limit checks
- Middleware
- Upgrade prompts
- Access control

**Week 24: Launch Premium**
- Testing payments
- Security audit
- Documentation
- **💳 PREMIUM LAUNCH**

---

#### Month 7: Premium Features (Days 169-196)
**Week 25-26: Templates**
- 10+ premium templates
- Advanced customization
- Custom branding

**Week 27: Advanced Features**
- Analytics dashboard
- Email notifications
- Usage insights

**Week 28: Security**
- 2FA implementation
- Encryption at rest
- GDPR features
- Security audit

---

### Phase 3: Advanced & Scale (Months 8+)

#### Months 8-9: Cloud Migration
- Terraform setup
- AWS EKS / Azure AKS
- Managed databases
- Production deployment
- Monitoring & logging

#### Months 10-12: Advanced Features
- AI resume suggestions
- Cover letter generator
- LinkedIn integration
- Team collaboration
- Chrome extension

---

## 📊 Timeline & Milestones

### Visual Timeline

```
Month 1  Month 2  Month 3  Month 4  Month 5  Month 6  Month 7  Month 8+
│        │        │        │        │        │        │        │
├─Setup─►├Resume─►├Export─►├Jobs──►├Launch─►├Payment►├Premium►├Scale──►
│        │Builder │& More │Tracker │MVP     │System  │Features│Cloud   │
│        │        │Templates        │        │        │        │        │
▼        ▼        ▼        ▼        ▼        ▼        ▼        ▼
Auth     3 Temps  Customize Kanban  Polish   Stripe   10+Temps Terraform
+Infra   +Sections +PDF     +Mobile  +Test   +Limits  +AI      +AWS/AZ
+Design  +Editor   +Manage  +Details +Docs   +Checkout +2FA     +Monitor

🎯       🎯       🎯       🎯       🚀       💳       ⭐       ☁️
Ready    Working   Export   Jobs     LAUNCH   PREMIUM  ADVANCED CLOUD
```

### Key Milestones

| Milestone | Target Date | Description |
|-----------|------------|-------------|
| **M1: Dev Environment** | Week 1 | Local K8s + ArgoCD working |
| **M2: Authentication** | Week 2 | User can register/login |
| **M3: First Resume** | Week 6 | Create basic resume |
| **M4: PDF Export** | Week 11 | Download resume as PDF |
| **M5: Job Tracker** | Week 14 | Kanban board functional |
| **M6: Mobile Ready** | Week 16 | All features work on mobile |
| **M7: 🚀 MVP LAUNCH** | Week 20 | Public release (free) |
| **M8: Payment Live** | Week 24 | Premium plans available |
| **M9: Premium Features** | Week 28 | Advanced features released |
| **M10: Cloud Production** | Month 9 | Deployed to AWS/Azure |

---

## 🎯 Success Metrics

### Phase 1 (Free MVP)
- ✅ 100 registered users in Month 1
- ✅ 50 resumes created
- ✅ 100 job applications tracked
- ✅ <2 second page load time
- ✅ Mobile usage >40%

### Phase 2 (Premium)
- ✅ 10% free-to-paid conversion
- ✅ $500 MRR (Monthly Recurring Revenue)
- ✅ <5% churn rate

### Phase 3 (Scale)
- ✅ 1000+ active users
- ✅ $5000 MRR
- ✅ 99.9% uptime

---

## 📞 Support & Resources

### Documentation Links
- **Setup Guide:** `/docs/guides/setup/local-development.md`
- **API Docs:** `/docs/api/openapi.yaml`
- **Architecture:** `/docs/architecture/overview.md`
- **Deployment:** `/docs/guides/deployment/`

### Tools & Services
- **GitHub:** Version control + CI/CD
- **Docker Hub:** Container registry (or GHCR)
- **ArgoCD:** GitOps deployments
- **Stripe:** Payment processing
- **SendGrid:** Email delivery

### Community
- **Issues:** GitHub Issues for bugs
- **Discussions:** GitHub Discussions for questions
- **Wiki:** GitHub Wiki for knowledge base

---

## 🚦 Getting Started

### Quick Start

```bash
# 1. Clone repositories
git clone https://github.com/username/resume-builder-backend.git
git clone https://github.com/username/resume-builder-frontend.git
git clone https://github.com/username/resume-builder-infrastructure.git

# 2. Start local environment
cd resume-builder-infrastructure/docker-compose
docker-compose -f development.yml up -d

# 3. Install backend dependencies
cd ../../resume-builder-backend
composer install
php artisan migrate --seed

# 4. Install frontend dependencies
cd ../resume-builder-frontend
npm install
npm run dev

# 5. Access application
# Frontend: http://localhost:5173
# Backend: http://localhost:8000
```

### Next Steps
1. Read `/docs/guides/setup/local-development.md`
2. Setup GitHub Projects board
3. Start Week 1 tasks
4. Join daily stand-up (with yourself! 😄)

---

## 📝 Notes

- **Solo Development:** 1-2 hours/day = realistic timeline
- **Flexibility:** Adjust timeline based on progress
- **Documentation:** Update as you build
- **Testing:** Write tests alongside features
- **Deployment:** Use GitOps from day 1
- **Scaling:** Architecture ready for growth

---

**Version:** 1.0.0  
**Last Updated:** [Date]  
**Status:** Planning Complete ✅  
**Next Phase:** Week 1 - Setup

---

*This is a living document. Update as the project evolves.*