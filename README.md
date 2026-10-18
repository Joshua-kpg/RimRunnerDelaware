# RimRunnerDelaware

Unofficial Delaware HS boys basketball ratings. Not affiliated with the DIAA or MaxPreps.
Status: **HELD (waiting on hosting)**. Preview: https://joshua-kpg.github.io/RimRunnerDelaware/ (GitHub Pages). No Firebase project yet
(the Google accounts are at their project quota) and Cloudflare Pages is at its project limit, so accounts, picks and follows save only in the
visitor's browser until the site's own Firebase project exists.

## Files
- `index.html` — the whole app (data embedded). `logos/` — small WebP school logos (from MaxPreps school profiles), served with the site.
- `data/results.json` — 2026-27 finals ledger written by the nightly updater.
- `firebase/` — Firestore rules and auth config for the site's future Firebase project (accounts, picks, follows).

## Teams
58 teams: the DIAA (Delaware Interscholastic Athletic Association) 2026-27 member high schools (DIAA athletic director directory, by conference)
that have a MaxPreps boys varsity team with games. DIAA boys basketball has one state tournament and no classes, so every team is in one class (DIAA).
Conferences (DIAA; Blue Hen and Henlopen split into their divisions as listed on each school's 2026-27 MaxPreps league):
Blue Hen Flight A (8), Blue Hen Flight B (9), Henlopen Northern (8), Henlopen Southern (8), Diamond State (8), Independent Conference (6).
DIAA Non-Conference schools (11 on the site) are independents. No Other (non-DIAA) programs met the 8-game rule.

## Season rule
DIAA 2026-27 winter practice starts Mon Nov 9, 2026; competition starts Mon Nov 30, 2026; last regular-season date Wed Feb 24, 2027.
Games involving a DIAA school before Nov 30 are left out (schedule build and nightly updater); games between two non-DIAA schools are kept.
Boys state tournament: Mar 1, 3, 6-7, 10; final Sat Mar 13, 2027.

## Nightly scores
`.github/workflows/nightly-scores.yml` runs `scripts/update_scores.py` at 06:30 and 14:00 UTC (1:30 am / 9:00 am Eastern standard time) and
on manual dispatch. Before `SEASON_START` in index.html (the first game on the MaxPreps schedules) the script makes no requests. From then on it
reads boys basketball finals for the last 3 days from the MaxPreps Delaware scores-by-date page (team-page fallback), matches them to the schedule
by MaxPreps team id + date, records them in `data/results.json` and bakes scores and W-L records into `index.html`. The page recomputes Elo
from those finals. It commits only when data changed; GitHub Pages updates from the commit.
