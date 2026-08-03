# CLAUDE.md — ad-marathon-prep

Working notes for anyone (human or Claude) editing this repo. Keep this file current.

## What this repo is

Training plan **and** training log for the **Abu Dhabi Marathon, Sat 12 Dec 2026**.
Goal: **sub-3:50** (~5:27/km), recalibrated from the initial sub-4:00 after the Wk1 5K test.
Training starts **Wed 22 Jul 2026**. 21 weeks, Sunday→Saturday weeks (UAE week).

**Weekly template (from Wk3/Aug 2026 onward — Wk1-2 predate this change):** all 3 gym sessions
(Legs/Push/Pull) stay, but running is capped at 4 sessions/week by pairing each gym day with a
run rather than leaving quality/medium-long runs standalone: Mon Gym Legs + easy run, Tue Gym
Push + quality (tempo/intervals), **Wed full rest**, Thu Gym Pull + medium-long run, **Fri full
rest** (optional: 20-25min elliptical + hip/knee mobility work, entirely optional, not a
prescribed day), Sat long run (run-only, the one day never paired with gym), Sun full rest.
4 training days, max 2 in a row (Mon-Tue), 2 full rest days (Wed, Sun) plus Fri as a third
mostly-rest day — changed from an original 6-day/1-rest template, then from a since-corrected
"drop Push/Pull to 1 gym day" version, because the user wants all 3 gym days kept but running
volume/frequency reduced instead; see `Plan Changelog` for both revisions.

The whole thing lives in one workbook so it works on laptop (Excel/LibreOffice) and phone
(Excel mobile).

## `Marathon_Training_Plan.xlsx` — sheet structure

| Sheet | What it is |
|---|---|
| `Overview` | Race date/goal, live countdown, pace zones (placeholders until the time trials), phase legend. Yellow cells = user-editable pace zones. |
| `Weekly Plan` | One row per planned session, 22 Jul → race day. Columns **A–K are the plan**, **L–R are the log** (yellow input cells). |
| `Workouts` | Named workout library. The `Workout` column on `Weekly Plan` references these names exactly. |
| `Weekly Summary` | Formula rollups per week (planned vs. completed, km, avg RPE, adherence). |
| `Plan Changelog` | Dated record of every change to upcoming weeks and why. |

### `Weekly Plan` columns (after the Workout column was added)

`A` Week · `B` Phase · `C` Deload · `D` Date · `E` Day · `F` Session Type · `G` Discipline ·
`H` Planned (km) · `I` Planned Pace/Effort · `J` Planned Focus · **`K` Workout (→ Workouts sheet)** ·
`L` Completed (Y/N) · `M` Actual (km) · `N` Actual Duration (min) · `O` Actual Pace (min/km) ·
`P` RPE (1-10) · `Q` Felt · `R` Notes.

> **Duration/pace convention:** `N` (Actual Duration) is logged in **whole minutes only** —
> no seconds, no h:mm:ss. `O` (Actual Pace) is **never typed in** — it's a formula,
> `=IF(OR(M="",N="",M=0),"",(N/M)/1440)` formatted as `mm:ss`, i.e. duration ÷ distance. If
> someone reports a pace instead of a duration, convert `round(pace × distance)` to a
> whole-minute duration before logging — the displayed pace will then be that rounded value,
> not necessarily their exact reported pace.

> **Important:** the log columns are now **L–R** (they used to be K–Q before the `Workout`
> column was inserted at K). Any formula or note that references the log columns must use the
> L–R positions. `Weekly Summary` formulas reference: `F` (session type), `H` (planned km),
> `L` (Completed), `M` (Actual km), `P` (RPE). Data validations: `L2:L199` = Y/N,
> `Q2:Q199` = Felt.

### The `Workouts` sheet / `Workout` column

Each structured session (intervals, tempo, time trials, strides, race) and each generic run
type (easy / medium-long / long) has a **named** entry on `Workouts` spelling out warm-up,
main set (e.g. *"10 x 2 min @ 4:40-4:55/km, 2 min easy jog between"*), cool-down, target paces
and approx. km. The `Weekly Plan` `Workout` cell holds the matching name so a row like
"Wk15 Tue Intervals" just says **`10 x 2 min`** and the detail lives in one place.

Paces on `Workouts` are **placeholders** pulled from the `Overview` pace zones (pre-time-trial).
Recalibrate them after the **Wk1 5K** and **Wk13 half-marathon** time trials. If you change a
workout's prescription, edit it once on `Workouts` — every referencing row inherits it.

## Editing conventions (do this, not that)

- **Always edit via openpyxl** (or the `xlsx` skill). Never hand-edit the XML.
- After writing formulas, **recalculate**: `python3 <xlsx-skill>/scripts/recalc.py Marathon_Training_Plan.xlsx`.
  If recalc can't run in the current environment (LibreOffice missing/no profile), say so
  plainly — Excel/LibreOffice will recalc on open anyway.
- **Never inefficiently reverse a range** when remapping formulas: rewrite BOTH endpoints of
  a range (`$L$2:$L$999`), not just the first cell.
- If you shift columns again, remember to also update: data validations, cell fills/widths,
  and every cross-sheet formula in `Weekly Summary`.
- A `~$Marathon_Training_Plan.xlsx` file means the workbook is open in Excel. Close Excel
  (without saving) before/after scripted edits so it doesn't overwrite your changes.

## Logging & adapting the plan

See `.claude/skills/adapt-training-plan/SKILL.md` — it defines how to log a session (fill the
yellow L–R columns on the matching row) and the bounded rules for adapting upcoming weeks.
Every adaptation gets a `Plan Changelog` row.

## Git / GitHub

- Remote: `origin` → `https://github.com/ricardopicon/ad-marathon-prep`
- Default workflow after making changes:

```bash
git add Marathon_Training_Plan.xlsx CLAUDE.md README.md
git commit -m "…describe the change…"
git push origin main
```

- Only commit when the user asks. Don't commit the Excel lock file (`~$*.xlsx`) or `.DS_Store`.
- **Push straight to `main`** — routine updates (logging sessions, plan adjustments) commit
  directly on `main`, no feature branch or pull request. Work directly on `main` locally
  (`git checkout main && git pull` first if it's been a while). PRs were used for the initial
  two changes but that's no longer the workflow going forward.
