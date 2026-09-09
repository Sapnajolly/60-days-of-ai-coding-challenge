# PROJECT-STRUCTURE.md
## Insurance Eligibility Manager — Folder Structure
**Day 2 — System Design**  
**Stack:** Vite + React + Tailwind CSS + Supabase  

---

## Full Folder Structure

```
insurance-eligibility-manager/
│
├── public/
│   └── favicon.ico                    # App favicon
│
├── src/
│   │
│   ├── lib/
│   │   └── supabase.js                # Supabase client — initialized once, imported everywhere
│   │
│   ├── hooks/
│   │   ├── useCustomers.js            # All customer CRUD operations
│   │   ├── useChecks.js               # All eligibility check CRUD operations
│   │   └── useDashboard.js            # Dashboard stats + recent activity
│   │
│   ├── components/
│   │   │
│   │   ├── ui/                        # Base reusable components (no business logic)
│   │   │   ├── Button.jsx             # Primary, secondary, ghost variants
│   │   │   ├── Input.jsx              # Text, date, number inputs with label + error
│   │   │   ├── Select.jsx             # Dropdown with label + error
│   │   │   ├── Textarea.jsx           # Multi-line text input
│   │   │   ├── Card.jsx               # Generic card wrapper
│   │   │   ├── Badge.jsx              # Status badges (Active, Expired, etc.)
│   │   │   ├── Spinner.jsx            # Loading indicator
│   │   │   └── EmptyState.jsx         # Empty list state with icon + message + CTA
│   │   │
│   │   ├── layout/
│   │   │   ├── Navbar.jsx             # Top navigation bar
│   │   │   └── PageWrapper.jsx        # Consistent page padding/max-width wrapper
│   │   │
│   │   ├── CustomerCard.jsx           # Customer row/card used in the list
│   │   ├── EligibilitySummaryCard.jsx # The main callback-reference card
│   │   ├── CheckHistoryList.jsx       # Collapsible list of past checks
│   │   ├── CheckHistoryRow.jsx        # Single collapsed/expanded row in history
│   │   ├── StatTile.jsx               # Dashboard stat tile (number + label)
│   │   └── RecentActivity.jsx         # Dashboard recent checks list
│   │
│   ├── pages/
│   │   ├── Dashboard.jsx              # Route: /
│   │   ├── CustomersList.jsx          # Route: /customers
│   │   ├── AddCustomer.jsx            # Route: /customers/new
│   │   ├── CustomerDetail.jsx         # Route: /customers/:id
│   │   └── LogCheck.jsx               # Route: /customers/:id/check
│   │
│   ├── utils/
│   │   ├── formatters.js              # Date, currency, plan type formatters
│   │   └── validators.js              # Form validation functions
│   │
│   ├── App.jsx                        # Router setup — defines all routes
│   ├── main.jsx                       # React entry point — mounts App
│   └── index.css                      # Tailwind directives + global CSS resets
│
├── .env.local                         # VITE_SUPABASE_URL and VITE_SUPABASE_ANON_KEY (gitignored)
├── .env.example                       # Template showing required env vars (committed to git)
├── .gitignore                         # node_modules, .env.local, dist/
├── index.html                         # Vite HTML entry point
├── package.json                       # Dependencies and scripts
├── tailwind.config.js                 # Tailwind configuration
├── vite.config.js                     # Vite configuration
└── README.md                          # Project description + setup instructions
```

---

## Folder Responsibilities

### `src/lib/`
**One job:** Initialize and export the Supabase client. Every hook and component imports `supabase` from here. This is the single place where credentials are consumed.

```js
// src/lib/supabase.js
import { createClient } from '@supabase/supabase-js'
export const supabase = createClient(
  import.meta.env.VITE_SUPABASE_URL,
  import.meta.env.VITE_SUPABASE_ANON_KEY
)
```

---

### `src/hooks/`
**One job:** All database operations. Pages and components never call Supabase directly — they call hooks. This keeps database logic out of UI components and makes it easy to swap the data layer later.

| Hook | Exports |
|------|---------|
| `useCustomers.js` | `customers`, `loading`, `error`, `createCustomer(data)` |
| `useChecks.js` | `checks`, `loading`, `error`, `logCheck(data)` — takes `customerId` as argument |
| `useDashboard.js` | `stats`, `recentChecks`, `loading` |

