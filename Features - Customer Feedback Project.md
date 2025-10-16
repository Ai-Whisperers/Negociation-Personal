# Customer AI Driven Feedback Analyzer - Comprehensive Project Analysis

## Executive Summary

The Customer AI Driven Feedback Analyzer is a sophisticated, production-ready SaaS application that leverages artificial intelligence to analyze customer feedback at scale. The system processes customer comments in Spanish and English, extracting actionable insights including emotions, pain points, churn risk scores, and NPS classifications.

**Key Metrics:**
- **Version:** 3.2.0
- **Status:** Production-Ready
- **Cost Optimization:** 87% reduction in AI processing costs
- **Performance:** Processes 1000 comments in ~10 seconds
- **Scalability:** Handles up to 3000 comments per file
- **Architecture:** Microservices-based monorepo

---

## 1. Project Overview

### 1.1 Purpose and Value Proposition

The application transforms raw customer feedback into structured, actionable business intelligence by:

- **Emotion Analysis:** Detects 7 core emotions (satisfaction, frustration, anger, trust, disappointment, confusion, anticipation)
- **Pain Point Extraction:** Identifies and categorizes customer problems
- **Churn Risk Assessment:** Calculates probability of customer attrition (0-1 scale)
- **NPS Classification:** Categorizes customers as Promoters, Passives, or Detractors
- **Sentiment Scoring:** Provides overall sentiment (-1 to 1)
- **Data Visualization:** Interactive charts and exportable reports

### 1.2 Target Users

- **Customer Service Teams:** Identify at-risk customers requiring immediate attention
- **Product Managers:** Discover pain points and feature improvement opportunities
- **Marketing Teams:** Find promoters for referral programs and understand brand sentiment
- **Business Analysts:** Access structured data for strategic decision-making

### 1.3 Business Impact

- **Time Savings:** Automated analysis replaces hours of manual review
- **Cost Efficiency:** 87% lower processing costs vs. traditional AI solutions
- **Actionable Insights:** Prioritized action items based on churn risk
- **Scalability:** Handles enterprise-level feedback volumes

---

## 2. Architecture Overview

### 2.1 High-Level Architecture

The system follows a modern microservices architecture with clear separation of concerns:

```
┌─────────────────────────────────────────────────────────────┐
│                         USER LAYER                           │
│  (Browser - React SPA with Glass Design System)             │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                    BFF PROXY LAYER                           │
│  (Node.js/Express - Port 3000)                              │
│  • Static file serving (production)                          │
│  • API request proxying (avoids CORS)                        │
│  • Request/response logging                                  │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                    API LAYER (Private)                       │
│  (FastAPI - Python - Port 8000)                             │
│  • File upload validation                                    │
│  • Task orchestration                                        │
│  • Results retrieval                                         │
│  • Export generation                                         │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                   WORKER LAYER                               │
│  (Celery - Python - 2-4 concurrent workers)                 │
│  • Batch processing orchestration                            │
│  • Hybrid analysis (Local + OpenAI)                          │
│  • Progress tracking                                         │
│  • Error handling & retries                                  │
└────────────────────────┬────────────────────────────────────┘
                         │
          ┌──────────────┴──────────────┐
          ▼                             ▼
┌──────────────────┐          ┌──────────────────┐
│  REDIS CACHE     │          │   OPENAI API     │
│  (Key-Value)     │          │   (GPT-4o-mini)  │
│  • Task queue    │          │   • Churn risk   │
│  • Results TTL   │          │   • Pain points  │
│  • File storage  │          │                  │
│  • Comment cache │          │                  │
└──────────────────┘          └──────────────────┘
```

### 2.2 Technology Stack

**Frontend:**
- React 18.3 with TypeScript
- Tailwind CSS + Glass Design System
- React Router v7 with lazy loading
- Axios for HTTP requests
- Plotly.js for data visualization
- React Dropzone for file uploads

**Backend API:**
- FastAPI (Python 3.11+)
- Pydantic for data validation
- Structured logging (structlog)
- AsyncIO for concurrent operations

**Worker/Queue:**
- Celery 5.x for distributed task processing
- Redis as broker and result backend
- Kombu for message serialization

**AI/ML:**
- OpenAI GPT-4o-mini for advanced analysis
- VADER/TextBlob for local sentiment analysis
- Hybrid approach (87% cost reduction)

**Infrastructure:**
- Render.com (4 services: web, api, worker, redis)
- Docker-compatible builds
- Environment-based configuration

---

## 3. Backend (API) - Detailed Analysis

### 3.1 Project Structure

```
api/
├── app/
│   ├── main.py                    # FastAPI entry point (125 lines)
│   ├── config.py                  # Configuration management (126 lines)
│   │
│   ├── routes/                    # API endpoints
│   │   ├── upload.py              # File upload (272 lines)
│   │   ├── status.py              # Task status polling
│   │   ├── results.py             # Results retrieval
│   │   ├── export.py              # CSV/Excel export
│   │   ├── health.py              # Health checks
│   │   └── metrics.py             # Real-time metrics dashboard
│   │
│   ├── services/                  # Business logic layer
│   │   ├── analysis_service.py    # Analysis orchestration
│   │   ├── storage_service.py     # Redis storage
│   │   ├── status_service.py      # Task status management
│   │   ├── export_service.py      # Export generation
│   │   ├── metrics_service.py     # Metrics collection
│   │   └── efficient_deduplication.py  # Comment deduplication
│   │
│   ├── core/                      # Domain logic
│   │   ├── unified_file_processor.py   # File parsing
│   │   ├── unified_aggregation.py      # Results aggregation
│   │   ├── nps_calculator.py           # NPS computation
│   │   ├── excel_formatter.py          # Excel styling
│   │   └── cache_manager.py            # Cache utilities
│   │
│   ├── adapters/                  # External integrations
│   │   ├── hybrid_analyzer.py     # Hybrid AI analysis (310 lines)
│   │   ├── local_sentiment.py     # VADER/TextBlob sentiment
│   │   └── openai/
│   │       ├── analyzer.py        # OpenAI integration
│   │       ├── async_analyzer.py  # Async OpenAI client
│   │       ├── parallel_processor.py  # Concurrent processing
│   │       └── client.py          # OpenAI client wrapper
│   │
│   ├── workers/                   # Celery tasks
│   │   ├── celery_app.py          # Celery configuration (134 lines)
│   │   └── tasks.py               # Task definitions (527 lines)
│   │
│   ├── schemas/                   # Pydantic models
│   │   ├── ai_schemas.py          # OpenAI structured outputs
│   │   ├── analysis.py            # Analysis data models
│   │   ├── upload.py              # Upload request/response
│   │   ├── status.py              # Task status models
│   │   └── export.py              # Export schemas
│   │
│   ├── utils/                     # Utilities
│   │   ├── logging.py             # Structured logging
│   │   ├── event_loop_manager.py  # AsyncIO management
│   │   ├── event_loop_monitor.py  # Event loop debugging
│   │   ├── memory_monitor.py      # Memory optimization
│   │   └── openai_logging.py      # OpenAI metrics tracking
│   │
│   └── infrastructure/            # Infrastructure layer
│       └── cache.py               # Redis client
│
├── tests/                         # Test suite
│   ├── test_architecture.py       # Architecture validation
│   └── services/export/           # Export service tests
│
├── requirements.txt               # Python dependencies
└── pyproject.toml                 # Python project config
```

