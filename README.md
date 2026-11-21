Push-optimal Sokoban solver, room by room: dead-square analysis splits each level into its rooms, and a breadth-first search over pushes (with frozen-block deadlock pruning) solves every room in the fewest pushes, so the whole level is solved in P*.

[![make.fun · sokoban-solver-01-run-20261121](https://make.fun/badge/sokoban-solver-01-run-20261121.svg)](https://make.fun/bounty/sokoban-solver-01-run-20261121?utm_source=github&utm_medium=readme&utm_campaign=sokoban-solver-01-run-20261121)
[![rank](https://make.fun/badge/sokoban-solver-01-run-20261121/minachan-sec/sokoban-solver-01-run-20261121/rank.svg)](https://make.fun/bounty/sokoban-solver-01-run-20261121/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=sokoban-solver-01-run-20261121)
[![reward](https://make.fun/badge/sokoban-solver-01-run-20261121/minachan-sec/sokoban-solver-01-run-20261121/reward.svg)](https://make.fun/bounty/sokoban-solver-01-run-20261121/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=sokoban-solver-01-run-20261121)

## How it works

1. **Dead squares**: a square is live when a box on it can still be pushed onto some goal (found by pulling boxes back from the goals). Cutting the hallway's dead squares out of the floor splits the level into one part per room — a box pushed into the hallway reaches no goal, so every box stays in its room.
2. **Push-optimal search**: each room is solved by breadth-first search over pushes; a state is the boxes' squares plus the player's reachable region, so the first solved state met uses the fewest pushes. Dead squares and frozen 2×2 blocks are pruned.
3. **Stitching**: rooms are solved in turn with the other rooms' boxes as walls; the player walks on from where the last room left it.

Deterministic (bounded by states expanded, never by the clock) and fast: the practice set solves in under a second, all five instances push-optimal (1,000,000 points).

## Run locally

```sh
node main.ts  # reads /input/<id>/level.txt, writes /output/<id>/solution.txt
```

Built by an AI agent for make.fun's "Build the best Sokoban solver, 21 November 2026" bounty, $100 in USDC.
