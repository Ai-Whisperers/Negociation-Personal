# Work Hours Automated Reports - Comprehensive Analysis

## Overview

**Automation tool bridging Clockify and Azure DevOps**
- Repository: github.com/Ai-Whisperers/work-hours-automated-reports
- Last Updated: Oct 16, 2025
- Status: Production-ready
- Technology: Python 3.11+, FastAPI, Celery, Redis

---

## What We're Working On

The **Work-Hours-Automated-Reports** system is our internal automation tool that automatically generates comprehensive work hour reports by intelligently matching time entries from Clockify (time tracking) with work items from Azure DevOps (project management).

### Core Problem Solved
**Manual time tracking reconciliation is tedious and error-prone.**

This tool automates the entire process:
1. Fetches time entries from Clockify
2. Extracts work item IDs from descriptions
3. Fetches work items from Azure DevOps
4. Intelligently matches entries to work items
5. Generates professional reports in multiple formats

---

## Technology Stack

### Backend
- **Python 3.11+** - Modern Python features
- **FastAPI 0.109.0** - Async web framework
- **Celery 5.4.0** - Distributed task queue
- **Redis** - Cache and message broker
- **Typer 0.9.0** - CLI interface

### Data Processing
- **Polars 0.20.2** - Fast DataFrame library
- **Pandas 2.1.4** - Data manipulation
- **NumPy 1.26.3** - Numerical computing

### Report Generation
- **OpenPyXL 3.1.2** - Excel generation
- **XlsxWriter 3.1.9** - Excel formatting
- **Jinja2 3.1.3** - HTML templating
- **WeasyPrint 60.2** - PDF generation
- **Plotly 5.18.0** - Interactive charts

### API Clients
- **httpx 0.26.0** - Async HTTP client
- **Tenacity 8.2.3** - Retry logic
- **Requests 2.31.0** - GitHub API

---

## Main Features

### 1. Time Entry Fetching
- Connects to Clockify API
- Fetches entries by date range
- Supports filtering by user/project
- Async parallel fetching for all users
- Caching with 2-hour TTL

### 2. Work Item Extraction
Recognizes multiple patterns:
- `#12345` - Hash format (highest confidence)
- `ADO-12345` - ADO prefix
- `WI:12345` - Work item prefix
- `[12345]` - Bracket format
- `(12345)` - Parenthesis format
- Plain numbers - Validated (lowest confidence)

### 3. Intelligent Matching
Three strategies:
- **STRICT**: Only explicit patterns
- **FUZZY**: Include fuzzy text matching
- **HYBRID**: Strict first, then fuzzy (default)

Confidence scoring:
- Hash/ADO format: 95% confidence
- WI/Bracket format: 85% confidence
- Parenthesis: 75% confidence
- Plain numbers: 50% confidence

### 4. Report Generation
Multiple formats:
- **Excel**: Multi-sheet with summary, by person, by work item, raw data
- **HTML**: Dark-themed responsive design with charts
- **JSON**: Structured data export
- **PDF**: Print-friendly format

### 5. Activity Tracking
- Auto-starts Clockify timer on activity
- Monitors mouse/keyboard events
- Auto-stops after inactivity (configurable, default 5 min)
- Thread-safe operations

### 6. GitHub Integration
- Auto-creates entries for commits
- Intelligent session clustering
- Prevents duplicates
- Supports entire organizations

---

## Architecture

### Hexagonal Architecture (Ports & Adapters)

```
┌─────────────────────────────────────────┐
│         Presentation Layer              │
│  CLI (Typer) │ Web API (FastAPI)        │
└─────────────────┬───────────────────────┘
                  │
┌─────────────────▼───────────────────────┐
│         Application Layer               │
│  Use Cases │ Services │ DTOs            │
└─────────────────┬───────────────────────┘
                  │
┌─────────────────▼───────────────────────┐
│         Domain Layer                    │
│  Entities │ Value Objects │ Interfaces  │
└─────────────────┬───────────────────────┘
                  │
┌─────────────────▼───────────────────────┐
│         Infrastructure Layer            │
│  API Clients │ Repositories │ Adapters  │
└─────────────────────────────────────────┘
```

