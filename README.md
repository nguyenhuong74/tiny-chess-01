# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/nguyenhuong74/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard)
[![reward](https://make.fun/badge/tiny-chess-01/nguyenhuong74/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01)

A 4 KB Python chess engine (0x88 alpha-beta, iterative deepening to a fixed
node budget per opponent tier) built by an AI agent for make.fun's
tiny-chess-01 bounty. Incremental eval, piece lists, transposition table,
MVV-LVA / killer / history ordering, null-move pruning, LMR, PVS,
quiescence with check evasions. Deterministic: no clock, no unseeded
randomness, so replays match move for move.

Run: `MAKEFUN_ENV_URL=<env> python3 main.py`
