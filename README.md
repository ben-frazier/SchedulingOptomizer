# SchedulingOptomizer
Link to my dynamic CP-SAT website for solving scheduling employees with scheduling constraints.

# 24-Hour Shift Scheduler

A full-stack web app that builds **repeating weekly staff schedules** for around-the-clock operations. You give it each employee's constraints and the number of people you need on each day; it returns a fair, constraint-satisfying weekly template designed to repeat.

🔗 **Live app:** https://bfrazier.pythonanywhere.com/Twenty4HourScheduler

---

## Why I built it

This came out of working in 24/7 security operations, where weekly rosters were put together by hand — slow, error-prone, and hard to keep fair across a team. The app turns that into something you configure once: define the constraints, and it generates a workable schedule for you.

## What it does

- Takes user-supplied **per-employee constraints** and the **number of employees required each day**.
- Produces a **weekly schedule template** built to repeat week over week.
- **Maximizes employee preferences** within the user-defined staffing requirements.
- Keeps each person's worked days and days off **grouped into blocks** rather than scattered, for more livable schedules.
- Full **create / read / update / delete** on employees and constraints through a live web interface.

## How it works

The scheduling problem is modeled as a constraint-optimization problem and solved with **Google OR-Tools**. Hard constraints — required coverage per day and individual availability — define the feasible space, and a preference-and-grouping objective steers the solver toward schedules that respect employee preferences and cluster on/off days. The app is a full-stack Flask service with SQLite persistence and a live front end.

## Tech stack

| Layer | Tools |
|---|---|
| Optimization | Python, Google OR-Tools |
| Backend | Flask |
| Database | SQLite |
| Frontend | HTML / CSS / JavaScript |

## Running locally

```bash
git clone https://github.com/ben-frazier/shift-scheduler.git
cd shift-scheduler
pip install -r requirements.txt
flask run
```

Then open the local URL Flask prints in your browser.

## Limitations & future work

- **Headcount is an input, not an output.** The required number of employees per day is supplied by the user; the app does not currently solve for the *optimal* staffing level itself. Letting the model recommend headcount rather than take it as a given is a substantially harder problem, and a deliberate scope boundary for this version.
- Scheduling is handled at the day/weekly-template level rather than continuous intra-day shift assignment.
