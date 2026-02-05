# Amber CI Workflow

GitHub Actions workflow for running [amber](https://github.com/RDI-Foundation/amber) scenarios.

## Usage

Call as a reusable workflow:

```yaml
jobs:
  run:
    uses: rdi-foundation/amber-runner/.github/workflows/amber-runner.yaml@main
    with:
      scenario: path/to/scenario.json5
    secrets: inherit
```

Or trigger manually via workflow dispatch in the GitHub Actions UI.

## Requirements

Your scenario must have an export named `results`. The exported service must return JSON with a `status` field. The workflow polls until `status` is not `"running"`, then saves the response and stops the scenario.

## Artifacts

Uploaded as `scenario-results`:

- `results.json` — the final JSON response, with a `participants` field added that maps component monikers to their `agentbeats_id` (from manifest metadata)
- `provenance.json` — image digests, manifest digests, and GitHub Actions run metadata
