# Implementation Blueprint — Momentum (Capstone Days 2-10 / Program Days 52-60)

Single source of truth for the rest of the build. Each day is scoped so that finishing its checklist leaves the app in a working, demoable state — never a half-broken intermediate.

---

## Day 52 (Capstone Day 2) — System Design

**🎯 Objective:** Turn the Day 51 PRD into a concrete technical design: data model, file structure, state-management approach, and the "AI Coach" templating design.

**📖 Learn:** How to design a client-only data model that still supports export/import and future backend migration.

**🛠 Build:** `ARCHITECTURE.md` only — no code yet.

**📝 Plan:** Define `Goal`, `Habit`, `CheckIn`, `WeeklyReport` schemas; define the file layout (`index.html`, `styles.css`, `app.js`, `coach.js`, `storage.js`); define the coaching-engine interface (`generateWeeklyPlan(data)`, `generateReflection(data)`) so Day 56 just implements it.

**✅ End-of-day checklist:** `ARCHITECTURE.md` committed, describing schema + file layout + coach interface.

**➡️ Handoff:** Day 53 scaffolds exactly the files named here.

---

## Day 53 (Capstone Day 3) — Project Setup & Foundation

**🎯 Objective:** Working, empty-but-running skeleton.

**🛠 Build:** `index.html` shell with header/nav/main/footer regions, `styles.css` with CSS variables for theming (light/dark), `storage.js` with `loadState()`/`saveState()` wrapping `localStorage`, `app.js` that boots and renders "No goals yet" empty state.

**🧪 Testing:** Open in browser, confirm no console errors, confirm empty state renders.

**✅ Checklist:** Skeleton renders, zero console errors, theme variables in place.

**➡️ Handoff:** Day 54 builds real CRUD on top of this shell.

---

## Day 54 (Capstone Day 4) — Core Feature Implementation: Goals & Habits

**🎯 Objective:** Users can create a goal, see it broken into 3-5 habits, edit/delete goals.

**🛠 Features:** "Add Goal" form → rule-based habit-breakdown function (`suggestHabits(goalText)` in `coach.js`, keyword-matched templates for common goal categories — fitness, learning, project/creative, health — with a sensible generic fallback); goal list UI; edit/delete.

**📂 Files touched:** `app.js` (UI + event handlers), `coach.js` (`suggestHabits`), `storage.js` (persist goals).

**🧪 Testing:** Create/edit/delete a goal; refresh page, confirm persistence; create a goal with no keyword match, confirm generic fallback habits appear (never an empty list).

**🐞 Watch for:** losing existing goals on save (always merge, never overwrite the whole state blob); duplicate habit IDs.

**✅ Checklist:** Full goal/habit CRUD works and survives a page refresh.

**➡️ Handoff:** Day 55 adds daily check-ins against these habits.

---

## Day 55 (Capstone Day 5) — Continue Core Feature Development: Check-ins & Streaks

**🎯 Objective:** Daily check-in per habit, streak counting, calendar heatmap.

**🛠 Features:** "Check in today" toggle per habit; `CheckIn` records keyed by date; streak calculation (consecutive days including today); a simple CSS-grid calendar heatmap (last 8 weeks) shaded by completion %.

**📂 Files touched:** `app.js`, `storage.js` (add check-ins), new `heatmap.js` (pure function: check-ins → grid data).

**🧪 Testing:** Check in today, streak becomes 1; simulate a gap (manually edit stored check-ins in devtools) and confirm streak resets correctly; heatmap renders with no check-ins (all-empty grid, not a crash).

**✅ Checklist:** Streaks compute correctly across a gap; heatmap renders in both empty and populated states.

**➡️ Handoff:** Day 56 feeds this check-in data into the AI Coach + stats dashboard.

---

## Day 56 (Capstone Day 6) — Complete the MVP & Deliver a Working Demo

**🎯 Objective:** The app is now feature-complete for v1.0 — AI Coach panel + stats dashboard.

**🛠 Features:** `generateWeeklyPlan(data)` and `generateReflection(data)` implemented in `coach.js` — both read real streak/completion numbers per habit and produce a plan/reflection that names specific habits ("Your morning run streak is at 6 days — keep the same time this week" vs. "Journaling slipped to 40% — try attaching it to a habit you already hold, like check-in itself"); stats dashboard (completion %, current streak, longest streak, per-goal breakdown) as a summary panel.

**🧪 Testing:** Run through the full flow start-to-finish (empty app → goal → habits → several days of check-ins → weekly plan/reflection → stats) and confirm every screen reflects real data, no placeholder text left anywhere.

**✅ Checklist:** End-to-end demo runs clean; this is the "MVP is real" milestone — from here it's polish, not new features.

**➡️ Handoff:** Day 57 only touches presentation, not logic.

---

## Day 57 (Capstone Day 7) — Product Refinement & UX

**🎯 Objective:** Make the MVP feel like a shipped product, not a prototype.

**🛠 Features:** Light/dark theme toggle (persisted); onboarding empty-state copy that explains the app in one glance; micro-animations (check-in tick, streak increment); responsive layout down to a 375px viewport; consistent empty states for every panel (no goals / no check-ins yet / no weekly report yet).

**🧪 Testing:** Resize to phone width and re-run the full flow; toggle theme and confirm every panel (including the heatmap) respects it.

**✅ Checklist:** No layout breakage at 375px; theme toggle covers 100% of the UI, including dynamically rendered panels.

---

## Day 58 (Capstone Day 8) — Testing, Debugging & Production Optimization

**🎯 Objective:** Harden what's built; this day adds no features.

**🛠 Work:** Input validation (empty goal text, absurdly long text); defensive `JSON.parse` around `localStorage` reads (corrupted/missing data must not crash the app — fall back to empty state); debounce the heatmap re-render on rapid check-in clicks; run a manual test pass against a written checklist (documented in `TEST_PLAN.md` with each case's result).

**🐞 Common issues:** stale closures over `state` after a re-render; `localStorage` quota edge cases; timezone bugs in "today" calculation (use local midnight consistently).

**✅ Checklist:** `TEST_PLAN.md` committed with every case passing; no known open bugs.

---

## Day 59 (Capstone Day 9) — Launch & Production Readiness

**🎯 Objective:** Ship it publicly.

**🛠 Work:** Deploy the static site via GitHub Pages; write the public-facing `README.md` (what it is, screenshot, how to run locally, tech stack, roadmap); tag `v1.0.0-rc`; run the Day 58 test plan once more against the deployed URL (not just localhost).

**✅ Checklist:** Public URL live and working; README complete; tag pushed.

---

## Day 60 (Capstone Day 10) — Final Review, Portfolio & Graduation

**🎯 Objective:** Close the loop.

**🛠 Work:** Final pass against the Day 51 PRD's Success Criteria; `CHANGELOG.md`; tag `v1.0.0`; short portfolio write-up (what was built, what was learned across the 10 days, what v2 would add — e.g. a real Claude API call behind a tiny serverless function instead of the rule-based coach).

**✅ Checklist:** Every Day 51 success criterion checked off explicitly; `v1.0.0` tagged; portfolio write-up committed.
