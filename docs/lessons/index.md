---
icon: lucide/graduation-cap
---

# dbt Ecosystem curriculum

Follow one shop analytics project from its first local build to a production incident drill. Each lesson includes a diagram, a practice task with an expected result, and recall questions with answer guidance. A checkmark indicates a published lesson.

Start with the engine lessons for context or start building in [the DuckDB lab](0004-adapters-profiles-and-the-local-shop-lab.md). The local exercises use full dbt v2 with DuckDB. Managed features have design or local alternatives when you lack a platform account.

## 1. Foundations and execution engines

Build and inspect the first model in an isolated database.

- [x] [0001 · From loaded data to a dbt DAG](0001-from-loaded-data-to-a-dbt-dag.md)
- [x] [0002 · dbt Core v1 and the parse-to-run lifecycle](0002-dbt-core-v1-and-the-parse-to-run-lifecycle.md)
- [x] [0003 · Fusion, dbt v2 and dbt OSS](0003-fusion-dbt-v2-and-dbt-oss.md)
- [x] [0004 · Adapters, profiles and the local shop lab](0004-adapters-profiles-and-the-local-shop-lab.md)
- [x] [0005 · dbt Cloud CLI, platform CLI and VS Code](0005-dbt-cloud-cli-platform-cli-and-vs-code.md)

## 2. Models, sources and materializations

Represent upstream data, establish grain, and build safe transformations.

- [x] [0006 · Models, refs and project configuration](0006-models-refs-and-project-configuration.md)
- [x] [0007 · Sources and freshness](0007-sources-and-freshness.md)
- [x] [0008 · Seeds and lookup data](0008-seeds-and-lookup-data.md)
- [x] [0009 · Views, tables, ephemeral models and adapter choices](0009-views-tables-ephemeral-models-and-adapter-choices.md)
- [x] [0010 · Incremental models, late data and backfills](0010-incremental-models-late-data-and-backfills.md)

## 3. History, testing and reusable SQL

Capture mutable history and validate both transformations and warehouse data.

- [x] [0011 · Snapshots and slowly changing dimensions](0011-snapshots-and-slowly-changing-dimensions.md)
- [x] [0012 · Generic and singular data tests](0012-generic-and-singular-data-tests.md)
- [x] [0013 · Unit tests and edge cases](0013-unit-tests-and-edge-cases.md)
- [x] [0014 · Macros, Jinja and dispatch](0014-macros-jinja-and-dispatch.md)
- [x] [0015 · Analyses, hooks and user-defined functions](0015-analyses-hooks-and-user-defined-functions.md)

## 4. Selection, artifacts and operations

Inspect what dbt intends to do and build repeatable commands around it.

- [x] [0016 · Selectors, graph operators and named selections](0016-selectors-graph-operators-and-named-selections.md)
- [x] [0017 · Artifacts and run evidence](0017-artifacts-and-run-evidence.md)
- [x] [0018 · State comparison and deferral](0018-state-comparison-and-deferral.md)
- [x] [0019 · Model documentation, exposures and ownership](0019-model-documentation-exposures-and-ownership.md)
- [x] [0020 · Production safety, profiling and recovery](0020-production-safety-profiling-and-recovery.md)

## 5. The managed platform and jobs

Take a tested model from development to production.

- [x] [0021 · Studio IDE, Git and environment roles](0021-studio-ide-git-and-environment-roles.md)
- [x] [0022 · Deploy jobs, triggers and scheduling](0022-deploy-jobs-triggers-and-scheduling.md)
- [x] [0023 · CI jobs, temporary schemas and slim CI](0023-ci-jobs-temporary-schemas-and-slim-ci.md)
- [x] [0024 · Merge jobs and continuous deployment](0024-merge-jobs-and-continuous-deployment.md)
- [x] [0025 · dbt Canvas and visual model development](0025-dbt-canvas-and-visual-model-development.md)

## 6. Semantic Layer, Catalog and Mesh

Publish governed metrics, document lineage and define stable domain boundaries.

- [x] [0026 · MetricFlow, semantic models and entities](0026-metricflow-semantic-models-and-entities.md)
- [x] [0027 · Metrics, time spine and downstream integrations](0027-metrics-time-spine-and-downstream-integrations.md)
- [x] [0028 · dbt Explorer, Catalog and column-level lineage](0028-dbt-explorer-catalog-and-column-level-lineage.md)
- [x] [0029 · Contracts, model versions and groups](0029-contracts-model-versions-and-groups.md)
- [x] [0030 · dbt Mesh and cross-project references](0030-dbt-mesh-and-cross-project-references.md)

## 7. Packages, observability and developer tooling

Add tests and automation as reviewable dependencies.

- [x] [0031 · Package Hub, dbt deps and dbt-utils](0031-package-hub-dbt-deps-and-dbt-utils.md)
- [x] [0032 · dbt-expectations for richer data assertions](0032-dbt-expectations-for-richer-data-assertions.md)
- [x] [0033 · dbt-project-evaluator and architecture rules](0033-dbt-project-evaluator-and-architecture-rules.md)
- [x] [0034 · dbt-codegen, sqlfmt and dbt-checkpoint](0034-dbt-codegen-sqlfmt-and-dbt-checkpoint.md)
- [x] [0035 · dbt-artifacts and Elementary observability](0035-dbt-artifacts-and-elementary-observability.md)

## 8. Automation, AI and the production capstone

Connect the lifecycle and prove that the system can be operated.

- [x] [0036 · dbt Copilot, Wizard and reviewed AI changes](0036-dbt-copilot-wizard-and-reviewed-ai-changes.md)
- [x] [0037 · dbt State and freshness-aware orchestration](0037-dbt-state-and-freshness-aware-orchestration.md)
- [x] [0038 · Platform APIs, integrations and dbt MCP](0038-platform-apis-integrations-and-dbt-mcp.md)
- [x] [0039 · Capstone build and release plan](0039-capstone-build-and-release-plan.md)
- [x] [0040 · Capstone incident drill and portfolio review](0040-capstone-incident-drill-and-portfolio-review.md)

## 9. Serverless dbt workloads on Google Cloud

Run the shop project against BigQuery in Cloud Run Jobs, then schedule, monitor, and recover it.

- [x] [0041 · Choose a GCP runtime for dbt](0041-cloud-run-jobs-and-bigquery.md)
- [x] [0042 · Package and deploy dbt Core to Cloud Run Jobs](0042-build-and-deploy-dbt-to-cloud-run.md)
- [x] [0043 · Schedule and orchestrate dbt on GCP](0043-schedule-and-orchestrate-gcp-dbt-jobs.md)
- [x] [0044 · Operate, retry, and recover serverless dbt builds](0044-operate-and-recover-gcp-dbt-jobs.md)
- [x] [0045 · Capstone · Ship and recover a dbt job on GCP](0045-gcp-serverless-dbt-capstone.md)