---

### `src/components/ui/`
**One job:** Low-level, reusable building blocks. No Supabase imports. No business logic. Just styled React components that accept props and render consistently. These are built once on Day 3 and reused throughout.

Example: `Input.jsx` accepts `label`, `error`, `type`, and all standard HTML input props. It renders the label, input, and error message in a consistent style.

---

### `src/components/layout/`
**One job:** App shell and page structure. `Navbar.jsx` is rendered once in `App.jsx` and appears on every page. `PageWrapper.jsx` applies consistent horizontal padding and max-width.

---

### `src/components/` (root level)
**One job:** Business-logic components that know about the app's data model. These import from `hooks/` and render data. `EligibilitySummaryCard.jsx` takes a `check` object and renders the full callback reference card. `CustomerCard.jsx` takes a `customer` object and renders a list row.

---

### `src/pages/`
**One job:** Route-level components. Each page:
1. Gets its data via hooks
2. Handles loading and error states
3. Renders the appropriate components
4. Handles navigation (using `useNavigate` from React Router)

Pages are thin orchestrators — they don't contain business logic or styling decisions.

---

### `src/utils/`
**One job:** Pure utility functions with no React dependencies.

| File | Contains |
|------|---------|
| `formatters.js` | `formatDate(isoString)` → "Sep 7, 2026" · `formatCurrency(num)` → "$1,500.00" · `formatPlanType(str)` → "PPO" |
| `validators.js` | `validateCustomerForm(data)` → `{ errors }` · `validateCheckForm(data)` → `{ errors }` |

---

### `src/App.jsx`
**One job:** Define all routes and render the nav shell.

```jsx
import { BrowserRouter, Routes, Route } from 'react-router-dom'
import Navbar from './components/layout/Navbar'
import Dashboard from './pages/Dashboard'
import CustomersList from './pages/CustomersList'
import AddCustomer from './pages/AddCustomer'
import CustomerDetail from './pages/CustomerDetail'
import LogCheck from './pages/LogCheck'

export default function App() {
  return (
    <BrowserRouter>
      <Navbar />
      <Routes>
        <Route path="/"                        element={<Dashboard />} />
        <Route path="/customers"               element={<CustomersList />} />
        <Route path="/customers/new"           element={<AddCustomer />} />
        <Route path="/customers/:id"           element={<CustomerDetail />} />
        <Route path="/customers/:id/check"     element={<LogCheck />} />
      </Routes>
    </BrowserRouter>
  )
}
```

---

## Why This Structure?

1. **Separation of concerns** — UI, data access, and business logic are never mixed in the same file.
2. **No prop drilling** — Hooks manage all state. Components request what they need directly.
3. **Predictable file locations** — A new developer (or your future self on Day 8) can find any piece of the app in under 30 seconds.
4. **Scales cleanly** — Adding a new feature (a new page, a new data entity) follows the same pattern: new hook → new page → new components.
5. **Easy to test** — Validators and formatters in `utils/` are pure functions with no dependencies — trivial to unit test.

---

## Dependencies (package.json)

```json
{
  "dependencies": {
    "react": "^18.3.1",
    "react-dom": "^18.3.1",
    "react-router-dom": "^6.26.0",
    "@supabase/supabase-js": "^2.45.0"
  },
  "devDependencies": {
    "@vitejs/plugin-react": "^4.3.0",
    "autoprefixer": "^10.4.20",
    "postcss": "^8.4.41",
    "tailwindcss": "^3.4.10",
    "vite": "^5.4.0"
  }
}
```

Total runtime dependencies: **2** (React + Supabase). Small, fast, auditable.

---

## Environment Variables

```bash
# .env.example (commit this)
VITE_SUPABASE_URL=your_supabase_project_url_here
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key_here
```

```bash
# .env.local (DO NOT commit — already in .gitignore)
VITE_SUPABASE_URL=https://xyzxyz.supabase.co
VITE_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

Vite requires the `VITE_` prefix for any env variable used in frontend code.

---

*PROJECT-STRUCTURE.md — Insurance Eligibility Manager v1.0*
