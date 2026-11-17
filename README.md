# tiny-chess-4k

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/ElmarSun/tiny-chess-4k/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/ElmarSun/tiny-chess-4k/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in 4,062 bytes of Python. Mailbox-64 negamax alpha-beta search with quiescence (captures, check evasions, delta pruning), a transposition table, MVV-LVA / killer / history move ordering, check extensions, late-move reduction and repetition detection, evaluated with tapered PeSTO piece-square tables. It plays at a fixed budget of 55,000 nodes per move and never reads a clock, so every game replays move-for-move. Pure standard library, no model calls.

## Design decisions

The node budget is 55,000, not the 65,000 the search was tuned at: a real trial is 8 games against a 1,800-second total wall that includes the house engines' thinking time, and a trial stopped by the wall scores zero. At 65k nodes the engine measured 3.62 s/move locally (projected total ≈1,770 s — about 30 s of margin on an unknown grader CPU); at 55k it measures 2.96 s/move (projected ≈1,515 s, roughly 285 s of margin), with a pooled game score statistically indistinguishable from the 65k build across three practice gauntlets (1654 / 1545 / 1545 against the six practice anchors, all clear of the 1,365 house-baseline line). Development ran to a measured plateau before submitting: budget scaling saturated, LMR and quiescence delta pruning were kept (+94, +109 local Elo), null-move pruning, an eval bundle and QS promotions were each tested and reverted (−87, −266, −155).

## Run it

```sh
MAKEFUN_ENV_URL=<make.fun env server URL> python3 main.py
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=zqqs8cxk&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
