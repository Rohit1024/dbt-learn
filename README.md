# DBT-Learn

A Zensical course on the dbt ecosystem. The [curriculum](docs/lessons/index.md) takes one shop analytics project from its first DuckDB build through CI, deployment, governed metrics, and incident recovery.

## Local development

Requires Python 3.14 or later, uv, and Node.js 22.13 or later for diagram rendering.

```bash
uv sync --locked
npm ci
uv run --locked python .agents/skills/teach/scripts/validate_mermaid.py
uv run --locked zensical build --clean
```

The generated entry point is `site/index.html`. For local browsing, run `uv run --locked zensical serve`. Use `/teach` in an agent session from this project for guided learning.

## GitHub Pages

The [Documentation workflow](.github/workflows/docs.yml) builds and deploys the site on pushes to `main` or `master`. In the GitHub repository's **Settings → Pages**, set the source to **GitHub Actions**. The configured project URL is [rohit1024.github.io/dbt-learn](https://rohit1024.github.io/dbt-learn/).
