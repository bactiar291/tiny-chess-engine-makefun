# Orbit Chess

[![make.fun](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/bactiar291/tiny-chess-engine-makefun/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard)
[![reward](https://make.fun/badge/tiny-chess-01/bactiar291/tiny-chess-engine-makefun/reward.svg)](https://make.fun/bounty/tiny-chess-01)

Original compact chess engine for tiny-chess-01. Python 3.13 standard library only. The entry is main.py, packed unchanged from locally retained readable source with the official makefun compressor. No other repository file is used at runtime.

Run with MAKEFUN_ENV_URL set to the competition environment:

    python3.13 -P -s main.py

The engine posts documented JSON to /game and /move, with /resign only for a turn without supplied legal moves, and exits after status done. No model calls, opening book, external weights, or network services are used. The supplied FEN and game history determine moves; no randomness or clock controls search.

Search uses a 0x88 board, legal move filtering, all promotion choices, castling and en passant, negamax/PVS, capture/check quiescence, iterative deepening, capture and killer ordering, and a per-move transposition ordering table. Evaluation combines material, generated piece-square terms, bishop pair, pawn structure, passed pawns and phase-dependent king safety. Pawn-file counts, rank masks and extrema preserve the original integer arithmetic; a bounded 16,384-entry board/king cache avoids repeated evaluation. The fixed search allowance is 80,000 nodes; incomplete iterations are discarded. Local checks found exact evaluation agreement and faster search at equal budgets; these measurements establish no Elo or playing-strength improvement. Supplied root legal moves are checked against local generation, with a deterministic legal fallback on unsupported input.

Limitations: small handcrafted evaluation, no endgame tablebases, no cached transposition score bounds, and a fixed depth ceiling. Local timings are machine-dependent. Practice results do not establish a statistical lead over the baseline or a paid placing. Qualification and replay must be verified before submission.

MIT licensed. Readable source and development tests remain local and are excluded from the submitted snapshot; the source accompanies the authorship bundle.
