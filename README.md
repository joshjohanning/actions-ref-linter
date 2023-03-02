# actions-ref-linter
Check to see if there are references to `@main` or `@branch-name` in actions workflow files

## Example usage

```yml
- uses: joshjohanning/actions-ref-linter@v0.0.1
  if: github.event_name == 'pull_request' # suggsted to run this only on PR jobs
  with:
    workflow-path: .github # optionally specify root directory where workflows reside
```


## Example output

This will `exit 1` if it finds any violations and fail the workflow.

```
> Checking workflow file: ./.github/workflows/new-file.yml
  >> Policy violation: "uses: actions/checkout@main"
> Checking workflow file: ./.github/workflows/docker-test.yml
  >> Policy violation: "uses: joshjohanning-org/reusable-workflows/.github/workflows/docker-build.yml@main"
> Checking workflow file: ./.github/workflows/broken.yml
> Checking workflow file: ./.github/workflows/blank.yml
  >> Policy violation: "uses: actions/checkout@main"
> Checking workflow file: ./.github/workflows/lint-testing.yml
  >> Policy violation: "uses: actions/checkout@main"
  >> Policy violation: "uses: actions/checkout@my-fake-branch"
  >> Policy violation: "uses: actions/checkout@my-other-fake-branch"
> Checking workflow file: ./.github/workflows/lint-me.yml
  >> Policy violation: "uses: joshjohanning/actions-ref-linter@main"

Summary: Found 7 policy violations
Error: Found 7 policy violations
```