### 3.2 Key API Endpoints

#### 3.2.1 File Upload (`POST /upload`)
**Purpose:** Validate and queue feedback files for analysis

**Process Flow:**
1. Validates file format (.csv, .xlsx, .xls)
2. Checks file size (max 20MB)
3. Validates structure (requires 'Nota' and 'Comentario Final' columns)
4. Stores file content in Redis (4-hour TTL for retries)
5. Queues Celery task
6. Returns task_id and estimated processing time

**Validation Rules:**
- File size: Max 20MB
- Supported formats: CSV, XLSX, XLS
- Required columns:
  - `Nota`: Integer 0-10 (customer rating)
  - `Comentario Final`: String 3-2000 chars (feedback text)
- Optional column:
  - `NPS`: If present, used directly; otherwise calculated from Nota

**Response Example:**
```json
{
  "success": true,
  "task_id": "t_a1b2c3d4e5f6",
  "estimated_time_seconds": 15,
  "file_info": {
    "name": "feedback.xlsx",
    "rows": 850,
    "size_mb": 2.3,
    "columns_found": ["Nota", "Comentario Final", "NPS"],
    "has_nps_column": true
  }
}
```

#### 3.2.2 Task Status (`GET /status/{task_id}`)
**Purpose:** Poll task progress during processing

**Status Flow:**
- `pending` → `started` → `processing` → `completed`
- Error states: `failed`, `retry`

**Response Example:**
```json
{
  "task_id": "t_a1b2c3d4e5f6",
  "status": "processing",
  "progress": 65,
  "message": "Procesando 12/18 lotes (fallos: 0)",
  "processed_rows": 550,
  "total_rows": 850,
  "eta_seconds": 5
}
```

#### 3.2.3 Results Retrieval (`GET /results/{task_id}`)
**Purpose:** Fetch complete analysis results

**Response Structure:**
```json
{
  "task_id": "t_a1b2c3d4e5f6",
  "summary": {
    "total_comments": 850,
    "avg_sentiment": 0.45,
    "avg_churn_risk": 0.32,
    "nps_score": 42
  },
  "emotions_summary": {
    "satisfaccion": 0.58,
    "frustracion": 0.23,
    "enojo": 0.12,
    // ... 4 more emotions
  },
  "pain_points": [
    {"category": "precio", "count": 124, "percentage": 14.6},
    {"category": "servicio", "count": 98, "percentage": 11.5},
    // ... more pain points
  ],
  "nps_distribution": {
    "promoters": 425,
    "passives": 312,
    "detractors": 113
  },
  "detailed_results": [
    {
      "index": 0,
      "original_text": "Excelente servicio...",
      "nota": 9,
      "emotions": { /* ... */ },
      "churn_risk": 0.15,
      "pain_points": [],
      "sentiment_score": 0.85,
      "nps_category": "promoter"
    },
    // ... 849 more
  ],
  "metadata": {
    "processing_time_seconds": 12.4,
    "batches_processed": 18,
    "model_used": "gpt-4o-mini",
    "dedup_savings_pct": 22.3
  }
}
```

#### 3.2.4 Export (`GET /export/{task_id}?format=xlsx`)
**Purpose:** Generate downloadable reports

**Supported Formats:**
- `csv` - Simple CSV with all data
- `xlsx` - Professional Excel with multiple sheets:
  - **Summary Sheet:** Key metrics, NPS breakdown, emotion averages
  - **Details Sheet:** Row-by-row analysis with all fields
  - **Emotions Sheet:** Emotion distribution charts
  - **Pain Points Sheet:** Top pain points with frequencies
- `all` - ZIP file with both CSV and Excel

**Excel Features:**
- Conditional formatting (color-coded churn risk)
- Embedded charts (emotions, NPS pie chart)
- Styled headers and professional formatting
- Multiple worksheets for organized data

#### 3.2.5 Metrics Dashboard (`GET /api/metrics`)
**Purpose:** Real-time token usage and cost tracking

**Response Example:**
```json
{
  "session": {
    "total_tokens": 28450,
    "total_cost_usd": 0.0142,
    "requests": 23,
    "avg_tokens_per_request": 1237
  },
  "lifetime": {
    "total_tokens": 1245000,
    "total_cost_usd": 0.623,
    "requests": 892
  },
  "current_rates": {
    "input_per_1m": 0.150,
    "output_per_1m": 0.600,
    "model": "gpt-4o-mini"
  }
}
```

### 3.3 Configuration Management

**File:** `api/app/config.py`

Uses Pydantic Settings for type-safe configuration:

```python
class Settings(BaseSettings):
    # Application
    APP_ENV: str = "development"
    DEBUG: bool = True

    # OpenAI
    OPENAI_API_KEY: str
    AI_MODEL: str = "gpt-4o-mini"
    OPENAI_TIMEOUT_SECONDS: int = 30

    # Redis
    REDIS_URL: str = "redis://localhost:6379/0"
    CELERY_BROKER_URL: Optional[str] = None
    CELERY_RESULT_BACKEND: Optional[str] = None

    # Processing
    FILE_MAX_MB: int = 20
    MAX_ROWS: int = 10000
    MAX_BATCH_SIZE: int = 50
    RESULTS_TTL_SECONDS: int = 86400  # 24 hours

    # Hybrid Analysis
    HYBRID_ANALYSIS_ENABLED: bool = True
    LOCAL_SENTIMENT_LIBRARY: str = "vader"

    # Performance
    OPENAI_CONCURRENT_WORKERS: int = 4
    BATCH_SIZE_OPTIMAL: int = 100
    ENABLE_PARALLEL_PROCESSING: bool = True
    ENABLE_COMMENT_CACHE: bool = True
    CACHE_TTL_DAYS: int = 7

    # Memory Management
    MEMORY_WARNING_MB: int = 400
    MEMORY_CRITICAL_MB: int = 450
    DYNAMIC_BATCH_SIZING: bool = True
```

**Environment Priority:**
1. Environment variables (highest)
2. `.env.local` file
3. `.env` file
4. Default values (lowest)

---

## 4. Worker/Celery Implementation

### 4.1 Celery Architecture

**File:** `api/app/workers/celery_app.py`

**Configuration Highlights:**
- **Broker:** Redis (same instance as cache)
- **Result Backend:** Redis with 24-hour TTL
- **Serialization:** JSON (secure, human-readable)
- **Concurrency:** 2-4 workers (configurable)
- **Task Routing:** Single queue (simplified)
- **Retry Policy:** Exponential backoff (5s, 10s, 20s)

