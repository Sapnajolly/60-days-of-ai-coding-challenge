# Implementation Blueprint — Days 2–10
## Insurance Eligibility Manager
**Challenge:** AB Talks 60-Day Claude AI Challenge  
**Builder:** Orbit (Orbit Boyzz)  
**Project:** Insurance Eligibility Manager — a web app to log, organize, and retrieve insurance eligibility data during customer benefit callbacks.

---

## How to Use This Document

This blueprint is the **single source of truth** for Days 2–10. Each day's section is self-contained — it includes enough context that a fresh AI assistant can guide you through that day's work from start to finish without needing to re-plan or redesign anything.

At the start of each day, paste the relevant day's section into a new AI conversation along with this project summary:

> **Project:** Insurance Eligibility Manager — a web app where a benefits professional can add customers, log insurance eligibility data (member ID, coverage dates, plan type, deductible, co-payment), view a clean summary per customer, and search/browse check history. Single-user. Desktop-first. Free deployment.

---

## Project Summary

| Field | Value |
|-------|-------|
| App Name | Insurance Eligibility Manager |
| Type | Web application |
| Primary User | Solo benefits/insurance rep |
| Core Workflow | Add customer → Log eligibility check → View summary for callback |
| Key Data | Member ID, coverage dates, plan type, deductible, co-payment |
| Deployment Target | Free hosting (determined Day 2) |
| Database | To be selected Day 2 |

---

## Day 2 — Tech Stack, Setup & Project Scaffold

### 🎯 Objective
Choose the tech stack, set up the development environment, initialize the project, and get a "Hello World" running locally.

### 📖 What You'll Learn
- How to scaffold a modern web project
- How to structure a full-stack or frontend-only project
- How version control works with Git

### 🛠 Features to Build
- Blank app running locally with routing
- Navigation shell (sidebar or top nav with placeholder pages: Customers, Add Check, History)
- Basic color scheme and font applied

### 📝 Step-by-Step Implementation Plan

**Step 1 — Choose your stack**
Tell your AI assistant: "I'm building a single-user web app with a form, a list view, and a detail view. I want the simplest free stack possible. Recommend between Next.js + Supabase, plain React + localStorage, and Vite + SQLite. I'm comfortable with JavaScript."

Let the AI recommend based on your comfort level. Most likely recommendation: **Next.js (React) + Supabase** (free tier covers this easily) or **Vite + React + localStorage** (zero backend needed).

**Step 2 — Install prerequisites**
- Node.js (LTS version) — download from nodejs.org
- Git — download from git-scm.com
- VS Code — download from code.visualstudio.com

**Step 3 — Initialize the project**
Follow your AI's exact commands to scaffold the project (e.g., `npm create vite@latest` or `npx create-next-app@latest`).

**Step 4 — Create a GitHub repository**
- Go to github.com → New Repository
- Name it: `insurance-eligibility-manager`
- Initialize with README
- Clone it locally

**Step 5 — Push scaffold to GitHub**
Follow your AI's git commands: `git add .`, `git commit -m "initial scaffold"`, `git push`.

**Step 6 — Build the nav shell**
Create placeholder pages/components: Customers, Add Check, History. Apply basic styling.

### 📂 Files and Folders to Create
```
insurance-eligibility-manager/
├── src/
│   ├── components/
│   │   └── Navbar.jsx
│   ├── pages/ (or app/ if Next.js)
│   │   ├── index.jsx        ← Customers list (placeholder)
│   │   ├── add-check.jsx    ← Add check form (placeholder)
│   │   └── history.jsx      ← History view (placeholder)
│   ├── App.jsx
│   └── main.jsx
├── public/
├── package.json
└── README.md
```

### 🔗 Tools & Services
- Node.js + npm
- Git + GitHub (free)
- VS Code
- Vite or Next.js (free, open source)

