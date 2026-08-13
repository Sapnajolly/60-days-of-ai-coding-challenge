# Day 26

## User

Prior Authorization Workflow Simulator (gamified, drag-and-drop)
Build a single-file, self-contained HTML application (HTML + CSS + vanilla JavaScript, no external dependencies, no build step) that visually simulates the US healthcare Prior Authorization (PA) workflow as an interactive, gamified, drag-and-drop experience.
The simulator should include:
• Three workflow lanes: Patient, Provider, and Payer.
• Interactive drag-and-drop movement of cases between stages.
• Multiple patient scenarios (elective surgery, MRI, specialty medication, inpatient admission).
• Medical necessity evaluation.
• Prior Authorization document collection.
• Submission to payer.
• Review outcomes including Approval, Pend, Denial, Appeal, and Peer-to-Peer Review.
• Educational explanations after every step.
• Progress tracker across the top.
• Days elapsed counter.
• Efficiency score.
• Celebration animation on approval.
• Workflow summary on completion.
• Responsive modern UI using shades of blue with black text.
• Working Restart / New Patient button.
• Fully functional buttons and interactions.
Technical Requirements:
- Single HTML file.
- HTML, CSS and Vanilla JavaScript only.
- No frameworks.
- No CDNs.
- No localStorage.
- All workflow state managed in JavaScript memory.
- Well-commented code.
- Scenario data stored in an editable array near the top.
- Output only the complete HTML file without truncation.

## Assistant

Built a single-file Prior Authorization Workflow Simulator (`pa_simulator.html`) meeting all requirements:

- Three workflow lanes — **Patient, Provider, Payer** — each with its own dropzones.
- Drag-and-drop movement of a case card through a linear stage sequence, with gates that lock progression until required actions (medical necessity check, document collection, submission, payer review) are completed.
- Four editable patient scenarios in a `SCENARIOS` array near the top of the script: elective knee surgery, lumbar MRI, specialty biologic medication, and inpatient pneumonia admission — each with its own required docs, day costs, and decision-weighting.
- Medical necessity evaluation step, document checklist, and submission action.
- Payer review producing a weighted-random outcome: **Approval, Pend, or Denial**, with **Appeal** and **Peer-to-Peer Review** branches available after a denial (each with its own odds of reversing the decision).
- Educational panel with plain-language explanations and "why this matters" context after every step.
- Progress tracker across the top showing all 7 stages with done/active/skipped states.
- Days elapsed counter and Efficiency Score that both update live based on actions taken.
- Canvas-based confetti celebration animation on approval (no external libraries).
- Workflow summary modal on completion showing total days, final score, outcome, and a full timeline log.
- Responsive, modern blue-shades UI with black text throughout.
- Working Restart / New Patient button (with a confirmation prompt if a case is in progress) and a "How To Play" modal.
- Pure HTML/CSS/vanilla JS, no frameworks, no CDNs, no localStorage — all state lives in a single in-memory `state` object.

File delivered: `pa_simulator.html`.

## User

save the entire chat as Day 26.md
