# TaskFlow — Personal Productivity API

> **Status:** Planning / Initial Setup  
> **Level:** Beginner · Full-Stack Portfolio Project  
> **Industry:** SaaS / Productivity

## Project Overview

TaskFlow is a planned full-stack personal productivity application that helps users organize tasks, priorities, deadlines, categories, and tags in one place.

The project is designed as a **backend-first ASP.NET Core REST API** with a responsive **React + TypeScript** client. Its primary goal is to demonstrate practical full-stack fundamentals: secure authentication, validated APIs, database design, reliable error handling, automated tests, and a reproducible development workflow.

**Planned capabilities:**
- Account registration, login, JWT access tokens, and rotating refresh tokens delivered through HttpOnly cookies.
- Task creation, editing, listing, and soft deletion.
- Task categories and tags.
- Paginated task lists with filtering, sorting, and debounced search.
- Responsive task dashboard with protected routes and accessible forms.
- Structured logging, API documentation, health checks, automated testing, and CI.

These capabilities are **requirements, not completed features**.

## Tech Stack

| Area | Planned technologies |
| --- | --- |
| Frontend | React, TypeScript, Vite, Material UI (MUI), React Router |
| Frontend data & forms | TanStack Query, TanStack Table, React Hook Form, Zod, Axios |
| Backend | ASP.NET Core Web API, C#, ASP.NET Core Identity |
| Persistence | Entity Framework Core, SQL Server |
| Validation & API docs | FluentValidation, Swagger / OpenAPI, ProblemDetails |
| Logging & monitoring | Serilog (console and file sinks), ASP.NET Core Health Checks |
| Testing | xUnit, Moq, WebApplicationFactory, Vitest, React Testing Library |
| DevOps | Git, GitHub Actions, Docker, Docker Compose, nginx |
| Planned hosting | Azure App Service and Azure SQL Database or containerized SQL Server |

**Optional stretch goals:** Hangfire, SignalR, and API versioning.

## Planned Architecture

TaskFlow will follow a deliberately simple **N-Layer Architecture** rather than Clean Architecture for this first project.

```text
React + TypeScript Client
          |
          | HTTPS / REST (Axios, typed OpenAPI client)
          v
ASP.NET Core API Controllers
          |
          v
Application Services / Business Logic
          |
          v
Repositories + Unit of Work
          |
          v
Entity Framework Core
          |
          v
SQL Server
```

The backend will separate API endpoints, application services, domain entities, and persistence concerns. Authentication will use ASP.NET Core Identity, short-lived JWT access tokens held in frontend memory, and refresh-token rotation via HttpOnly cookies. Protected endpoints will enforce authorization on the server.

Validation failures will return standard `ValidationProblemDetails` responses, while unexpected errors will be handled consistently using `ProblemDetails`. The React client will map field validation errors to forms and show unexpected failures through notifications.

The planned data model includes **User, Task, Category, Tag, and TaskTag**, with user-owned tasks, task-to-tag many-to-many relationships, indexes, and soft deletion.

## Project Structure

The repository will use the following **top-level structure**:

```text
taskflow-fullstack/
├── backend/
├── frontend/
├── docs/
├── .github/
│   └── workflows/
├── .gitignore
└── README.md
```

| Path | Purpose |
| --- | --- |
| `backend/` | ASP.NET Core API, domain model, services, repositories, EF Core persistence, and backend tests. |
| `frontend/` | Vite React + TypeScript application, UI, API integration, and frontend tests. |
| `docs/` | Architecture notes, ER diagram, API examples, Postman collection, and demo assets when created. |
| `.github/workflows/` | GitHub Actions CI workflows for building, testing, and reporting coverage. |
| `.gitignore` | Ignore generated artifacts, local secrets, and development-only files. |
| `README.md` | Project overview, technical decisions, workflow, and setup instructions. |

Internal directories will be defined as implementation begins; they are intentionally not prescribed here.

## Development Workflow

Development will follow an issue-driven workflow inspired by a software engineering team:

1. **Plan:** Translate roadmap requirements into GitHub Issues with clear acceptance criteria, estimates, and dependencies.
2. **Prioritize:** Organize issues into short sprints, working approximately **3–4 hours per day**.
3. **Branch:** Create a focused feature or fix branch from the current integration branch (for example, `feature/task-crud`).
4. **Implement:** Make small, reviewable commits; include validation, security, and error handling where relevant.
5. **Test:** Run applicable backend and frontend tests; add integration tests for critical API workflows.
6. **Review:** Open a Pull Request, check acceptance criteria and CI results, then merge after review.
7. **Document:** Update relevant documentation and record any technical decisions or known limitations.

### Planned implementation sequence

1. Scaffold backend and frontend; configure local development proxy.
2. Design entities, EF Core configuration, migrations, and seed data.
3. Implement registration, login, JWT authentication, and rotating refresh tokens.
4. Add validation, exception handling, structured logging, and health checks.
5. Implement Task, Category, and Tag APIs with pagination, filtering, sorting, search, and soft deletion.
6. Publish OpenAPI documentation and generate a typed TypeScript client.
7. Implement React authentication, protected routes, and Axios refresh handling.
8. Build task management UI, forms, filters, debounced search, and responsive layouts.
9. Add unit, integration, and frontend tests; target **at least 70% backend coverage**.
10. Add Docker Compose, GitHub Actions, coverage reporting, deployment, and demo documentation.

### Definition of Done

An issue is ready to close when its acceptance criteria are met, relevant tests pass, code has been reviewed, and documentation is updated where necessary.

Key project-level acceptance criteria include refresh-token replay rejection, standardized validation errors, correct task filtering/pagination, exclusion of soft-deleted tasks, authenticated API protection, cancellation of superseded searches, and passing CI.

## Getting Started

> **Placeholder — setup instructions will be added after the initial project scaffold is implemented.**

Planned setup documentation will cover:

- Prerequisites and required tool versions.
- Local environment variables and secure secret configuration.
- SQL Server connection and EF Core migrations.
- Backend API startup.
- Frontend development server startup and Vite proxy configuration.
- Running automated tests.
- Running the full stack with Docker Compose.

**No installation commands are provided yet**, because the project files and configuration have not been created or verified.

---

*This README describes the intended scope and development process for TaskFlow. Implementation status will be updated as milestones are completed.*
