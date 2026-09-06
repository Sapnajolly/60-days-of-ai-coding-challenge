# Day 51 — AB Talks 60-Day Claude AI Challenge
## Capstone: Product Discovery & Sprint Planning
**Date:** September 6, 2026  
**Session Type:** Day 1 of 10-Day Capstone  

---

## Interview Summary

| Question | Answer |
|----------|--------|
| Starting from scratch or existing idea? | Scratch |
| What do you spend time on day-to-day? | Work |
| What does a typical workday look like? | Managing customer calls and responding to queries about health and welfare benefits |
| Most repetitive/painful part? | Checking eligibility of customers — verifying if they're still active on the insurance side |
| How do you currently check eligibility? | Making calls to insurance companies |
| What info do you look up? | Member ID, coverage dates, plan type, deductibles, co-payments |
| What do you do with the info after? | Relay it to the customer |
| How many checks per day? | 6–7 |
| Do insurance companies have a portal? | Yes |
| How do you relay info to the customer? | Phone call |

---

## Project Selected

**Insurance Eligibility Manager** — a web app where a benefits professional can add customers, log insurance eligibility data (member ID, coverage dates, plan type, deductible, co-payment), view a clean summary per customer, and search/browse check history.

---

## v1.0 Scope

### Included
- Customer management (add, search, list)
- Eligibility check logging (all 6 fields + date + notes)
- Summary card view (clean reference for callback calls)
- Check history per customer (sorted newest first)

### Intentionally Excluded
- Insurance portal automation / scraping
- Email or SMS output
- Multi-user / team accounts
- Mobile app
- PDF export
- Carrier API integrations

### Day 10 Success Definition
A deployed, publicly accessible web app used for real customers — logging eligibility data in under 90 seconds per check.

---

## Future Scope

### v1.1
- Multi-user accounts
- PDF summary export
- Email summary to customer
- Batch check logging

### v2.0
- Coverage expiration alerts
- Re-check reminders
- Carrier API integrations
- Analytics dashboard

---

## Data Schema

```
Customer {
  id:               uuid
  name:             string (required)
  dateOfBirth:      date (required)
  insuranceCompany: string (required)
  createdAt:        timestamp
}

EligibilityCheck {
  id:                  uuid
  customerId:          → Customer.id
  memberID:            string (required)
  coverageStartDate:   date (required)
  coverageEndDate:     date (required)
  planType:            HMO | PPO | EPO | POS | Other
  deductibleIndividual: number (required)
  deductibleFamily:    number (required)
  copayPrimaryCare:    number (required)
  copaySpecialist:     number (required)
  notes:               string (optional)
  checkedAt:           timestamp (auto)
}
```

---

## Deliverables Produced

| Deliverable | File |
|-------------|------|
| Product Requirements Document | `PRD_Insurance_Eligibility_Manager.md` |
| Implementation Blueprint (Days 2–10) | `Blueprint_Insurance_Eligibility_Manager.md` |
| Project Pitch Deck | Interactive artifact (8 slides) |

---

## 10-Day Sprint Overview

| Day | Focus |
|-----|-------|
| **Day 1 (today)** | Product discovery, PRD, blueprint, pitch deck |
| **Day 2** | Tech stack selection, project scaffold, GitHub setup |
| **Day 3** | Data layer, customer management (add, list, search) |
| **Day 4** | Eligibility check form (all 6 fields) |
| **Day 5** | Customer detail page — summary card + check history |
| **Day 6** | Dashboard, UX polish, empty states |
| **Day 7** | Full end-to-end testing, bug fixes |
| **Day 8** | Deployment preparation, production build |
| **Day 9** | Live deployment to Vercel |
| **Day 10** | Final polish, demo recording, challenge submission |

---

## Standing Rules for Days 2–10

1. Assume guidance is needed for every manual step
2. Explain manual tasks step by step with actual buttons, menus, and commands
3. Wait for confirmation and a screenshot before continuing
4. Never assume a step is completed
5. Do not recommend paid tools or services
6. Protect scope — refer back to this document if feature creep appears

---

## How to Start Day 2

Open a fresh AI conversation and begin with:

> "I'm building the Insurance Eligibility Manager for the AB Talks 60-Day Claude AI Challenge capstone. This is Day 2. The app is a single-user web app where a benefits professional logs insurance eligibility data (member ID, coverage dates, plan type, deductible, co-payment) for customers and views a clean summary during callback calls. Today's goal is to choose my tech stack, set up the dev environment, initialize the project, and get a working scaffold running locally with three placeholder pages. Please guide me step by step."

Then paste the full Day 2 section from `Blueprint_Insurance_Eligibility_Manager.md`.

---

*Day 51 complete. Day 52 = Day 2 of the capstone build.*
