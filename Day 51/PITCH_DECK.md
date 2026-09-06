# Momentum — Pitch Deck

## Slide 1 — Problem
Habit trackers record what you did. They don't help you decide what to do next, and they don't adapt when you fall behind. Most people quit within a few weeks because the app only produces guilt, never guidance.

## Slide 2 — Target Users
People with 1-3 real goals (fitness, learning, a side project) who want that goal broken into a small, trackable set of daily habits — and a nudge each week that's actually based on what they did, not a form letter.

## Slide 3 — Solution
**Momentum**: define a goal, get it broken into habits, check in daily, build streaks, and get a weekly AI-generated plan + reflection that names your actual habits and actual numbers.

## Slide 4 — Key Features
- Goal → habit breakdown (AI-coaching engine)
- Daily check-ins with streaks + calendar heatmap
- Weekly plan and reflection generated from real completion data
- Stats dashboard (completion %, current/longest streak)
- Light/dark theme, fully responsive, zero login

## Slide 5 — Technical Approach
Static, client-only web app (HTML/CSS/vanilla JS), `localStorage` for persistence, a small rule-based coaching engine with a clean interface so a real LLM call can be swapped in later without touching the UI. Deployed on GitHub Pages — zero infrastructure cost.

## Slide 6 — Future Scope (v2+)
- Real Claude API call for the weekly coach (via a small serverless function to hold the key)
- Cross-device sync (a lightweight backend)
- Reminders/notifications
- Shareable weekly-report cards

## Slide 7 — Vision
A habit app whose only job is to notice what's actually happening in your data and say something useful about it — not a checklist, a coach.
