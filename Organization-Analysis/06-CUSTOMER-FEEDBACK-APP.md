# Customer Feedback App - Comprehensive Analysis

## Overview

**AI-powered customer feedback analyzer**
- Repository: github.com/Ai-Whisperers/customer-feedback-app
- Last Updated: Oct 5, 2025
- Status: Production (deployed on Render)
- Technology: Python (FastAPI), React (TypeScript), OpenAI

---

## What We're Working On

The **Customer AI Driven Feedback Analyzer** is a sophisticated SaaS application that automatically analyzes customer feedback using AI to extract actionable business insights. Built for organizations that want to understand customer satisfaction, identify pain points, and predict churn risk.

### Key Achievement
**87% cost reduction** compared to traditional AI-only solutions through hybrid analysis.

---

## Technology Stack

### Backend (Python 3.11+)
- **FastAPI 0.115.0** - Modern async web framework
- **Celery 5.4.0** - Distributed task processing
- **Redis 7.0+** - Cache and message broker
- **OpenAI 1.54.3** - GPT-4o-mini integration
- **pandas 2.2.3** - Data processing
- **vaderSentiment 3.3.2** - Local sentiment analysis
- **textblob 0.17.1** - Text processing

### Frontend (Node.js 20+)
- **React 18.3.1** - UI library
- **TypeScript 5.6.3** - Type safety
- **Vite 5.4.10** - Fast bundling
- **Tailwind CSS** - Utility-first styling
- **Plotly.js** - Interactive charts

### Infrastructure
- **Render.com** - PaaS hosting
- **Redis** - External key-value store
- **GitHub Actions** - CI/CD (integration)

---

## What This Application Does

### Input
Users upload customer feedback files:
- **Formats**: CSV or XLSX
- **Size**: Up to 20MB, 3,000 rows max
- **Required columns**:
  - `Nota` (rating 0-10)
  - `Comentario Final` (feedback text)
- **Optional**: `NPS` column

### Processing
For each customer comment, the AI extracts:

**1. Seven Emotions (0-1 scale)**
- Satisfacción (Satisfaction)
- Frustración (Frustration)
- Enojo (Anger)
- Confianza (Trust)
- Decepción (Disappointment)
- Confusión (Confusion)
- Anticipación (Anticipation)

**2. Churn Risk (0-1 probability)**
- ML-predicted likelihood of customer leaving
- Analyzes dissatisfaction signals

**3. Pain Points**
- Top 10 recurring issues/keywords
- Categories: pricing, quality, service, speed, app, etc.

**4. NPS Classification**
- Promoter (9-10)
- Passive (7-8)
- Detractor (0-6)

**5. Sentiment Score (-1 to 1)**
- Overall sentiment direction

### Output
Professional reports in multiple formats:
- **Excel**: Multi-sheet with charts and formatting
- **CSV**: Raw data export
- **Web Dashboard**: Interactive visualizations

---

## Hybrid Analysis Architecture

### The Innovation: 87% Cost Reduction

```
┌─────────────────────────────────────┐
│    Traditional Approach             │
│    (100% OpenAI for everything)     │
│    Cost: $0.15 per 1000 comments    │
└─────────────────────────────────────┘

┌─────────────────────────────────────┐
│    Our Hybrid Approach              │
│    (Local + Selective OpenAI)       │
│    Cost: $0.02 per 1000 comments    │
│    Savings: 87%                     │
└─────────────────────────────────────┘
```

### How It Works

**Level 1: Local Sentiment (FREE)**
- VADER Sentiment Analyzer
- TextBlob polarity detection
- Emotion pattern matching via rules
- Processes ALL comments at zero cost

**Level 2: OpenAI Analysis (SELECTIVE)**
- GPT-4o-mini with structured outputs
- Ultra-minimal prompts (25-30 tokens/comment)
- Only for churn risk and pain points
- Processes in optimized batches

**Level 3: Merging**
```python
hybrid_result = {
  "emotions": local_analysis,      # Free
  "sentiment": local_analysis,     # Free
  "churn_risk": openai_analysis,   # Paid
  "pain_points": openai_analysis,  # Paid
}
```

---

## Data Flow

### 1. Upload Phase
```
User uploads file
  ↓
Validate format and structure
  ↓
Store in Redis (4-hour TTL)
  ↓
Queue for processing (Celery)
  ↓
Return task_id to user
```

### 2. Processing Phase
```
Celery task starts
  ↓
Load file from Redis
  ↓
Deduplicate comments (15-20% savings)
  ↓
Batch processing (50-100 comments/batch)
  ↓
  For each batch:
    - Local sentiment analysis (VADER/TextBlob)
    - OpenAI analysis (churn + pain points)
    - Merge results
  ↓
Aggregate all results
  ↓
Calculate NPS and metrics
  ↓
Store in Redis (24-hour TTL)
```

