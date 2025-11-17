# Contributing to boardRL

Thanks for checking out boardRL. This is mainly a learning / side project around reinforcement learning for board games, but I am happy for people to experiment, break things (in a safe way), and open pull requests.

The main things that would be helpful right now are:

- Better support for new games via `rules.txt`
- Integrations or experiments with different backends (for example, CoreML)

If you are unsure whether an idea fits, feel free to open an issue first and describe what you want to do.

## Basic Workflow

1. Fork the repository.
2. Create a new branch for your changes:
   ```bash
   git checkout -b feature/my-change
   ```

3. Make your changes in `src/` and add or update tests if it makes sense.
4. Run any basic checks you can (for example, a quick training run).
5. Commit and push:

   ```bash
   git commit -m "Describe your change"
   git push origin feature/my-change
   ```
6. Open a pull request with a short summary of what you changed and why.

The codebase is still small and evolving, so things may move around. Try to keep changes focused and avoid huge “do everything” PRs.

## Adding a New Game via `rules.txt`

If you want to add a new game definition (for example, another Reversi variant, Checkers variant, or a simple experimental game):

1. Add a new rules file under `rules/`, for example:

   - `rules/reversi_10x10.txt`
   - `rules/checkers_8x8_kings.txt`
   - `rules/custom_5x5_capture_all.txt`

2. Follow the same general structure used by existing rules files:
   - `[board]` section for size and layout
   - `[players]` section for player count and symbols
   - `[setup]` for initial positions
   - `[moves]` for movement / capture rules
   - `[terminal]` for end conditions and rewards

3. Update or add documentation:

   - Add a short description of the game and any special rules in `docs/rules_format.md` (if it exists).
   - Mention your new rules file in the README or another suitable place, so people know it is there.

4. Test it:

   - Run a small training run to check that the parser does not crash:

     ```bash
     python src/train.py \
       --rules rules/my_new_game.txt \
       --episodes 1000
     ```
   - If something is weird (for example, the game never terminates or always ends in a draw), note this in the PR.

5. Open a pull request:

   - Include a short explanation of what the game is and what you expect the agent to learn (for example: “capture all pieces”, “majority of pieces at the end”, etc.).

## Adding or Requesting CoreML Support

There are two levels here: suggesting CoreML support as a feature, and actually contributing an implementation.

### 1. Opening a CoreML feature request

If you want boardRL to support exporting models to CoreML (for example, to run on macOS or iOS):

- Open a GitHub issue with the title like: `Feature request: CoreML export / integration`.
- Explain:

  - Which RL agent you care about (for example, the DQN agent).
  - What the target platform is (for example, “I want to run the model in a small macOS GUI”).
  - Any constraints you have (for example, model size, latency, etc.).

This helps shape how the integration should look (simple export script vs full pipeline).

### 2. Contributing CoreML integration

If you want to actually implement CoreML support:

1. Pick a starting point:

   - Most likely the DQN agent under `src/agents/dqn_agent.py`.

2. Decide what “CoreML support” means for your contribution:

   - Exporting an existing trained PyTorch/TF model to CoreML (`.mlmodel`).
   - Adding a script like `src/export_coreml.py`.
   - Or wiring CoreML into a separate runtime/front end that queries the trained model.

3. Keep the RL training loop clean:

   - Training can still happen in PyTorch/TF.
   - CoreML is mostly for deployment / inference.
   - Try not to hardwire CoreML-specific code into everything; isolating it in one or two files is ideal.

4. Add simple usage examples:

   - For example, a short section in the README:

     ```bash
     python src/export_coreml.py \
       --model-path models/reversi_8x8_dqn.pt \
       --output models/reversi_8x8_dqn.mlmodel
     ```
   - If you have a small demo app or script, briefly explain how to use it.

5. Test the export:

   - At minimum, check that the exported CoreML model loads and can produce an action for a valid board state.
   - If you have access to Xcode or a macOS/iOS app, mention how you verified it.

6. Open a pull request:

   - Explain what you added, how to run it, and any limitations (for example, “only supports the current DQN architecture, not arbitrary networks”).

## Code Style and General Guidelines

The project does not follow a strict style guide yet, but a few things help:

- Stick to reasonably clear naming (no one-letter variables for important things).
- Keep functions short when possible.
- Add comments where behaviour is not obvious, especially around rules parsing.
- If you add a new dependency, update `environment.yml` and mention it in your PR.

If you are making larger changes, consider opening an issue first so we can talk it through before you write a lot of code.

## Questions

If anything in this document is unclear, open an issue and ask. The project is still in progress, so the contribution process will probably evolve over time.