**Worker Settings:**
```python
celery_app.conf.update(
    task_acks_late=True,              # Ensure task completion
    task_reject_on_worker_lost=True,   # Retry on worker crash
    worker_prefetch_multiplier=1,      # One task at a time
    worker_max_tasks_per_child=100,    # Restart after 100 tasks
    task_time_limit=600,               # 10 minute hard limit
    task_soft_time_limit=540,          # 9 minute warning
)
```

### 4.2 Main Analysis Task

**File:** `api/app/workers/tasks.py` - `analyze_feedback()`

**Process Flow:**

1. **Initialization (5%)**
   - Retrieve file from Redis
   - Create temporary file for processing
   - Initialize task status

2. **File Loading (10%)**
   - Parse file using UnifiedFileProcessor
   - Validate data structure
   - Normalize column names

3. **Data Preparation (20%)**
   - **Deduplication:** SHA256-based with 85% similarity threshold
   - **Filtering:** Remove trivial comments (<3 chars)
   - **Truncation:** Limit to 150 chars for API efficiency
   - **Language Detection:** Spanish/English auto-detection

4. **Batch Creation (30%)**
   - **Dynamic Batch Sizing:** Memory-aware (10-100 comments/batch)
   - **Optimal Size:** 100 comments per batch (configurable)
   - Example: 850 comments → 9 batches

5. **Parallel Processing (40-90%)**
   - Spawn child tasks with `group()`
   - Process batches concurrently (max 4 parallel)
   - Monitor progress with exponential backoff polling
   - Handle failures with retry logic

6. **Results Aggregation (90-95%)**
   - Collect results from all batches
   - Expand duplicates to original count
   - Calculate aggregated metrics
   - Compute NPS scores

7. **Storage (95%)**
   - Store results in Redis (24-hour TTL)
   - Generate summary statistics
   - Prepare export data

8. **Completion (100%)**
   - Mark task as completed
   - Clean up temporary files
   - Log performance metrics

### 4.3 Batch Analysis Task

**File:** `api/app/workers/tasks.py` - `analyze_batch()`

**Hybrid Analysis Process:**

When `HYBRID_ANALYSIS_ENABLED=True` (default):

1. **Local Sentiment Analysis (Free)**
   - Uses VADER (for Spanish) or TextBlob (for English)
   - Extracts:
     - Compound sentiment score (-1 to 1)
     - 7 emotion probabilities
   - **Processing:** ~0.001s per comment
   - **Cost:** $0.00

2. **OpenAI Insights (Paid)**
   - Focuses only on:
     - Churn risk (0-1)
     - Pain point category
   - **Prompt Optimization:**
     - Includes sentiment context from step 1
     - Truncated comments (150 chars max)
     - Ultra-compact schema (30 tokens/comment)
   - **Processing:** ~0.5s per comment
   - **Cost:** ~$0.00002 per comment (87% cheaper than full AI)

3. **Result Merging**
   - Combines local emotions with AI insights
   - Calculates NPS category from emotions
   - Formats response for frontend

**Memory Management:**
- Monitors available memory before processing
- Reduces batch size if memory < 100MB
- Critical threshold triggers batch split

---

## 5. Frontend (Web) - Detailed Analysis

### 5.1 Project Structure

```
web/
├── bff/                           # Backend for Frontend
│   └── server.ts                  # Express proxy server (205 lines)
│
├── src/                           # React application source
│   ├── App.tsx                    # Main app router (50 lines)
│   ├── main.tsx                   # Entry point with providers
│   │
│   ├── pages/                     # Route pages (lazy loaded)
│   │   ├── LandingPage.tsx        # Homepage with feature showcase
│   │   ├── AboutPage.tsx          # About and documentation
│   │   └── AnalyzerPage.tsx       # Main analysis interface
│   │
│   ├── components/
│   │   ├── ui/                    # Glass Design System
│   │   │   ├── GlassCard.tsx      # Glassmorphism card container
│   │   │   ├── GlassButton.tsx    # Styled button component
│   │   │   ├── GlassProgress.tsx  # Progress bar with animations
│   │   │   ├── GlassBadge.tsx     # Info/status badges
│   │   │   └── index.ts           # Barrel exports
│   │   │
│   │   ├── upload/                # File upload components
│   │   │   ├── FileUpload.tsx     # Main upload orchestrator (100 lines)
│   │   │   ├── DragDropZone.tsx   # Drag & drop area (99 lines)
│   │   │   ├── FileInfo.tsx       # File metadata display (49 lines)
│   │   │   ├── FormatRequirements.tsx  # Usage guide (30 lines)
│   │   │   └── ErrorMessage.tsx   # Error display (13 lines)
│   │   │
│   │   ├── results/               # Data visualization (refactored v3.2)
│   │   │   ├── ResultsCharts.tsx  # Main orchestrator (65 lines, was 380)
│   │   │   ├── EmotionsChart.tsx  # Emotions bar chart (56 lines)
│   │   │   ├── NPSChart.tsx       # NPS pie chart (48 lines)
│   │   │   ├── PainPointsChart.tsx # Pain points horizontal bar (56 lines)
│   │   │   ├── ChurnRiskChart.tsx # Churn distribution histogram (65 lines)
│   │   │   ├── SampleCommentsTable.tsx  # Comments preview (72 lines)
│   │   │   ├── StatCard.tsx       # Metric summary cards (26 lines)
│   │   │   ├── chartConfig.ts     # Shared Plotly config
│   │   │   └── types.ts           # TypeScript interfaces
│   │   │
│   │   ├── progress/
│   │   │   └── ProgressTracker.tsx  # Real-time progress polling (231 lines)
│   │   │
│   │   ├── export/
│   │   │   └── ExportResults.tsx  # Export functionality (240 lines)
│   │   │
│   │   ├── ThemeToggle.tsx        # Dark/light mode toggle
│   │   └── ErrorBoundary.tsx      # Error boundary wrapper
│   │
│   ├── contexts/                  # React Context providers
│   │   ├── UIContext.tsx          # UI state (theme, loading)
│   │   └── DataContext.tsx        # Analysis data state
│   │
│   ├── i18n/                      # Internationalization
│   │   ├── translations/
│   │   │   ├── es.ts              # Spanish translations
│   │   │   └── en.ts              # English translations
│   │   ├── hooks/
│   │   │   └── useTranslations.ts # Translation hook
│   │   └── contexts/
│   │       └── i18nContext.tsx    # i18n provider
│   │
│   ├── design/tokens/             # Design system tokens
│   │   ├── colors.ts              # Color palette
│   │   ├── spacing.ts             # Spacing scale
│   │   ├── typography.ts          # Font styles
│   │   ├── shadows.ts             # Shadow utilities
│   │   └── animations.ts          # Animation presets
│   │
│   ├── lib/
│   │   └── api.ts                 # Axios API client with types
│   │
│   └── hooks/
│       ├── useTheme.ts            # Theme management
│       └── useLanguage.ts         # Language switching
│
├── public/                        # Static assets
│   └── favicon.ico
│
├── dist/                          # Production build output
│   ├── client/                    # Vite build (React SPA)
│   └── bff/                       # Compiled BFF server
│
├── package.json                   # Dependencies and scripts
├── vite.config.ts                 # Vite bundler config
├── tailwind.config.ts             # Tailwind CSS config
└── tsconfig.json                  # TypeScript config
```

