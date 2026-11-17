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
## Engine
The search is 0x88 alpha-beta with iterative deepening, driven by a fixed node budget per opponent tier.
Search effort scales with the opponent, so stronger tiers get a larger node budget for each move.
Quiescence search settles captures and escapes checks before the position is evaluated at the leaves.
Null-move pruning trims branches where giving the opponent a free move still fails to improve the score.
Late-move reductions spend less time on moves ordered late, then re-search them when they look promising.
Principal-variation search tests the best move with a full window and probes the rest with a narrow one.
A transposition table remembers positions already searched, keyed by a Zobrist hash of the board.
Move ordering starts with MVV-LVA captures, then killer moves and history scores guide the quiet moves.
Evaluation adds material values to tuned piece-square tables built for each piece type.
Piece-square tables reward central knights, advanced pawns, rooks on open files and safe kings.
The engine keeps an incremental evaluation and piece lists so each move costs only a small update.
Pawn, knight, bishop, rook, queen and king tables were tuned together against the practice opponents.
Mate-distance pruning was removed after testing showed it was a bug rather than a safe shortcut.
The build with mate-distance pruning lost to the nodes-500k opponent in the first practice trial.
The same build without mate-distance pruning beat the nodes-500k opponent, so the pruning stayed out.
Each move searches roughly 120,000 to 130,000 nodes, capped by the per-tier budget for the game.
## Validation
Validation ran three six-game practice trials against depth and node-budget opponents of rising strength.
Trial zero scored five and a half points for an Elo estimate of 1809, losing none of its six games.
Trial one scored three and a half points for an Elo estimate of 1364, the weakest of the three runs.
Trial two scored five points for an Elo estimate of 1654, with five wins against a single loss.
Across the three trials the v2 engine won thirteen games, drew two and lost three out of eighteen.
The mean Elo across the three trials is 1609, up from 1425 for the earlier v1 engine.
The v1 engine had won eleven games, drawn one and lost six in the same practice format.
Games were adjudicated after two hundred plies when neither side had forced a result.
Opponent tiers ran from depth two up to a five hundred thousand node budget per move.
