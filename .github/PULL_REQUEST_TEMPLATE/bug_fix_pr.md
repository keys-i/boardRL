---
name: Bug fix
about: Fix a bug in boardRL (training, rules parsing, agents, etc.)
title: "[Bug] "
labels: ["bug", "to be triaged"]
---

## Summary

Describe the bug you are fixing and what this PR changes.

- What was broken?
- What is the fix in plain language?

## Related issue(s)

Link any related issues:

- Closes #ISSUE_ID

## Type of change

Select all that apply:

- [ ] Bug fix (non-breaking)
- [ ] Bug fix (breaking / changes behaviour)

## How to reproduce the original bug

Explain how to trigger the bug on `main`:

1. Rules file (if relevant): `rules/...`
2. Command(s) run:
   ```bash
   # example
   python src/train.py --rules rules/reversi_8x8.txt --episodes 1000
   ```

3. What you saw (logs, error, wrong behaviour):
  
    ```text
    <paste relevant output / traceback>
    ```

## How you tested the fix

Describe what you did to check the fix works:

* [ ] Ran the failing command again and it now works
* [ ] Tried different board sizes / rules
* [ ] Other checks:

Commands / notes:

```bash
# example
python src/train.py --rules rules/reversi_8x8.txt --episodes 1000
```

## Impact

- Does this change break existing behaviour?
- Any changes to `rules.txt` format or CLI flags?
- Anything users should know when updating?

## Checklist

- [ ] Code compiles / runs
- [ ] New or changed behaviour is documented (if needed)
- [ ] Tests added or updated (if applicable)
