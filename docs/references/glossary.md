# dbt glossary

## Project and execution

| Term | Meaning |
| --- | --- |
| Adapter | The database integration for connections, SQL dialect conventions and materializations. |
| DAG | A directed acyclic graph that records resource dependencies. |
| Grain | The entity or key combination represented by one row. |
| Relation | A dataset reference in the data platform, often a table or view. |
| Materialization | The strategy dbt uses to build or expose a model's query. |
| Source | A declared upstream relation, typically managed by ingestion. |
| Seed | A version-controlled CSV loaded as a relation for lookup or fixture data. |
| Snapshot | A history table that records observed changes to mutable rows over time. |
| Exposure | Metadata describing a downstream use of dbt resources and its owner. |
| Unit test | A test that compares model output against expected rows from controlled input fixtures. |
| Data test | A SQL assertion that returns rows violating a data rule. |

## Deployment and governance

| Term | Meaning |
| --- | --- |
| Target | A named output or environment context used to resolve connection settings and relation names. |
| Manifest | An artifact containing the parsed project graph, resource properties and dependency metadata. |
| State selection | Selecting resources using differences from a recorded baseline. |
| Deferral | Resolving eligible unselected refs to relations from another environment or state artifact. |
| Contract | A declared shape for a model's output, with adapter-dependent constraint support. |
| Public model | A model configured for cross-project use where project dependencies are supported. |
| Semantic model | MetricFlow metadata that describes entities, dimensions, and available aggregations for a model. |
| Metric | A governed calculation over model data with defined aggregation, time and filtering semantics. |
| Time spine | A regular date or time series used for calendar-based metric computation. |
