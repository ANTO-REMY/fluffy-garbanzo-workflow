# Remy Care Connect — Security Workflow Hub

This repo is the single source of truth for **GitHub Actions security workflows** used across the Remy Care Connect project. It holds ready-to-use workflow templates, a vulnerability-testing plan, and setup notes for both repositories below.

| Repository | Stack | Link |
|---|---|---|
| `remy-care-connect` | TypeScript · React 18 · Vite · Shadcn/Radix | [ANTO-REMY/remy-care-connect](https://github.com/ANTO-REMY/remy-care-connect) |
| `remy-care-connect-backend` | Python 3.11 · Flask · PostgreSQL · JWT | [ANTO-REMY/remy-care-connect-backend](https://github.com/ANTO-REMY/remy-care-connect-backend) |

Yes — **this repo is meant to serve both** `remy-care-connect` (frontend) and `remy-care-connect-backend`. The `workflows/` directory contains a separate template for each:

- [`workflows/frontend-security.yml`](./workflows/frontend-security.yml) → copy into `remy-care-connect/.github/workflows/security.yml`
- [`workflows/backend-security.yml`](./workflows/backend-security.yml) → copy into `remy-care-connect-backend/.github/workflows/security.yml`

---

## What the workflows do

### Frontend (`remy-care-connect`)
- **npm audit** — flags high/critical CVEs in npm dependencies
- **CodeQL** — static analysis for JavaScript/TypeScript security vulnerabilities

### Backend (`remy-care-connect-backend`)
- **pip-audit** — checks Python dependencies against the PyPI advisory database
- **Bandit** — SAST for Flask-specific issues (hardcoded secrets, `DEBUG=True`, SQL injection hints)
- **CodeQL** — semantic analysis for Python
- **Trivy** — scans the Docker image for OS-level and pip CVEs

Both workflows run on every push to `main`, on pull requests targeting `main`, and on a weekly schedule (Mondays at 08:00 UTC) to catch new CVEs even when no code changes are made.

---

## Getting started

1. Copy the relevant workflow file into the target repo's `.github/workflows/` directory.
2. Commit to `main` or open a PR — the workflow will trigger automatically.
3. Check the **Security** tab of each repo for CodeQL and Trivy SARIF results.

For the full rollout plan and priority checklist, see [VULNERABILITY_TESTING_PLAN.md](./VULNERABILITY_TESTING_PLAN.md).

---

&copy; 2025 ANTO-REMY &bull; [MIT License](https://gh.io/mit)

