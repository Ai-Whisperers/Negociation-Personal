# Company Information (Org OS) - Comprehensive Analysis

## Overview

**Centralized infrastructure hub for AI Whisperers organization**
- Repository: github.com/Ai-Whisperers/Company-Information
- Last Updated: Oct 16, 2025
- Status: MVP (Pre-release)
- Technology: PowerShell, NestJS, Express, Prisma

---

## What We're Working On

The **Company-Information** repository (internally called "Org OS") is our **organizational operating system** - a centralized control plane that manages, monitors, and orchestrates our entire infrastructure across all repositories.

Think of it as the "mission control" for AI Whisperers.

### Core Purpose
A modern web-based dashboard that provides:
1. **Real-time visibility** into all repository health
2. **Automated synchronization** across projects
3. **GitHub ↔ Azure DevOps integration**
4. **Organization-wide health monitoring**
5. **Centralized automation workflows**

---

## Technology Stack

### Frontend (Dashboard)
- **Express.js** - Web server (Port 3001)
- **Vanilla JavaScript** - No build step required
- **WebSocket** - Real-time updates
- **HTML/CSS** - Glass-morphism UI

### Backend (Jobs Service)
- **NestJS** - TypeScript framework (Port 4000)
- **Prisma** - Type-safe ORM
- **SQLite** - Development database
- **PostgreSQL** - Production database
- **Redis** - Job queue (optional)
- **Bull** - Background job processing

### Automation
- **PowerShell 7+** - Cross-platform scripting
- **GitHub Actions** - CI/CD pipelines
- **Octokit** - GitHub API client
- **Azure DevOps SDK** - ADO integration

---

## Main Components

### 1. Web Dashboard (Port 3001)
Real-time control panel showing:
- **Repository health scores** (0-100)
- **Project status** for all repos
- **Activity feed** with recent commits
- **TODO tracking** and management
- **Health metrics** and trends
- **Download capabilities** for reports

Features:
- WebSocket live updates
- No build step (vanilla JS)
- Responsive design
- Export functionality (HTML, JSON, Markdown)

### 2. NestJS Jobs Service (Port 4000)
Backend API handling:
- **Integrations**: GitHub, Azure DevOps, Slack
- **Scanners**: Repository health checks
- **Sync**: Bidirectional GitHub ↔ ADO
- **Reporters**: Weekly org pulse reports
- **Reports API**: Historical report access

### 3. PowerShell Automation Framework
Cross-platform scripts for:
- Azure DevOps synchronization
- GitHub monitoring
- File synchronization across repos
- TODO management
- Testing automation
- Release coordination
- Weekly activity reports

### 4. GitHub Actions Workflows
Automated CI/CD pipelines:
- **Scheduled tasks** (weekly reports, daily scans)
- **Azure DevOps sync** on documentation changes
- **File synchronization** across repositories
- **Documentation gate** for PRs
- **Test suite** execution
- **Repository status** tracking

---

## Key Features

### 1. Repository Health Monitoring
Tracks health metrics:
- Branch protection status
- Required documentation presence
- Recent activity levels
- Test coverage
- Security vulnerabilities
- Dependency updates

**Health Score Calculation:**
```
Score = (
  Branch Protection × 20 +
  Documentation × 25 +
  Activity × 15 +
  Tests × 20 +
  Security × 20
) / 100
```

### 2. Bidirectional GitHub ↔ Azure DevOps Sync
- **Work item linking** to PRs and commits
- **Drift detection** (<10 minute SLO)
- **Automatic repair** capabilities
- **Audit logging** for all changes
- **Repository mirroring** option

### 3. File Synchronization
Syncs files across 7+ repositories:
- Configuration files
- Documentation templates
- CI/CD workflows
- Shared scripts
- Policy documents

**Sync Modes:**
- Replace (overwrite)
- Merge-append (add to end)
- Merge-prepend (add to beginning)

### 4. TODO Management
Centralized TODO tracking:
- Scan all repositories for TODO comments
- Aggregate into central database
- Track completion status
- Generate TODO reports
- Download capabilities

### 5. Weekly Org Pulse Reports
Automated weekly reports containing:
- Organization-wide activity summary
- Repository health trends
- Contributor insights
- Completion metrics
- Recommendations

---

## Database Schema (Prisma)

### Core Models (19 tables total)

**1. Repository**
- Stores repo metadata
- Health scores
- Protection status
- Last scan timestamp

