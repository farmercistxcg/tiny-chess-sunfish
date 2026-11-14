# tiny-chess-01 — sunfish fork (75k nodes)

A 4 KB chess engine for the make.fun tiny-chess-01 bounty: build the
strongest chess engine in 4,096 bytes of Python.

## What it is

A fork of sunfish's 4 KB entry — `nnue_4k/pst_entry.py` of
[thomasahle/sunfish](https://github.com/thomasahle/sunfish) at commit
`e396948acbd80cdcbad3dccfb07e878fba9df8f4` (2026-08-27), by Thomas Ahle
and contributors, GPL-3.0-only — adapted to the make.fun environment:

- The UCI loop is replaced by a driver for the env at `MAKEFUN_ENV_URL`
  (`POST /game`, `/move`, `/resign`).
- The search is a fixed **75,000 nodes per move** (the house baseline uses
  50,000). The node cap is enforced inside the search, so move choice is
  deterministic — no wall clock is used.
- Packed with `pyminify` (`--rename-globals --remove-literal-statements
  --no-hoist-literals`) and `xz --format=lzma --lzma1=preset=9e,pb=0`,
  embedded as a base85 payload with a small Python unpacker.

## Engine

- 120-character string board; the side to move is always "white"
  (the board is rotated after each move).
- MTD-bi iterative-deepening search with a transposition table,
  null-move pruning, internal iterative deepening, late-move reduction
  and quiescence search.
- Classic piece-square evaluation.
- Deterministic: fixed node budget, no clock, no randomness.

## Files

- `main.py` — the whole engine, **4,089 bytes**. Python 3.13 standard
  library only; reads no other file.
- `sunfish_fork.py` — the readable source (sunfish core + env driver).
- `LICENSE` — GPL-3.0-only (SPDX).

## License

GPL-3.0-only. See `LICENSE`. Original sunfish code copyright Thomas Ahle
and contributors.
