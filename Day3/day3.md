# Day 3: Role-Based Prompting

**Date:** July 18, 2026

**Challenge:** ABTalks 60-Day Claude AI Mastery Challenge

## What role-based prompting is

Role-based prompting means telling the AI what perspective, expertise, and priorities it should use before giving it a task. A role does not give the model new knowledge, but it changes what it emphasizes, which tradeoffs it notices, and how it structures the answer.

For this experiment I kept the core question the same: **How should I plan and launch a simple habit-tracking app for students?**

## Test 1: No role

### Prompt

> How should I plan and launch a simple habit-tracking app for students?

### Output

The response suggested identifying the audience, choosing basic features such as habit creation, reminders, streaks, and progress charts, building a prototype, testing it with students, and launching it through an app store or website. It also recommended collecting feedback after launch.

### Observation

The answer was useful but broad. It mixed product, technical, and marketing advice without clear priorities or sequence.

## Test 2: Founder persona

### Prompt

> You are a startup founder who has launched several lean consumer apps. How should I plan and launch a simple habit-tracking app for students? Focus on validating demand, choosing a narrow first customer, defining an MVP, getting the first 100 users, and deciding what to measure. Keep the plan lean for one person with a small budget.

### Output

The founder response narrowed the customer to first-year college students who struggle with study consistency. It proposed interviewing 10 students before building, testing a clickable prototype, and defining the MVP as only three flows: create a habit, check in daily, and view a weekly streak. It recommended recruiting the first users through one campus community, measuring activation and seven-day retention, and postponing advanced features until students returned without reminders from the founder.

### Observation

This answer prioritized business risk. It challenged the assumption that the app should be built immediately and focused on evidence, distribution, retention, and scope control.

## Test 3: Developer persona

### Prompt

> You are a senior full-stack developer who specializes in reliable, low-cost MVPs. How should I plan and launch a simple habit-tracking app for students? Focus on the data model, core screens, API boundaries, authentication, reminders, testing, deployment, and technical risks. Assume one developer and a small budget.

### Output

The developer response proposed users, habits, and check-ins as the main entities. It mapped the MVP to onboarding, today's habits, habit editing, and weekly progress screens. It recommended managed authentication, a hosted relational database, scheduled notification jobs, server-side validation, and clear timezone handling. It also suggested unit tests for streak calculations, end-to-end tests for daily check-ins, error monitoring, backups, and a staged launch.

### Observation

This answer prioritized delivery and reliability. It surfaced implementation details and technical failure modes missing from the generic and founder answers.

## Comparison

| Version | Perspective | Strongest contribution | What it missed |
| --- | --- | --- | --- |
| No role | General assistant | Broad checklist | Priorities and depth |
| Founder | Market and business | Validation, scope, acquisition, retention | Detailed implementation |
| Developer | Product engineering | Architecture, testing, deployment, risks | Customer discovery and distribution |

## What I learned

1. A role changes priorities, not just tone.
2. A strong role includes experience and constraints, not only a job title.
3. Keeping the question constant makes the role's effect easy to compare.
4. Founder and developer personas complement each other: one reduces market risk and the other reduces delivery risk.
5. For important work, I can ask several roles independently and combine their strongest recommendations.

## Reusable template

> You are a [specific role] with experience in [relevant domain]. [Task or question]. Focus on [priorities]. Assume [constraints]. Return the answer as [format].

## LinkedIn-ready image concept

- Square 1080 x 1080 post
- Claude-inspired brown, beige, and cream palette
- Title: Role-Based Prompting
- Subheading: ABTalks 60-Day Claude AI Mastery Challenge
- Subtitle: Turn Claude into Any Expert You Need
- Comparison: Without Role Prompt -> Generic Answer / With Role Prompt -> Expert-Level Answer
- Persona cards: Developer, Product Manager, HR Manager, Founder, Marketer
- Minimal, professional, and readable on mobile
