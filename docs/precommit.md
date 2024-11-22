# Pre-commit Hooks

## Motivation

Pre-commit hooks help maintain code quality and consistency by running automated checks before each commit. This prevents problematic code from being committed and ensures all contributors follow the same standards. Our pre-commit configuration helps with:

- Code formatting
- Linting
- Type checking
- Security checks
- Import sorting
- Trailing whitespace removal
- And more!

## Usage

1. First, install pre-commit:
```bash
pip install pre-commit
```
2. Prepare the git hooks:
This is the configuration file for the pre-commit hooks. The file must be named `.pre-commit-config.yaml` and placed in the root of the repository.
```bash
repos:
-   repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.5.0
    hooks:
    -   id: trailing-whitespace
    -   id: end-of-file-fixer
    -   id: check-yaml
    -   id: check-added-large-files
    -   id: check-case-conflict
    -   id: check-merge-conflict

-   repo: https://github.com/psf/black
    rev: 24.2.0
    hooks:
    -   id: black
        language_version: python3
```

3. Install the git hooks:
```bash
pre-commit install
```

## Interesting hooks

- `check-merge-conflict`: This hook checks for merge conflicts in the code. If a merge conflict is found, the commit is rejected.
- `check-case-conflict`: This hook checks for case conflicts in the code. If a case conflict is found, the commit is rejected.
- `check-added-large-files`: This hook checks for added large files in the code. If a large file is found, the commit is rejected.
- `check-yaml`: This hook checks for YAML syntax errors in the code. If a YAML syntax error is found, the commit is rejected.
- `black`: This hook formats the code using the Black formatter.
[..., TBC]


