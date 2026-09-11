# Day 54 — Insurance Eligibility Manager: Core Features

**Challenge:** AB Talks 60-Day Claude AI Challenge
**Builder:** Orbit (Orbit Boyzz)
**Date:** September 11, 2026

---

## What Was Built Today

### Milestone 1 — Customer List + Add Customer Form
- `src/hooks/useCustomers.js` — Supabase data hook (fetch all customers, add customer)
- `src/pages/CustomersList.jsx` — Full customer list with search bar, customer cards, Log Check + View buttons
- `src/pages/AddCustomer.jsx` — Add Customer form with validation, saves to Supabase
- `src/pages/Dashboard.jsx` — Updated dashboard with quick action buttons

### Milestone 2 — Eligibility Check Form (Day 4 Core Feature)
- `src/hooks/useChecks.js` — Supabase data hook (fetch checks by customer, add check)
- `src/pages/LogCheck.jsx` — Full eligibility check form with all required fields

---

## Eligibility Check Schema

---

## Tech Stack

- Vite + React 18
- Tailwind CSS v4
- React Router v6
- Supabase (PostgreSQL)

---

## Status

- [ ] Customer list loads from Supabase
- [ ] Add Customer form saves to Supabase
- [ ] Log Check form accessible from customer cards
- [ ] All eligibility fields save correctly
- [ ] Success confirmation on check save
- [ ] Code pushed to GitHub

---

## GitHub

Repo: https://github.com/Sapnajolly/insurance-eligibility-manager
Status: Committed locally — push pending (account suspension)

---

## Day 5 Preview

Build the Customer Detail page — eligibility summary card showing the most recent check, plus full check history list.