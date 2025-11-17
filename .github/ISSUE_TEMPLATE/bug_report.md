---
name: Bug report
about: Report a bug in boardRL (training, rules parsing, agents, etc.)
title: ''
labels: ['bug', 'to be triaged']
assignees: ''
---


## Describe the bug

A clear and concise description of what the bug is.

Examples:
- Crash during training when using a specific `rules.txt`
- Agent picks invalid moves
- Game never finishes / gets stuck
- Model save/load not working

## To Reproduce

Steps to reproduce the behaviour (as specific as you can):

1. Rules file used (path and name), for example:
   - `rules/reversi_8x8.txt`
2. Exact command you ran:
   
    ```bash
    python src/train.py --rules rules/reversi_8x8.txt --episodes 1000
    ```

3. What happened (logs, error messages, stack trace):

   ```text
   <paste traceback or key log lines here>
   ```

If it only happens with a particular `rules.txt`, please either attach it or paste a minimal version that still triggers the bug.

## Expected behaviour

A clear and concise description of what you expected to happen.

Examples:

- Training should finish without errors.
- The environment should reject illegal moves instead of crashing.
- The game should end after one player has no legal moves.

## Environment

Fill in what you are running on:

| Item           | Value                                      |
| -------------- | ------------------------------------------ |
| OS             | e.g. Ubuntu 22.04 / macOS 14 / Windows 11  |
| Python         | e.g. 3.10                                  |
| Environment    | e.g. conda from `environment.yml` / custom |
| boardRL branch | e.g. `main`                                |
| boardRL commit | e.g. `abcd1234` (if known)                 |

## Training / Run Settings

If the bug happens during training or when running agents, please fill this in:

| Setting          | Value example                              |
| ---------------- | ------------------------------------------ |
| Script           | e.g. `src/train.py` / `src/play_agents.py` |
| Rules file       | e.g. `rules/reversi_8x8.txt`               |
| Algorithm        | e.g. `q_learning`, `dqn`                   |
| Episodes / Games | e.g. `100000`                              |
| Board size       | e.g. `8x8`                                 |
| Other flags      | e.g. `--gamma 0.99 --lr 1e-3`              |

You can paste the exact command you ran as well:

```bash
<your command here>
```

## Rules / Game Details (if relevant)

If the bug seems related to a specific game setup:

| Field         | Value                                  |
| ------------- | -------------------------------------- |
| Rules file    | e.g. `rules/custom_5x5.txt`            |
| Game type     | e.g. Reversi-like, Checkers-like, etc. |
| Custom tweaks | e.g. modified terminal conditions      |

If possible, include the relevant parts of your `rules.txt` (or attach the whole file if it is not too long):

```text
<paste relevant rules sections here>
```

## Logs / Output

If you have logs, stack traces, or training output, please include them here:

```text
<paste error or relevant training output>
```

If you have plots or screenshots (for example, weird win-rate curves), you can link or attach them and briefly describe what they show.

## Additional context

Anything else that might help:

- Did this work on a previous commit?
- Does it only happen with a certain algorithm (`q_learning`, `dqn`, etc.)?
- Does it depend on board size or specific rules?
- Anything you already tried (different seed, fewer episodes, smaller board, etc.).
