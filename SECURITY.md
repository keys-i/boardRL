# Security Policy

## Supported Versions

boardRL is a small learning / side project. There are no formal releases yet, so security support is very informal.

Right now, only the main branch is actively maintained:

| Version / Branch | Supported |
| ---------------- | --------- |
| main             | Yes       |
| tags / older commits | No    |

If the project ever moves to tagged releases (for example, `v0.1.0`, `v0.2.0`), this table will be updated to list which versions still receive fixes.

---

## Reporting a Vulnerability

If you think you have found a security issue in boardRL (for example, something that could allow arbitrary code execution through `rules.txt` parsing, or unsafe file handling), please report it.

You can do this in one of the following ways:

1. **Preferred**: Open a **private security report** (GitHub “Security” tab, if enabled for the repo).
2. Or, if that is not available, email the maintainer (see the email address in the repo’s profile or commit history).
3. As a last resort, open a GitHub issue with a minimal description and mark it clearly as a security concern. Please avoid posting full exploit details publicly straight away.

When you report a vulnerability, please include:

- A short description of the issue.
- Steps to reproduce (for example, a sample `rules.txt` or command line).
- Which commit or branch you tested on.
- Any suggested fixes or workarounds (if you have them).

Since this is a student / side project, there is no guaranteed response time. That said, the aim is to:

- Acknowledge valid reports as soon as they are seen.
- Confirm the issue and discuss possible fixes.
- Patch the problem on `main` and, if needed, mention it in the README or CHANGELOG.

If a report turns out not to be a vulnerability (for example, expected behaviour, or outside the scope of the project), this will be explained in the response.

Please do not use security issues as a place to request general features or RL improvements; open a normal issue for that instead.
