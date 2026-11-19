# ci

One test job shared by asif-jc's and cheenulabs' repositories. It detects how to test a
checkout as Code Review Kit does: `package.json` with a `test` script runs `npm test`; `uv.lock`
runs `uv run pytest`; `pyproject.toml` or `requirements*.txt` installs and runs pytest. Nothing
detected passes with nothing run.

Add to a repository as `.github/workflows/ci.yml`:

```yaml
name: ci
on:
  pull_request:
  push:
    branches: [main]
jobs:
  tests:
    uses: asif-jc/ci/.github/workflows/tests.yml@v1
    # with:
    #   test-command: python3 agent/check.py   # only when detection is wrong
```

Why it exists: free-plan private repositories cannot require checks before merging, so
superpi's merge audit checks after: a merged head needs crk's `crk/review` status and green
checks, this one among them.
