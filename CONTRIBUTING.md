# Contributing

## 1. Introduction

Thank you for your interest in contributing to this project.

Mass Ads.txt Checker is maintained as a lightweight, dependency-free Chrome extension for large-scale `ads.txt` validation workflows. Contributions that improve correctness, reliability, usability, documentation, and maintainability are welcome. This document explains how to contribute effectively, reduce review cycles, and keep changes aligned with the project's current architecture.

Before you open an issue or pull request, please read this guide end to end. Following the conventions below helps maintainers review your work quickly and keeps the repository easy to operate for everyone.

## 2. I Have a Question

The issue tracker is reserved strictly for:

- Reproducible bugs.
- Concrete feature requests.
- Clearly scoped improvements with actionable implementation context.

Please do **not** use GitHub Issues for:

- General usage questions.
- Debugging help for your own environment when the project itself is not demonstrably broken.
- Broad support requests.
- Open-ended architectural discussions without a specific proposal.

If you have a general question, use one of these channels instead:

- **GitHub Discussions** for project-level usage questions, implementation ideas, or design conversations.
- **Stack Overflow** for generic JavaScript, Chrome Extension, Manifest V3, or browser API questions. Tag your post with the most relevant technology tags.
- **Team or community channels** if your organization maintains an internal support space for extension usage.

When asking for help outside the issue tracker, include:

- What you are trying to do.
- What you expected to happen.
- What actually happened.
- Your browser version and operating system.
- Any relevant input domains or sanitized sample data.

## 3. Reporting Bugs

High-quality bug reports are actionable, reproducible, and narrowly scoped. A maintainer should be able to read your report and reproduce the behavior without guessing.

### Search duplicates first

Before opening a new issue:

- Search open issues for the same or similar symptoms.
- Search closed issues in case the problem has already been addressed or documented.
- If an existing issue matches your problem, add relevant reproduction details there instead of opening a duplicate.

### Include complete environment details

Every bug report must include the environment in which the problem occurs. At minimum, provide:

- Operating system and version.
- Browser and version.
- Extension version from `manifest.json` or the installed package.
- Whether you are running a locally loaded unpacked extension or a packaged build.
- If relevant, local runtime versions used for validation checks, such as `node --version` and `python3 --version`.
- Any proxy, VPN, enterprise security tooling, or network restrictions that may affect HTTP or HTTPS requests.

### Provide exact steps to reproduce

Write reproduction steps as a deterministic algorithm, not a summary. Use numbered steps and be explicit.

A strong reproduction section should include:

1. The exact version or branch you tested.
2. How the extension was loaded into Chrome.
3. The exact input data used.
4. The sequence of clicks or actions performed.
5. The observed output, including UI state and network behavior if relevant.

If possible, attach:

- A minimal input list that reproduces the bug.
- Screenshots or screen recordings.
- Sanitized console errors.
- Relevant Chrome extension logs.

### Expected behavior vs. actual behavior

Your report must clearly distinguish between:

- **Expected behavior:** What should have happened, and why.
- **Actual behavior:** What happened instead.

Avoid statements like "it does not work." Instead, describe the precise failure mode, for example:

- The popup never updates past `0/3`.
- A valid `ads.txt` file is classified as `Error / Not Found`.
- CSV export contains malformed rows when domains contain whitespace.
- The popup window opens, but the results table never renders new rows.

### Suggested bug report template

Use this format when creating a bug report:

```md
## Summary
Brief description of the problem.

## Environment
- OS:
- Browser:
- Extension version:
- Install mode:
- Node version (if applicable):
- Python version (if applicable):

## Steps to Reproduce
1.
2.
3.

## Expected Behavior

## Actual Behavior

## Supporting Evidence
- Logs:
- Screenshots:
- Sample input:
```

## 4. Suggesting Enhancements

Enhancement requests are welcome, but they must be grounded in a real operational problem.

The strongest proposals explain not only **what** should change, but also **why** the change is necessary and **how** it will be used in practice.

### Justification

When proposing an enhancement, explain:

