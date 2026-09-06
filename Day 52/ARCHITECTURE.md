# Technical Architecture — Momentum (Capstone Day 2 / Program Day 52)

Turns the Day 51 PRD + Blueprint into a concrete design so Day 53 can scaffold it directly and Day 54+ can build against it without re-deciding anything.

## 1. Tech Stack

Vanilla HTML/CSS/JavaScript, no build step, no framework, no backend. Chosen deliberately: the whole point of v1.0 is a zero-infrastructure static site that deploys to GitHub Pages with no server, no API keys in the client, and no dependency-update burden during a 10-day sprint. A framework would cost setup time this sprint can't afford and buys nothing a 4-file vanilla app can't already do at this scale.

## 2. File Layout

```
momentum/
├── index.html        # shell: header, nav (Goals / Coach / Stats), main content mount, footer
├── styles.css         # CSS custom properties for theme (light/dark), layout, components
├── storage.js         # localStorage read/write, the only module that touches localStorage
├── coach.js           # pure functions: suggestHabits(), generateWeeklyPlan(), generateReflection()
├── heatmap.js          # pure function: checkIns -> calendar grid data
└── app.js             # state, rendering, event wiring — imports the above as plain <script> globals
```

No bundler: files are loaded via `<script>` tags in dependency order (`storage.js`, `coach.js`, `heatmap.js`, then `app.js`), each attaching to a small shared namespace (`window.Momentum = {...}`) instead of ES module imports, so the app runs by opening `index.html` directly with no local server required.

## 3. Data Model

```js
// Goal
{ id: "g_<timestamp>", title: "Run a 5K", category: "fitness", createdAt: <iso> }

// Habit (belongs to a Goal)
{ id: "h_<timestamp>", goalId: "g_...", title: "Run 20 minutes", cadence: "daily" }

// CheckIn (one per habit per calendar day)
{ habitId: "h_...", date: "YYYY-MM-DD", done: true }

// WeeklyReport (generated, cached so re-opening the app doesn't regenerate mid-week)
{ weekStart: "YYYY-MM-DD", plan: "...", reflection: "...", generatedAt: <iso> }
```

Top-level persisted shape in `localStorage` under key `momentum_state_v1`:

```js
{ goals: Goal[], habits: Habit[], checkIns: CheckIn[], weeklyReports: WeeklyReport[], theme: "light" | "dark" }
```

A single top-level key (not one key per collection) keeps export/import a single JSON blob and avoids partial-write inconsistency between collections.

## 4. State Management Approach

No reactive framework — a deliberately simple pattern for a 10-day solo build:

1. `storage.loadState()` on boot → in-memory `state` object in `app.js`.
2. Every user action mutates `state` then calls `storage.saveState(state)` (debounced 250ms for rapid actions like heatmap scrubbing) and `render()`.
3. `render()` is idempotent and re-renders the active panel from `state` — no diffing, the DOM trees here are small enough (a handful of goals/habits) that full re-render per action is imperceptible.

This trades "framework best practice" for "zero dependencies, entirely readable by Day 58's debugging pass" — appropriate for the project's actual size.

## 5. Coaching-Engine Interface

Defined now so Day 54 and Day 56 implement against a fixed contract instead of improvising:

```js
// coach.js
suggestHabits(goalTitle: string) -> Habit[]           // Day 54
generateWeeklyPlan(state) -> string                    // Day 56
generateReflection(state) -> string                    // Day 56
```

`suggestHabits` keyword-matches the goal title against category templates (fitness/learning/project/health) with a generic 3-habit fallback so it never returns an empty list. `generateWeeklyPlan`/`generateReflection` both take the full `state`, compute per-habit streak/completion numbers, and interpolate the strongest and weakest habit by name and number into a short templated paragraph — real data in, not a static string. This interface is intentionally the same shape a real LLM call would have (`(context) -> string`), so a v2 swap to an actual Claude API call behind a serverless endpoint changes only the function body, never the caller.

## 6. Theming

CSS custom properties on `:root` (`--bg`, `--fg`, `--accent`, `--card`, etc.), redefined under `[data-theme="dark"]`. `app.js` toggles `document.documentElement.dataset.theme` and persists the choice in `state.theme`.

## 7. Non-Goals (carried from the PRD)

No bundler, no framework, no backend, no real API calls in v1.0 — confirmed here at the architecture level so Day 53 scaffolds exactly 5 files and nothing else.