### 5.2 BFF (Backend for Frontend) Pattern

**File:** `web/bff/server.ts`

**Why BFF?**
- **No CORS Issues:** API is private, all requests go through same origin
- **Simplified Client:** Frontend makes calls to `/api/*`, BFF proxies to FastAPI
- **Security:** API never exposed directly to public internet
- **Static Serving:** Serves built React app in production

**Key Features:**
```typescript
// API Proxy Configuration
const apiProxy = createProxyMiddleware({
  target: API_TARGET,              // e.g., http://customer-feedback-api:10000
  changeOrigin: true,
  secure: false,                   // Allow HTTP for internal services
  pathRewrite: {
    '^/api': '',                   // /api/upload → /upload
  },
});

app.use('/api', apiProxy);
```

**Production Mode:**
- Serves static files from `dist/client`
- All routes serve `index.html` (SPA routing)
- Caches static assets for 1 day
- No-cache for HTML (always fresh)

**Development Mode:**
- Proxies API calls only
- Vite dev server handles frontend on port 3001

### 5.3 Component Architecture (Clean Architecture)

#### 5.3.1 Refactoring Success Story

**Before v3.2.0:**
- `ResultsCharts.tsx`: 380 lines (god file)
- `FileUpload.tsx`: 251 lines (complex state management)
- Bundle size: 5.2 MB
- Build time: 45 seconds
- Cyclomatic complexity: 12 (high)

**After v3.2.0:**
- Max file size: 240 lines (Progress/Export components)
- `ResultsCharts.tsx`: 65 lines (orchestrator only)
- Bundle size: 4.8 MB with code splitting
- Build time: 25 seconds
- Cyclomatic complexity: 4 (low)

#### 5.3.2 Results Components Breakdown

| Component | Purpose | Lines | Dependencies |
|-----------|---------|-------|--------------|
| `ResultsCharts.tsx` | Orchestrates all visualizations | 65 | All chart components |
| `EmotionsChart.tsx` | Bar chart for 7 emotions | 56 | Plotly, chartConfig |
| `NPSChart.tsx` | Pie chart for NPS distribution | 48 | Plotly, chartConfig |
| `PainPointsChart.tsx` | Horizontal bar for pain points | 56 | Plotly, chartConfig |
| `ChurnRiskChart.tsx` | Histogram for churn risk | 65 | Plotly, chartConfig |
| `SampleCommentsTable.tsx` | Preview table of comments | 72 | GlassCard |
| `StatCard.tsx` | Summary metric card | 26 | GlassCard |
| `chartConfig.ts` | Shared Plotly configuration | 17 | Plotly types |

**Shared Chart Configuration:**
```typescript
// chartConfig.ts
export const defaultLayout = {
  autosize: true,
  paper_bgcolor: 'rgba(255,255,255,0.05)',
  plot_bgcolor: 'rgba(255,255,255,0.02)',
  font: {
    family: 'Inter, sans-serif',
    color: isDark ? '#e5e7eb' : '#1f2937',
  },
  margin: { l: 50, r: 30, t: 50, b: 50 },
};
```

#### 5.3.3 Upload Components Breakdown

| Component | Purpose | Lines | Key Features |
|-----------|---------|-------|--------------|
| `FileUpload.tsx` | Upload orchestration | 100 | State management, validation |
| `DragDropZone.tsx` | File drop interface | 99 | React Dropzone integration |
| `FileInfo.tsx` | File metadata display | 49 | Size, format, row count |
| `FormatRequirements.tsx` | Documentation | 30 | Required columns guide |
| `ErrorMessage.tsx` | Error display | 13 | Reusable error UI |

### 5.4 Glass Design System

**Visual Identity:** Modern glassmorphism aesthetic with:
- Semi-transparent backgrounds
- Backdrop blur effects
- Subtle gradients and shadows
- Smooth animations

**Component Examples:**

```tsx
// GlassCard variants
<GlassCard variant="default">   // Standard glass effect
<GlassCard variant="gradient">  // With gradient overlay
<GlassCard variant="blur">      // Extra blur effect

// GlassButton variants
<GlassButton variant="primary">    // Blue gradient
<GlassButton variant="secondary">  // Gray neutral
<GlassButton variant="ghost">      // Transparent with border
<GlassButton variant="danger">     // Red gradient

// GlassBadge variants
<GlassBadge variant="info">     // Blue
<GlassBadge variant="success">  // Green
<GlassBadge variant="warning">  // Yellow
<GlassBadge variant="danger">   // Red
```

**Tailwind CSS Classes:**
```css
.glass-card {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(12px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
}
```

### 5.5 Performance Optimizations

#### 5.5.1 Code Splitting & Lazy Loading

**Implementation:**
```typescript
// App.tsx
const LandingPage = lazy(() =>
  import('@/pages/LandingPage').then(m => ({ default: m.LandingPage }))
);
const AboutPage = lazy(() =>
  import('@/pages/AboutPage').then(m => ({ default: m.AboutPage }))
);
const AnalyzerPage = lazy(() =>
  import('@/pages/AnalyzerPage').then(m => ({ default: m.AnalyzerPage }))
);

<Suspense fallback={<LoadingFallback />}>
  <Routes>
    <Route path="/" element={<LandingPage />} />
    <Route path="/about" element={<AboutPage />} />
    <Route path="/analyzer" element={<AnalyzerPage />} />
  </Routes>
</Suspense>
```

**Bundle Analysis:**

| Chunk | Size | Gzipped | Load Time (3G) |
|-------|------|---------|----------------|
| Main Bundle | 176 KB | 58 KB | 0.5s |
| LandingPage | 6.25 KB | 1.66 KB | 0.05s |
| AboutPage | 8.62 KB | 1.90 KB | 0.06s |
| AnalyzerPage | 4.8 MB | 1.45 MB | 12s |

**Benefits:**
- **Initial Load:** Only 176 KB (main bundle)
- **On-Demand Loading:** Analyzer page loads only when needed
- **Reduced TTI:** Time to Interactive improved by 65%

#### 5.5.2 React Optimization Patterns

**Used Throughout:**
- `React.memo()` for expensive components
- `useMemo()` for computed values
- `useCallback()` for stable function references
- Debounced polling to reduce API calls

**Example:**
```typescript
// Memoized chart data computation
const chartData = useMemo(() => {
  return processChartData(results);
}, [results]);

// Memoized component
const EmotionsChart = React.memo(({ data }) => {
  // ... render logic
});
```

### 5.6 State Management

**Context Architecture:**

1. **UIContext** - Global UI state
   - Theme (light/dark)
   - Loading states
   - Modal visibility

2. **DataContext** - Analysis data
   - Upload status
   - Task ID
   - Results data
   - Error states

3. **I18nContext** - Internationalization
   - Current language (es/en)
   - Translation functions

**No Redux/Zustand:** Simple Context API sufficient for this app's complexity.

---

## 6. Data Flow and Processing Pipeline