- The specific limitation in the current implementation.
- Why the existing behavior is insufficient.
- Whether the request improves correctness, performance, UX, maintainability, or security.
- Whether the change is incremental or architectural.

### Real-world use cases

Every enhancement request should include at least one concrete use case. Helpful examples include:

- AdOps teams auditing thousands of domains and needing additional export metadata.
- Publishers wanting more granular classification beyond `Valid`, `Empty File`, and `Error / Not Found`.
- Teams needing retry controls or configurable concurrency for unstable networks.
- Reviewers wanting improved diagnostics when parsing malformed `ads.txt` content.

### Scope your proposal carefully

Please include:

- A concise problem statement.
- The proposed behavior.
- Any UX impact.
- Any API or file-format impact.
- Any tradeoffs, backward compatibility concerns, or security implications.

For larger changes, provide a short design outline before submitting implementation code. This is especially important for proposals involving:

- New permissions.
- Changes to host access behavior.
- Architectural refactors in `popup.js`.
- Significant UI changes in `popup.html`.
- Build tooling, packaging, or release-process changes.

## 5. Local Development / Setup

This repository is a static Chrome Extension project. There is currently no package manager lockfile, bundler, or framework-specific setup step.

### Fork and clone

1. Fork the repository on GitHub.
2. Clone your fork locally:

```bash
git clone https://github.com/<your-account>/Mass-Ads-Checker.git
cd Mass-Ads-Checker
```

3. Add the upstream remote so you can sync changes later:

```bash
git remote add upstream https://github.com/<upstream-owner>/Mass-Ads-Checker.git
git remote -v
```

### Dependencies

There are no required runtime dependencies to install for normal development because the extension is implemented with plain JavaScript, HTML, and the Chrome Extensions platform.

Optional tooling used for local validation:

```bash
node --version
python3 --version
```

If you do not already have them installed:

- Install **Node.js** to run JavaScript syntax checks.
- Install **Python 3** to validate JSON formatting with the standard library.
- Install **Google Chrome** or another Chromium-compatible browser to load the unpacked extension.

### Environment variables

This project does not currently require any environment variables and does not ship a `.env.example` file.

If future changes introduce environment-based configuration for development tooling, the expected workflow should be:

```bash
cp .env.example .env
```

Until then, no `.env` setup is necessary.

### Running locally

1. Open the browser extension management page:

```text
chrome://extensions/
```

2. Enable **Developer mode**.
3. Click **Load unpacked**.
4. Select your local repository directory.
5. Pin the extension to the toolbar for easier manual testing.
6. Click the extension icon to launch the popup window.

When you update source files, reload the unpacked extension from the extensions page before re-testing.

## 6. Pull Request Process

### Branching strategy

Create all changes on a dedicated topic branch. Do not work directly on `main`.

Use one of the following naming conventions:

- `feature/short-kebab-name`
- `bugfix/issue-number-short-kebab-name`
- `docs/short-kebab-name`
- `refactor/short-kebab-name`
- `chore/short-kebab-name`

Examples:

- `feature/configurable-timeout`
- `bugfix/123-handle-bom-lines`
- `docs/improve-readme-testing-section`

### Commit messages

This repository uses the **Conventional Commits** specification. Write commit messages in the form:

```text
type(scope): short summary
```

Examples:

- `feat: add configurable request timeout`
- `fix: avoid false positives for html responses`
- `docs: add contributor workflow guide`
- `refactor: extract ads txt parsing helper`

Use these common commit types where applicable:

- `feat`
- `fix`
- `docs`
- `refactor`
- `test`
- `chore`

### Upstream synchronization

Before opening a pull request, sync your branch with the latest upstream `main` branch:

```bash
git fetch upstream
git checkout main
git pull --ff-only upstream main
git checkout <your-branch>
git rebase main
```

Resolve conflicts locally and rerun all relevant checks before pushing.

### Pull request description requirements

Every pull request should contain a complete description that helps reviewers understand the change quickly.

Your PR body must include:

- A short summary of the change.
- The problem being solved.
- Links to related issues, if any, using closing keywords when appropriate.
- A description of the implementation approach.
- Evidence of testing, including exact commands run.
- Screenshots or recordings for visible UI changes.
- Notes about follow-up work, tradeoffs, or known limitations.