### 3. Results Phase
```
User polls /status/{task_id}
  ↓
When complete: Fetch /results/{task_id}
  ↓
Display interactive dashboard
  ↓
Export to Excel/CSV
```

---

## Key Features

### 1. Intelligent Deduplication
- SHA256 hash matching for exact duplicates
- Fuzzy matching (85% threshold) for near-duplicates
- Saves 15-20% on API calls
- Maintains index mapping for result expansion

### 2. Dynamic Batching
- Memory-aware batch sizing
- Adapts to available system memory
- Prevents OOM errors
- Typical batch size: 50-100 comments

### 3. Professional Excel Export
- Executive summary sheet
- Detailed analysis by comment
- Emotion distribution analysis
- Pain points ranking
- Visual charts embedded
- Conditional formatting (color scales)

### 4. Real-Time Progress
- WebSocket-like polling
- Progress updates (5-95%)
- Per-batch completion tracking
- Estimated time remaining

### 5. Error Recovery
- Automatic JSON repair for truncated responses
- Fallback to local-only if OpenAI fails
- Exponential backoff retry logic
- Graceful degradation

---

## Storage Architecture

### Redis Keys
```
file_content:{task_id}     # Uploaded file (4-hour TTL)
task_status:{task_id}      # Processing status (24-hour TTL)
task_results:{task_id}     # Analysis results (24-hour TTL)
comment_cache:{hash}       # Cached analysis (7-day TTL)
```

### Why Redis?
- In-memory speed
- Automatic expiration (TTL)
- No persistent database needed
- Volatile-LRU eviction policy
- 25MB limit in production

---

## API Endpoints

### Core Routes
```
POST /upload                # Upload feedback file
GET /status/{task_id}       # Get processing status
GET /results/{task_id}      # Get analysis results
GET /export/{task_id}       # Export (Excel/CSV/both)
GET /health/simple          # Basic health check
GET /health/deep            # With dependencies
```

### Request/Response Example
```bash
# Upload
curl -X POST -F "file=@feedback.csv" http://api/upload

Response:
{
  "task_id": "abc123",
  "estimated_time_seconds": 45,
  "file_info": {
    "rows": 500,
    "format": "csv"
  }
}

# Status
curl http://api/status/abc123

Response:
{
  "status": "processing",
  "progress": 65,
  "message": "Analyzing batch 13 of 20",
  "processed_rows": 325
}

# Results
curl http://api/results/abc123

Response:
{
  "summary": {
    "total_comments": 500,
    "nps_score": 42,
    "emotions": {...},
    "top_pain_points": [...]
  },
  "detailed_results": [...],
  "metadata": {
    "processing_time": 43.2,
    "model_used": "gpt-4o-mini"
  }
}
```

---

## Frontend Architecture

### Pages
1. **Landing Page** - Welcome and feature overview
2. **Analyzer Page** - Main workflow (upload → results)
3. **About Page** - Documentation and FAQ

### Key Components
- **FileUpload** - Drag-and-drop file upload
- **ProgressTracker** - Real-time progress display
- **ResultsCharts** - Visualization suite
  - NPSChart (pie)
  - EmotionsChart (bar)
  - PainPointsChart (ranking)
  - ChurnRiskChart (heatmap)
  - SampleCommentsTable
- **ExportResults** - Download buttons

### Design System
- **Glass Design** - Modern frosted aesthetic
- **Dark/Light Mode** - Theme toggle
- **Responsive** - Mobile, tablet, desktop
- **Accessibility** - WCAG compliance

### Internationalization
- Spanish (es) - Primary
- English (en) - Secondary
- Auto-detection
- Manual toggle

---

## Project Structure

```
customer-feedback-app/
├── api/                    # Python FastAPI backend
│   ├── app/
│   │   ├── main.py        # FastAPI app
│   │   ├── routes/        # API endpoints
│   │   ├── services/      # Business logic
│   │   ├── adapters/      # AI integrations
│   │   ├── core/          # Data processing
│   │   ├── workers/       # Celery tasks
│   │   └── schemas/       # Pydantic models
│   ├── requirements.txt
│   └── start.sh
├── web/                    # React frontend
│   ├── src/
│   │   ├── App.tsx
│   │   ├── pages/
│   │   ├── components/
│   │   └── i18n/
│   ├── bff/
│   │   └── server.ts      # Node.js BFF proxy
│   ├── package.json
│   └── build.sh
├── docs/                   # Documentation
└── render.yaml             # Render deployment config
```

