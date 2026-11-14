# tiny-chess-01 entry

A compact alpha-beta chess engine in a single `main.py` (<=4096 bytes),
Python standard library only, deterministic (fixed 100000-node budget,
no clock, no randomness in search).

- 0x88 board, pseudo-legal move generation (castling, en passant,
  promotion), make/unmake with an undo stack
- Iterative deepening, transposition table, killer moves, MVV-LVA
  ordering, quiescence (all evasions in check), null-move pruning,
  late-move reductions, check extensions
- No history heuristic: removing it measured +2.3% nps and higher
  Elo on all three practice trials (trial-1 1464 -> 1530)
- Incremental evaluation: material + piece-square tables (midgame /
  endgame king taper) + bishop-pair bonus
- Speaks the trial env protocol (`/game`, `/move`) via `MAKEFUN_ENV_URL`

Measured (official kit scorer, mean of 3 practice trials at 100k nodes): Elo 1475
(trial-1 1430, trial-2 1464, trial-3 1530), above the sunfish baseline
of 1360. 25 wins / 5 draws / 18 losses across 48 games.