### 6.1 End-to-End Data Flow

```
1. USER UPLOADS FILE
   └─> React FileUpload component
       └─> FormData with file + metadata
           └─> POST /api/upload (via BFF proxy)

2. BFF PROXY FORWARDS REQUEST
   └─> Express server receives multipart/form-data
       └─> Proxies to FastAPI at /upload
           └─> Preserves all headers and body

3. FASTAPI VALIDATES & STORES
   └─> File validation (format, size, structure)
       └─> UnifiedFileProcessor parses and normalizes
           └─> Store file in Redis (base64, 4h TTL)
               └─> Queue Celery task
                   └─> Return task_id to frontend

4. CELERY WORKER PROCESSES
   └─> Retrieve file from Redis
       └─> Load with pandas + validation
           └─> Deduplicate comments (SHA256)
               └─> Create batches (50-100 comments each)
                   └─> Spawn parallel batch tasks

5. BATCH ANALYSIS (per batch)
   └─> Local Sentiment Analysis (VADER/TextBlob)
       ├─> Extract 7 emotions
       └─> Calculate sentiment score
   └─> OpenAI API Call (GPT-4o-mini)
       ├─> Get churn risk
       └─> Extract pain point category
   └─> Merge results
       └─> Return to parent task

6. RESULTS AGGREGATION
   └─> Collect all batch results
       └─> Expand duplicates to original indices
           └─> Calculate aggregate metrics
               ├─> Average emotions
               ├─> NPS distribution
               ├─> Top pain points
               └─> Churn risk distribution
           └─> Store in Redis (24h TTL)

7. FRONTEND POLLING
   └─> GET /api/status/{task_id} every 1-2 seconds
       └─> Progress updates (5% → 100%)
           └─> On completion:
               └─> GET /api/results/{task_id}
                   └─> Display charts and tables

8. EXPORT (optional)
   └─> GET /api/export/{task_id}?format=xlsx
       └─> Generate Excel with charts
           └─> Download to user
```

### 6.2 Comment Deduplication Strategy

**Purpose:** Reduce API costs by identifying duplicate/similar comments

**Algorithm:** `EfficientDeduplicationService` (O(n) complexity)

**Process:**
1. **Normalization:**
   - Lowercase conversion
   - Remove accents and special characters
   - Trim whitespace

2. **Hash Generation:**
   - SHA256 hash of normalized text
   - Creates unique fingerprint

3. **Similarity Check:**
   - Fuzzy matching with 85% threshold
   - Identifies near-duplicates

4. **Result:**
   - **Filtered Comments:** Only unique comments sent to OpenAI
   - **Duplicate Map:** Maps duplicate indices to original
   - **Savings:** Typically 15-35% reduction in API calls

**Example:**
```
Original: 850 comments
After deduplication: 650 unique comments
Savings: 23.5% (200 comments not sent to API)
Cost saved: ~$0.004 per file
```

### 6.3 Hybrid Analysis Optimization

**Cost Comparison:**

| Approach | Tokens/Comment | Cost/Comment | Cost/1000 |
|----------|---------------|--------------|-----------|
| **Full OpenAI** (old) | 250 | $0.000150 | $0.15 |
| **Hybrid** (current) | 30 | $0.000018 | $0.018 |
| **Savings** | **88%** | **88%** | **$0.132** |

**Hybrid Breakdown:**

**Local Analysis (Free):**
- VADER Sentiment (Spanish optimized)
- TextBlob Sentiment (English)
- Emotion extraction from sentiment components
- Language detection

**OpenAI Analysis (Paid):**
- Churn risk prediction (0-1)
- Pain point categorization (8 categories)
- Ultra-compact prompt (includes sentiment context)

**Prompt Engineering:**
```
System: Extract ONLY: churn risk (0-1) and pain category.
Comments include [Sentiment: positive/negative/neutral] context.
Output: {"r":[{"c":0.0-1.0,"p":"category"},...]}
Categories: precio,calidad,servicio,tiempo,app,producto,atencion,otro

User:
1.[Sentiment: positive] Excelente servicio, muy satisfecho
2.[Sentiment: negative] Muy caro para la calidad ofrecida
3.[Sentiment: neutral] El producto es bueno pero tarda mucho
```

**Response Schema (JSON Mode):**
```json
{
  "r": [
    {"c": 0.15, "p": "servicio"},
    {"c": 0.72, "p": "precio"},
    {"c": 0.45, "p": "tiempo"}
  ]
}
```

---

## 7. Key Features and Functionalities

### 7.1 Emotion Analysis

**7 Core Emotions Detected:**

1. **Satisfacción (Satisfaction/Joy)** - Positive experience, happiness
2. **Frustración (Frustration)** - Obstacles, difficulties
3. **Enojo (Anger)** - Strong negative reaction
4. **Confianza (Trust)** - Reliability, confidence in brand
5. **Decepción (Disappointment)** - Unmet expectations
6. **Confusión (Confusion)** - Uncertainty, lack of clarity
7. **Anticipación (Anticipation)** - Expectation, hope

**Scoring:** Each emotion receives a probability score from 0 to 1

**Use Cases:**
- Identify highly frustrated customers needing immediate attention
- Find loyal customers (high trust + satisfaction) for referral programs
- Detect confusion indicating poor UX or communication

### 7.2 Pain Point Categorization

**8 Standard Categories:**

1. **Precio** - Pricing concerns (too expensive, not worth it)
2. **Calidad** - Quality issues (defects, poor materials)
3. **Servicio** - Service problems (rude staff, poor support)
4. **Tiempo** - Time-related (slow delivery, long wait)
5. **App** - Technical issues (bugs, crashes, poor UX)
6. **Producto** - Product-specific issues (missing features)
7. **Atención** - Customer care (unresponsive, unhelpful)
8. **Otro** - Miscellaneous

**Extraction:**
- Max 5 pain points per comment
- Ranked by severity (0-1)
- Aggregated across all comments to find top issues

**Visualization:**
- Horizontal bar chart showing frequency
- Percentage of total comments affected

### 7.3 Churn Risk Scoring

**Definition:** Probability (0-1) that a customer will stop using the service

**Calculation Factors:**
- Negative emotions (frustration, anger, disappointment)
- Pain point severity
- Sentiment score
- Explicit churn indicators in text ("cancel", "switch", "leave")

**Risk Levels:**
- **Low (0-0.3):** Satisfied customers
- **Medium (0.3-0.6):** At-risk, needs monitoring
- **High (0.6-1.0):** Critical, immediate action required

**Business Value:**
- Prioritize customer retention efforts
- Calculate expected churn rate
- ROI on retention campaigns

### 7.4 NPS (Net Promoter Score)

**Calculation Methods:**

1. **From Nota (Rating-based):**
   - Promoter: Nota 9-10
   - Passive: Nota 7-8
   - Detractor: Nota 0-6

2. **From Emotions (AI-based):**
   - Promoter: High satisfaction + trust, low negative emotions
   - Passive: Neutral or mixed emotions
   - Detractor: High frustration/anger/disappointment