---

## Clockify Integration

### API Endpoints Used
```python
GET /workspaces/{workspaceId}/user          # Current user
GET /workspaces/{workspaceId}/users         # All users
GET /workspaces/{workspaceId}/projects      # Projects
GET /workspaces/{workspaceId}/time-entries  # Time entries
POST /workspaces/{workspaceId}/time-entries # Create entry
PATCH /workspaces/{workspaceId}/time-entries/{id} # Update
DELETE /workspaces/{workspaceId}/time-entries/{id} # Delete
```

### Authentication
- **Method**: X-Api-Key header
- **Required**: CLOCKIFY_API_KEY environment variable

### Features
- Async parallel fetching for multiple users
- Automatic retry with exponential backoff
- Request throttling (respects rate limits)
- 2-hour cache for time entries

---

## Azure DevOps Integration

### API Endpoints Used
```python
GET /_apis/wit/workitems/{id}               # Single work item
POST /_apis/wit/workitemsbatch              # Batch fetch (max 200)
POST /_apis/wit/wiql                        # Query work items
GET /_apis/work/teamsettings/iterations     # Iterations
POST /_apis/wit/workitems/${type}           # Create work item
```

### Authentication
- **Method**: Basic Auth with PAT (Personal Access Token)
- **Required**: ADO_PAT environment variable

### Features
- Batch processing (groups of 200 IDs)
- WIQL query support
- Iteration filtering
- Work item creation
- Automatic retry logic

---

## Matching Engine

### Matching Process
```
1. Parse time entry description
   ↓
2. Extract work item IDs using regex patterns
   ↓
3. Calculate confidence scores
   ↓
4. Fetch work items from Azure DevOps
   ↓
5. Apply fuzzy matching if needed
   ↓
6. Return MatchingResult with confidence
```

### Example Matching
```
Time Entry: "Fixed bug #12345 in authentication"
Extracted ID: 12345
Pattern: Hash (#)
Confidence: 95%
Work Item: Fetched from ADO
Match: SUCCESS
```

---

## Report Formats

### Excel Report Structure
```
Sheet 1: Summary
- Total hours
- Hours by person
- Hours by work item
- Match statistics

Sheet 2: By Person
- Person name
- Total hours
- Work items worked on
- Time breakdown

Sheet 3: By Work Item
- Work item ID
- Title
- Total hours
- Contributors
- Status

Sheet 4: Raw Data
- All time entries
- Matched work items
- Confidence scores
- Full details
```

### HTML Report Features
- Dark-themed responsive design
- Interactive Plotly charts
- Sortable tables
- Export buttons
- Print-friendly CSS

---

## Project Structure

```
work-hours-automated-reports/
├── src/
│   ├── domain/                 # Business logic
│   │   ├── entities/          # TimeEntry, WorkItem
│   │   ├── services/          # MatchingService
│   │   └── value_objects/     # Duration, DateRange
│   ├── application/            # Use cases
│   │   ├── use_cases/         # Main orchestration
│   │   ├── services/          # Application services
│   │   └── dto/               # Data transfer objects
│   ├── infrastructure/         # External adapters
│   │   ├── api_clients/       # Clockify, Azure DevOps
│   │   ├── repositories/      # Data access
│   │   ├── adapters/          # Report generators, cache
│   │   └── config/            # Settings
│   └── presentation/           # User interfaces
│       ├── cli/               # Command-line
│       └── api/               # Web API
├── .github/workflows/          # GitHub Actions
├── docker-compose.yml          # Multi-service deployment
└── README.md                   # Documentation
```

---

## Configuration

### Required Environment Variables
```bash
# Clockify
CLOCKIFY_API_KEY=your-api-key
CLOCKIFY_WORKSPACE_ID=workspace-id

# Azure DevOps
ADO_ORG=your-organization
ADO_PROJECT=your-project
ADO_PAT=your-personal-access-token

# Optional
CACHE_BACKEND=local|redis|memory
CACHE_TTL=3600
LOG_LEVEL=INFO
ENABLE_FUZZY_MATCHING=true
```

