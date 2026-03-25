# 🤖 ResumeAI — Intelligent Career Platform

AI-powered resume analyzer with job matching, ATS scoring, and personalized improvement suggestions.

## 🚀 Quick Start (3 Steps)

### Prerequisites
- Node.js 18+ → https://nodejs.org
- PostgreSQL 15+ → https://postgresql.org/download
- MongoDB 6+ → https://mongodb.com/try/download/community

---

## Step 1 — Create PostgreSQL Database

```bash
psql -U postgres
CREATE DATABASE resumeai;
\q
```

---

## Step 2 — Setup & Run Backend

```bash
cd backend
npm install
# Edit .env → change DB_PASS to your PostgreSQL password if needed
npm run seed     # Creates tables + loads 8 sample jobs + 2 test users
npm run dev      # Starts API on http://localhost:5000
```

✅ You should see:
```
PostgreSQL connected
MongoDB connected
Server running → http://localhost:5000
```

---

## Step 3 — Setup & Run Frontend

```bash
# Open a new terminal
cd frontend
npm install
npm start        # Opens http://localhost:3000
```

---

## 🔑 Test Credentials

| Role  | Email                 | Password   |
|-------|-----------------------|------------|
| Admin | admin@resumeai.com    | Admin@123  |
| User  | demo@resumeai.com     | Demo@123   |

---

## 📁 Project Structure

```
resumeai/
├── backend/
│   ├── .env                      ← DB config, JWT secret, OpenAI key
│   ├── src/
│   │   ├── app.js                ← Express entry point
│   │   ├── config/               ← database.js, mongodb.js, multer.js
│   │   ├── models/
│   │   │   ├── postgres/         ← User, Job, Application (Sequelize)
│   │   │   └── mongo/            ← Resume, Analysis (Mongoose)
│   │   ├── controllers/          ← auth, resume, job, analysis, admin
│   │   ├── services/
│   │   │   ├── resumeParser.js   ← PDF/DOCX text extraction
│   │   │   ├── jobMatcher.js     ← TF-IDF cosine similarity
│   │   │   └── aiAnalyzer.js     ← Rule-based + optional OpenAI
│   │   ├── routes/               ← All API routes
│   │   ├── middleware/           ← JWT auth, error handler
│   │   └── utils/                ← logger, seeder
└── frontend/
    └── src/
        ├── App.js                ← Routes + providers
        ├── context/              ← AuthContext, ResumeContext
        ├── services/             ← API calls (axios)
        └── components/
            ├── common/           ← Layout, LoginPage, styles
            ├── dashboard/        ← Dashboard with score + matches
            ├── upload/           ← Resume upload with progress
            ├── jobs/             ← Job matches with detail panel
            ├── analysis/         ← AI analysis + ATS report
            ├── suggestions/      ← Improvement suggestions
            ├── history/          ← Resume version history
            └── admin/            ← Admin panel (jobs + users)
```

---

## 🌐 API Endpoints

| Method | Path                              | Description            |
|--------|-----------------------------------|------------------------|
| POST   | /api/auth/register                | Create account         |
| POST   | /api/auth/login                   | Login → JWT token      |
| POST   | /api/resumes                      | Upload resume (multipart) |
| GET    | /api/resumes/latest               | Get latest resume      |
| GET    | /api/analysis/:resumeId           | Get full AI analysis   |
| GET    | /api/analysis/:resumeId/suggestions | Get suggestions      |
| GET    | /api/jobs                         | List all jobs          |
| GET    | /api/jobs/matches/:resumeId       | Get job matches        |
| POST   | /api/jobs/apply/:jobId            | Apply to a job         |
| POST   | /api/admin/jobs                   | Create job (admin)     |
| GET    | /api/admin/stats                  | Platform stats (admin) |

---

## ⚙️ Optional: OpenAI Integration

To enable GPT-powered suggestions, add your key to `backend/.env`:
```
OPENAI_API_KEY=sk-...
```
Without it, the platform uses the built-in rule-based AI (works great!).
