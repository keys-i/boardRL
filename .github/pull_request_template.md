---
name: Pull request
about: Open a pull request for boardRL (bug fix, feature, or security fix)
title: ''
labels: ['to be triaged']
assignees: ''
---

## Summary

Briefly describe what this PR does.

- Is it a bug fix, feature addition, security fix, or something else?
- One or two sentences is enough here.

## Type of change

Tick all that apply:

- [ ] Bug fix (non-breaking)
- [ ] Bug fix (breaking / changes behaviour)
- [ ] New feature
- [ ] Security fix
- [ ] Documentation / cleanup
- [ ] Other (describe below)

If “Other”, explain here:

```text
<optional>
```

## Related issue(s)

Link any related issues or discussions:

- Closes #ISSUE_ID
- Related to #ISSUE_ID

## Details of the change

Explain what you actually changed.

You can use the table below if it helps:

| Area         | Description                                   |
| ------------ | --------------------------------------------- |
| Code         | e.g. new agent, rule parser change, CLI flag  |
| Behaviour    | e.g. how training / games behave now          |
| API / CLI    | e.g. new flags, changed defaults              |
| Rules format | e.g. new fields or constraints in `rules.txt` |
| Other        | Anything else worth calling out               |

Then add some more detail in plain text:

- New files or modules:

  - `src/...`
- Key functions/classes changed:

  - `...`
- Any changes to how `rules.txt` is parsed or validated:

  - `...`

## How to test

Describe how you tested the change, and how reviewers can reproduce it.

### Example commands

```bash
# Example training run
python src/train.py --rules rules/reversi_8x8.txt --episodes 1000

# Example agent vs agent run
python src/play_agents.py \
  --rules rules/reversi_8x8.txt \
  --model-a models/reversi_8x8_dqn.pt \
  --model-b models/reversi_8x8_dqn.pt \
  --games 10
```

What you checked:

- [ ] Script runs without errors
- [ ] Behaviour looks correct (games finish, no weird crashes)
- [ ] Any new feature behaves as expected
- [ ] For security fixes: confirmed the original issue no longer reproduces

If you added tests, mention them here:

```text
e.g. Added tests in tests/test_rules_parser.py
```

## Security notes (only if relevant)

If this PR is security-related, add a short note here:

* What was the risk in simple terms?
* Does this change reject any previously valid input (e.g. stricter `rules.txt` checks)?
* Any follow-up needed (e.g. documentation, migration notes)?

If not security-related, you can just leave this section as:

```text
Not security-related.
```

## Screenshots / logs (optional)

If it helps to understand the change, include screenshots, logs, or short snippets here:

```text
<paste relevant output or short log here>
```

## Checklist

- [ ] I have run the relevant scripts/commands locally
- [ ] I updated documentation / README / docstrings where it made sense
- [ ] I considered the impact on existing `rules.txt` files and CLI usage
- [ ] I believe this change is reasonably safe for other users of boardRL