---

## Deployment (Render.com)

### Services Architecture
```
1. Redis (External Key-Value Store)
   - Type: keyvalue
   - Memory: volatile-lru
   - Max size: 25MB

2. FastAPI Backend (Private Service)
   - Type: Python Web Service
   - Port: 10000 (internal)
   - Start: uvicorn app.main:app
   - Health: /health/simple

3. Celery Worker (Background Worker)
   - Type: Background Worker
   - Start: celery worker
   - Concurrency: 4 workers

4. React BFF (Public Service)
   - Type: Node.js Web Service
   - Port: 3000 (public)
   - Start: Express BFF server
   - Proxy: /api → FastAPI
```

### Deployment Flow
```
1. Push to GitHub main
   ↓
2. Render webhook triggered
   ↓
3. Build steps:
   - pip install (Python deps)
   - npm install (Node deps)
   - npm run build (React build)
   ↓
4. Services start:
   - Redis first
   - FastAPI API
   - Celery Worker
   - Express BFF
   ↓
5. Health checks validate
```

---

## Configuration

### Environment Variables
```bash
# Application
APP_ENV=production
DEBUG=false
SECRET_KEY=<auto-generated>

# OpenAI
OPENAI_API_KEY=sk-...
AI_MODEL=gpt-4o-mini
OPENAI_TIMEOUT_SECONDS=30

# Redis
REDIS_URL=redis://host:6379/0
CELERY_BROKER_URL=redis://...
CELERY_RESULT_BACKEND=redis://...

# File Processing
FILE_MAX_MB=20
MAX_BATCH_SIZE=50
RESULTS_TTL_SECONDS=86400

# Hybrid Analysis
HYBRID_ANALYSIS_ENABLED=true
LOCAL_SENTIMENT_LIBRARY=vader

# Performance
CELERY_WORKER_CONCURRENCY=4
ENABLE_PARALLEL_PROCESSING=true
DYNAMIC_BATCH_SIZING=true
```

---

## Performance Metrics

### Processing Speed
```
100 comments:  ~3 seconds    ($0.002 cost)
500 comments:  ~12 seconds   ($0.010 cost)
1000 comments: ~25 seconds   ($0.020 cost)
3000 comments: ~75 seconds   ($0.060 cost)
```

### Accuracy
- Emotion detection: 92% precision
- Pain point identification: 88% precision
- Churn risk: ML-based probability

### System Reliability
- Success rate: >99%
- Availability: 99.9% SLA
- No data loss (Redis TTL)

---

## Business Value

### Target Customers
- Customer service teams
- Product management
- Marketing departments
- Executive leadership
- Any business with customer feedback

### Use Cases
1. **Customer Service** - Identify at-risk customers
2. **Product** - Discover pain points and feature requests
3. **Marketing** - Segment by satisfaction level
4. **Executive** - Track NPS trends and business health

### ROI
- **Time savings**: Automated analysis (vs. manual review)
- **Cost savings**: 87% cheaper than pure AI
- **Actionable insights**: Data-driven decisions
- **Churn prevention**: Early warning system

---

## Development Commands

```bash
# Backend
cd api
pip install -r requirements.txt
uvicorn app.main:app --reload

# Celery worker
celery -A app.workers.celery_app worker --loglevel=info

# Frontend
cd web
npm install
npm run dev

# BFF
cd web/bff
npm install
npm start
```

---

## Key Metrics

| Metric | Value |
|--------|-------|
| Cost Reduction | 87% vs traditional |
| Processing Speed | ~3s for 100 comments |
| Max File Size | 20MB |
| Max Rows | 3,000 |
| Emotions Detected | 7 |
| Pain Point Categories | 10+ |
| Export Formats | 2 (Excel, CSV) |
| Deployment Platform | Render.com |

---

## Current Status

### Production Features
- Complete feedback analysis
- Hybrid AI architecture
- Multi-format export
- Real-time progress
- Professional Excel reports
- Deployed on Render
- CI/CD integration

### Future Enhancements
- Advanced analytics dashboard
- Historical trend analysis
- Multi-tenant support
- API for integration
- Slack/Teams notifications

---

## Our Role

This is a **client project for Personal Paraguay**, demonstrating our capability to build:
1. Production-grade SaaS applications
2. Cost-efficient AI solutions
3. Professional data analysis tools
4. Modern web applications with React + FastAPI
5. Deployed, scalable infrastructure

The hybrid analysis approach showcases our innovative thinking in reducing AI costs while maintaining quality, making advanced AI analysis accessible to businesses of all sizes.