**2. WorkItem**
- Azure DevOps work items
- Status tracking
- Assignment info

**3. WorkItemLink**
- Bidirectional PR/commit ↔ work item
- Relationship tracking
- Drift detection

**4. HealthCheck**
- Historical health metrics
- Trend analysis
- Alert thresholds

**5. Report**
- Generated reports
- Weekly org pulse
- Custom reports

**6. SyncLog**
- Synchronization audit trail
- Success/failure tracking
- Error logging

**7. User**
- Team member authentication
- Roles: VIEWER, EDITOR, ADMIN
- GitHub/ADO mapping

**8. Policy**
- Compliance rules
- Governance policies
- Enforcement settings

**9. PolicyResult**
- Policy violation tracking
- Remediation status

---

## PowerShell Scripts

### Common Utilities
**PathResolver.ps1** - Cross-platform path resolution
- `Get-ProjectRoot` - Auto-detect project root
- `Get-ProjectPath` - Resolve relative paths
- `Ensure-DirectoryExists` - Create directories
- Eliminates hardcoded paths

### Azure DevOps Integration
**azure-devops-sync.ps1**
- Actions: status, configure, test, sync
- Tests Azure CLI and DevOps extension
- Validates organization/project access

### GitHub Monitoring
- **github-commit-tracker.ps1** - Daily commit summary
- **new-repo-monitor.ps1** - New repository alerts
- **simple-commit-tracker.ps1** - Lightweight tracking

### File Synchronization
- **file-sync.ps1** - Core synchronization
- **file-sync-manager.ps1** - Configuration management
- **file-sync-advanced.ps1** - Advanced operations

### Monitoring
**dashboard.ps1** - Interactive management
- Modes: interactive, summary, export
- Formats: HTML, JSON, Markdown
- Real-time monitoring
- Recommendation engine

### TODO Management
- **manage-todos.ps1** - TODO lifecycle
- **todo-manager.ps1** - Centralized management
- **excalibur-command.ps1** - Advanced operations

### Testing
- **test-runner.ps1** - Test execution
- **real-data-test-runner.ps1** - Production-like testing

---

## GitHub Actions Workflows

### 1. Schedule.yml (Org OS Scheduled Tasks)
```yaml
Triggers:
- Weekly Org Pulse: Mondays 9 AM UTC
- Daily Health Scan: 2 AM UTC
- ADO Sync: Every 6 hours
- Manual trigger with task selection
```

### 2. Azure DevOps Sync
```yaml
Triggers:
- Documentation changes
- Work item references in commits
- Manual trigger

Actions:
- Mirror repositories to ADO
- Sync work items bidirectionally
- Extract work item IDs (AB# format)
```

### 3. File Sync
```yaml
Triggers:
- Changes to sync configuration
- Changed files detection
- Manual trigger

Actions:
- Validate sync config
- Detect changed files
- Matrix parallel sync (max 3)
- Dry-run capability
- Auto-create issues on failure
```

### 4. Documentation Gate
```yaml
Triggers:
- Pull requests

Actions:
- Validate required files (README, LICENSE, etc.)
- Check optional files
- Validate README structure
- Auto-comment with remediation steps
- Generate documentation report
```

### 5. Test Suite
```yaml
Triggers:
- Push to main
- Pull requests

Actions:
- Unit tests
- Integration tests
- E2E tests (Playwright)
- Coverage reporting
```

---

## Project Structure

```
Company-Information/
├── apps/
│   └── dashboard/              # Express dashboard (3001)
│       ├── dashboard.js
│       ├── api-server.js
│       └── package.json
├── services/
│   └── jobs/                   # NestJS service (4000)
│       ├── src/
│       │   ├── integrations/   # GitHub, ADO, Slack
│       │   ├── scanners/       # Health scanning
│       │   ├── sync/           # ADO-GitHub sync
│       │   ├── reporters/      # Report generation
│       │   └── db/             # Prisma ORM
│       ├── prisma/
│       │   └── schema.prisma
│       └── package.json
├── scripts/                    # PowerShell automation
│   ├── common/
│   ├── azure-devops/
│   ├── github/
│   ├── file-sync/
│   ├── monitoring/
│   ├── testing/
│   └── todos/
├── .github/workflows/          # CI/CD pipelines
├── docs/                       # Documentation
├── data/                       # Data storage
└── templates/                  # Templates
```

---

## Configuration