### 🧪 Testing Tasks
- Confirm the app runs locally without errors (`npm run dev`)
- Confirm all three placeholder pages are reachable by clicking nav links
- Confirm changes are pushed to GitHub

### 🐞 Common Issues
- `npm` not found → Node.js not installed correctly; reinstall from nodejs.org
- Port already in use → Change port with `npm run dev -- --port 3001`
- Git push rejected → Make sure you cloned the repo before adding files

### ✅ End-of-Day Checklist
- [ ] Tech stack chosen and documented
- [ ] Project scaffold created and running locally
- [ ] GitHub repo created and code pushed
- [ ] Three placeholder pages accessible via navigation
- [ ] Basic styling applied (colors, font, layout)

### 📸 Screenshots to Capture
- App running in browser showing the nav and placeholder pages
- GitHub repo showing the pushed code

### ➡️ Handoff to Day 3
Note your exact stack choice (e.g., "Vite + React + localStorage" or "Next.js + Supabase") and paste it at the top of Day 3's AI prompt. The Day 3 AI will need to know this to guide the correct data layer setup.

---

## Day 3 — Data Layer & Customer Management

### 🎯 Objective
Set up the data layer and build the full customer management feature: add a customer, list all customers, and search by name.

### 📖 What You'll Learn
- How to design a simple data schema
- How to create, read, and display data
- How to implement live search/filter

### 🛠 Features to Build
- Customer data model (name, date of birth, insurance company, created date)
- Add Customer form with validation
- Customer list page with all customers displayed as cards
- Search bar that filters customers by name in real time

### 📝 Step-by-Step Implementation Plan

**Step 1 — Define the data schema**
Show your AI this schema and confirm it before building:
```
Customer {
  id: unique identifier
  name: string (required)
  dateOfBirth: string (required)
  insuranceCompany: string (required)
  createdAt: timestamp
}
```

**Step 2 — Set up the data layer**
- If using localStorage: create a `useCustomers` hook or utility file that handles CRUD operations against localStorage.
- If using Supabase: create the `customers` table in Supabase dashboard, configure the client, set up the SDK.

**Step 3 — Build Add Customer form**
Fields: Full Name, Date of Birth, Insurance Company. Add form validation (all fields required). On submit, save to data layer and redirect to customer list.

**Step 4 — Build Customer List page**
Display all customers as a list or card grid. Each card shows: name, insurance company, date of birth, and a "View" button.

**Step 5 — Add search/filter**
Add a text input above the list. Filter the displayed customers in real time as the user types (client-side filtering on name field).

### 📂 Files and Folders to Create/Modify
```
src/
├── components/
│   ├── CustomerCard.jsx       ← Single customer display component
│   └── SearchBar.jsx          ← Reusable search input
├── hooks/ (if applicable)
│   └── useCustomers.js        ← Data access hook
├── pages/
│   ├── index.jsx              ← Customer list (replace placeholder)
│   └── add-customer.jsx       ← New: Add customer form
├── lib/ (if applicable)
│   └── storage.js             ← localStorage or Supabase client
```

### 🔗 Tools & Services
- Supabase (if chosen) — supabase.com, free tier
- React Hook Form or plain HTML forms for validation

### 🧪 Testing Tasks
- Add 3 test customers using the form
- Confirm all 3 appear in the list
- Search for each by name and confirm filtering works
- Refresh the page and confirm data persists

### 🐞 Common Issues
- Data not persisting on refresh → Check localStorage.setItem is being called on save; or Supabase insert is awaited
- Search not filtering → Check that filter is applied to the displayed array, not the data source
- Form submitting without validation → Add `required` to inputs and handle empty checks

### ✅ End-of-Day Checklist
- [ ] Customer schema defined and documented
- [ ] Add Customer form works with validation
- [ ] Customer list shows all added customers
- [ ] Search filters by name in real time
- [ ] Data persists after page refresh
- [ ] Code pushed to GitHub

