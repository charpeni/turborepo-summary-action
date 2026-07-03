# Turborepo Summary

This action generates human-readable markdown reports from [Turborepo](https://turborepo.com/) run [summary](https://turborepo.com/docs/reference/run#--summarize) JSON output.

> [!NOTE]
> This is a thin GitHub Action wrapper around the [`turborepo-summary`](https://github.com/charpeni/turborepo-summary) CLI. To generate reports outside of GitHub Actions, use the [CLI directly](https://www.npmjs.com/package/turborepo-summary).

<p align="center">
  <img height="800" alt="Example" src="https://github.com/user-attachments/assets/f870a9c5-5eb3-4902-a1a1-729831852f10" />
</p>

## Usage

> [!NOTE]
> If you are using [Remote Caching with Turbo](https://turborepo.com/docs/guides/ci-vendors/github-actions), ensure not to cache `.turbo/runs` (e.g., from [`actions/cache`](https://github.com/actions/cache)), otherwise, all included runs will be summarized.

First, you need to enable summary on the tasks you want to summarize. You can either:

Use [`--summarize`](https://turborepo.com/docs/reference/run#--summarize) flag:

```diff
-pnpm check-types
+pnpm check-types --summarize
```

Or, define [`TURBO_RUN_SUMMARY`](https://turborepo.com/docs/reference/system-environment-variables#turbo_run_summary) environment variable:

```diff
jobs:
  tests:
    runs-on: ubuntu-latest
+   env:
+     TURBO_RUN_SUMMARY: true
```

Finally, as one of the latest steps, run Turborepo Summary action to generate a summary:

```yml
- uses: charpeni/turborepo-summary-action@v1
  if: always()
```