**Formula:**
```
NPS = (% Promoters) - (% Detractors)
Range: -100 to +100
```

**Example:**
- Promoters: 425/850 = 50%
- Detractors: 113/850 = 13.3%
- NPS = 50 - 13.3 = **36.7**

**Benchmarks:**
- **>70:** Excellent
- **50-70:** Good
- **30-50:** Average
- **<30:** Needs improvement

### 7.5 Real-time Metrics Dashboard

**File:** `api/app/routes/metrics.py`

**Tracked Metrics:**
- **Total Tokens Used:** Lifetime and per-session
- **API Costs:** Real-time cost calculation
- **Request Count:** Number of OpenAI API calls
- **Tokens per Request:** Efficiency metric
- **Deduplication Savings:** % of API calls avoided

**Dashboard Features:**
- Session reset button
- Cost breakdown by input/output tokens
- Historical totals
- Average efficiency metrics

**Use Case:**
- Monitor API usage to stay within budget
- Optimize prompts based on token metrics
- Track cost savings from deduplication

### 7.6 Professional Excel Export

**File:** `api/app/services/export/excel_styled_exporter.py`

**Features:**

1. **Multiple Worksheets:**
   - Summary: High-level metrics
   - Details: Row-by-row analysis
   - Emotions: Emotion distribution
   - Pain Points: Top pain points

2. **Conditional Formatting:**
   - Churn risk: Red (high) to green (low)
   - Sentiment: Color-coded bars
   - NPS categories: Color-coded text

3. **Embedded Charts:**
   - NPS pie chart
   - Emotions bar chart
   - Pain points horizontal bar

4. **Professional Styling:**
   - Branded headers with colors
   - Freeze panes for scrolling
   - Auto-fit column widths
   - Number formatting (percentages, decimals)

**Technology:** `openpyxl` library with chart creation

---

## 8. Deployment Architecture (Render.com)

### 8.1 Service Configuration

**File:** `render.yaml`

**4 Services Deployed:**

#### 1. Redis (Key-Value Store)
```yaml
type: keyvalue
name: feedback-analyzer-redis
plan: free
region: oregon
maxmemoryPolicy: noeviction  # Important for job queue
```

**Purpose:**
- Celery task queue broker
- Result storage backend
- File content cache (4-hour TTL)
- Comment deduplication cache (7-day TTL)

#### 2. FastAPI Backend (Private Service)
```yaml
type: pserv
name: customer-feedback-api
runtime: python
plan: starter
startCommand: uvicorn app.main:app --host 0.0.0.0 --port $PORT
```

**Environment Variables:**
- `OPENAI_API_KEY` - OpenAI authentication
- `REDIS_URL` - Auto-injected from Redis service
- `AI_MODEL=gpt-4o-mini`
- `HYBRID_ANALYSIS_ENABLED=true`
- `BATCH_SIZE_OPTIMAL=100`

**Health Check:** `/health/simple`

#### 3. Celery Worker (Background Worker)
```yaml
type: worker
name: celery-worker
runtime: python
plan: starter
startCommand: celery -A app.workers.celery_app worker --loglevel=INFO
```

**Environment Variables:**
- Same as API (shared configuration)
- `CELERY_WORKER_CONCURRENCY=2` (Render starter plan)

