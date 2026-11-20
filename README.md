# DBT-Learn

Learn dbt by building a shop analytics project. Start with a local DuckDB model, then take the same project through testing, deployment, governed metrics, and incident recovery.

**[Open the course](https://rohit1024.github.io/dbt-learn/)** · **[Browse all lessons](docs/lessons/index.md)** · **[Start the DuckDB lab](docs/lessons/0004-adapters-profiles-and-the-local-shop-lab.md)**

## What you’ll build

The course has **45 lessons across 9 modules**. Each lesson includes a diagram, a practice task with expected results, and recall questions with answer guidance.

| Start here | You'll learn to |
| --- | --- |
| [Engines and the local lab](docs/lessons/0004-adapters-profiles-and-the-local-shop-lab.md) | Choose a runtime and adapter, build your first model, and inspect the generated SQL. |
| [Models and incremental builds](docs/lessons/0010-incremental-models-late-data-and-backfills.md) | Define model grain, test key assumptions, and handle late-arriving data. |
| [Managed dbt jobs](docs/lessons/0023-ci-jobs-temporary-schemas-and-slim-ci.md) | Use isolated CI schemas, deferral, and separate deploy and merge jobs. |
| [Semantic Layer and Mesh](docs/lessons/0026-metricflow-semantic-models-and-entities.md) | Define governed metrics, trace their lineage, and publish stable model interfaces. |
| [Serverless dbt on Google Cloud](docs/lessons/0041-cloud-run-jobs-and-bigquery.md) | Run dbt against BigQuery with Cloud Run Jobs and recover a failed release. |

The local lab needs no cloud account. Managed lessons offer local or design walkthroughs where possible. Use the [cheatsheet](docs/cheatsheet/index.md) during exercises and the [debugging playbooks](docs/debugging/index.md) when a build fails.

## Run the docs locally

Install [uv](https://docs.astral.sh/uv/) and use Python 3.14 or later.

```bash
uv sync --locked
uv run --locked zensical serve
```

Open the local URL printed by Zensical. For guided learning in a compatible coding agent, run `/teach` from this repository.

## Validate and publish

With Node.js 22.13 or later, install the locked diagram renderer and run the site checks.

```bash
npm ci
uv run --locked python .agents/skills/teach/scripts/validate_mermaid.py
uv run --locked zensical build --strict
```

The [Documentation workflow](.github/workflows/docs.yml) publishes the built site to GitHub Pages from `main`.