### 📸 Screenshots to Capture
- Add Customer form filled out
- Customer list showing 3 customers
- Search bar filtering results

### ➡️ Handoff to Day 4
Carry forward: the exact schema for `Customer`, and whether you're using localStorage or Supabase. Day 4 builds the Eligibility Check form on top of this foundation.

---

## Day 4 — Eligibility Check Form

### 🎯 Objective
Build the core feature of the app: the eligibility check logging form. A user selects a customer, fills in all eligibility fields, and saves the check to the data layer.

### 📖 What You'll Learn
- How to build multi-field forms with dropdowns and date pickers
- How to link two data entities (customer → check)
- How to auto-populate fields (date of check)

### 🛠 Features to Build
- Eligibility Check data model
- "Log New Check" form linked to a specific customer
- All 6 eligibility fields + auto-filled date + optional notes
- Success confirmation on save

### 📝 Step-by-Step Implementation Plan

**Step 1 — Define the Eligibility Check schema**
```
EligibilityCheck {
  id: unique identifier
  customerId: reference to Customer.id
  memberID: string (required)
  coverageStartDate: date (required)
  coverageEndDate: date (required)
  planType: string — dropdown: HMO, PPO, EPO, POS, Other
  deductibleIndividual: number (required)
  deductibleFamily: number (required)
  copayPrimaryCare: number (required)
  copaySpecialist: number (required)
  notes: string (optional)
  checkedAt: timestamp (auto-filled to now)
}
```

**Step 2 — Add "Log Check" button to each customer card**
From the customer list, each card gets a "Log Check" button that navigates to the eligibility form pre-loaded with that customer's ID and name.

**Step 3 — Build the Eligibility Check form**
Build the form with all fields. Use:
- Text input for Member ID
- Date pickers for coverage dates
- Dropdown (select) for Plan Type
- Number inputs for deductibles and co-pays
- Textarea for Notes
- Read-only field showing today's date as "Date of Check"
- Read-only field showing the customer's name

**Step 4 — Save logic**
On submit, validate all required fields, save the check to the data layer linked to the customer ID, and show a success message or redirect to that customer's summary.

### 📂 Files and Folders to Create/Modify
```
src/
├── components/
│   └── EligibilityForm.jsx    ← The full eligibility check form
├── hooks/
│   └── useChecks.js           ← Data access for eligibility checks
├── pages/
│   └── log-check.jsx          ← New: Log check page (takes customerId as param)
```

### 🔗 Tools & Services
- No new tools needed — uses existing data layer

### 🧪 Testing Tasks
- Log a check for 2 different customers
- Confirm all fields save correctly
- Confirm the checkedAt timestamp is today's date
- Refresh page and confirm checks persist

### 🐞 Common Issues
- Customer ID not passing to form → Use URL params or state to pass customerId from list to form
- Number fields accepting text → Add `type="number"` and `min="0"` to inputs
- Date pickers not working cross-browser → Use `type="date"` input (native, works in all modern browsers)

### ✅ End-of-Day Checklist
- [ ] Eligibility Check schema defined
- [ ] Log Check form accessible from customer list
- [ ] All fields render correctly with appropriate input types
- [ ] Required field validation works
- [ ] Data saves and persists
- [ ] Code pushed to GitHub

### 📸 Screenshots to Capture
- Eligibility form fully filled out before saving
- Success confirmation after saving

### ➡️ Handoff to Day 5
Carry forward: both schemas (Customer + EligibilityCheck). Day 5 builds the customer detail page (summary + history) which reads from both.

---

## Day 5 — Customer Detail Page (Summary + History)

### 🎯 Objective
Build the most important screen in the app: the customer detail page showing their latest eligibility summary and full check history.

### 📖 What You'll Learn
- How to fetch and display related data (customer + their checks)
- How to design a reference card for quick verbal use
- How to display a sorted list of historical records

