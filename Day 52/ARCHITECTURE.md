# ARCHITECTURE.md
## Insurance Eligibility Manager
**Day 2 — System Design**  
**Date:** September 7, 2026  

---

## 1. Tech Stack Decision

### Final Stack

| Layer | Technology | Reason | Cost |
|-------|-----------|--------|------|
| **Frontend Framework** | Vite + React 18 | Fastest scaffold for a single-page app; simpler than Next.js for a tool with no SSR requirements; massive community | Free |
| **Styling** | Tailwind CSS v3 | Utility-first; no design decisions in CSS files; fast to prototype; tree-shaken in production | Free |
| **Routing** | React Router v6 | Standard client-side routing for React SPAs; simple, declarative | Free |
| **Database** | Supabase (PostgreSQL) | Free tier covers this project entirely; auto-generates a REST API; built-in JS client; real database (not localStorage) means data persists across devices and sessions | Free |
| **Data Access** | Supabase JS Client v2 | Official SDK; handles all CRUD; no custom backend needed | Free |
| **Authentication** | None (v1.0) | Single-user tool; no login screen; data is accessed directly via Supabase anon key scoped to this project | Free |
| **Hosting** | Vercel | One-click deploy from GitHub; auto-redeploys on push; free hobby tier covers this app easily | Free |
| **Version Control** | GitHub | Standard; integrates directly with Vercel | Free |

### Why NOT Next.js?
Next.js adds server-side rendering complexity that this project doesn't need. Every page in this app is a client-side data fetch — no SEO, no pre-rendering benefit. Vite + React is faster to build and easier to debug for a 10-day sprint.

### Why NOT localStorage?
localStorage is device-specific and lost on browser clears. Supabase's free tier is more than enough for this project, and using a real database makes the capstone significantly more impressive and realistic.

### Why NO authentication?
The PRD explicitly scopes v1.0 as a single-user tool. Adding auth adds 1–2 days of complexity with no benefit in this phase. The Supabase anon key is scoped to only this project and deployed privately.

---

## 2. System Architecture

### High-Level Overview

```mermaid
graph TB
    User["👤 Benefits Rep<br/>(Desktop Browser)"]
    
    subgraph Frontend ["Frontend — Vercel CDN"]
        Vite["Vite + React SPA"]
        Router["React Router v6<br/>(Client-side routing)"]
        Pages["Pages<br/>Dashboard · Customers<br/>Add Customer · Detail<br/>Log Check"]
        Hooks["Custom Hooks<br/>useCustomers · useChecks"]
        SDK["Supabase JS Client v2"]
    end
    
    subgraph Supabase ["Supabase (Cloud)"]
        API["Auto-generated REST API<br/>(PostgREST)"]
        DB["PostgreSQL Database<br/>customers · eligibility_checks"]
        RLS["Row Level Security<br/>(anon key policy)"]
    end
    
    User -->|"HTTP / HTTPS"| Vite
    Vite --> Router
    Router --> Pages
    Pages --> Hooks
    Hooks --> SDK
    SDK -->|"HTTPS REST"| API
    API --> RLS
    RLS --> DB
```

### Component Architecture

```mermaid
graph TD
    App["App.jsx<br/>(Router shell)"]
    
    App --> Dashboard
    App --> CustomersList
    App --> AddCustomer
    App --> CustomerDetail
    App --> LogCheck

    Dashboard --> StatTile
    Dashboard --> RecentActivity
    
    CustomersList --> SearchBar
    CustomersList --> CustomerCard

    CustomerDetail --> EligibilitySummaryCard
    CustomerDetail --> CheckHistoryList
    CustomerDetail --> NavButton["Log New Check button"]

    LogCheck --> EligibilityForm

    subgraph Shared ["Shared Components (src/components/ui/)"]
        Button
        Input
        Select
        Textarea
        Card
        Badge
        EmptyState
        Spinner
    end
```

### Data Flow

```mermaid
sequenceDiagram
    participant User
    participant Page as React Page
    participant Hook as Custom Hook
    participant SDK as Supabase SDK
    participant DB as PostgreSQL

    User->>Page: Lands on Customer Detail
    Page->>Hook: useCustomer(id) + useChecks(customerId)
    Hook->>SDK: supabase.from('customers').select()
    Hook->>SDK: supabase.from('eligibility_checks').select()
    SDK->>DB: REST GET /customers?id=eq.{id}
    SDK->>DB: REST GET /eligibility_checks?customer_id=eq.{id}
    DB-->>SDK: rows[]
    SDK-->>Hook: { data, error }
    Hook-->>Page: { customer, checks, loading }
    Page-->>User: Renders summary card + history

    User->>Page: Clicks "Log New Check"
    Page->>Page: Navigate to /log-check?customerId={id}
    User->>Page: Fills form + submits
    Page->>Hook: logCheck(formData)
    Hook->>SDK: supabase.from('eligibility_checks').insert()
    SDK->>DB: REST POST /eligibility_checks
    DB-->>SDK: { id, ...newRow }
    SDK-->>Hook: { data, error }
    Hook-->>Page: success
    Page-->>User: Redirect to Customer Detail
```

---

## 3. Request Lifecycle

For every data operation in the app:

```
1. User interaction (click, form submit)
2. React event handler fires
3. Custom hook function called (e.g., useChecks().logCheck(data))
4. Input validated client-side (required fields, types)
5. Supabase SDK constructs REST request
6. HTTPS request to Supabase PostgREST endpoint
7. RLS policy checked (anon key grants full access to this project's tables)
8. PostgreSQL executes query
9. Response returned to SDK
10. Hook updates React state (data / error / loading)
11. Page re-renders with new state
12. User sees updated UI or error message
```

---

## 4. External Services

| Service | Purpose | Free Tier Limits | Used For |
|---------|---------|-----------------|---------|
| **Supabase** | Database + REST API | 500MB storage, 2GB bandwidth/month, unlimited API calls | All data storage and retrieval |
| **Vercel** | Hosting + CDN | 100GB bandwidth/month, unlimited deploys | Serving the React app |
| **GitHub** | Version control | Unlimited public/private repos | Source control + Vercel integration |
| **Google Fonts** | Typography | Unlimited | UI fonts |

All limits are far beyond what a single-user tool handling 6–7 checks/day will ever reach.

---

## 5. Security Considerations (v1.0)

- Supabase anon key is **not a secret** — it's designed to be used client-side
- Row Level Security (RLS) is enabled on both tables with an `anon` select/insert/update/delete policy
- No PII beyond name and DOB is stored (no SSN, no contact info)
- The app is deployed privately on Vercel (URL not publicly advertised)
- No HIPAA compliance required for this capstone personal tool

---

## 6. Deployment Architecture

```mermaid
graph LR
    Dev["Local Dev<br/>localhost:5173"]
    GitHub["GitHub<br/>main branch"]
    Vercel["Vercel CDN<br/>insurance-eligibility-manager.vercel.app"]
    Supabase["Supabase<br/>Cloud Database"]

    Dev -->|"git push"| GitHub
    GitHub -->|"Auto-deploy trigger"| Vercel
    Vercel -->|"Serves SPA"| Browser["User's Browser"]
    Browser -->|"API calls"| Supabase
```

**Workflow:** Every `git push` to `main` triggers an automatic Vercel redeploy. No manual deployment steps after initial setup.

---

*ARCHITECTURE.md — Insurance Eligibility Manager v1.0*