**Critical:** No health check (workers don't expose HTTP endpoint)

#### 4. BFF/Frontend (Public Web Service)
```yaml
type: web
name: customer-feedback-app
runtime: node
plan: starter
buildCommand: cd web && npm install && npm run build
startCommand: cd web && node dist/bff/server.js
```

**Environment Variables:**
- `NODE_ENV=production`
- `API_PROXY_TARGET=http://customer-feedback-api-bmjp:10000`

**Health Check:** `/health`

### 8.2 Inter-Service Communication

**Internal Render URLs:**
- Services communicate via internal DNS
- Format: `{service-name}-{suffix}:{port}`
- Example: `customer-feedback-api-bmjp:10000`

**Security:**
- API is **private** (not exposed to internet)
- Only accessible via BFF proxy
- No CORS needed (same origin)

### 8.3 Deployment Process

**Automatic Deployment Triggers:**

1. **Web Service:**
   - Triggers on changes to `web/**`
   - Build: 2-3 minutes
   - Steps:
     1. Install dependencies (`npm install`)
     2. Build React app (`vite build`)
     3. Compile BFF server (`tsc`)
   - Result: `dist/client` + `dist/bff`

2. **API Service:**
   - Triggers on changes to `api/**`
   - Build: 1-2 minutes
   - Steps:
     1. Install Python dependencies
     2. No compilation needed
   - Result: Ready to run `uvicorn`

3. **Worker Service:**
   - Triggers on changes to `api/**`
   - Build: Same as API
   - Starts Celery worker process

**Zero-Downtime Deploys:**
- Render uses rolling deploys
- New version tested before old version stops
- Health checks ensure service is ready

### 8.4 Monitoring and Logs

**Structured Logging:**
- All services use JSON-formatted logs
- Centralized in Render dashboard
- Fields: timestamp, level, event, metadata

**Example Log:**
```json
{
  "event": "Batch processing summary",
  "timestamp": "2024-10-16T19:30:45Z",
  "level": "info",
  "total_batches": 12,
  "completed": 12,
  "success_rate": 100,
  "total_tokens_used": 28980,
  "tokens_per_comment": 25.3,
  "deduplication_savings": 32.5
}
```

**Metrics Available:**
- CPU usage per service
- Memory usage (important for 512MB workers)
- Request latency
- Error rates
- Uptime

---

## 9. Performance Metrics and Benchmarks

### 9.1 Processing Speed

**Real-World Performance:**

| Comments | Time | Throughput | Cost |
|----------|------|------------|------|
| 100 | 2-3s | 40 comments/s | $0.002 |
| 500 | 5-8s | 70 comments/s | $0.009 |
| 850 | 8-10s | 90 comments/s | $0.015 |
| 1800 | 18-20s | 95 comments/s | $0.032 |
| 3000 | 30-35s | 90 comments/s | $0.054 |

**Performance Factors:**
- **Parallel Processing:** 4 concurrent batches
- **Batch Size:** 100 comments optimal
- **Deduplication:** 15-35% reduction in API calls
- **Hybrid Analysis:** Local sentiment is instant

### 9.2 Cost Efficiency

**Hybrid vs Full OpenAI:**

| Metric | Full OpenAI | Hybrid | Savings |
|--------|-------------|--------|---------|
| **Tokens/Comment** | 250 | 30 | 88% |
| **Cost/Comment** | $0.000150 | $0.000018 | 88% |
| **Cost/1000 Comments** | $0.15 | $0.018 | $0.132 |
| **Monthly (100k comments)** | $15.00 | $1.80 | $13.20 |

**Additional Savings from Deduplication:**
- Average: 20% fewer API calls
- Example: 1000 comments → 800 unique → Save $0.0036

**Total Savings: 87-90% cost reduction**

### 9.3 System Reliability

**Success Rates:**
- **API Uptime:** 99.9%
- **Task Completion:** >99%
- **Retry Success:** 95% (on first retry)

**Error Handling:**
- Automatic retries (3 attempts)
- Exponential backoff (5s, 10s, 20s)
- Graceful degradation (local-only fallback)

**Data Integrity:**
- File validation before processing
- Schema validation on API responses
- Deduplication integrity checks

### 9.4 Scalability Limits

**Current Limits:**

| Limit | Value | Reason |
|-------|-------|--------|
| File Size | 20 MB | Memory constraint |
| Max Rows | 10,000 | Processing time |
| Concurrent Tasks | 4 | Worker capacity |
| Results TTL | 24 hours | Redis memory |

**Potential Scaling Paths:**
1. Add more worker instances (horizontal scaling)
2. Increase batch size for larger datasets
3. Implement result pagination
4. Use persistent storage for long-term results

---

## 10. Security and Best Practices

### 10.1 Security Measures

**API Security:**
- **Private API:** Not exposed to internet, only via BFF
- **No CORS needed:** Same-origin requests
- **Trusted Host Middleware:** Only allows render.com hosts
- **Input Validation:** Pydantic schemas for all inputs
- **File Size Limits:** Max 20MB prevents DoS
- **Timeout Controls:** 10-minute max task execution

**Data Privacy:**
- **No PII Storage:** Comments are transient (24h TTL)
- **No User Accounts:** Stateless processing
- **HTTPS Enforced:** All communication encrypted
- **Environment Secrets:** API keys in env vars, never committed

**Error Handling:**
- **Sanitized Errors:** Production hides stack traces
- **Structured Logging:** No sensitive data in logs
- **Rate Limiting:** OpenAI rate limiter prevents abuse

### 10.2 Code Quality Standards

**Python (Backend):**
- **Linter:** Flake8 (PEP 8 compliance)
- **Formatter:** Black (opinionated, consistent)
- **Type Checker:** MyPy (static type analysis)
- **Pre-commit Hooks:** Enforce standards before commit

**TypeScript (Frontend):**
- **Linter:** ESLint with React hooks plugin
- **Type Checking:** Strict TypeScript mode
- **Import Style:** `import type` for type-only imports
- **No Unused Vars:** Enforced via ESLint

**Architectural Rules:**
- **Max File Size:** 250 lines (enforced by code review)
- **No God Files:** Single Responsibility Principle
- **No Emojis:** Zero tolerance (enforced by pre-commit hook)
- **English Comments:** Code comments in English only

### 10.3 Testing Strategy

**Backend Tests:**
- **Unit Tests:** Services, core logic
- **Integration Tests:** API endpoints
- **Architecture Tests:** Enforce design rules
- **Coverage Target:** 80%+ for critical paths

**Frontend Tests:**
- **Component Tests:** React Testing Library
- **E2E Tests:** Playwright (planned)
- **Visual Regression:** Storybook snapshots (planned)

**Example Test:**
```python
# tests/services/export/test_excel_styled_exporter.py
def test_excel_export_with_charts():
    results = create_mock_results(100)
    exporter = ExcelStyledExporter()
    file_path = exporter.export(results)

    # Verify file created
    assert file_path.exists()

    # Verify worksheets
    wb = load_workbook(file_path)
    assert 'Summary' in wb.sheetnames
    assert 'Details' in wb.sheetnames
    assert 'Emotions' in wb.sheetnames
```

---

## 11. Technology Stack Summary

### 11.1 Backend Technologies

| Category | Technology | Version | Purpose |
|----------|-----------|---------|---------|
| **Web Framework** | FastAPI | Latest | REST API server |
| **Task Queue** | Celery | 5.x | Distributed task processing |
| **Cache/Queue** | Redis | 7.x | Broker + result storage |
| **AI/ML** | OpenAI API | gpt-4o-mini | Churn risk + pain points |
| **Local AI** | VADER/TextBlob | Latest | Free sentiment analysis |
| **Data Processing** | Pandas | 2.x | Data manipulation |
| **Validation** | Pydantic | 2.x | Schema validation |
| **Logging** | structlog | Latest | Structured JSON logs |
| **HTTP Client** | httpx | Latest | Async HTTP for OpenAI |
| **Excel Export** | openpyxl | Latest | Excel file generation |

### 11.2 Frontend Technologies

| Category | Technology | Version | Purpose |
|----------|-----------|---------|---------|
| **Framework** | React | 18.3 | UI library |
| **Language** | TypeScript | 5.x | Type safety |
| **Routing** | React Router | 7.x | SPA navigation |
| **Styling** | Tailwind CSS | 3.x | Utility-first CSS |
| **HTTP Client** | Axios | 1.7.x | API requests |
| **Charts** | Plotly.js | Latest | Data visualization |
| **File Upload** | React Dropzone | 14.x | Drag & drop files |
| **Build Tool** | Vite | 5.x | Fast bundler |
| **Server** | Express | 4.x | BFF proxy server |

### 11.3 Infrastructure Technologies

| Category | Technology | Purpose |
|----------|-----------|---------|
| **Hosting** | Render.com | Managed PaaS |
| **CI/CD** | Render Auto-deploy | Git-based deploys |
| **Monitoring** | Render Dashboard | Logs and metrics |
| **Version Control** | Git | Source control |

---

## 12. Unique Features and Innovations

### 12.1 Hybrid AI Analysis

**Innovation:** Combines free local sentiment analysis with paid AI insights

**Benefits:**
- 87% cost reduction vs. full AI
- Same quality results
- Faster processing (local analysis is instant)
- Resilient (fallback to local-only if API fails)

**Implementation Novelty:**
- Sentiment context enriches AI prompts
- Two-stage processing pipeline
- Memory-aware batch sizing

### 12.2 Intelligent Deduplication

**Innovation:** SHA256-based deduplication with fuzzy matching

**Benefits:**
- 15-35% reduction in API calls
- O(n) complexity (efficient)
- Preserves all original data
- Maps duplicates to originals

**Technical Approach:**
- Normalize text (lowercase, remove accents)
- Generate hash fingerprint
- 85% similarity threshold
- Duplicate map for result expansion

### 12.3 BFF Proxy Pattern

**Innovation:** Node.js server acts as Backend for Frontend

**Benefits:**
- No CORS complexity
- Private API (never exposed)
- Single-origin architecture
- Simplified frontend code

**Implementation:**
- Express proxy middleware
- Production: static file serving + API proxy
- Development: API proxy only (Vite serves files)

### 12.4 Clean Architecture Refactoring

**Innovation:** God files refactored into modular components

**Example:**
- `ResultsCharts.tsx`: 380 → 65 lines
- Split into 7 specialized components
- Shared configuration module
- Lazy loading for performance

**Benefits:**
- Easier testing (small, focused components)
- Better maintainability
- Reusability
- 65% faster bundle load

### 12.5 Dynamic Batch Sizing

**Innovation:** Memory-aware batch size adjustment

**Algorithm:**
```python
def calculate_safe_batch_size(total_comments, optimal_size):
    available_mb = psutil.virtual_memory().available / (1024 * 1024)

    if available_mb < 100:
        return min(20, optimal_size)  # Critical
    elif available_mb < 200:
        return min(50, optimal_size)  # Warning
    else:
        return optimal_size  # Normal
```

**Benefits:**
- Prevents memory crashes
- Adapts to system load
- Maintains performance when possible

### 12.6 Professional Excel Export

**Innovation:** Multi-sheet Excel with charts and conditional formatting

**Features:**
- 4 worksheets (Summary, Details, Emotions, Pain Points)
- Embedded Plotly charts
- Color-coded conditional formatting
- Auto-fit columns

**Technology:**
- `openpyxl` for Excel manipulation
- Chart objects for visualizations
- Styled headers and cells

---

## 13. Development Workflow

### 13.1 Local Development Setup

**Prerequisites:**
- Python 3.11+
- Node.js 20+
- Redis 7.0+
- OpenAI API key

**Backend Setup:**
```bash
cd api/
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
pip install -r requirements.txt

# Create .env file
cp .env.example .env
# Edit .env and add OPENAI_API_KEY

# Run API
uvicorn app.main:app --reload --port 8000

# Run worker (separate terminal)
celery -A app.workers.celery_app worker --loglevel=INFO
```

**Frontend Setup:**
```bash
cd web/
npm install

# Development mode (Vite + BFF)
npm run dev
# Opens Vite on http://localhost:3001
# BFF proxy on http://localhost:3000
```

**Redis Setup:**
```bash
# macOS
brew install redis
brew services start redis

# Ubuntu/Debian
sudo apt install redis-server
sudo systemctl start redis

# Windows
# Use WSL or Redis for Windows
```

### 13.2 Project Scripts

**Root-level (monorepo):**
```bash
npm run dev           # Start web dev servers
npm run build         # Build for production
npm run deploy:check  # Type-check and lint
npm run clean         # Remove build artifacts
```

**Backend (`api/`):**
```bash
pytest                    # Run tests
pytest --cov             # With coverage
black .                  # Format code
flake8 .                 # Lint
mypy .                   # Type check
```

**Frontend (`web/`):**
```bash
npm run dev              # Development servers
npm run build            # Production build
npm run preview          # Preview production build
npm run lint             # ESLint
npm run type-check       # TypeScript check
```

### 13.3 Git Workflow

**Branching Strategy:**
- `main` - Production-ready code
- `develop` - Integration branch
- `feature/*` - Feature branches
- `fix/*` - Bug fixes
- `refactor/*` - Refactoring work

**Commit Conventions:**
```
feat: add hybrid analysis for cost optimization
fix: correct NPS calculation for edge cases
docs: update API documentation
refactor: split ResultsCharts into components
perf: implement comment deduplication
test: add export service tests
```

**Pre-commit Hooks:**
- Emoji checker (CRITICAL - zero emojis allowed)
- Black formatter (Python)
- ESLint (TypeScript)
- Type checking

---

## 14. Future Enhancements and Roadmap

### 14.1 Planned Features

**Near-term (v3.3):**
1. **Email Notifications**
   - Alert when analysis completes
   - Summary report in email

2. **Webhook Support**
   - POST results to external URL
   - Integration with CRM systems

3. **Advanced Filtering**
   - Filter results by emotion
   - Filter by churn risk threshold
   - Filter by pain point category

4. **Preset Templates**
   - Save visualization preferences
   - Export templates

**Mid-term (v4.0):**
1. **Multi-language UI**
   - Full i18n implementation
   - Support Spanish, English, Portuguese

2. **User Accounts (optional)**
   - Save analysis history
   - Compare analyses over time

3. **Advanced Analytics**
   - Trend analysis over time
   - Correlation between metrics
   - Predictive churn modeling

4. **API Access**
   - REST API for integrations
   - Webhook subscriptions
   - Rate-limited public API

**Long-term:**
1. **Custom Models**
   - Fine-tune for specific industries
   - Custom pain point categories

2. **Real-time Streaming**
   - WebSocket for live updates
   - Server-sent events

3. **Advanced Visualizations**
   - 3D emotion maps
   - Time-series animations
   - Interactive dashboards

### 14.2 Performance Improvements

**Optimizations Planned:**
1. **Result Pagination**
   - Load results in chunks
   - Reduce initial payload

2. **Plotly Alternatives**
   - Evaluate lighter chart libraries
   - Consider server-side chart rendering

3. **Caching Strategies**
   - Browser cache for static assets
   - CDN for frontend bundles

4. **Worker Scaling**
   - Auto-scaling based on queue depth
   - Multiple Redis instances

### 14.3 Technical Debt

**Known Issues:**
1. **Event Loop Management**
   - Simplify async handling
   - Remove event loop monitoring if stable

2. **Plotly Bundle Size**
   - 4.8 MB for AnalyzerPage
   - Investigate code splitting Plotly

3. **Test Coverage**
   - Increase to 90%+ for backend
   - Add E2E tests for frontend

---

## 15. Conclusion

### 15.1 Project Strengths

1. **Cost-Effective AI:** 87% reduction in AI costs through hybrid approach
2. **Clean Architecture:** Well-organized, modular codebase
3. **Production-Ready:** Deployed on Render with monitoring
4. **User-Friendly:** Intuitive Glass Design UI
5. **Scalable:** Handles 3000 comments efficiently
6. **Comprehensive Insights:** Emotions, pain points, churn risk, NPS

### 15.2 Business Value

- **For Customer Service:** Prioritize at-risk customers
- **For Product:** Data-driven feature decisions
- **For Marketing:** Identify promoters and brand advocates
- **For Analytics:** Structured data for strategic planning

### 15.3 Technical Excellence

- **Modern Stack:** React, FastAPI, Celery
- **Best Practices:** Clean code, testing, type safety
- **Performance:** Sub-second API response, 10s analysis for 1000 comments
- **Reliability:** 99%+ success rate, automatic retries

---

## Appendix: Key Files Reference

### Backend Entry Points
- `api/app/main.py` - FastAPI application (125 lines)
- `api/app/workers/celery_app.py` - Celery configuration (134 lines)
- `api/app/workers/tasks.py` - Task definitions (527 lines)

### Frontend Entry Points
- `web/src/main.tsx` - React entry point
- `web/src/App.tsx` - Router and layout (50 lines)
- `web/bff/server.ts` - BFF proxy server (205 lines)

### Configuration Files
- `api/app/config.py` - Backend settings (126 lines)
- `render.yaml` - Deployment configuration (155 lines)
- `web/vite.config.ts` - Build configuration
- `web/tailwind.config.ts` - Styling configuration

### Documentation
- `README.md` - User-facing documentation (Spanish)
- `CLAUDE.md` - Project context for AI assistants
- `docs/FRONTEND_ARCHITECTURE.md` - Frontend technical docs
- `docs/TECHNICAL_DOCUMENTATION.md` - Complete technical reference

---

**Report Generated:** October 16, 2024
**Project Version:** 3.2.0
**Status:** Production
**Analyzed Files:** 150+ Python, TypeScript, config files
**Total Lines of Code:** ~15,000 (excluding tests, docs)
