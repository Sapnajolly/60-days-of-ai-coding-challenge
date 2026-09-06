# Product Requirements Document — Momentum: AI Habit & Goal Coach

**Author:** Sapna Jolly · **Capstone Day:** 51 (Day 1 of 10) · **Status:** Approved for build

## 1. Problem

Most habit trackers are glorified checklists — they record whether you did something, but they don't help you decide *what* to do next, don't adapt when you fall behind, and don't turn a big vague goal ("get fit", "learn Spanish") into a realistic daily plan. People abandon them within a few weeks because the app gives no coaching, only guilt.

## 2. Target Users

- Someone with 1-3 real goals (fitness, learning, a side project) who wants a daily habit broken out of that goal, not a spreadsheet.
- Self-directed learners/builders who want lightweight AI coaching (a weekly plan + reflection) without a subscription or a human coach.

## 3. Solution

**Momentum** is a single-page web app where a user:
1. Defines a goal ("Run a 5K", "Ship my side project").
2. Gets it broken into a small set of trackable daily/weekly habits.
3. Checks habits off each day and builds visible streaks.
4. Gets an AI-generated weekly plan and end-of-week reflection that adapts to what was actually completed (not a static template).

No backend, no login, no subscription — everything runs client-side with `localStorage`, so it is deployable as a static site (GitHub Pages) with zero infrastructure cost.

## 4. v1.0 Scope (what ships by Day 60)

**In scope:**
- Goal creation with AI-assisted habit breakdown (rule-based coaching engine that mimics an AI coach's reasoning; designed with a clean seam to swap in a real Claude API call later)
- Daily check-in UI with streak counting and a calendar heatmap
- Weekly AI Coach panel: plan for the upcoming week + reflection on the week just finished, both generated from the user's actual completion data
- Stats dashboard: completion %, current streak, longest streak, per-goal breakdown
- Light/dark theme, responsive layout, onboarding for first-time users
- Data persistence via `localStorage`; export/import as JSON (so a user isn't locked in)
- Deployed as a static site (GitHub Pages) with a versioned v1.0.0 release

**Explicitly out of scope for v1.0:**
- Real backend/database or multi-device sync
- Real Claude/OpenAI API calls (would require a backend to hold the key) — the coaching engine is rule-based but structured so a real LLM call is a drop-in replacement later
- Social features (sharing, leaderboards, friends)
- Native mobile app
- Notifications/reminders (no backend to schedule them from)

## 5. Success Criteria for Day 10 (Day 60)

- A user can, with zero instructions, create a goal, see it broken into habits, check in for several days, and get a weekly plan + reflection that clearly reflects what they actually did (not generic text).
- The app has zero console errors, handles empty states gracefully (no goals yet, no check-ins yet), and works on both a phone-width and desktop viewport.
- The app is live at a public GitHub Pages URL, tagged `v1.0.0`, with a README a stranger could use to understand and run the project in under a minute.

## 6. Risks / Open Questions

- **Risk:** a rule-based "AI Coach" could feel gimmicky if it's too generic. **Mitigation:** the coaching logic reads the user's actual streak/completion data (which habits are slipping, which are solid) and generates plans/reflections from that data rather than fixed strings — see Day 52's design for the templating approach.
- **Risk:** scope creep into "the ultimate habit app." **Mitigation:** the blueprint below fixes exactly one milestone per remaining day; nothing is added outside that day's milestone.
