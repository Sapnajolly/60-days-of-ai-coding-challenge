# Day 53 — Insurance Eligibility Manager
## AB Talks 60-Day Claude AI Challenge

---

## Project Overview
Building an Insurance Eligibility Manager as the capstone project for the 60-Day Claude AI Challenge. Used by agents during customer callbacks to log and retrieve insurance eligibility data.

---

## Tech Stack
- **Vite v8.2.2** — build tool / dev server
- **React 18** — UI framework with hooks (useState, useEffect)
- **Tailwind CSS v4** — configured via `@tailwindcss/vite` plugin; single `@import "tailwindcss"` in index.css
- **React Router v6** — BrowserRouter, Routes, Route, useParams, useNavigate, Link
- **Supabase** — PostgreSQL backend + REST API, JS Client v2
- **PowerShell** — used for all terminal commands on Windows

## Project Path
`C:\Users\rrus3\insurance-eligibility-manager`

## Dev Server
Runs at `http://localhost:5174` (or :5176)

---

## Supabase Setup

### Project
- Name: Sapnajolly's Project
- URL: `https://ciofzjvywztiwgjikwlm.supabase.co`
- **VITE_SUPABASE_URL** = base domain only — no `/rest/v1` suffix

### Database Schema (created in SQL Editor)

**Table: `customers`**
| Column | Type | Notes |
|---|---|---|
| id | UUID | Primary Key, auto-generated |
| name | text | |
| date_of_birth | date | |
| insurance_company | text | |
| created_at | timestamptz | default now() |

**Table: `eligibility_checks`**
| Column | Type | Notes |
|---|---|---|
| id | UUID | Primary Key |
| customer_id | UUID | FK → customers.id, CASCADE delete |
| member_id | text | |
| coverage_start_date | date | |
| coverage_end_date | date | |
| plan_type | text | CHECK: HMO/PPO/EPO/POS/Other |
| deductible_individual | numeric | |
| deductible_family | numeric | |
| copay_primary_care | numeric | |
| copay_specialist | numeric | |
| notes | text | |
| checked_at | timestamptz | default now() |

### RLS (Row Level Security)
- Enabled on both tables
- Anon full access policy on both tables (INSERT, SELECT, UPDATE, DELETE)

---

## ✅ Day 3 — Complete

### What Was Built

#### Project Scaffold
All folders and placeholder files created:
```
insurance-eligibility-manager/
├── src/
│   ├── lib/
│   │   └── supabase.js
│   ├── hooks/
│   │   ├── useCustomers.js   (placeholder)
│   │   └── useChecks.js      (placeholder)
│   ├── pages/
│   │   ├── Dashboard.jsx     (placeholder)
│   │   ├── CustomersList.jsx (placeholder)
│   │   ├── AddCustomer.jsx   (placeholder)
│   │   ├── LogCheck.jsx      (placeholder)
│   │   └── CustomerDetail.jsx(placeholder)
│   ├── App.jsx
│   ├── App.css               (empty)
│   └── index.css
├── .env.local                (NEVER commit — real credentials)
├── .env.example              (safe to commit — placeholders only)
├── .gitignore
├── vite.config.js
└── package.json
```

#### Key Files

**`src/lib/supabase.js`**
```js
import { createClient } from '@supabase/supabase-js'
const supabaseUrl = import.meta.env.VITE_SUPABASE_URL
const supabaseAnonKey = import.meta.env.VITE_SUPABASE_ANON_KEY
export const supabase = createClient(supabaseUrl, supabaseAnonKey)
```

**`vite.config.js`**
```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
  plugins: [react(), tailwindcss()],
})
```

**`src/index.css`**
```css
@import "tailwindcss";
```

**`src/App.jsx`** — React Router setup
```jsx
import { BrowserRouter, Routes, Route } from 'react-router-dom'
// Routes:
// /                   → Dashboard
// /customers          → CustomersList
// /customers/new      → AddCustomer
// /customers/:id      → CustomerDetail
// /customers/:id/log  → LogCheck
```

**`.env.local`** (NEVER commit — real credentials)
```
VITE_SUPABASE_URL=https://ciofzjvywztiwgjikwlm.supabase.co
VITE_SUPABASE_ANON_KEY=<real anon key>
```

**`.env.example`** (safe to commit — placeholders only)
```
VITE_SUPABASE_URL=your_supabase_project_url_here
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key_here
```

#### Navigation Shell
- Blue top nav bar with: **InsuranceEM** logo | Dashboard | Customers | Add Customer
- Renders on all pages via App.jsx layout wrapper

### Git Setup
```powershell
git init
git add .
git commit -m "Day 3: project scaffold, Tailwind, Supabase, nav shell"
git remote add origin https://github.com/Sapnajolly/insurance-eligibility-manager.git
git push -u origin main   # ⛔ BLOCKED — see below
```

---

## Errors & Fixes

| Error | Cause | Fix |
|---|---|---|
| `.env.example` had real anon key | User accidentally pasted real credentials | Replaced with placeholder text immediately — before any commit |
| `fatal: not a git repository` | `git add .` run before `git init` | Ran `git init` first |
| `git push` 403 error | GitHub account `Sapnajolly` is suspended | Pending resolution at https://support.github.com |
| `remote origin already exists` | Remote already set from earlier attempt | Harmless — ignored |
| `npm run dev` ENOENT error | Run from wrong directory (`C:\Users\rrus3` instead of project folder) | `cd C:\Users\rrus3\insurance-eligibility-manager` then `npm run dev` |

---

## Security Rules (MUST NEVER BE VIOLATED)
- `.env.local` must **NEVER** be committed to GitHub
- `.env.example` must contain **only placeholder text** — never real credentials
- `*.local` is covered by `.gitignore`
- Real Supabase anon key lives **only** in `.env.local`

---

## Project State at End of Day 3

| Item | Status |
|---|---|
| Vite + React + Tailwind installed | ✅ |
| Supabase tables created | ✅ |
| RLS policies set | ✅ |
| supabase.js client configured | ✅ |
| Nav shell rendering | ✅ |
| .env.local created (local only) | ✅ |
| .env.example created (safe) | ✅ |
| Git initialized + committed | ✅ |
| GitHub push | ⏳ Blocked — Sapnajolly account suspended |
| Page files | ⏳ Placeholder only — filled in Day 4 |

---

## Next: Day 4
- Fill in `useCustomers.js`, `useChecks.js`
- Build `Dashboard.jsx`, `CustomersList.jsx`, `AddCustomer.jsx`, `LogCheck.jsx`
- Core feature: log eligibility check form saving to Supabase