### Environment Variables
```bash
# GitHub
GITHUB_TOKEN=ghp_...
GITHUB_ORG=Ai-Whisperers

# Azure DevOps
AZURE_DEVOPS_PAT=...
AZURE_DEVOPS_ORG=ai-whisperers
AZURE_DEVOPS_PROJECT=Company-Information

# Database
DATABASE_URL=postgresql://...
# or
DATABASE_URL=file:./dev.db

# Redis (optional)
REDIS_HOST=localhost
REDIS_PORT=6379

# Service Ports
DASHBOARD_PORT=3001
JOBS_PORT=4000

# Feature Flags
ENABLE_ADO_SYNC=true
ENABLE_SLACK=true
ENABLE_AUTO_REPAIR=true
```

---

## Deployment

### Local Development
```bash
# Install dependencies
npm install

# Setup database
npx prisma migrate dev

# Start dashboard
cd apps/dashboard
npm start

# Start jobs service
cd services/jobs
npm run start:dev
```

### Production (Docker)
```bash
# Build and run
docker-compose up -d

# Services:
# - PostgreSQL database
# - Redis cache
# - Jobs service (NestJS)
# - Dashboard (Express)
```

---

## Usage

### Dashboard Access
```
http://localhost:3001
```
Features:
- View all repository health
- Track TODOs
- Monitor activity
- Download reports
- Configure settings

### API Access
```
http://localhost:4000/api
```
Endpoints:
- `GET /health` - Service health
- `GET /repositories` - All repositories
- `GET /reports` - Generated reports
- `POST /sync/trigger` - Trigger sync
- `GET /todos` - All TODOs

### PowerShell Commands
```powershell
# Run health check
./scripts/monitoring/dashboard.ps1 -Mode summary

# Sync files
./scripts/file-sync/file-sync.ps1 -Action sync

# Generate report
./scripts/monitoring/weekly-activity-report.ps1

# Manage TODOs
./scripts/todos/manage-todos.ps1 -Action scan
```

---

## Infrastructure Managed

### Repositories Monitored
All 17 AI-Whisperers repositories:
- ai-whisperers-portfolio-website
- WPG-Amenities
- AI-Whisperers-Website
- work-hours-automated-reports
- Company-Information (self)
- customer-feedback-app
- AI-Whisperers-website-and-courses
- Plus 10 private repositories

### Centralized Governance
- **Documentation standards** enforcement
- **Branch protection** validation
- **Security policies** monitoring
- **Code quality** standards
- **CI/CD pipeline** templates

---

## Key Metrics

| Metric | Value |
|--------|-------|
| Repositories Managed | 17 |
| Active Workflows | 6+ |
| PowerShell Scripts | 20+ |
| Database Tables | 19 |
| Services Running | 2 (Dashboard + Jobs) |
| Automation Coverage | 80%+ |

---

## Current Status

### Operational (MVP)
- Dashboard running
- GitHub integration working
- PowerShell framework solid
- CI/CD workflows active
- File sync operational

### In Development
- Azure DevOps sync (framework ready)
- Advanced reporting
- Policy enforcement engine
- Alerting system

---

## Business Value

### What This Solves
1. **Visibility Gap** → Real-time org dashboard
2. **Manual Sync** → Automated file/work item sync
3. **Scattered Info** → Centralized control plane
4. **Compliance** → Automated policy enforcement
5. **Operational Overhead** → Reduced by 60%+

### Time Savings
- **Weekly reports**: Automated (saved 4 hours/week)
- **File sync**: Automated (saved 2 hours/week)
- **Health monitoring**: Real-time (saved 3 hours/week)
- **TODO tracking**: Centralized (saved 1 hour/week)

**Total**: ~10 hours/week saved

---

## Future Roadmap

1. **Complete ADO sync** implementation
2. **Advanced analytics** dashboard
3. **AI-powered** health recommendations
4. **Mobile app** for monitoring
5. **Slack bot** integration
6. **Automated remediation** for issues

---

## Development Commands

```bash
# Dashboard
cd apps/dashboard
npm start

# Jobs service
cd services/jobs
npm run start:dev

# Database
npx prisma studio       # Visual editor
npx prisma migrate dev  # Run migrations

# Tests
npm test
npm run test:e2e
```

---

This repository represents the **operational backbone** of AI Whisperers, providing centralized visibility, automation, and governance across our entire infrastructure. It's our "one pane of glass" for managing the organization.
