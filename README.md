# SchedulingOptomizer
Link to my dynamic CP-SAT website for solving scheduling employees with scheduling constraints.

# 24-Hour Shift Scheduler

A full-stack web app that builds **repeating weekly staff schedules** for around-the-clock operations. You give it each employee's constraints and the number of people you need on each day; it returns a fair, constraint-satisfying weekly template designed to repeat.

🔗 **Live app:** https://bfrazier.pythonanywhere.com/Twenty4HourScheduler

---

## How to use

- Load a save file to see an example! 
- 1. There are 4 different shift types, 1,2,3 and Off. The amount is arbitrary but was intendend for a 24 schedule with individual 8 hour shifts.
- 2. Select how many workers! (Very important to do first)
- 2. Click a scheduling type, then drag along workers days to change their color to indicate differing shifts.
  - You can deselect by redrawing over the same fields with the same shift type (color).
- 3. When finished click the Save and Optomize Button!

- Notes:
- If a run is successfully a success message will inform you of it! 
- Changing the number of workers resets preferences, this will be addressed in future updates.
- SAVE FILES ARE STORED GLOBALLY DUE TO PII ISSUES AND MY DESIRE TO AVOID A TERMS OF SERVICE AND USER AGREEMENT
- 


## Why I built it

This came out of working in 24/7 security operations, where weekly rosters were put together by hand — slow, error-prone, and hard to keep fair across a team. The app turns that into something you configure once: define the constraints, and it generates a workable schedule for you.

## What it does

- Takes user-supplied **per-employee constraints** and the **number of employees required each day**.
- Produces a **weekly schedule template** built to repeat week over week.
- **Maximizes employee preferences** within the user-defined staffing requirements.
- Biases toward each person's worked days and days off **grouped into blocks** rather than scattered, for more livable schedules.
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



## Limitations & future work

- **Headcount is an input, not an output.** The required number of employees per day is supplied by the user; the app does not currently solve for the *optimal* staffing level itself. Letting the model recommend headcount rather than take it as a given is a substantially harder problem, and a deliberate scope boundary for this version.
- Scheduling is handled at the day/weekly-template level rather than continuous intra-day shift assignment.