### 🛠 Features to Build
- Customer detail page (accessed via "View" button on customer card)
- Eligibility Summary card (most recent check, prominently displayed)
- Check History list (all checks, newest first)
- "Log New Check" button on the detail page

### 📝 Step-by-Step Implementation Plan

**Step 1 — Customer detail page route**
Create a route like `/customer/[id]` or `/customer?id=...`. Load the customer record and all their associated eligibility checks.

**Step 2 — Build the Eligibility Summary card**
Find the most recent check (sort by `checkedAt`, take the first). Display all 6 eligibility fields in a clean card layout:
```
MEMBER ID        |  PLAN TYPE
ABC123456        |  PPO

COVERAGE PERIOD
Jan 1, 2026 – Dec 31, 2026

DEDUCTIBLE (Individual / Family)
$1,500 / $3,000

CO-PAY (Primary / Specialist)
$25 / $50

Last checked: Sep 6, 2026
```

**Step 3 — Build the Check History list**
Below the summary card, list all checks sorted newest first. Each row shows: date checked, plan type, and a "View" toggle to expand full details.

**Step 4 — Add "Log New Check" button**
A clearly visible button at the top of the page that navigates to the log-check form pre-filled with this customer's ID.

### 📂 Files and Folders to Create/Modify
```
src/
├── components/
│   ├── EligibilitySummaryCard.jsx   ← The main reference card
│   └── CheckHistoryList.jsx         ← Scrollable check history
├── pages/
│   └── customer/[id].jsx            ← Customer detail page
```

### 🧪 Testing Tasks
- Log 3 checks for the same customer on different dates
- Confirm the summary card shows the most recent check
- Confirm the history shows all 3 checks in correct order
- Click "Log New Check" and confirm the form loads with the correct customer

### 🐞 Common Issues
- Wrong check showing in summary → Make sure you're sorting by `checkedAt` descending before taking index 0
- Customer not loading → Confirm the ID in the URL matches the stored ID format
- History not showing → Confirm you're filtering checks by `customerId`

### ✅ End-of-Day Checklist
- [ ] Customer detail page loads from customer list
- [ ] Summary card shows most recent check correctly
- [ ] All 6 fields display clearly in the summary card
- [ ] Check history shows all checks, newest first
- [ ] "Log New Check" button works from the detail page
- [ ] Code pushed to GitHub

### 📸 Screenshots to Capture
- Customer detail page with summary card populated
- Check history showing multiple records

### ➡️ Handoff to Day 6
The core feature set is now fully functional. Day 6 focuses on dashboard/home page refinement and global UX polish. No new data features are added.

---

## Day 6 — Dashboard & UX Polish

### 🎯 Objective
Polish the overall user experience: improve the home dashboard, refine the UI across all pages, and make the app feel complete and professional.

### 📖 What You'll Learn
- How to create a useful dashboard/home view
- How to apply consistent styling across a multi-page app
- UX principles for professional tools

### 🛠 Features to Build
- Dashboard home page with stats (total customers, total checks today, last check performed)
- Consistent card styling across all pages
- Empty states (what to show when there are no customers or no checks yet)
- Loading states (if applicable)
- Consistent color scheme and typography finalized

### 📝 Step-by-Step Implementation Plan

**Step 1 — Build the Dashboard**
Replace or enhance the home/index page with:
- Stat tiles: Total Customers, Checks Today, Last Check Performed
- Quick action button: "Add Customer" and "Log New Check"
- Recent activity list: last 5 checks performed (customer name + date)

**Step 2 — Add empty states**
Every list page should handle the empty case gracefully:
- No customers: "No customers yet. Add your first customer to get started." + Add button
- No checks: "No eligibility checks logged yet. Log a check to get started." + Log button

**Step 3 — Audit all pages for visual consistency**
Go through every page and verify:
- Same font and font sizes
- Same button styles (primary, secondary)
- Same card border radius and shadow
- Same spacing/padding

