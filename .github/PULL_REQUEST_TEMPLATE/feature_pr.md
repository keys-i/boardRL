---
name: Feature addition
about: Add a new feature to boardRL (games, rules support, agents, CoreML, etc.)
title: "[Feature] "
labels: ["enhancement", "to be triaged"]
---

## Summary

Briefly describe the feature you are adding.

- What does it do?
- Where does it fit (rules, agents, training, logging, CoreML, etc.)?

## Motivation

Why is this feature useful for boardRL?

You can use the table if it helps:

| Aspect          | Description                                     |
|-----------------|-------------------------------------------------|
| Feature summary | Short one-line summary                          |
| Area            | e.g. rules parsing, agents, logging, CoreML, UI |
| Type            | e.g. new feature / improvement / refactor       |

## What changed

List the main changes:

- New files
- Key functions or classes
- Any updates to `rules.txt` format, CLI flags, or config

Example:

- Added `src/agents/new_agent.py`
- Added `--algo new_agent` flag to `src/train.py`
- Updated `README.md` with usage instructions

## Usage examples

Show how to use the new feature:

```bash
# Example command(s)
python src/train.py \
  --rules rules/reversi_8x8.txt \
  --algo new_agent \
  --episodes 50000
```

If relevant, mention any changes to rules format or configuration files.

## Alternatives considered

Short note on other approaches you considered and why you chose this one.

## How you tested it

Describe the tests you ran:

- [ ] Basic training run completes
- [ ] Feature works with at least one `rules.txt`
- [ ] Behaviour is reasonable / stable
- [ ] New tests added (if applicable)

Commands / notes:

```bash
# Example
python src/train.py --rules rules/custom_5x5.txt --episodes 10000
```

## Impact

- Does this change break anything for existing users?
- Do they need to change their `rules.txt` files or scripts?
- Any new dependencies added (remember to update `environment.yml`)?

## Checklist

- [ ] Feature is documented (README or docs)
- [ ] Code is reasonably commented where non-obvious
- [ ] `environment.yml` updated if new dependencies were added
