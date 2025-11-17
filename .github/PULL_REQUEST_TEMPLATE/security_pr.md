---
name: Security fix
about: Submit a security-related fix for boardRL
title: "[Security] "
labels: ["security", "to be triaged"]
---

## Summary

Short description of the security issue you are fixing.

- What was the risk?
- Where in the code did it live (e.g. rules parsing, file I/O, subprocess, etc.)?

If the details are sensitive and not yet disclosed, keep this section high-level and avoid copy-pasting exploit steps.

## Background

Explain the context of the issue:

- How could it be triggered? (e.g. specially crafted `rules.txt`)
- What kind of impact could it have? (e.g. arbitrary code execution, denial of service, data leak)
- Any related issue or private report ID (if applicable)

## What changed

Describe the core of the fix:

- Files and functions modified
- New checks or validations
- Any changes to the `rules.txt` format or allowed input

Example:

- Added input validation to `src/rules_parser.py`
- Disallowed certain patterns or unsafe constructs in `rules.txt`
- Removed or replaced unsafe calls

## How you tested it

Explain how you verified the fix:

- [ ] Reproduced the original issue (locally or in a controlled setup)
- [ ] Confirmed the issue no longer occurs with the fix
- [ ] Checked that normal usage still works

Testing commands or steps:

```bash
# example
python src/train.py --rules rules/reversi_8x8.txt --episodes 1000
```

If you used a malicious or proof-of-concept file, keep details minimal or attach it privately if needed.

## Compatibility / Breaking changes

- Does this fix reject previously valid input (e.g. some old `rules.txt` files)?
- Any changes users need to make after this fix (for example, updating rules or scripts)?
- Any performance impact?

## Disclosure notes

If this fix is tied to a reported vulnerability:

- Has the reporter been notified?
- Are there any timelines or disclosure expectations?
- Any CVE or tracking ID (if applicable)?

## Checklist

- [ ] Fix addresses the security issue described
- [ ] Normal, non-malicious usage still works as expected
- [ ] Comments or docs updated to explain important security assumptions
- [ ] No unnecessary new attack surface introduced