**Step 4 — Mobile responsiveness check**
Open the app on a phone or use browser DevTools to simulate mobile. Fix any layout breaks. (Desktop-first is fine; just make sure nothing is completely broken.)

### 📂 Files and Folders to Create/Modify
```
src/
├── components/
│   ├── StatTile.jsx           ← Reusable dashboard stat tile
│   ├── EmptyState.jsx         ← Reusable empty state component
│   └── RecentActivity.jsx     ← Recent checks list for dashboard
├── styles/
│   └── globals.css            ← Finalize global styles
├── pages/
│   └── index.jsx              ← Replace with dashboard
```

### 🧪 Testing Tasks
- Verify stats on dashboard are accurate
- Clear all data (or use a fresh browser) to test empty states
- Check the app on a tablet or phone screen

### 🐞 Common Issues
- Stats showing wrong count → Recount from the actual data source, not a cached variable
- Empty state not showing → Make sure conditional rendering checks array length === 0, not just falsy

### ✅ End-of-Day Checklist
- [ ] Dashboard shows accurate stats
- [ ] All empty states are handled
- [ ] Visual consistency confirmed across all pages
- [ ] No broken layouts on tablet
- [ ] Code pushed to GitHub

### 📸 Screenshots to Capture
- Dashboard with real data populated
- An empty state screen

### ➡️ Handoff to Day 7
Day 7 is for thorough testing and bug fixing. The app should be fully feature-complete as of today.

---

## Day 7 — Testing & Bug Fixing

### 🎯 Objective
Thoroughly test the entire application, document and fix all bugs, and ensure the app is stable and ready for deployment.

### 📖 What You'll Learn
- How to systematically test a web application
- How to identify and prioritize bugs
- How to write a test checklist

### 🛠 Tasks
- Full end-to-end walkthrough of every user flow
- Fix all identified bugs
- Test edge cases (empty fields, special characters, long names)
- Test browser compatibility (Chrome, Firefox, Edge)

### 📝 Step-by-Step Test Plan

**Flow 1 — New Customer**
1. Click Add Customer
2. Submit empty form → confirm validation errors appear
3. Fill all fields → confirm customer saves and appears in list
4. Search for the customer by name → confirm they appear

**Flow 2 — Log Eligibility Check**
1. Click "Log Check" from customer card
2. Submit empty form → confirm validation
3. Fill all fields with realistic data → confirm save
4. Navigate to customer detail → confirm summary card shows new check

**Flow 3 — Multiple Checks**
1. Log 3 checks for the same customer on different dates
2. Confirm summary shows the most recent
3. Confirm history shows all 3 in correct order