### Optional Settings
- Cache configuration (local/Redis)
- Logging levels
- Retry attempts
- Timeout settings
- Notification settings (SMTP)

---

## Usage

### CLI Commands
```bash
# Generate report for last 7 days
python main.py run

# Generate for specific date range
python main.py run --start 2024-01-01 --end 2024-01-31

# Validate credentials
python main.py validate

# Clear cache
python main.py cache clear

# View cache stats
python main.py cache stats
```

### Web API
```bash
# Start FastAPI server
uvicorn src.presentation.api.app:app

# Generate report via API
POST http://localhost:8000/reports/generate
{
  "start_date": "2024-01-01",
  "end_date": "2024-01-31",
  "format": "excel"
}

# Check status
GET http://localhost:8000/reports/{task_id}/status

# Download report
GET http://localhost:8000/reports/{task_id}/download
```

---

## Automation & Scheduling

### GitHub Actions Workflows

**1. Scheduled Report** (schedule.yml)
- Runs every Monday at 9 AM UTC
- Generates weekly reports
- Uploads as artifacts (30-day retention)
- Manual trigger with parameters

**2. Activity Tracker** (activity-tracker.yml)
- Monitors GitHub commits
- Auto-creates time entries
- Tracks work sessions

**3. Docker Compose Scheduler**
- Runs report every 24 hours
- Uses Redis for distributed caching
- Production-ready

---

## Deployment

### Docker
```bash
# Build and run all services
docker-compose up -d

# Services included:
# - Redis (cache/broker)
# - FastAPI API
# - Celery worker
# - Scheduler (cron jobs)
```

### Production Setup
1. Deploy Redis instance
2. Deploy FastAPI service
3. Deploy Celery workers
4. Configure environment variables
5. Set up scheduled jobs

---

## Performance Optimizations

### 1. Caching Strategy
- Time entries: 2-hour TTL
- Work items: 2-hour TTL
- User data: 24-hour TTL
- Backend: Local/Redis/Memory

### 2. Async Processing
- Parallel user fetching
- Batch work item requests
- Non-blocking I/O
- Celery distributed tasks

### 3. Batch Processing
- Azure DevOps: 200 items/request
- Clockify: All users in parallel
- Reduces API calls by 90%+

---

## Business Value

### What This Solves
1. **Manual Reconciliation** → Automated matching
2. **Time Waste** → 25-30s for 500 entries
3. **Errors** → 95%+ accuracy
4. **Reporting** → Professional multi-format reports
5. **Visibility** → Real-time activity tracking

### Use Cases
- Weekly team reports
- Project time allocation
- Client billing
- Resource planning
- Performance tracking

---

## Key Metrics

| Metric | Value |
|--------|-------|
| Processing Speed | ~3s for 100 entries |
| Accuracy | 95%+ matching |
| API Efficiency | 90% fewer calls (batching) |
| Cache Hit Rate | 70-80% |
| Supported Users | Unlimited |
| Report Formats | 4 (Excel, HTML, JSON, PDF) |

---

## Development Commands

```bash
# Setup
pip install -r requirements.txt

# Run CLI
python src/presentation/cli/main.py run

# Run API
uvicorn src.presentation.api.app:app --reload

# Run Celery worker
celery -A src.application.workers.celery_app worker

# Run tests
pytest tests/ -v --cov
```

---

## Current Status

### Production-Ready Features
- Complete Clockify integration
- Complete Azure DevOps integration
- Intelligent matching engine
- Multi-format report generation
- Activity tracking
- GitHub integration
- Caching system
- CLI and Web API
- Docker deployment

### Future Enhancements
- Jira integration
- Advanced analytics dashboard
- Machine learning matching
- Custom report templates
- Email notifications

---

## Our Internal Use

This tool is used internally at AI Whisperers to:
1. Track billable hours for clients
2. Generate weekly team reports
3. Monitor project progress
4. Allocate resources efficiently
5. Automate time tracking workflows

It saves us approximately **10 hours per week** in manual reconciliation and reporting, demonstrating the power of intelligent automation.
