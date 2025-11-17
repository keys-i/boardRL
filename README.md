# boardRL

boardRL is a small reinforcement learning project for turn-based X×X board games where the game logic lives in a separate rules file.

Instead of hardcoding each game (Reversi, Checkers, custom n-in-a-row, etc.), you write a `rules.txt` file. boardRL reads that file, builds an environment from it, and then trains an RL agent (through self-play or against a simple baseline) to try to win that specific game.

The main goal is: once the rules are written down, you should not have to keep rewriting the RL training loop every time you want to try a new board game.

## Key Ideas

- Generic core, game-specific behaviour defined in `rules.txt`
- Works with any X×X board (8×8 Reversi, 8×8 Checkers, 5×5 custom games, and so on)
- Agents learn via self-play by playing against each other repeatedly
- You can swap RL backends (tabular Q-learning for small games, DQN or other deep RL for bigger ones)
- Define the rules once, then reuse the same training and evaluation scripts

## How Rules Work

boardRL uses a simple text-based format for describing games. A typical `rules.txt` includes things like:

- Board size (X×X)
- Piece types and initial layout
- Turn order (player 1 vs player 2)
- Legal moves for each piece type
- Capture / flipping rules (for example, Reversi-style line captures or Checkers jumps)
- Terminal conditions (win, loss, draw)
- Reward values (for example, win = +1, loss = −1, draw = 0)

Very rough example of what a Reversi-style file could look like (this is just a sketch, not a strict spec):

```text
[board]
size = 8

[players]
count = 2
symbols = X,O

[setup]
X: d4,e5
O: d5,e4

[moves]
type = directional_flips
directions = N, NE, E, SE, S, SW, W, NW
must_flip_opponent = true

[terminal]
condition = no_legal_moves_for_both
winner = max_pieces
reward_win = 1.0
reward_loss = -1.0
reward_draw = 0.0
````

The parser turns this into an environment that follows a standard RL-style API:

* `state = env.reset()`
* `next_state, reward, done, info = env.step(action)`
* `valid_actions = env.get_valid_actions(state)`

So once the rules are parsed, the rest of the code just treats it like any other RL environment.

## Environment Setup

The project uses conda with an `environment.yml` file.

Create and activate the environment:

```bash
conda env create -f environment.yml
conda activate boardrl
```

If the environment name in `environment.yml` is different, use that instead of `boardrl`.

## Quick Start

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/boardRL.git
cd boardRL
```

### 2. Describe your game

Create a `rules.txt` file, for example:

* `rules/reversi_8x8.txt`
* `rules/checkers_8x8.txt`
* `rules/custom_5x5.txt`

You can document the exact format later in something like `docs/rules_format.md` once it stabilises.

### 3. Train a model for that game

Example: training on an 8×8 Reversi game:

```bash
python src/train.py \
  --rules rules/reversi_8x8.txt \
  --episodes 100000 \
  --algo dqn \
  --save-model models/reversi_8x8_dqn.pt
```

### Common flags

These are the main flags used by `train.py` (names may change as the project evolves):

| Flag              |      Default | Description                                                   |
| ----------------- | -----------: | ------------------------------------------------------------- |
| `--rules`         |     required | Path to the rules file (for example `rules/reversi_8x8.txt`). |
| `--episodes`      |      `50000` | Number of training episodes / self-play games.                |
| `--algo`          | `q_learning` | RL algorithm to use (`q_learning`, `dqn`, etc.).              |
| `--gamma`         |       `0.99` | Discount factor for future rewards.                           |
| `--lr`            |       `1e-3` | Learning rate for the optimiser.                              |
| `--epsilon-start` |        `1.0` | Starting exploration rate (epsilon-greedy).                   |
| `--epsilon-end`   |       `0.05` | Minimum exploration rate.                                     |
| `--epsilon-decay` |     `100000` | Steps or episodes over which epsilon is decayed.              |
| `--save-model`    |       `None` | If set, path where the trained model is saved.                |
| `--log-dir`       |      `runs/` | Directory for logs / metrics (if logging is enabled).         |

Change the defaults in the table to whatever you actually have in your code.

### 4. Evaluate or play

Run two trained models against each other:

```bash
python src/play_agents.py \
  --rules rules/reversi_8x8.txt \
  --model-a models/reversi_8x8_dqn.pt \
  --model-b models/reversi_8x8_dqn.pt \
  --games 50
```

Play against the model yourself:

```bash
python src/play_human.py \
  --rules rules/reversi_8x8.txt \
  --model models/reversi_8x8_dqn.pt
```

## Project Structure

Rough structure at the moment:

```text
boardRL/
├─ rules/
│  ├─ reversi_8x8.txt
│  ├─ checkers_8x8.txt
│  └─ custom_5x5.txt
├─ models/
│  └─ ...                # Saved models
├─ runs/
│  └─ ...                # Logs / metrics
├─ src/
│  ├─ rules_parser.py      # Reads rules.txt and builds an environment spec
│  ├─ envs/
│  │  ├─ base_env.py       # Abstract environment class
│  │  └─ generic_board.py  # Generic X×X board env driven by parsed rules
│  ├─ agents/
│  │  ├─ base_agent.py     # Agent interface
│  │  ├─ q_learning.py     # Tabular Q-learning agent
│  │  └─ dqn_agent.py      # DQN-based agent for larger games
│  ├─ selfplay.py          # Self-play training loop
│  ├─ utils/
│  │  ├─ replay_buffer.py
│  │  ├─ logger.py
│  │  └─ serialization.py
│  ├─ train.py             # Command line training entry point
│  ├─ play_agents.py       # Agent vs agent matches
│  └─ play_human.py        # Human vs model
├─ environment.yml         # Conda environment definition
└─ README.md
```

This is just how it is structured right now. It will probably get rearranged as things get refactored.

## Training Loop Overview

High-level idea of what happens during training:

1. Parse `rules.txt` into an internal description of the game.
2. Build a `GenericBoardEnv` that handles:

   * State representation (board, current player, etc.)
   * Legal moves based on the parsed rules
   * Transition logic and reward calculation
   * End-of-game checks
3. Attach an agent:

   * For small games, use tabular Q-learning over state–action pairs.
   * For larger boards, use DQN or some other neural network based agent.
4. Run self-play:

   * Alternate moves between agent A and agent B.
   * Store transitions `(state, action, reward, next_state, done)`.
   * Periodically update the model using the stored experience.
5. Save the trained model and optionally dump stats/plots for later.

## Metrics and Logging

During training you can log things like:

* Win / loss / draw rates over a sliding window
* Average return per episode
* Average episode length
* Performance against a random or simple scripted opponent

Example call (if logging is implemented):

```bash
python src/train.py \
  --rules rules/reversi_8x8.txt \
  --episodes 100000 \
  --log-dir runs/reversi_8x8/
```

Then you could have a small script to plot results, for example:

```bash
python src/plot_metrics.py --log-dir runs/reversi_8x8/
```

## Roadmap

Stuff that would be nice to add when there is time:
- More expressive rules language (multiple piece types, more complex capture rules)
- Support for random or stochastic rules (dice, events, etc.)
- AlphaZero-style setup with MCTS and policy/value networks
- Simple visualiser (web or desktop) to watch the games
- Tests that check new rules files actually behave as expected

## Contributing

This is mostly a learning / side project, but contributions are welcome.

For details on how to set up the project, coding style, and how to submit changes, see  
[CONTRIBUTING.md](CONTRIBUTING.md).


## License

This project uses the MIT License (or whatever is in the `LICENSE` file).
See [LICENSE](LICENSE) for details.
