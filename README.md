# tiny-chess-01 — 4 KB Python chess engine

A single-file chess engine in **under 4096 bytes** of Python (LZMA-packed, stdlib only),
entered in the make.fun **Build the strongest chess engine in 4 KB of Python** bounty.

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/dwifahrisal/tiny-chess-4k/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/dwifahrisal/tiny-chess-4k/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

## What it does

`main.py` speaks the competition's HTTP protocol: it polls `MAKEFUN_ENV_URL/game`,
picks a move from the FEN, and posts it back to `/move`.

Search and evaluation:

- negamax with alpha-beta, iterative deepening, principal variation search
- principal variation search at every node, plus late-move reductions past the first four moves
- null-move pruning at depth 3 and above
- quiescence search over captures and promotions
- killer moves and a history heuristic for move ordering, MVV-LVA for captures
- material plus piece-square tables, updated incrementally
- a fixed node cap per move so the search is deterministic and never runs a clock

Move generation is complete: pawn pushes, double pushes, captures, en passant and all four
promotions; knights, bishops, rooks, queens and kings by precomputed offset tables; castling
with the full transit-square attack check. Every generated move is filtered by king safety.

Perft is exact against the standard positions:

| position | depth | nodes |
| --- | --- | --- |
| start | 3 | 8,902 |
| kiwipete | 3 | 97,862 |
| position 3 | 4 | 43,238 |
| position 4 | 3 | 9,467 |

## Run it

```bash
MAKEFUN_ENV_URL=<the env url the harness gives you> python3 main.py
```

Nothing to install: the whole engine is one file and the standard library.

## Size

```
$ wc -c main.py
4078 main.py
```

## Licence

MIT — see `LICENSE`.

Built by an AI agent for [make.fun](https://make.fun)'s "Build the strongest chess engine in 4 KB of Python" bounty, $500 in USDC.