**Flow 4 — Edge Cases**
1. Customer name with apostrophe (O'Brien) → confirm no crash
2. Very long name (50+ characters) → confirm card doesn't break
3. Zero value for deductible → confirm it saves and displays as $0
4. Add 10+ customers → confirm list scrolls correctly

**Flow 5 — Data Persistence**
1. Add a customer and log a check
2. Close the browser completely
3. Reopen the app → confirm data is still there

### 📂 Files to Modify
- Any file with bugs identified during testing

### 🧪 Bug Log Template
For each bug found:
```
Bug: [description]
Steps to reproduce: [numbered steps]
Expected: [what should happen]
Actual: [what happens]
Fix: [what you changed]
```

### ✅ End-of-Day Checklist
- [ ] All 5 test flows completed without critical bugs
- [ ] All identified bugs fixed
- [ ] App tested in Chrome and at least one other browser
- [ ] Code pushed to GitHub
- [ ] App is stable and ready for deployment

### 📸 Screenshots to Capture
- Summary card with real eligibility data (this becomes your demo screenshot)
- Customer list with 5+ real-looking customers

### ➡️ Handoff to Day 8
App is fully tested and stable. Day 8 is deployment prep: setting up the hosting account, environment variables, and a production build.

---

## Day 8 — Deployment Preparation

### 🎯 Objective
Prepare the app for production deployment: configure environment variables, optimize the build, and set up the hosting platform account.

### 📖 What You'll Learn
- How to set up environment variables for production
- How to create a production build
- How to configure a free hosting platform

### 🛠 Tasks
- Create account on chosen hosting platform (Vercel or Netlify — both free)
- Set up environment variables (if using Supabase or any external service)
- Run production build locally and verify no errors
- Configure deployment settings

### 📝 Step-by-Step Implementation Plan

**Step 1 — Create hosting account**
- Go to vercel.com (recommended) and sign up with your GitHub account
- This links Vercel directly to your GitHub repo

**Step 2 — Environment variables**
If using Supabase:
- Copy your Supabase URL and anon key from the Supabase dashboard
- Create a `.env.local` file in your project root:
  ```
  NEXT_PUBLIC_SUPABASE_URL=your_url_here
  NEXT_PUBLIC_SUPABASE_ANON_KEY=your_key_here
  ```
- Add `.env.local` to `.gitignore` (never commit secrets)

If using localStorage only:
- No environment variables needed — skip this step

**Step 3 — Test production build locally**
Run: `npm run build` then `npm run preview` (Vite) or `npm run start` (Next.js)
Confirm the production build works identically to development.

**Step 4 — Fix any build errors**
Common: missing imports, TypeScript errors if using TS, missing environment variables. Fix all until `npm run build` completes with no errors.

**Step 5 — Update README**
Write a short README explaining what the app is and how to run it locally.

### 📂 Files to Create/Modify
```
├── .env.local           ← Environment variables (DO NOT commit)
├── .gitignore           ← Add .env.local if not already there
├── README.md            ← Update with project description
```

### 🧪 Testing Tasks
- `npm run build` completes without errors
- Production preview runs and all features work
- Environment variables load correctly in production build

### 🐞 Common Issues
- Build error: "Cannot find module" → Check all import paths are correct
- Environment variable undefined in production → Must be prefixed with `NEXT_PUBLIC_` (Next.js) or `VITE_` (Vite)
- White screen in production build → Open browser console for error messages

### ✅ End-of-Day Checklist
- [ ] Hosting account created (Vercel or Netlify)
- [ ] Environment variables configured correctly
- [ ] Production build completes without errors
- [ ] Production preview fully functional
- [ ] README written
- [ ] `.env.local` in `.gitignore`
- [ ] Code pushed to GitHub

### 📸 Screenshots to Capture
- Successful `npm run build` terminal output
- App running from production build locally

### ➡️ Handoff to Day 9
Everything is ready to deploy. Day 9 is the actual live deployment.

---

## Day 9 — Live Deployment

### 🎯 Objective
Deploy the app to production and verify it works live on the internet with a real URL.

### 📖 What You'll Learn
- How to deploy a web app to a free hosting platform
- How to configure environment variables in production
- How to verify a live deployment

### 🛠 Tasks
- Deploy to Vercel (or Netlify) from GitHub
- Set environment variables in hosting platform dashboard
- Test the live URL end-to-end
- Fix any production-only issues

### 📝 Step-by-Step Deployment (Vercel)

**Step 1 — Import project**
- Log into vercel.com
- Click "Add New Project"
- Select your `insurance-eligibility-manager` GitHub repo
- Click "Import"

**Step 2 — Configure build settings**
Vercel auto-detects Next.js and Vite. Confirm:
- Framework Preset: Next.js or Vite (auto-detected)
- Build Command: `npm run build`
- Output Directory: `.next` (Next.js) or `dist` (Vite)

**Step 3 — Add environment variables**
In the Vercel project setup screen, find "Environment Variables."
Add each variable from your `.env.local` file.

**Step 4 — Deploy**
Click "Deploy." Watch the build log. A successful deploy shows a green checkmark and gives you a URL like: `https://insurance-eligibility-manager.vercel.app`

**Step 5 — Test the live URL**
Open the live URL in a new browser (or incognito window). Run through all test flows from Day 7. Confirm everything works end-to-end on the live deployment.

**Step 6 — Fix production issues**
If anything is broken:
- Check Vercel's "Functions" tab and "Deployments" logs for errors
- Fix locally, push to GitHub — Vercel auto-redeploys on every push

### 🧪 Testing Tasks
- Add a customer on the live URL
- Log an eligibility check
- View the summary card
- Confirm data persists after closing and reopening the browser

### 🐞 Common Issues
- 404 on page refresh (Vite SPA) → In Vercel project settings, add a rewrite rule: `/* → /index.html`
- Supabase not connecting → Double-check environment variables are set correctly in Vercel dashboard (not just locally)
- Build fails on Vercel → Check build logs; usually a missing dependency or env var

### ✅ End-of-Day Checklist
- [ ] App live at a public URL
- [ ] All features work on the live URL
- [ ] Data persists on the live URL
- [ ] URL noted and saved
- [ ] Code is up to date on GitHub

### 📸 Screenshots to Capture
- Live URL in browser address bar with the app running
- Eligibility summary card on the live deployment (key demo screenshot)

### ➡️ Handoff to Day 10
App is live. Day 10 is final polish, documentation, and challenge submission.

---

## Day 10 — Final Polish, Demo & Submission

### 🎯 Objective
Add any final UX touches, write the challenge submission documentation, record a demo, and submit your capstone.

### 📖 What You'll Learn
- How to write a clear product README for a public project
- How to present a technical project effectively
- How to reflect on a build sprint

### 🛠 Tasks
- Final visual review and any remaining polish
- Write submission README / post for the AB Talks challenge
- Record a short screen demo (2–3 min) walking through all features
- Submit to the challenge

### 📝 Step-by-Step

**Step 1 — Final review**
Open the live app. Walk through every page with fresh eyes. Fix anything that feels unfinished or broken. Common last-minute fixes: spacing, button labels, loading states.

**Step 2 — Write the challenge submission post**
Include:
- What the app does (2–3 sentences)
- The problem it solves
- The tech stack used
- The live URL
- A screenshot of the summary card (your hero screenshot)
- What you'd build next (1–2 features)

**Step 3 — Record the demo video**
Use a free screen recorder (OBS, Loom free tier, or your OS built-in recorder):
- Show the live URL in the address bar
- Add a customer
- Log an eligibility check
- Show the summary card
- Show the check history
- Talk through what the app does as you demo it

**Step 4 — Submit**
Post to the AB Talks challenge thread/platform with your live URL, demo video, and submission post.

### 📂 Files to Create/Modify
```
├── README.md    ← Final public README with live URL and description
```

### ✅ Final Capstone Checklist
- [ ] App is live and fully functional
- [ ] README is complete with live URL
- [ ] Demo video recorded
- [ ] Challenge submission posted
- [ ] GitHub repo is public and clean

### 📸 Final Screenshots to Capture
- Dashboard with data
- Customer list
- Eligibility form
- **Eligibility summary card** (most important — this is your hero shot)
- Check history

---

## Appendix: Project Data Schema

```
Customer {
  id: string (uuid)
  name: string
  dateOfBirth: string (YYYY-MM-DD)
  insuranceCompany: string
  createdAt: timestamp
}

EligibilityCheck {
  id: string (uuid)
  customerId: string (foreign key → Customer.id)
  memberID: string
  coverageStartDate: string (YYYY-MM-DD)
  coverageEndDate: string (YYYY-MM-DD)
  planType: enum [HMO, PPO, EPO, POS, Other]
  deductibleIndividual: number
  deductibleFamily: number
  copayPrimaryCare: number
  copaySpecialist: number
  notes: string (nullable)
  checkedAt: timestamp
}
```

---

*This blueprint is the single source of truth for Days 2–10. Do not deviate from the schema or feature set without first evaluating scope impact.*
