# Package Hub, dbt deps and dbt-utils

A **dbt package** is a reusable dbt project (containing macros, tests, models, or hooks) installed into your project under `dbt_packages/`. Because installed package code compiles and runs inside your own dbt invocations with your warehouse credentials, always check compatibility, inspect release diffs, and pin versions before running `dbt deps`.

## Managing packages and dependencies

On [Package Hub](https://hub.getdbt.com/), check `require-dbt-version` against `dbt --version`, verify adapter support, and confirm what any dbt v2 badge covers before adopting a package.

Declare dependencies in root `packages.yml` using Hub pins, Git URLs (for private internal macro repos using `git:` + `revision:` + optional `subdirectory:`), or local monorepo paths (`local:`):

```yaml
packages:
  - package: dbt-labs/dbt_utils
    version: 1.3.3
  # Private or internal Git example:
  # - git: "https://github.com/org/internal-dbt-macros.git"
  #   revision: v1.2.0
```

Run `dbt deps` to resolve and download dependencies into `dbt_packages/`. Commit `packages.yml` and `package-lock.yml` to Git, and keep `dbt_packages/` in `.gitignore` so CI runs `dbt deps` cleanly with identical locked versions. When upgrading via `dbt deps --upgrade`, inspect the `package-lock.yml` diff for transitive dependency bumps and test affected builds. [dbt deps reference](https://docs.getdbt.com/reference/commands/deps)

## Core `dbt-utils` macros and tests

```mermaid
flowchart TD
    Hub["Package Hub release constraints"] --> Pin["Pin dbt_utils in packages.yml"]
    Pin --> Deps["dbt deps resolves and installs"]
    Deps --> Lock["Review and commit package-lock.yml"]
    Deps --> Macro["Compile key macro for DuckDB"]
    Macro --> Build["Build scratch model and check the grain"]
```

`dbt-utils` provides battle-tested SQL helpers and generic data tests: [dbt-utils](https://github.com/dbt-labs/dbt-utils)

- **SQL generators.** `generate_surrogate_key`, `date_spine`, `star` (select all columns except excluded ones), `pivot` / `unpivot`, `union_relations`, and `deduplicate`.
- **Data tests.** `unique_combination_of_columns`, `expression_is_true`, `recency`, `equal_rowcount`, and `at_least_one`.

`generate_surrogate_key` casts each input column to string, replaces `null` with a fixed sentinel by default, concatenates, and hashes. Never pass extra columns (such as `customer_id`) just to force uniqueness if your grain should be `order_id`, or duplicate orders with different customers will quietly pass! When upgrading from older `surrogate_key`, compare persisted hashes first (note the legacy `surrogate_key_treat_nulls_as_empty_strings` flag changes null hashing).

Hashing a key changes its representation. If two input rows both carry order 1 and customer 101, the same macro inputs produce the same hash on each row. If order 1 appears with two *different* customers, the composite hashes can differ while the promised one-row-per-order grain still fails. Keep a test on the business key.

## Practice with dbt v2 and DuckDB

### What you need

Work from the root of [shop_lab](0004-adapters-profiles-and-the-local-shop-lab.md). This lab pins [dbt-utils 1.3.3](https://hub.getdbt.com/dbt-labs/dbt_utils/1.3.3/).

### Steps

1. Merge this dependency into `packages.yml`:

```yaml
packages:
  - package: dbt-labs/dbt_utils
    version: 1.3.3
```

2. Create `models/orders_package_keys.sql` to compare how `generate_surrogate_key` hashes `null` versus empty string `''`:

```sql
with orders as (
    select
        order_id,
        customer_id,
        cast(null as varchar) as null_marker,
        cast('' as varchar) as empty_marker
    from {{ ref('stg_orders') }}
)
select
    order_id,
    customer_id,
    {{ dbt_utils.generate_surrogate_key(['order_id', 'customer_id']) }} as order_key,
    {{ dbt_utils.generate_surrogate_key(['order_id', 'null_marker']) }}
        <> {{ dbt_utils.generate_surrogate_key(['order_id', 'empty_marker']) }}
        as null_and_empty_differ
from orders
```

3. Create `models/orders_package_keys.yml`:

```yaml
models:
  - name: orders_package_keys
    data_tests:
      - dbt_utils.unique_combination_of_columns:
          arguments:
            combination_of_columns: [order_id, customer_id]
    columns:
      - name: order_id
        data_tests: [unique, not_null]
```

4. Install packages, build, and preview:

```bash
dbt --version
dbt deps --profiles-dir .
dbt build --profiles-dir . --select +orders_package_keys
dbt show --profiles-dir . --select orders_package_keys
```

**Expected result.** Three rows return with three distinct `order_key` hashes, all three tests pass, and `null_and_empty_differ` is `true` in every row. Run `dbt deps --profiles-dir .` again and confirm `package-lock.yml` resolves the exact same version. (On Core v1 releases earlier than 1.10.5, place test arguments directly under the test name instead of `arguments:`). [Data test properties](https://docs.getdbt.com/reference/resource-properties/data-tests)

## Recall

1. Which files should you review and commit during a package upgrade, and which directory should stay out of Git?
2. Can a table containing two rows with the same `order_id` still pass `unique_combination_of_columns: [order_id, customer_id]`?
3. Why should you inspect a newly added third-party package's `dbt_project.yml` and hooks before running `dbt build` in production?

??? note "Answer guidance"
    1. Review and commit `packages.yml` and `package-lock.yml` (plus any code diff in the package release), and keep `dbt_packages/` ignored in `.gitignore`.
    2. Yes, if those two rows have different `customer_id` values. Always enforce the primary `order_id` grain with its own `unique` test.
    3. Package models, hooks (`on-run-start`, `on-run-end`), and macros execute inside your project under your warehouse role, so unreviewed packages can run unexpected DDL/DML or incur heavy compute.

| Previous | Curriculum | Next |
| --- | --- | --- |
| [Previous lesson](0030-dbt-mesh-and-cross-project-references.md) | [All lessons](index.md) | [Next lesson](0032-dbt-expectations-for-richer-data-assertions.md) |
