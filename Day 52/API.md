# API.md
## Insurance Eligibility Manager — Data Access Layer
**Day 2 — System Design**  
**Note:** This app has no custom backend. All data access goes through the Supabase JS Client v2, which communicates with Supabase's auto-generated PostgREST API. This document describes each logical operation as if it were an endpoint.

---

## Base Configuration

```js
// src/lib/supabase.js
import { createClient } from '@supabase/supabase-js'

const supabaseUrl  = import.meta.env.VITE_SUPABASE_URL
const supabaseKey  = import.meta.env.VITE_SUPABASE_ANON_KEY

export const supabase = createClient(supabaseUrl, supabaseKey)
```

All operations below are performed using this client.

---

## Customers

---

### GET /customers — List All Customers

**Purpose:** Fetch all customers for the list page and dashboard.

**Hook:** `useCustomers().customers`

```js
const { data, error } = await supabase
  .from('customers')
  .select('*')
  .order('created_at', { ascending: false })
```

**Response — Success:**
```json
[
  {
    "id": "uuid",
    "name": "Maria Johnson",
    "date_of_birth": "1985-04-12",
    "insurance_company": "Aetna",
    "created_at": "2026-09-07T14:30:00Z"
  }
]
```

**Response — Empty:**
```json
[]
```

**Error Cases:**
| Error | Cause | UI Behavior |
|-------|-------|-------------|
| Network error | No internet | Show "Unable to load customers. Check your connection." |
| Supabase error | Misconfigured keys | Show "Something went wrong. Please refresh." |

---

### GET /customers/:id — Get Single Customer

**Purpose:** Fetch one customer record for the detail page.

**Hook:** `useCustomer(id).customer`

```js
const { data, error } = await supabase
  .from('customers')
  .select('*')
  .eq('id', customerId)
  .single()
```

**Response — Success:**
```json
{
  "id": "uuid",
  "name": "Maria Johnson",
  "date_of_birth": "1985-04-12",
  "insurance_company": "Aetna",
  "created_at": "2026-09-07T14:30:00Z"
}
```

**Error Cases:**
| Error | Cause | UI Behavior |
|-------|-------|-------------|
| `PGRST116` (no rows) | ID not found | Redirect to Customers list with toast "Customer not found" |
| Network error | No internet | Show error state on detail page |

---

### GET /customers?name=search — Search Customers

**Purpose:** Filter customers by name in real time (client-side, not a separate API call).

**Implementation:** Filter the already-fetched `customers` array in component state.

```js
const filtered = customers.filter(c =>
  c.name.toLowerCase().includes(query.toLowerCase())
)
```

**Note:** With 6–7 checks per day, the customers list will never exceed a few hundred records. Client-side filtering is fast enough — no server-side search endpoint needed.

---

### POST /customers — Create Customer

**Purpose:** Save a new customer from the Add Customer form.

**Hook:** `useCustomers().createCustomer(data)`

```js
const { data, error } = await supabase
  .from('customers')
  .insert({
    name:              formData.name.trim(),
    date_of_birth:     formData.dateOfBirth,
    insurance_company: formData.insuranceCompany.trim()
  })
  .select()
  .single()
```

**Request Body (form fields):**
```json
{
  "name":              "Maria Johnson",
  "dateOfBirth":       "1985-04-12",
  "insuranceCompany":  "Aetna"
}
```

**Validation (client-side before insert):**
| Field | Rule |
|-------|------|
| `name` | Required, non-empty after trim, max 100 chars |
| `dateOfBirth` | Required, valid date, not in the future |
| `insuranceCompany` | Required, non-empty after trim, max 100 chars |

**Response — Success:**
```json
{
  "id": "new-uuid",
  "name": "Maria Johnson",
  "date_of_birth": "1985-04-12",
  "insurance_company": "Aetna",
  "created_at": "2026-09-07T14:30:00Z"
}
```

**On success:** Navigate to `/customer/:newId`

**Error Cases:**
| Error | Cause | UI Behavior |
|-------|-------|-------------|
| Validation fail | Empty field | Show inline field error, do not submit |
| Supabase error | Insert failed | Show toast "Failed to save customer. Try again." |

---

### DELETE /customers/:id — Delete Customer

**Note:** Not in v1.0 UI but supported at database level (cascade). No delete button is exposed in the interface.

---

## Eligibility Checks

---

### GET /eligibility_checks?customer_id=:id — List Checks for Customer

**Purpose:** Fetch all checks for a customer. Used on the Customer Detail page for both the summary card (most recent) and the history list (all).

**Hook:** `useChecks(customerId).checks`

```js
const { data, error } = await supabase
  .from('eligibility_checks')
  .select('*')
  .eq('customer_id', customerId)
  .order('checked_at', { ascending: false })
```

**Response — Success:**
```json
[
  {
    "id": "uuid",
    "customer_id": "customer-uuid",
    "member_id": "AET123456789",
    "coverage_start_date": "2026-01-01",
    "coverage_end_date": "2026-12-31",
    "plan_type": "PPO",
    "deductible_individual": 1500.00,
    "deductible_family": 3000.00,
    "copay_primary_care": 25.00,
    "copay_specialist": 50.00,
    "notes": "Active. Confirmed by rep James at Aetna.",
    "checked_at": "2026-09-07T14:30:00Z"
  }
]
```

