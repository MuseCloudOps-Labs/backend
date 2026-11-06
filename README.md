# Zen Pharma Backend

**Author: Abdirahman Muse**

A Spring Boot microservices monorepo for the Zen Pharma platform. The project is designed around a modular backend architecture consisting of seven services, with automated CI/CD, containerization, security checks, and GitOps-based deployment workflows.

**Technology stack:** Java 17 · Spring Boot · Spring Cloud Gateway · Node.js 20 · PostgreSQL · Docker · Kubernetes · AWS EKS · Terraform · GitHub Actions · Argo CD · Helm

> **Project status:** Update this README to reflect the features that are actually implemented and tested. Planned integrations and deployment capabilities should not be presented as completed.

---

## Companion Repositories

The Zen Pharma platform is organized into separate repositories:

- **Backend:** [zen-pharma-backend](https://github.com/MuseCloudOps-Labs/backend) — Backend microservices and CI workflows.
- **Frontend:** [zen-pharma-frontend](https://github.com/MuseCloudOps-Labs/frontend) — React application.
- **Infrastructure:** [zen-infra](https://github.com/MuseCloudOps-Labs/infra) — Terraform infrastructure configuration.
- **GitOps:** [zen-gitops](https://github.com/MuseCloudOps-Labs/gitops) — Argo CD applications and Helm deployment configuration.

---

## 1. Backend Services

The backend consists of seven services, each responsible for a specific business capability.

| Service                 | Description                                                  | Port | Database   |
| ----------------------- | ------------------------------------------------------------ | ---: | ---------- |
| `api-gateway`           | Spring Cloud Gateway for routing external requests           | 8080 | No         |
| `auth-service`          | JWT authentication and user management                       | 8081 | PostgreSQL |
| `drug-catalog-service`  | Drug catalogue, search and categories                        | 8082 | PostgreSQL |
| `inventory-service`     | Stock levels, replenishment and batch tracking               | 8083 | PostgreSQL |
| `manufacturing-service` | Production orders and batch manufacturing                    | 8084 | PostgreSQL |
| `supplier-service`      | Supplier management and purchase orders                      | 8085 | PostgreSQL |
| `notification-service`  | Email and SMS notification service using Node.js and Express | 8086 | No         |

---

## 2. Repository Structure

```text
backend/
├── api-gateway/
│   ├── src/
│   ├── pom.xml
│   └── Dockerfile
├── auth-service/
├── drug-catalog-service/
├── inventory-service/
├── manufacturing-service/
├── notification-service/
├── supplier-service/
└── .github/
    └── workflows/
        ├── _java-build.yml
        ├── _java-pr-check.yml
        ├── _node-build.yml
        ├── _node-pr-check.yml
        ├── ci-<service>.yml
        ├── ci-pr-<service>.yml
        └── promote-prod.yml
```

The Java services use Maven. The notification service uses Node.js 20 and Express.

---

## 3. CI/CD and DevSecOps Pipeline

The intended CI/CD workflow automates build, testing, security analysis, container image publishing and deployment promotion.

### Full pipeline

1. **Secret scanning** — Gitleaks.
2. **Build and testing** — Maven verification and JaCoCo coverage.
3. **Static analysis** — CodeQL.
4. **Security analysis** — Semgrep.
5. **Dependency scanning** — OWASP Dependency-Check.
6. **Container build** — Multi-stage Docker builds.
7. **Container security** — Trivy image scanning.
8. **Image publishing** — Amazon ECR.
9. **Image signing** — Cosign keyless signing.
10. **Development deployment update** — Update GitOps Helm values.
11. **QA promotion** — Create a promotion pull request.

Feature branch workflows are designed to run lightweight validation and security checks before changes
