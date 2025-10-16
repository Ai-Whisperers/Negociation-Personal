# Customer AI Driven Feedback Analyzer - Architecture Documentation

**Version:** 3.2.0
**Last Updated:** October 2025
**Architecture Type:** Monorepo Multi-Service
**Deployment Platform:** Render.com

---

## Table of Contents

1. [System Overview](#system-overview)
2. [Architecture Principles](#architecture-principles)
3. [Technology Stack](#technology-stack)
4. [System Architecture](#system-architecture)
5. [Backend Architecture](#backend-architecture)
6. [Frontend Architecture](#frontend-architecture)
7. [Data Flow](#data-flow)
8. [Deployment Architecture](#deployment-architecture)
9. [Technical Constraints & Limits](#technical-constraints--limits)
10. [Security Architecture](#security-architecture)
11. [Performance Characteristics](#performance-characteristics)
12. [Scalability Analysis](#scalability-analysis)

---

## System Overview

The Customer AI Driven Feedback Analyzer is an AI-powered application that processes customer feedback comments to extract emotional insights, pain points, churn risk assessment, and NPS (Net Promoter Score) classification.

### Core Capabilities

- **Multi-format File Upload**: CSV, XLSX, XLS support
- **AI-Powered Analysis**: OpenAI GPT-4o-mini for text analysis
- **Emotion Detection**: 16 distinct emotion classifications with probability scores
- **Pain Point Extraction**: Automated identification and frequency analysis
- **Churn Risk Assessment**: 0-1 risk score calculation
- **NPS Classification**: Promoter/Passive/Detractor categorization
- **Bilingual Support**: Spanish and English comment processing
- **Interactive Visualization**: Plotly-based charts and dashboards
- **Export Functionality**: CSV and styled Excel exports

### Business Context

- **Target Users**: Customer experience teams, product managers, business analysts
- **Use Case**: Batch analysis of customer feedback surveys
- **Processing Scale**: 3,000-10,000 rows per upload
- **Response Time**: 5-100 seconds depending on dataset size
- **Data Retention**: 24-hour result TTL, 7-day comment cache

---

## Architecture Principles

### Design Philosophy

1. **Anti-Overengineering**: Simple, predictable, maintainable solutions
2. **Clean Architecture**: Clear separation of concerns, SOLID principles
3. **Modularity**: Small, focused components (files ≤250 lines, entry points ≤150 lines)
4. **No User Accounts**: Stateless processing, no authentication layer
5. **No CORS Issues**: BFF proxy pattern eliminates cross-origin complexity
6. **Performance First**: Lazy loading, code splitting, batch processing
7. **Zero Emoji Policy**: Enforced by pre-commit hooks and linting

### Code Quality Standards

- **Backend**: Black, Flake8, MyPy, pytest
- **Frontend**: ESLint, TypeScript strict mode, Vite
- **Documentation**: Spanish (public), English (code/internal)
- **Git Hooks**: Pre-commit validation for emoji policy and code quality

---

## Technology Stack

### Backend Stack

| Component | Technology | Version | Purpose |
|-----------|-----------|---------|---------|
| **API Framework** | FastAPI | Latest | REST API server |
| **Task Queue** | Celery | Latest | Async job processing |
| **Message Broker** | Redis | Latest | Task queue & caching |
| **AI Provider** | OpenAI API | GPT-4o-mini | Text analysis |
| **Data Processing** | Pandas | Latest | DataFrame operations |
| **Excel Export** | openpyxl | Latest | Styled Excel generation |
| **Validation** | Pydantic | v2 | Schema validation |
| **Logging** | structlog | Latest | Structured logging |

### Frontend Stack

| Component | Technology | Version | Purpose |
|-----------|-----------|---------|---------|
| **Framework** | React | 18+ | UI library |
| **Language** | TypeScript | Latest | Type safety |
| **Build Tool** | Vite | Latest | Fast builds & HMR |
| **Styling** | Tailwind CSS | Latest | Utility-first CSS |
| **Charts** | Plotly.js | Latest | Interactive visualizations |
| **State Management** | React Context | Built-in | Global state |
| **Routing** | React Router | Latest | Client-side routing |
| **BFF Server** | Express.js | Latest | Proxy & static serving |

### Development & Deployment

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Version Control** | Git + GitHub | Source control |
| **CI/CD** | Render Auto-deploy | Automated deployments |
| **Hosting** | Render.com | Cloud platform |
| **Container** | Docker (Render) | 512 MB containers |
| **Monitoring** | structlog + Render logs | Application monitoring |

---

## System Architecture

### High-Level Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                           USER BROWSER                           │
└────────────────────────────┬────────────────────────────────────┘
                             │
                             │ HTTPS
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│                    WEB SERVICE (Public)                          │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │              React SPA (Client-Side)                     │   │
│  │  - Lazy loaded pages & components                        │   │
│  │  - Plotly visualizations                                 │   │
│  │  - File upload UI                                        │   │
│  │  - Results display                                       │   │
│  └─────────────────────────────────────────────────────────┘   │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │         Node.js BFF Server (Express)                     │   │
│  │  - Static file serving                                   │   │
│  │  - API proxy (/api/* → Private API)                      │   │
│  │  - Health check endpoint                                 │   │
│  └─────────────────────────────────────────────────────────┘   │
│                          Render: 512 MB                          │
└────────────────────────────┬────────────────────────────────────┘
                             │
                             │ Internal HTTP (Private)
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│                   API SERVICE (Private)                          │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                  FastAPI Server                          │   │
│  │  Routes:                                                 │   │
│  │  - POST /upload      (file upload & validation)          │   │
│  │  - GET  /status/:id  (job status polling)                │   │
│  │  - GET  /results/:id (analysis results)                  │   │
│  │  - POST /export      (CSV/Excel export)                  │   │
│  │  - GET  /health      (health checks)                     │   │
│  │  - GET  /metrics     (performance metrics)               │   │
│  └─────────────────────────────────────────────────────────┘   │
│                          Render: 512 MB                          │
└────────────────┬───────────────────────────┬────────────────────┘
                 │                           │
                 │                           │ Redis Protocol
                 │                           ▼
                 │              ┌──────────────────────────┐
                 │              │   REDIS SERVICE          │
                 │              │  - Task queue (broker)   │
                 │              │  - Results backend       │
                 │              │  - Comment cache         │
                 │              │  - Rate limiting         │
                 │              │  - File storage (temp)   │
                 │              │    Render KV: Free Plan  │
                 │              └──────────────────────────┘
                 │                           ▲
                 │ Celery Task Queue         │
                 ▼                           │
┌─────────────────────────────────────────────────────────────────┐
│                  WORKER SERVICE (Private)                        │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │               Celery Worker Process                      │   │
│  │  Tasks:                                                  │   │
│  │  - analyze_feedback (main orchestrator)                  │   │
│  │  - analyze_batch    (batch processor)                    │   │
│  │  - cleanup_expired  (periodic cleanup)                   │   │
│  │                                                          │   │
│  │  Components:                                             │   │
│  │  - OpenAI API client (rate limited)                      │   │
│  │  - Batch processing engine                               │   │
│  │  - Memory monitor                                        │   │
│  │  - Cache manager                                         │   │
│  └─────────────────────────────────────────────────────────┘   │
│                          Render: 512 MB                          │
└────────────────────────────┬────────────────────────────────────┘
                             │
                             │ HTTPS API
                             ▼
                   ┌─────────────────────┐
                   │   OpenAI API        │
                   │   (GPT-4o-mini)     │
                   │   Rate: 8 RPS max   │
                   └─────────────────────┘
```

### Service Communication

**Public Traffic Flow:**
```
User → Web Service (BFF) → API Service → Worker Service → OpenAI API
                                ↓           ↓
                              Redis ←──────┘
```

**Internal Communication:**
- Web ↔ API: HTTP proxy (internal Render network)
- API ↔ Redis: Redis protocol
- Worker ↔ Redis: Redis protocol (broker + backend)
- Worker → OpenAI: HTTPS REST API

---

## Backend Architecture

### Layered Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    ENTRY POINT LAYER                         │
│  app/main.py (FastAPI app initialization)                   │
│  app/workers/celery_app.py (Celery initialization)          │
└────────────────────────────┬────────────────────────────────┘
                             │
┌────────────────────────────▼────────────────────────────────┐
│                      ROUTES LAYER                            │
│  app/routes/                                                 │
│  - upload.py      (file upload, validation, task queuing)   │
│  - status.py      (job status polling)                      │
│  - results.py     (analysis results retrieval)              │
│  - export.py      (CSV/Excel export)                        │
│  - health.py      (health checks)                           │
│  - metrics.py     (performance metrics)                     │
└────────────────────────────┬────────────────────────────────┘
                             │
┌────────────────────────────▼────────────────────────────────┐
│                     SERVICES LAYER                           │
│  app/services/                                               │
│  - analysis_service.py          (analysis orchestration)    │
│  - export_service.py            (export facade)             │
│  - export/excel_styled_exporter.py  (Excel formatting)      │
│  - export/csv_exporter.py       (CSV generation)            │
│  - efficient_deduplication.py   (duplicate detection)       │
└────────────────────────────┬────────────────────────────────┘
                             │
┌────────────────────────────▼────────────────────────────────┐
│                       CORE LAYER                             │
│  app/core/                                                   │
│  - unified_file_processor.py  (file parsing)                │
│  - unified_aggregation.py     (results aggregation)         │
│  - nps_calculator.py          (NPS logic)                   │
│  - cache_manager.py           (comment caching)             │
│  - excel_formatter.py         (Excel styling)               │
└────────────────────────────┬────────────────────────────────┘
                             │
┌────────────────────────────▼────────────────────────────────┐
│                    ADAPTERS LAYER                            │
│  app/adapters/                                               │
│  - openai/analyzer.py         (OpenAI integration)          │
│  - openai/client.py           (API client, rate limiting)   │
│  - openai/utils.py            (batch utils, tokenization)   │
│  - openai/parallel_processor.py  (concurrent processing)    │
│  - hybrid_analyzer.py         (fallback logic)              │
│  - local_sentiment.py         (local processing backup)     │
└────────────────────────────┬────────────────────────────────┘
                             │
┌────────────────────────────▼────────────────────────────────┐
│                 INFRASTRUCTURE LAYER                         │
│  app/infrastructure/                                         │
│  - cache.py  (Redis connection & operations)                │
└────────────────────────────┬────────────────────────────────┘
                             │
┌────────────────────────────▼────────────────────────────────┐
│                     WORKERS LAYER                            │
│  app/workers/                                                │
│  - celery_app.py  (Celery configuration)                    │
│  - tasks.py       (Celery task definitions)                 │
│      * analyze_feedback  (main task)                        │
│      * analyze_batch     (batch processing)                 │
│      * cleanup_expired   (periodic cleanup)                 │
└─────────────────────────────────────────────────────────────┘
```

### Backend Directory Structure

```
api/
├── app/
│   ├── main.py                      # FastAPI entry point (125 lines)
│   ├── config.py                    # Configuration management (126 lines)
│   │
│   ├── routes/                      # API endpoints
│   │   ├── upload.py                # File upload & task queuing (272 lines)
│   │   ├── status.py                # Job status polling
│   │   ├── results.py               # Results retrieval
│   │   ├── export.py                # Export handlers
│   │   ├── health.py                # Health checks
│   │   └── metrics.py               # Performance metrics
│   │
│   ├── services/                    # Business logic
│   │   ├── analysis_service.py      # Analysis orchestration
│   │   ├── export_service.py        # Export facade
│   │   ├── efficient_deduplication.py
│   │   └── export/
│   │       ├── base_exporter.py
│   │       ├── csv_exporter.py
│   │       ├── excel_basic_exporter.py
│   │       ├── excel_styled_exporter.py
│   │       ├── export_facade.py
│   │       ├── formatters/          # DataFrame & Excel styling
│   │       └── sheet_builders/      # Excel sheet construction
│   │
│   ├── core/                        # Core domain logic
│   │   ├── unified_file_processor.py    # CSV/Excel parsing
│   │   ├── unified_aggregation.py       # Results aggregation
│   │   ├── nps_calculator.py            # NPS classification
│   │   ├── cache_manager.py             # Comment caching (424 lines)
│   │   └── excel_formatter.py           # Excel styling
│   │
│   ├── adapters/                    # External integrations
│   │   ├── openai/
│   │   │   ├── analyzer.py              # AI analysis (449 lines)
│   │   │   ├── client.py                # Rate-limited client (116 lines)
│   │   │   ├── utils.py                 # Batch utilities (247 lines)
│   │   │   ├── async_analyzer.py        # Async processing
│   │   │   └── parallel_processor.py    # Concurrent batches
│   │   ├── hybrid_analyzer.py           # Fallback logic
│   │   └── local_sentiment.py           # Local processing
│   │
│   ├── infrastructure/              # Infrastructure concerns
│   │   └── cache.py                     # Redis client (171 lines)
│   │
│   ├── workers/                     # Celery workers
│   │   ├── celery_app.py                # Celery config (134 lines)
│   │   └── tasks.py                     # Task definitions (527 lines)
│   │
│   ├── schemas/                     # Pydantic models
│   │   ├── ai_schemas.py                # AI response schemas
│   │   ├── analysis.py                  # Analysis models
│   │   ├── base.py                      # Base schemas
│   │   ├── export.py                    # Export models
│   │   ├── processing.py                # Processing models
│   │   ├── status.py                    # Status models
│   │   └── upload.py                    # Upload models
│   │
│   └── utils/                       # Utilities
│       ├── logging.py                   # Structured logging
│       └── memory_monitor.py            # Memory management (123 lines)
│
├── requirements.txt                 # Python dependencies
└── .env.example                     # Environment template
```

### Key Backend Components

#### 1. File Upload & Validation (routes/upload.py)

**Responsibilities:**
- File format validation (CSV, XLSX, XLS)
- File size checks (20 MB limit)
- Column validation (required: Nota, Comentario Final; optional: NPS)
- Data quality checks (row count, text length)
- Task queuing to Celery
- Upload file caching in Redis (4-hour TTL)

**Flow:**
```
POST /upload
  ├── Validate file format & size
  ├── Parse CSV/Excel
  ├── Validate columns & data
  ├── Store file in Redis (base64)
  ├── Queue analyze_feedback task
  └── Return task_id
```

#### 2. Celery Worker (workers/tasks.py)

**Main Task: analyze_feedback**
- Retrieves file from Redis
- Splits data into batches (50 comments per batch)
- Monitors memory usage
- Dispatches analyze_batch subtasks
- Aggregates results
- Stores in Redis (24-hour TTL)

**Batch Task: analyze_batch**
- Rate-limited OpenAI API calls
- Comment deduplication via cache
- Emotion extraction (16 emotions)
- Pain point extraction
- Churn risk calculation
- NPS classification

**Cleanup Task: cleanup_expired**
- Runs hourly (cron schedule)
- Deletes expired results from Redis
- Cleans up old task metadata

#### 3. OpenAI Integration (adapters/openai/)

**Rate Limiting (client.py:20)**
- Global rate limiter: 8 RPS max
- Redis-based distributed limiting
- Exponential backoff on errors
- 3 retry attempts

**Analysis Logic (analyzer.py:71)**
- Model: GPT-4o-mini
- Temperature: 0.3 (low variability)
- Structured outputs (JSON schema)
- Token optimization (max 4096 per batch)
- Retry on: RateLimitError, APIConnectionError, APITimeoutError

**Batch Processing (utils.py:92)**
- Token-based batching (3000 tokens/batch)
- Dynamic batch sizing based on memory
- Comment truncation (1500 chars max)
- Optimal batch size: 50-100 comments

#### 4. Cache Management (core/cache_manager.py)

**Comment Caching:**
- 7-day TTL for analyzed comments
- Hash-based deduplication (MD5 + comment text)
- Batch get/set operations (Redis pipeline)
- Cache hit rate monitoring

**Benefits:**
- Reduces API costs (skip duplicate comments)
- Faster reprocessing of similar datasets
- Cross-upload deduplication

#### 5. Memory Monitoring (utils/memory_monitor.py)

**Thresholds (512 MB container):**
- Safe: < 300 MB (58%)
- Warning: 300-400 MB (58-78%)
- Critical: > 450 MB (90%)

**Adaptive Batch Sizing:**
- Critical: Reduce to 10 comments/batch
- Warning: Reduce to 30 comments/batch
- Safe: Use configured batch size (50)

---

## Frontend Architecture

### Component Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                         APP LAYER                            │
│  src/App.tsx                                                 │
│  - React Router with Suspense                                │
│  - Lazy-loaded pages                                         │
│  - Global error boundaries                                   │
└────────────────────────────┬────────────────────────────────┘
                             │
┌────────────────────────────▼────────────────────────────────┐
│                        PAGES LAYER                           │
│  src/pages/                                                  │
│  - HomePage.tsx        (lazy loaded)                        │
│  - AnalysisPage.tsx    (lazy loaded)                        │
│  - ResultsPage.tsx     (lazy loaded)                        │
│  - AboutPage.tsx       (lazy loaded)                        │
└────────────────────────────┬────────────────────────────────┘
                             │
┌────────────────────────────▼────────────────────────────────┐
│                    COMPONENTS LAYER                          │
│  src/components/                                             │
│  ├── upload/         (4 modular components, 100 lines total)│
│  │   ├── FileUploadArea.tsx      (drag & drop zone)        │
│  │   ├── FileInfo.tsx            (file details display)    │
│  │   ├── UploadProgress.tsx      (upload status)           │
│  │   └── ValidationErrors.tsx    (error messages)          │
│  │                                                          │
│  ├── results/        (7 modular components, 65 lines total)│
│  │   ├── EmotionsChart.tsx       (emotion visualization)   │
│  │   ├── NPSChart.tsx            (NPS distribution)        │
│  │   ├── ChurnRiskChart.tsx      (churn metrics)           │
│  │   ├── PainPointsChart.tsx     (pain points frequency)   │
│  │   ├── SummaryMetrics.tsx      (KPI cards)               │
│  │   ├── DataTable.tsx           (detailed results table)  │
│  │   └── ChartContainer.tsx      (shared chart wrapper)    │
│  │                                                          │
│  ├── progress/                                              │
│  │   ├── ProgressTracker.tsx     (job status polling)      │
│  │   └── ProgressBar.tsx         (visual progress)         │
│  │                                                          │
│  ├── export/                                                │
│  │   ├── ExportButton.tsx        (download trigger)        │
│  │   └── ExportOptions.tsx       (format selection)        │
│  │                                                          │
│  └── ui/             (Glass Design System components)      │
│      ├── Button.tsx                                         │
│      ├── Card.tsx                                           │
│      ├── Input.tsx                                          │
│      ├── Select.tsx                                         │
│      └── Spinner.tsx                                        │
└────────────────────────────┬────────────────────────────────┘
                             │
┌────────────────────────────▼────────────────────────────────┐
│                      CONTEXTS LAYER                          │
│  src/contexts/                                               │
│  - AnalysisContext.tsx   (global analysis state)            │
│  - ThemeContext.tsx      (dark/light mode)                  │
└────────────────────────────┬────────────────────────────────┘
                             │
┌────────────────────────────▼────────────────────────────────┐
│                        HOOKS LAYER                           │
│  src/hooks/                                                  │
│  - useFileUpload.ts      (upload logic)                     │
│  - usePolling.ts         (status polling)                   │
│  - useExport.ts          (export handling)                  │
└────────────────────────────┬────────────────────────────────┘
                             │
┌────────────────────────────▼────────────────────────────────┐
│                        UTILS LAYER                           │
│  src/utils/api/                                              │
│  - feedback-repository.ts  (API client)                     │
│  - http-client.ts          (axios wrapper)                  │
└─────────────────────────────────────────────────────────────┘
```

### Frontend Directory Structure

```
web/
├── bff/                             # Backend-for-Frontend
│   └── server.ts                    # Express proxy server (205 lines)
│
├── src/                             # React application
│   ├── App.tsx                      # Main app with routing
│   ├── main.tsx                     # Entry point
│   │
│   ├── pages/                       # Lazy-loaded pages
│   │   ├── HomePage.tsx
│   │   ├── AnalysisPage.tsx
│   │   ├── ResultsPage.tsx
│   │   └── AboutPage.tsx
│   │
│   ├── components/                  # UI components
│   │   ├── upload/                  # File upload (refactored v3.2)
│   │   │   ├── FileUploadArea.tsx
│   │   │   ├── FileInfo.tsx
│   │   │   ├── UploadProgress.tsx
│   │   │   └── ValidationErrors.tsx
│   │   │
│   │   ├── results/                 # Results display (refactored v3.2)
│   │   │   ├── EmotionsChart.tsx
│   │   │   ├── NPSChart.tsx
│   │   │   ├── ChurnRiskChart.tsx
│   │   │   ├── PainPointsChart.tsx
│   │   │   ├── SummaryMetrics.tsx
│   │   │   ├── DataTable.tsx
│   │   │   └── ChartContainer.tsx
│   │   │
│   │   ├── progress/                # Progress tracking
│   │   │   ├── ProgressTracker.tsx
│   │   │   └── ProgressBar.tsx
│   │   │
│   │   ├── export/                  # Export functionality
│   │   │   ├── ExportButton.tsx
│   │   │   └── ExportOptions.tsx
│   │   │
│   │   └── ui/                      # Design system components
│   │       ├── Button.tsx
│   │       ├── Card.tsx
│   │       ├── Input.tsx
│   │       ├── Select.tsx
│   │       └── Spinner.tsx
│   │
│   ├── contexts/                    # React contexts
│   │   ├── AnalysisContext.tsx
│   │   └── ThemeContext.tsx
│   │
│   ├── hooks/                       # Custom hooks
│   │   ├── useFileUpload.ts
│   │   ├── usePolling.ts
│   │   └── useExport.ts
│   │
│   ├── utils/                       # Utilities
│   │   └── api/
│   │       ├── feedback-repository.ts
│   │       └── http-client.ts
│   │
│   ├── types/                       # TypeScript types
│   │   ├── analysis.ts
│   │   └── api.ts
│   │
│   ├── i18n/                        # Internationalization
│   │   ├── translations/
│   │   ├── contexts/
│   │   └── hooks/
│   │
│   └── design/                      # Design tokens
│       ├── tokens/
│       └── css/
│
├── public/                          # Static assets
├── dist/                            # Build output
├── package.json                     # Dependencies
├── vite.config.ts                   # Vite configuration
├── tsconfig.json                    # TypeScript config
├── tailwind.config.js               # Tailwind config
├── build.sh                         # Production build script
└── start.sh                         # Production start script
```

### Key Frontend Features

#### 1. Code Splitting & Lazy Loading

**Bundle Optimization (v3.2.0):**
- Main bundle: 176 KB (reduced from 500+ KB)
- Pages loaded on-demand
- Plotly loaded asynchronously
- Build time: 25s (down from 45s)

**Implementation:**
```typescript
// src/App.tsx
const HomePage = lazy(() => import('./pages/HomePage'))
const AnalysisPage = lazy(() => import('./pages/AnalysisPage'))
const ResultsPage = lazy(() => import('./pages/ResultsPage'))
```

#### 2. BFF Proxy Pattern (bff/server.ts)

**Responsibilities:**
- Serve React static files
- Proxy API requests to private backend
- Handle CORS (not needed due to same-origin)
- Health check endpoint
- Cache control headers

**Routes:**
```
GET  /              → Serve React app
GET  /health        → Health check
POST /api/upload    → Proxy to backend:10000/upload
GET  /api/status/:id → Proxy to backend:10000/status/:id
GET  /api/results/:id → Proxy to backend:10000/results/:id
POST /api/export    → Proxy to backend:10000/export
```

#### 3. Glass Design System

**Characteristics:**
- Glassmorphism effects (backdrop blur)
- Consistent spacing & colors
- Accessible contrast ratios
- Responsive design
- Dark mode support

**Components:**
- Button: Primary, secondary, danger variants
- Card: Glassmorphic container
- Input: Form inputs with validation
- Select: Dropdown with styling
- Spinner: Loading indicators

#### 4. File Upload Component (refactored v3.2.0)

**Before:** Single 251-line component
**After:** 4 focused components, 100 lines total

**Modularity:**
- FileUploadArea: Drag & drop zone
- FileInfo: Display selected file details
- UploadProgress: Upload status tracking
- ValidationErrors: Error message display

#### 5. Results Charts Component (refactored v3.2.0)

**Before:** Single 380-line god component
**After:** 7 specialized components, 65 lines total

**Modularity:**
- EmotionsChart: 16 emotion bars
- NPSChart: Promoter/Passive/Detractor distribution
- ChurnRiskChart: Churn risk histogram
- PainPointsChart: Top pain points frequency
- SummaryMetrics: KPI cards (total comments, avg NPS, etc.)
- DataTable: Detailed row-by-row results
- ChartContainer: Shared wrapper with loading states

---

## Data Flow

### End-to-End Processing Flow

```
┌──────────────────────────────────────────────────────────────┐
│ PHASE 1: FILE UPLOAD                                         │
└──────────────────────────────────────────────────────────────┘

User selects file
    ↓
React FileUpload component validates client-side
    ↓
POST /api/upload (via BFF proxy)
    ↓
FastAPI upload.py validates file
    - Format: .csv, .xlsx, .xls
    - Size: ≤ 20 MB
    - Columns: Nota, Comentario Final (required), NPS (optional)
    - Rows: 1-10,000
    ↓
Store file in Redis (base64, 4-hour TTL)
    ↓
Queue analyze_feedback task to Celery
    ↓
Return task_id to frontend
    ↓
Frontend starts polling GET /api/status/:task_id

┌──────────────────────────────────────────────────────────────┐
│ PHASE 2: BACKGROUND PROCESSING (Celery Worker)               │
└──────────────────────────────────────────────────────────────┘

Celery worker picks up analyze_feedback task
    ↓
Retrieve file from Redis
    ↓
Parse CSV/Excel into DataFrame
    ↓
Split into batches (50 comments per batch)
    ↓
Check memory usage (adaptive batch sizing if needed)
    ↓
For each batch:
    ├── Check cache for duplicate comments (7-day cache)
    ├── Filter out cached comments
    ├── Rate-limit check (8 RPS max)
    ├── Call OpenAI API analyze_batch_of_comments()
    │   ├── Model: GPT-4o-mini
    │   ├── Temperature: 0.3
    │   ├── Structured output (JSON schema)
    │   └── Extract: emotions (16), pain_points, churn_risk, NPS
    ├── Store new results in cache (7-day TTL)
    ├── Update progress in Redis
    └── Aggregate batch results
    ↓
Combine all batch results
    ↓
Calculate aggregations:
    - Emotion frequencies & averages
    - Pain point frequencies
    - NPS distribution (promoter/passive/detractor)
    - Churn risk statistics
    ↓
Store final results in Redis (24-hour TTL)
    ↓
Update task status to "completed"

┌──────────────────────────────────────────────────────────────┐
│ PHASE 3: RESULTS RETRIEVAL                                   │
└──────────────────────────────────────────────────────────────┘

Frontend polling detects status = "completed"
    ↓
GET /api/results/:task_id
    ↓
FastAPI results.py retrieves from Redis
    ↓
Return JSON results to frontend
    ↓
Frontend renders:
    - EmotionsChart (16 emotion bars)
    - NPSChart (pie chart)
    - ChurnRiskChart (histogram)
    - PainPointsChart (top 10 bar chart)
    - SummaryMetrics (KPI cards)
    - DataTable (paginated detailed results)

┌──────────────────────────────────────────────────────────────┐
│ PHASE 4: EXPORT (Optional)                                   │
└──────────────────────────────────────────────────────────────┘

User clicks export button
    ↓
POST /api/export { task_id, format: "csv" | "xlsx" }
    ↓
FastAPI export.py retrieves results from Redis
    ↓
Generate export file:
    - CSV: Simple CSV with all columns
    - Excel: Styled workbook with multiple sheets
        * Summary sheet (KPIs, charts)
        * Emotions sheet (emotion details)
        * Pain Points sheet (frequency table)
        * Details sheet (row-by-row results)
    ↓
Return file as download
    ↓
Frontend triggers browser download
```

### Data Models

#### Input Data Model

```typescript
// Required columns in uploaded file
interface InputRow {
  Nota: number;                    // 0-10 score
  "Comentario Final": string;      // 3-2000 chars
  NPS?: number;                    // Optional, calculated from Nota if missing
}
```

#### AI Analysis Output

```python
# Structured output from OpenAI API (per comment)
{
  "emotions": [
    {"emotion": "satisfaccion", "score": 0.85},
    {"emotion": "frustracion", "score": 0.10},
    # ... 14 more emotions
  ],
  "pain_points": ["lentitud", "precio"],
  "churn_risk": 0.15,
  "nps_classification": "promoter"
}
```

#### Aggregated Results

```typescript
interface AnalysisResults {
  summary: {
    total_comments: number;
    average_nps: number;
    promoters: number;
    passives: number;
    detractors: number;
    average_churn_risk: number;
  };
  emotions: {
    [emotion: string]: {
      count: number;
      average_score: number;
      percentage: number;
    };
  };
  pain_points: {
    [pain_point: string]: number;  // frequency count
  };
  details: Array<{
    comment: string;
    nota: number;
    nps: string;
    churn_risk: number;
    emotions: Array<{emotion: string; score: number}>;
    pain_points: string[];
  }>;
}
```

---

## Deployment Architecture

### Render.com Services

**Service Configuration (render.yaml:5-155)**

#### 1. Redis Key-Value Store
- **Type:** Key-Value Store
- **Name:** feedback-analyzer-redis
- **Plan:** Free
- **Region:** Oregon
- **Memory Policy:** noeviction (preserve job queue)
- **Purpose:** Task broker, result backend, cache, rate limiting

#### 2. API Service (Private)
- **Type:** Private Service (pserv)
- **Name:** customer-feedback-api
- **Plan:** Starter (512 MB)
- **Region:** Oregon
- **Runtime:** Python 3.12.6
- **Build:** `pip install -r api/requirements.txt`
- **Start:** `uvicorn app.main:app --host 0.0.0.0 --port 10000`
- **Health Check:** /health/simple
- **Auto-deploy:** Enabled (on api/ changes)
- **Internal URL:** http://customer-feedback-api-bmjp:10000

#### 3. Celery Worker Service (Private)
- **Type:** Background Worker
- **Name:** celery-worker
- **Plan:** Starter (512 MB)
- **Region:** Oregon
- **Runtime:** Python 3.12.6
- **Build:** `pip install -r api/requirements.txt`
- **Start:** `celery -A app.workers.celery_app worker --loglevel=INFO`
- **Concurrency:** 2 workers
- **Max Tasks Per Child:** 100 (memory leak prevention)
- **Auto-deploy:** Enabled (on api/ changes)

#### 4. Web Service (Public)
- **Type:** Web Service
- **Name:** customer-feedback-app
- **Plan:** Starter (512 MB)
- **Region:** Oregon
- **Runtime:** Node.js 20.11.0
- **Build:** `cd web && rm -rf node_modules dist && ./build.sh`
- **Start:** `cd web && ./start.sh`
- **Health Check:** /health
- **Auto-deploy:** Enabled (on web/ changes)
- **Cache:** Disabled (no-cache profile for clean builds)

### Network Architecture

```
Internet (HTTPS)
    ↓
Render Edge (SSL termination)
    ↓
customer-feedback-app (Public Web Service)
    ├── Static: Serve React SPA
    └── /api/* → Proxy to customer-feedback-api-bmjp:10000 (Internal)
                      ↓
                customer-feedback-api (Private API Service)
                      ↓
                feedback-analyzer-redis (Redis KV Store)
                      ↑
                      ├── celery-worker (Private Worker Service)
                      └── OpenAI API (External HTTPS)
```

### Environment Variables

**Common Variables:**
```bash
# AI Configuration
OPENAI_API_KEY=<secret>
AI_MODEL=gpt-4o-mini
OPENAI_TIMEOUT_SECONDS=30

# Redis (auto-injected from KV service)
REDIS_URL=<auto>
CELERY_BROKER_URL=<auto>
CELERY_RESULT_BACKEND=<auto>

# Processing Limits
FILE_MAX_MB=20
MAX_ROWS=10000
MAX_BATCH_SIZE=50
MAX_RPS=8
RESULTS_TTL_SECONDS=86400

# Environment
APP_ENV=production
LOG_LEVEL=INFO
```

**Service-Specific:**

Web Service:
```bash
NODE_VERSION=20.11.0
NODE_ENV=production
API_PROXY_TARGET=http://customer-feedback-api-bmjp:10000
```

API Service:
```bash
PYTHON_VERSION=3.12.6
PORT=10000
API_WORKERS=1
```

Worker Service:
```bash
PYTHON_VERSION=3.12.6
CELERY_WORKER_CONCURRENCY=2
CELERY_MAX_TASKS_PER_CHILD=100
```

### Deployment Flow

```
Code Push to GitHub
    ↓
Render detects changes (via buildFilter)
    ↓
Trigger builds for affected services:
    - api/** changes → Rebuild API + Worker
    - web/** changes → Rebuild Web
    ↓
Build Phase:
    - Pull source code
    - Run buildCommand
    - Create deployment artifact
    ↓
Deploy Phase:
    - Health check old instance
    - Start new instance
    - Run health checks (healthCheckPath)
    - Zero-downtime swap
    ↓
Monitor Phase:
    - Render logs (stdout/stderr)
    - Health check monitoring
    - Auto-restart on failures
```

### Resource Allocation

| Service | CPU | Memory | Disk | Connections |
|---------|-----|--------|------|-------------|
| Web | Shared | 512 MB | 1 GB | HTTP pool |
| API | Shared | 512 MB | 1 GB | 1 Uvicorn worker |
| Worker | Shared | 512 MB | 1 GB | 2 Celery workers |
| Redis | Shared | 25 MB | N/A | 20 connections |

**Total Resources:**
- 3 containers × 512 MB = 1.5 GB RAM
- 1 Redis instance (25 MB free tier)
- Shared CPU across all services

---

## Technical Constraints & Limits

### Hard Limits (Configuration)

| Limit | Value | Location | Notes |
|-------|-------|----------|-------|
| **MAX_ROWS** | 10,000 | api/app/config.py:45 | Primary constraint |
| **FILE_MAX_MB** | 20 MB | api/app/config.py:44 | File upload limit |
| **MAX_BATCH_SIZE** | 50 | api/app/config.py:46 | Comments per batch |
| **MAX_RPS** | 8 | api/app/config.py:50 | OpenAI rate limit |
| **Task Timeout** | 600s | api/app/workers/celery_app.py:81 | 10-minute hard limit |
| **Task Soft Timeout** | 540s | api/app/workers/celery_app.py:82 | 9-minute warning |
| **RESULTS_TTL** | 86,400s | api/app/config.py:47 | 24-hour result retention |
| **CACHE_TTL** | 7 days | api/app/config.py:72 | Comment cache retention |
| **Upload Redis TTL** | 14,400s | api/app/routes/upload.py:119 | 4-hour file storage |

### Memory Constraints (512 MB Container)

| Threshold | Value | Percentage | Action |
|-----------|-------|------------|--------|
| **Safe** | < 300 MB | 58% | Normal operation |
| **Warning** | 300-400 MB | 58-78% | Reduce batch size to 30 |
| **Critical** | > 450 MB | 90% | Reduce batch size to 10 |

**Memory Monitoring:** api/app/utils/memory_monitor.py:19-21

### OpenAI API Constraints

| Parameter | Value | Location |
|-----------|-------|----------|
| **Model** | gpt-4o-mini | api/app/config.py:35 |
| **Temperature** | 0.3 | api/app/adapters/openai/analyzer.py:84 |
| **Max Tokens Input** | 4,096 | api/app/adapters/openai/analyzer.py:85 |
| **Max Tokens Output** | 4,096 | Schema definition |
| **Timeout** | 30s | api/app/config.py:36 |
| **Retry Attempts** | 3 | api/app/adapters/openai/analyzer.py:231 |
| **Backoff** | Exponential (1-8s) | api/app/adapters/openai/analyzer.py:232 |

### Batch Processing Constraints

| Parameter | Value | Location |
|-----------|-------|----------|
| **Optimal Batch Size** | 50-100 | api/app/adapters/openai/utils.py:69 |
| **Min Batch Size** | 10 | api/app/config.py:64 |
| **Max Tokens/Batch** | 3,000 | api/app/adapters/openai/utils.py:92 |
| **Reserved Tokens** | 2,000 | api/app/adapters/openai/utils.py:112 |
| **Comment Truncation** | 1,500 chars | api/app/adapters/openai/utils.py:122 |

### Celery Worker Constraints

| Parameter | Value | Location |
|-----------|-------|----------|
| **Concurrency** | 2-4 workers | render.yaml:118, config.py:84 |
| **Prefetch Multiplier** | 1 | api/app/workers/celery_app.py:70 |
| **Max Tasks/Child** | 100 | api/app/workers/celery_app.py:71 |
| **Visibility Timeout** | 3,600s | api/app/workers/celery_app.py:95 |

### Frontend Constraints

| Parameter | Value | Notes |
|-----------|-------|-------|
| **Upload Timeout** | 5s | Initial upload request |
| **Polling Interval** | 1-2s | Status check frequency |
| **Max Poll Duration** | 600s | Matches backend timeout |
| **Bundle Size** | 176 KB | Main chunk (v3.2.0) |

---

## Security Architecture

### Network Security

**Service Isolation:**
- Web Service: Public HTTPS access
- API Service: Private (internal Render network only)
- Worker Service: Private (no external access)
- Redis: Private (internal access only)

**Communication:**
- Client ↔ Web: HTTPS (TLS 1.2+)
- Web ↔ API: Internal HTTP (Render private network)
- API/Worker ↔ Redis: Redis protocol (internal)
- Worker → OpenAI: HTTPS (TLS 1.2+)

### API Security

**No CORS:** BFF proxy pattern eliminates CORS complexity

**Trusted Host Middleware:**
```python
# api/app/main.py:42-46
allowed_hosts = [
  "*.onrender.com",
  "localhost",
  "customer-feedback-api-bmjp"
]
```

**Input Validation:**
- Pydantic schema validation (all endpoints)
- File format whitelist (.csv, .xlsx, .xls)
- File size limits (20 MB)
- Row count limits (10,000 max)
- Text length limits (3-2000 chars)
- Column validation (required fields)

**Rate Limiting:**
- Global 8 RPS to OpenAI (distributed via Redis)
- Local fallback rate limiter
- Per-batch throttling

### Data Security

**No Persistent Storage:**
- No database (stateless architecture)
- Files stored in Redis (4-hour TTL)
- Results stored in Redis (24-hour TTL)
- No user authentication (no account data)

**Secrets Management:**
- Environment variables (not committed)
- Render secret management
- SECRET_KEY auto-generated
- OPENAI_API_KEY manually configured

**Data Retention:**
- Upload files: 4 hours
- Analysis results: 24 hours
- Comment cache: 7 days
- All data auto-expires (no manual cleanup needed)

### Code Security

**Pre-commit Hooks:**
- Emoji checker (CRITICAL: zero tolerance)
- Black formatting
- Flake8 linting
- MyPy type checking

**Dependencies:**
- Regular updates via dependabot
- Security scans (GitHub)
- Pin Python version (3.12.6)
- Pin Node version (20.11.0)

---

## Performance Characteristics

### Processing Performance

**Documented Performance (CLAUDE.md:108-111):**

| Rows | Time | Throughput | Status |
|------|------|------------|--------|
| 850-1,200 | 5-10s | 100-240 rows/s | Optimal |
| 1,800 | 18s | 100 rows/s | Good |
| 3,000 | 30s | 100 rows/s | Acceptable |
| 10,000 | ~100s | 100 rows/s | Max config |

**Performance Formula:**
```
Time (seconds) ≈ rows / 100
```

**Rate-Limiting Impact:**
```
Batches = rows / 50 (batch size)
Min Time = Batches / 8 (RPS) = rows / 400

Example: 10,000 rows
  Batches = 10,000 / 50 = 200 batches
  Min Time = 200 / 8 = 25 seconds
  Actual Time ≈ 100s (includes API latency, processing overhead)
```

### Frontend Performance

**Bundle Sizes (v3.2.0):**
- Main chunk: 176 KB (gzipped: ~60 KB)
- Plotly (lazy): ~3 MB (loaded on-demand)
- Page chunks: 10-30 KB each

**Load Times:**
- Initial load: < 2s (without Plotly)
- Page navigation: < 100ms (cached)
- Chart render: 1-3s (first time, Plotly load)

**Build Performance:**
- Build time: 25s (down from 45s)
- HMR: < 200ms (dev mode)

### Backend Performance

**API Latency:**
- Health check: < 50ms
- Upload validation: 100-500ms (depends on file size)
- Status check: < 100ms (Redis lookup)
- Results retrieval: 200-1000ms (Redis + serialization)
- Export generation: 1-5s (Excel formatting)

**Celery Task Latency:**
- Task queue delay: < 100ms
- Batch processing: ~1.25s per batch (50 comments)
  - OpenAI API call: ~800ms
  - Cache lookup: ~50ms
  - Processing overhead: ~400ms

### Redis Performance

**Operation Latency:**
- GET: < 5ms
- SET: < 10ms
- MGET (batch): < 20ms
- Pipeline operations: < 30ms

**Memory Usage:**
- 10,000 rows × 40 KB/row ≈ 400 MB
- Well within 512 MB container limit
- Redis: ~10-20 MB (free tier 25 MB limit)

---

## Scalability Analysis

### Current Bottlenecks (Ranked)

**1. Configuration Limit (Primary)**
- MAX_ROWS = 10,000 (api/app/config.py:45)
- Can be increased to 100,000 theoretically
- Memory becomes limiting factor beyond 15,000-20,000 rows

**2. Memory (512 MB Container)**
- Critical at 450 MB (90% of container)
- ~10,000-15,000 rows sustainable
- Dynamic batch sizing mitigates risk

**3. OpenAI Rate Limits**
- 8 RPS allows 240,000 rows in 10 minutes
- NOT a bottleneck for current limits
- Could process 48,000 rows in timeout window

**4. Task Timeout**
- 600s hard limit
- Allows ~48,000 rows at 100 rows/s
- NOT a bottleneck for current limits

### Scaling Strategies

#### Vertical Scaling (Render Plan Upgrade)

**Upgrade to 1 GB containers:**
- MAX_ROWS: 10,000 → 25,000
- Memory headroom: 512 MB → 1 GB
- Cost: +$7/month per service ($21 total)

**Upgrade to 2 GB containers:**
- MAX_ROWS: 25,000 → 50,000
- Memory headroom: 1 GB → 2 GB
- Cost: +$25/month per service ($75 total)

#### Horizontal Scaling (Multi-Worker)

**Add worker instances:**
- Current: 1 worker with 2 Celery processes
- Scale to: 3 workers with 2 processes each = 6 total
- Throughput: 100 rows/s → 300 rows/s (theoretical)
- Limitation: OpenAI rate limit (8 RPS shared across workers)

**Add Redis instances:**
- Current: 25 MB free tier
- Upgrade: 256 MB paid tier ($10/month)
- Benefit: More cache space, higher connection limit

#### Hybrid Scaling (Local Worker)

**Run worker locally:**
```bash
# Local machine with unlimited memory
celery -A app.workers.celery_app worker --loglevel=INFO
```

**Benefits:**
- Unlimited memory (process 100,000+ rows)
- Faster CPU (local hardware)
- No container limits
- Same Redis/API (cloud)

**Limitations:**
- Still limited by OpenAI rate limit (8 RPS)
- Network latency (local ↔ cloud Redis)
- Manual orchestration (not auto-scaling)

#### Architectural Changes (Future)

**For 50,000+ rows:**
1. **Database**: PostgreSQL for persistent storage
2. **Streaming**: Process results incrementally (don't load all in memory)
3. **Pagination**: Return results in chunks (reduce memory footprint)
4. **File Storage**: S3/blob storage for uploads (not Redis)
5. **Email Notifications**: Async processing with email on completion
6. **Result Expiry**: Shorter TTL or on-demand cleanup

**For 100,000+ rows:**
1. **Distributed Workers**: Kubernetes/ECS with auto-scaling
2. **Sharding**: Split large jobs into independent sub-jobs
3. **Queue Prioritization**: Separate queues for large/small jobs
4. **OpenAI Batching API**: Use batch API for higher throughput
5. **Alternative AI**: Fine-tuned local models (reduce API costs)

### Cost Analysis

**Current Monthly Cost (Starter Plan):**
- Web Service: $7/month
- API Service: $7/month
- Worker Service: $7/month
- Redis: Free (25 MB)
- **Total: $21/month**

**OpenAI API Costs (gpt-4o-mini):**
- Input: $0.15 / 1M tokens
- Output: $0.60 / 1M tokens
- Estimated: $0.01-0.05 per 1,000 comments
- 10,000 comments: ~$0.10-0.50
- 100,000 comments/month: ~$1-5/month

**Scaling Costs:**

| Configuration | Render | OpenAI (est) | Total |
|---------------|--------|--------------|-------|
| **Current (10K rows)** | $21 | $1 | $22/month |
| **1 GB containers (25K)** | $42 | $2 | $44/month |
| **2 GB containers (50K)** | $96 | $5 | $101/month |
| **3 workers (scale out)** | $35 | $5 | $40/month |

---

## Appendix: File References

### Key Configuration Files

| File | Lines | Purpose |
|------|-------|---------|
| api/app/config.py | 126 | Centralized configuration |
| api/app/workers/celery_app.py | 134 | Celery initialization |
| web/bff/server.ts | 205 | BFF proxy server |
| render.yaml | 155 | Render deployment config |
| .env.example | 65 | Environment template |

### Critical Business Logic Files

| File | Lines | Purpose |
|------|-------|---------|
| api/app/workers/tasks.py | 527 | Celery task definitions |
| api/app/adapters/openai/analyzer.py | 449 | OpenAI integration |
| api/app/core/cache_manager.py | 424 | Comment caching |
| api/app/routes/upload.py | 272 | File upload & validation |
| api/app/adapters/openai/utils.py | 247 | Batch processing utilities |
| api/app/infrastructure/cache.py | 171 | Redis client |
| api/app/utils/memory_monitor.py | 123 | Memory management |
| api/app/adapters/openai/client.py | 116 | Rate-limited API client |

### Frontend Key Files

| File | Purpose |
|------|---------|
| web/src/App.tsx | Router with lazy loading |
| web/src/components/upload/ | File upload (4 components) |
| web/src/components/results/ | Results display (7 components) |
| web/src/utils/api/feedback-repository.ts | API client |
| web/bff/server.ts | Express BFF proxy |

---

## Conclusion

The Customer AI Driven Feedback Analyzer is a well-architected, modular application following clean architecture principles. The system is designed for:

- **Simplicity**: No overengineering, predictable flow
- **Performance**: 100 rows/s throughput, optimized bundles
- **Scalability**: Vertical and horizontal scaling options
- **Maintainability**: Small files, clear separation of concerns
- **Cost-Efficiency**: $22/month for 10,000 rows/month processing

**Current Capacity:** 10,000 rows (configurable up to 100,000)
**Practical Limit:** 15,000-20,000 rows (512 MB memory constraint)
**Recommended Scale:** 3,000-5,000 rows for optimal UX

For higher scale, vertical scaling (1-2 GB containers) or hybrid scaling (local workers) are the most cost-effective strategies.