**Derived data in the component:**
- `checks[0]` = most recent check → shown in the Summary Card
- `checks` (all) = shown in the History list

**Error Cases:**
| Error | Cause | UI Behavior |
|-------|-------|-------------|
| Empty array | No checks yet | Show "No checks logged yet" empty state with Log Check button |
| Network error | No internet | Show error state |

---

### GET /eligibility_checks — Get Recent Checks (Dashboard)

**Purpose:** Show the last 5 checks across all customers on the dashboard.

**Hook:** `useDashboard().recentChecks`

```js
const { data, error } = await supabase
  .from('eligibility_checks')
  .select(`
    id,
    checked_at,
    plan_type,
    customers ( name, insurance_company )
  `)
  .order('checked_at', { ascending: false })
  .limit(5)
```

**Note:** Uses a Supabase join to pull the customer name alongside each check.

**Response:**
```json
[
  {
    "id": "uuid",
    "checked_at": "2026-09-07T14:30:00Z",
    "plan_type": "PPO",
    "customers": {
      "name": "Maria Johnson",
      "insurance_company": "Aetna"
    }
  }
]
```

---

### POST /eligibility_checks — Log New Check

**Purpose:** Save a new eligibility check from the Log Check form.

**Hook:** `useChecks(customerId).logCheck(data)`

```js
const { data, error } = await supabase
  .from('eligibility_checks')
  .insert({
    customer_id:           customerId,
    member_id:             formData.memberId.trim(),
    coverage_start_date:   formData.coverageStartDate,
    coverage_end_date:     formData.coverageEndDate,
    plan_type:             formData.planType,
    deductible_individual: parseFloat(formData.deductibleIndividual),
    deductible_family:     parseFloat(formData.deductibleFamily),
    copay_primary_care:    parseFloat(formData.copayPrimaryCare),
    copay_specialist:      parseFloat(formData.copaySpecialist),
    notes:                 formData.notes?.trim() || null
  })
  .select()
  .single()
```

**Request Body (form fields):**
```json
{
  "customerId":           "customer-uuid",
  "memberId":             "AET123456789",
  "coverageStartDate":    "2026-01-01",
  "coverageEndDate":      "2026-12-31",
  "planType":             "PPO",
  "deductibleIndividual": "1500",
  "deductibleFamily":     "3000",
  "copayPrimaryCare":     "25",
  "copaySpecialist":      "50",
  "notes":                "Active. Confirmed by rep James."
}
```

**Validation (client-side before insert):**
| Field | Rule |
|-------|------|
| `memberId` | Required, non-empty |
| `coverageStartDate` | Required, valid date |
| `coverageEndDate` | Required, valid date, must be after start date |
| `planType` | Required, must be one of: HMO, PPO, EPO, POS, Other |
| `deductibleIndividual` | Required, number ≥ 0 |
| `deductibleFamily` | Required, number ≥ 0 |
| `copayPrimaryCare` | Required, number ≥ 0 |
| `copaySpecialist` | Required, number ≥ 0 |
| `notes` | Optional |

**Response — Success:**
```json
{
  "id": "new-check-uuid",
  "customer_id": "customer-uuid",
  "member_id": "AET123456789",
  ...
  "checked_at": "2026-09-07T14:30:00Z"
}
```

**On success:** Navigate to `/customer/:customerId`

**Error Cases:**
| Error | Cause | UI Behavior |
|-------|-------|-------------|
| Validation fail | Invalid/empty field | Show inline field error, keep form open |
| `coverageEndDate` before start | Date logic error | "End date must be after start date" |
| Supabase insert error | Network/DB issue | Show toast "Failed to save check. Try again." |

---

## Dashboard Stats

**Purpose:** Power the stat tiles on the Dashboard page.

**Hook:** `useDashboard().stats`

```js
// Total customers
const { count: totalCustomers } = await supabase
  .from('customers')
  .select('*', { count: 'exact', head: true })

// Checks today
const today = new Date().toISOString().split('T')[0]
const { count: checksToday } = await supabase
  .from('eligibility_checks')
  .select('*', { count: 'exact', head: true })
  .gte('checked_at', `${today}T00:00:00Z`)
  .lte('checked_at', `${today}T23:59:59Z`)

// Most recent check (for "Last Check" stat)
const { data: lastCheck } = await supabase
  .from('eligibility_checks')
  .select('checked_at, customers(name)')
  .order('checked_at', { ascending: false })
  .limit(1)
  .single()
```

---

## Error Handling Standards

All hooks follow this pattern:

```js
const [data, setData]       = useState(null)
const [loading, setLoading] = useState(true)
const [error, setError]     = useState(null)

try {
  setLoading(true)
  const { data, error } = await supabase.from(...)...
  if (error) throw error
  setData(data)
} catch (err) {
  setError(err.message)
} finally {
  setLoading(false)
}
```

Every page that calls a hook renders three states:
1. **Loading:** Spinner component
2. **Error:** Error message with retry option
3. **Success:** The actual UI

---

*API.md — Insurance Eligibility Manager v1.0*
