# Day 8 — 🌍 Personal Environmental Health Analyzer 👍

Part of the **#60DaysOfAICodingChallenge**

## What this is

A single-file, fully interactive HTML dashboard that analyzes live air quality (AQI) and tap-water quality data across 16 major Indian cities, then turns it into a personal environmental health report — including how the air and water in a chosen city could affect your lungs, sleep, energy, skin, and hair.

No backend, no build step — open `index.html` in any browser and it just works.

## Live demo

Open [`index.html`](./index.html) directly in your browser, or enable GitHub Pages on this repo and point it at this folder.

## Features

**Key metrics bar** — average AQI, highest/lowest AQI city, number of cities analyzed, and a live-computed Environmental Health Score.

**Five interactive charts** (Chart.js) — AQI comparison, PM2.5 comparison, PM10 comparison, a best-to-worst city ranking chart, and an AQI-category distribution donut — all of which redraw instantly as you apply filters.

**Interactive filters** — city selector, AQI range slider, pollutant switcher (AQI / PM2.5 / PM10), health-risk checkboxes (Low / Moderate / High), and a side-by-side city comparison mode.

**16 city detail cards** — AQI, PM2.5, PM10, CPCB air-quality category badge, environmental health score, and water-quality score at a glance.

**AQI category system** — Good, Satisfactory, Moderate, Poor, Very Poor, Severe, color-coded per India's CPCB National AQI standard.

**Environmental Health Analysis (per selected city)** — plain-language impact of local air quality on lungs, sleep, energy levels, exercise performance, and long-term health; plus impact of local water quality on hair fall, hair dryness, scalp health, skin dryness, acne, and skin sensitivity — each tagged with a 🟢 Low / 🟡 Moderate / 🔴 High risk indicator.

**Personal Report Card** — a 0–100 Environmental Health Score with Air Quality, Water Quality, and Overall breakdowns, plus A–F letter grades for Air Quality, Water Quality, Hair Risk, and Skin Risk.

**Insights panel** — top 3 cleanest cities, top 3 most polluted cities, the biggest data anomaly, the most surprising finding, and recommended actions.

**Personalized recommendations** — daily actions, indoor air improvements, outdoor activity guidance, hair-care tips, skin-care tips, and water-quality improvement suggestions, all tailored to whichever city is selected.

**Design** — dark theme, glassmorphism cards, smooth animations, mobile-responsive grid layout, built to look good as a LinkedIn screenshot.

## Data & methodology

- **Air quality (AQI, PM2.5, PM10):** compiled from [AQI.in India Dashboard](https://www.aqi.in/dashboard/india) and [IQAir India / 2025 World Air Quality Report](https://www.iqair.com/in-en/air-quality/india), snapshot taken July 2026. AQI categories follow India's CPCB National AQI standard (0–500 scale, six bands).
- **Water quality:** compliance scores are derived from the [Bureau of Indian Standards (BIS) national tap-water quality study](https://theprint.in/india/tap-water-quality-best-in-mumbai-most-unsafe-in-delhi-finds-bureau-of-indian-standards/322188/), the most recent comprehensive government study covering 21 major Indian cities (Mumbai: 10/10 samples passed; Delhi: 0/11 samples passed). Cities not covered by that study are labeled as infrastructure-based **estimates** in the app.
- **Scoring:** Air Quality Score and Water Quality Score are each 0–100, banded from the raw readings. Overall Environmental Score = 55% Air Score + 45% Water Score. Letter grades: A ≥ 85, B ≥ 70, C ≥ 55, D ≥ 40, F < 40.
- **Data cleaning:** all rows validated for non-null, in-range values (AQI 0–500, scores 0–100) before being loaded into the dashboard; missing per-pollutant values were imputed from regional station averages where flagged.

This tool is for informational and awareness purposes only — it is not medical advice.

## Tech stack

Plain HTML/CSS/JavaScript + [Chart.js](https://www.chartjs.org/) (loaded from cdnjs). Zero dependencies to install, zero build step.

## How to run locally

```bash
git clone https://github.com/Sapnajolly/60-days-of-ai-coding-challenge.git
cd 60-days-of-ai-coding-challenge/day8
open index.html   # or just double-click it
```

## Files in this folder

| File | Description |
|---|---|
| `index.html` | The complete interactive dashboard (self-contained) |
| `README.md` | This file |

---

**#60DaysOfAICodingChallenge — Day 8 ✅**
