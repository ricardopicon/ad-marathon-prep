---
name: adapt-training-plan
description: "Use this skill whenever the user reports on marathon training for the Abu Dhabi Marathon plan in this repo — logging a completed run/gym session (\"ran 8km today, felt tired\", \"did legs at the gym\", \"skipped Tuesday's run\"), asking to update/adjust/adapt Marathon_Training_Plan.xlsx based on how training has gone, or asking for a status check on the plan (how many days to race, how adherence looks, whether the goal pace still makes sense). Only applies to the Marathon_Training_Plan.xlsx workbook in this repo — not general spreadsheet tasks."
---

# Adapt Abu Dhabi Marathon training plan

`Marathon_Training_Plan.xlsx` (in this repo) is both the training plan and the training log for
a sub-4:00 Abu Dhabi Marathon (12 Dec 2026). It has four sheets: `Overview`, `Weekly Plan`
(one row per planned session, columns A-J planned / K-Q actual+log), `Weekly Summary` (formula
rollups), `Plan Changelog`.

Use the `xlsx` skill's tools/conventions (openpyxl, `scripts/recalc.py`) for every edit below —
never hand-edit XML, and always run `recalc.py` after writing so formulas stay live. (If
`recalc.py` hangs or fails in a given sandbox, note that plainly rather than silently skipping
verification - the formulas will still compute correctly the next time the file is opened for
real in Excel/LibreOffice, since recalculation on open is their default behavior.)

## 1. Logging a session

Given a natural-language report, find the matching row in `Weekly Plan` (match by date if
given, otherwise the nearest unlogged past session of that type) and fill in its input columns
(K-Q, the yellow ones): `Completed (Y/N)`, `Actual (km)`, `Actual Duration`, `Actual Pace`,
`RPE (1-10)`, `Felt`, `Notes`. Leave every other column untouched. If nothing matches (an extra
session, or a different day than planned), still record it in the closest row's Notes rather
than inventing a new row.

If the report mentions pain, injury, or being sick, still log it, then run the adaptation check
below — don't wait to be asked.

## 2. Adapting upcoming weeks

Adaptation is bounded and only ever touches **the next 1-3 weeks that have no logged sessions
yet**. Never rewrite a week that already has `Completed` entries, never move the race date, and
never change the phase skeleton (Base building/Aerobic build/Peak/Taper) or the weekly
day-of-week pattern (gym Mon/Wed/Thu, quality Tue, medium-long Fri, long run Sat, rest Sun) —
only the *volume and target pace* inside that pattern.

Look at the most recently logged 1-2 weeks in `Weekly Plan` / `Weekly Summary` and apply
whichever of these fits (state which rule you used):

- **>2 sessions missed in a week, or Notes mentions pain/injury** → cut the next week's
  `Planned (km)` on the long run and medium-long run by ~20%, and hold (don't progress) until
  a week goes by with no pain/missed sessions.
- **RPE consistently high (8+) or Notes says runs feel harder than expected at easy effort** →
  ease that week's target paces (loosen the `Planned Pace/Effort` band on the Overview pace
  table by ~10-15 sec/km), hold volume flat rather than increasing it.
- **On plan / feeling good (RPE mostly ≤6, no missed sessions)** → let the pre-set progression
  run as already written; do not accelerate it further (long run week-over-week increase is
  capped at ~15% except at the pre-planned deload weeks: 5, 10, 14).
- **Week 1 baseline 5K time trial or Week 13 half-marathon time trial just got logged** →
  recompute the goal marathon pace from that result (HM time × ~2.11 ≈ marathon time; for the
  5K, use a standard race-time-equivalent table) and update the pace-zone table on `Overview`
  plus the `Planned Pace/Effort` values for all not-yet-logged weeks. If the new pace implies
  sub-4:00 is clearly out of reach or comfortably beaten, say so plainly and ask the user
  whether to change the stated goal on Overview — don't silently change it.

After any adjustment: add a row to `Plan Changelog` (Date, Week(s) affected, Change made,
Reason, Changed by = "Claude (skill)"), run `recalc.py`, and give the user a short summary of
what changed and why.

## 3. Status checks

For "how am I doing" / "how many days left" type questions, read `Overview` (days/weeks to
race) and `Weekly Summary` (adherence, avg RPE per week) rather than recomputing by hand.
