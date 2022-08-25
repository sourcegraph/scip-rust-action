# Sourcegraph Rust SCIP Indexer GitHub Action

This action generates SCIP data from Rust source code using [rust-analyzer](https://github.com/rust-analyzer/rust-analyzer). The SCIP data can be further uploaded to Sourcegraph using [scip-upload-action](https://github.com/sourcegraph/scip-upload-action).

## Pre-requisites

- GitHub-provided Runners should work out-of-the-box.
- Self-hosted runners need to have Python 3.5+ and `curl` installed, and the runner's target needs to be one for which [`rust-analyzer` release binaries](https://github.com/rust-analyzer/rust-analyzer/releases) are available.

## Usage

The following inputs can be set.

| name         | default   | description |
| ------------ | --------- | ----------- |
| `project_root` | `.`       | The root of the repository. |

The following is a complete example that generates the SCIP index and uploads it to [sourcegraph.com](https://sourcegraph.com). Save it in `.github/workflows/scip.yaml`.

```
name: SCIP
on:
  - push
jobs:
  index:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Generate SCIP data
        uses: sourcegraph/scip-rust-action@main
      - name: Upload scip data
        uses: sourcegraph/scip-upload-action@master
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
```

## Contributing

If you run into issues using this GitHub Action,
please [file an issue](https://github.com/sourcegraph/scip-rust-action/issues),
including relevant CI logs.

Contributors should abide by the [Sourcegraph Code of Conduct](https://handbook.sourcegraph.com/community/code_of_conduct).