A useful PR checklist looks like this:

```md
## Summary

## Related Issues
Closes #<issue-number>

## What Changed

## Testing
- `python3 -m json.tool manifest.json >/dev/null`
- `node --check background.js`
- `node --check popup.js`

## Screenshots

## Notes
```

## 7. Styleguides

Contributors are expected to preserve the repository's current lightweight, dependency-free style.

### Source formatting and linting

At the time of writing, this repository does **not** include committed configuration for tools such as:

- `ESLint`
- `Prettier`
- `Black`
- `Flake8`

That means there is no repository-enforced formatter or linter configuration yet. Until one is introduced, contributors must:

- Follow the existing plain JavaScript and HTML style already used in the repository.
- Keep diffs minimal and avoid unrelated formatting churn.
- Prefer readable, explicit code over clever abstractions.
- Use consistent indentation and naming within the touched file.

### Architectural expectations

The current architecture is intentionally simple:

- `manifest.json` owns extension metadata and permissions.
- `background.js` handles toolbar action behavior and popup-window creation.
- `popup.html` defines the UI and inline styles.
- `popup.js` owns input normalization, request orchestration, parsing, rendering, and CSV export.

When contributing, try to maintain these boundaries unless your change is explicitly a refactor.

### Naming conventions

Use these conventions consistently:

- Prefer descriptive function names such as `checkDomainSmart` and `countValidLines`.
- Use `camelCase` for JavaScript variables and functions.
- Keep status labels and user-facing strings explicit and easy to understand.
- Avoid introducing abbreviations that are unclear outside your local context.

### Implementation guidance

- Keep functions focused on a single responsibility where practical.
- Avoid introducing unnecessary dependencies for simple browser-native tasks.
- Preserve compatibility with Manifest V3 conventions.
- Be careful when changing network behavior, permission scope, or popup UX.
- If a change affects output classification or parsing heuristics, document the rationale in the PR.

## 8. Testing

All bug fixes, behavior changes, and new features must include relevant verification.

If you change logic, you are expected to add or update tests when an automated suite exists. Since this repository does not currently ship a formal automated test harness, contributors must at minimum provide:

- Static validation for touched files.
- Manual verification steps.
- Reproduction coverage for the bug or feature addressed.

### Required local checks

Run the following commands before submitting a pull request:

```bash
python3 -m json.tool manifest.json >/dev/null
node --check background.js
node --check popup.js
```

### Recommended manual test flow

1. Reload the unpacked extension in Chrome.
2. Open the popup window from the toolbar icon.
3. Test at least one known valid domain.
4. Test at least one invalid or unreachable domain.
5. Verify progress updates correctly.
6. Verify the results table renders expected statuses.
7. Verify CSV export still works for the updated behavior.

If your change touches parsing or result classification, include before-and-after examples in the PR description.

If your change affects UI or layout, include screenshots.

## 9. Code Review Process

After a pull request is opened, maintainers will review it for correctness, scope, regressions, and alignment with the project's design principles.

### Who reviews

Pull requests are reviewed by project maintainers or trusted collaborators with write access to the repository.

### Approval requirements

Unless a maintainer explicitly states otherwise, the expected merge bar is:

- At least **one maintainer approval**.
- No unresolved review comments.
- All requested changes addressed.
- All required checks and manual verification completed.

Larger refactors, permission changes, or UX-impacting changes may require additional review or a longer discussion period before merge.

### Addressing feedback

When responding to review comments:

- Reply directly to each substantive comment.
- Push focused follow-up commits rather than mixing unrelated changes.
- Rerun relevant checks after every significant update.
- Request re-review only after the feedback has been addressed.

If you disagree with requested feedback, explain your reasoning with technical evidence and propose an alternative. Productive review discussion is welcome; silent dismissal is not.

### Merge expectations

A PR is most likely to merge quickly when it is:

- Small and focused.
- Backed by reproducible validation.
- Clearly documented.
- Easy to review commit by commit.
- Limited to one concern per pull request.

Thank you again for contributing and helping improve the project.
