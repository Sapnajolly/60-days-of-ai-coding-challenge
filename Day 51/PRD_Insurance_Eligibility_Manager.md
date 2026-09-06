# Product Requirements Document
## Insurance Eligibility Manager
**Version:** 1.0  
**Date:** September 6, 2026  
**Author:** Orbit (Orbit Boyzz)  
**Challenge:** AB Talks 60-Day Claude AI Challenge — Capstone Project  

---

## 1. Executive Summary

Insurance Eligibility Manager is a lightweight web application that enables health and welfare benefits professionals to quickly log, organize, and retrieve insurance eligibility data for their clients. It eliminates the need for paper notes and manual memory during eligibility callbacks by providing a clean, structured record for every check performed.

---

## 2. Problem Statement

### Current Pain Points
Benefits professionals spend significant time on the phone with insurance companies checking client eligibility. After retrieving the data verbally, there is no structured system to:
- Store the information in a consistent, retrievable format
- Quickly reference key eligibility fields during a callback call
- Maintain a history of past checks per customer
- Avoid re-checking the same client twice in a short period

### Impact
- Time lost re-checking clients who were already verified
- Risk of miscommunicating incorrect benefit details during callbacks
- No audit trail of what was checked or when

---

## 3. Goals

### Primary Goal
Build a simple, fast, and reliable tool that replaces paper notes during the eligibility check workflow — from portal lookup to customer callback.

### Success Criteria (Day 10)
- A deployed, publicly accessible web app
- Ability to add a customer, log their eligibility data, and retrieve it in under 60 seconds
- Clean summary view usable as a live reference during a phone callback
- Searchable customer history

---

## 4. Target Users

### Primary User
**Benefits professional / customer service rep** who handles 5–10 insurance eligibility checks per day and relays the results to customers via phone call.

### User Profile
- Comfort level: basic to intermediate tech user
- Device: desktop/laptop (primary)
- Use context: seated at a desk, mid-workflow, often on the phone simultaneously

---

## 5. User Stories

| ID | As a... | I want to... | So that... |
|----|---------|--------------|------------|
| US-01 | Benefits rep | Add a new customer with their basic info | I can start tracking their eligibility |
| US-02 | Benefits rep | Log eligibility data after calling the insurance portal | I have a structured record of what I found |
| US-03 | Benefits rep | View a clean summary of a customer's eligibility | I can reference it clearly during my callback call |
| US-04 | Benefits rep | Search for a customer by name | I can quickly pull up past checks without scrolling |
| US-05 | Benefits rep | See a history of all eligibility checks for a customer | I can avoid redundant re-checks |
| US-06 | Benefits rep | Know when the last check was performed | I can assess whether the data is still current |

---

## 6. Features — v1.0 Scope

### 6.1 Customer Management
- Add a new customer (name, date of birth, insurance company)
- View a list of all customers
- Search/filter customers by name

### 6.2 Eligibility Check Logging
- Log a new eligibility check for any customer
- Fields captured per check:
  - **Member ID**
  - **Coverage Start Date**
  - **Coverage End Date**
  - **Plan Type** (e.g., HMO, PPO, EPO)
  - **Deductible** (individual / family)
  - **Co-payment** (primary care / specialist)
  - **Date of check** (auto-filled)
  - **Notes** (freeform, optional)

### 6.3 Eligibility Summary View
- One-tap access to a customer's most recent eligibility check
- Clean, card-style layout optimized for quick verbal reference
- Displays all 6 key eligibility fields prominently

### 6.4 Check History
- List of all past eligibility checks per customer
- Sorted by date, newest first
- Shows date of check and insurance company at a glance

---

## 7. Out of Scope (v1.0)

The following are explicitly excluded from v1.0 to protect scope:

| Feature | Reason Excluded |
|---------|-----------------|
| Insurance portal automation / scraping | Each carrier has a unique portal; reliable automation is a multi-week effort |
| Email or SMS output to customers | Callbacks are handled by phone; adds unnecessary complexity |
| Multi-user / team accounts | Single-user tool for now |
| Mobile app | Web app on desktop covers the primary use case |
| PDF export | Not needed for phone-based workflow |
| Billing or payment tracking | Out of domain for v1.0 |
| Insurance carrier API integrations | APIs are carrier-specific and often paywalled |

---

## 8. Technical Constraints

- Tech stack to be selected on Day 2
- Must be deployable for free
- No paid third-party services required to run the application
- Must work reliably on a desktop browser (Chrome, Firefox, Edge)

---

## 9. Non-Functional Requirements

| Requirement | Target |
|-------------|--------|
| Page load time | Under 2 seconds |
| Data entry time per check | Under 90 seconds |
| Accessibility | Keyboard-navigable forms |
| Responsiveness | Desktop-first; functional on tablet |
| Data persistence | Persistent across sessions (database-backed) |

---

## 10. Assumptions

- The user accesses the insurance portal manually and enters the data into the app themselves
- Data does not need to be shared with teammates in v1.0
- All users are in the same timezone (EST)
- No HIPAA compliance required for this capstone build (this is a personal productivity tool, not a production medical records system)

---

## 11. Risks

| Risk | Likelihood | Mitigation |
|------|-----------|------------|
| Scope creep adding features mid-build | Medium | Strict daily checklists; refer back to this PRD |
| Over-engineering the data model | Low | Keep schema minimal: customers + checks |
| Deployment issues on Day 9 | Low | Use a platform with one-click deploy |

---

## 12. Glossary

| Term | Definition |
|------|-----------|
| Eligibility Check | The process of verifying a customer's current insurance coverage status |
| Member ID | Unique identifier assigned to an insured member by their carrier |
| Plan Type | Category of insurance plan (HMO, PPO, EPO, POS, etc.) |
| Deductible | Amount the insured pays out-of-pocket before insurance kicks in |
| Co-payment | Fixed fee paid by the insured for a covered service |
| Carrier | The insurance company providing coverage |

---

*End of PRD v1.0*
