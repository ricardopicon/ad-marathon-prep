# ad-marathon-prep

Training plan and log for the **Abu Dhabi Marathon, Saturday 12 December 2026**.
Goal: **sub-4:00** (~5:41/km average pace). Training starts **Wednesday 22 July 2026**.

## Files

- **`Marathon_Training_Plan.xlsx`** — the plan and the log, in one workbook. Works on
  laptop (Excel/LibreOffice) and phone (Excel mobile app). Sheets:
  - `Overview` — race date/goal, live countdown, pace zones, phase legend.
  - `Weekly Plan` — every planned session from 22 Jul to race day, one row each, with
    columns to log what actually happened.
  - `Weekly Summary` — auto-computed adherence (planned vs. completed) and average RPE per week.
  - `Plan Changelog` — dated record of any changes made to the upcoming weeks and why.
- **`.claude/skills/adapt-training-plan/SKILL.md`** — how Claude logs sessions and adapts
  the plan when working in this repo (see below).

## The plan, in brief

21 weeks, **Sunday→Saturday** (matching the UAE week — weekend is Fri/Sat, both used for the
week's two key running sessions). 6 training days/week, 1 full rest day (Sunday), gym 3x/week
(Legs/Push/Pull) combined with easy runs on non-long-run days.

| Weeks | Phase | Focus |
|---|---|---|
| 1-7 | Base building | Build a running habit and gym routine, keep playing football |
| 8-13 | Aerobic build | Add tempo/marathon-pace work; **Wk13 = half-marathon time trial** |
| 14-18 | Peak | Highest volume, marathon-pace long runs, taper football to 1x/week then stop |
| 19-21 | Taper | Volume down, stay sharp; **race is Wk21's long-run slot, Sat 12 Dec** |

Deload (cutback) weeks: 5, 10, 14. The Week 1 baseline 5K time trial and Week 13
half-marathon time trial are checkpoints — their results recalibrate the pace zones on
`Overview`, since the current plan is built from a target time rather than a measured one.

## Logging your training

Fill in the yellow columns on `Weekly Plan` for each session as you go: mark it
`Completed`, and log actual distance, duration, pace, RPE (1-10), how it `Felt`, and any
notes. You can do this directly in Excel, or just tell Claude what you did (e.g. *"ran 8km
today at 5:50 pace, legs felt heavy"*) and it'll fill in the right row.

## How adaptation works

Ask Claude to update the plan based on recent training (or it'll offer to, when logged
sessions suggest it should). It only ever adjusts **upcoming, not-yet-logged weeks** — past
weeks and the race date are never touched — and follows fixed rules (documented in the skill):
cut volume after missed sessions or pain, ease paces if effort's consistently too high, hold
the pre-set progression if things are going well, and recalibrate goal pace at the two time
trials. Every change gets logged on `Plan Changelog` with the reasoning, so it's always
reviewable.

## Practical notes

- Football (2-3x/week) is fine through the Base phase — it's part of the current fitness
  base. Taper it to 1x/week during Peak, and stop entirely from the Taper phase (injury risk
  isn't worth it that close to race day).
- Easy pace should feel conversational. If a session hurts (not just "tired") — stop, log it
  honestly, and let the plan adapt rather than pushing through.
- Gym days are scheduled (Legs/Push/Pull) but exercise/weight selection is up to you — log
  it in the Notes column if you want to track progression.
