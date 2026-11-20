---
icon: lucide/book-open
hide:
  - toc
---

# Learn the dbt ecosystem

Build a shop analytics project from your first SQL model through a production release. Use DuckDB for the local labs, then learn how teams deploy, govern, and monitor the same kinds of models on the dbt platform.

[Start the curriculum](lessons/index.md){ .md-button .md-button--primary }
[Set up the DuckDB lab](lessons/0004-adapters-profiles-and-the-local-shop-lab.md){ .md-button }

<div class="grid cards" markdown>

-   **[Learning mission](mission.md)**

    See the project milestones and capstone outcomes.

-   **[Command cheatsheet](cheatsheet/index.md)**

    Look up selectors, commands, and project files.

-   **[Debugging playbooks](debugging/index.md)**

    Diagnose connection, graph, data, and production failures.

-   **[Interview practice](interview/index.md)**

    Work through technical and system design questions.

-   **[References and glossary](references/index.md)**

    Find official documentation and current product names.

</div>

## Learning roadmap

```mermaid
flowchart TD
    A["1. Foundations and execution engines"] --> B["2. Models, sources and materializations"]
    B --> C["3. History, testing and reusable SQL"]
    C --> D["4. Selection, artifacts and operations"]
    D --> E["5. The managed platform and jobs"]
    E --> F["6. Semantic Layer, Catalog and Mesh"]
    F --> G["7. Packages, observability and developer tooling"]
    G --> H["8. Automation, AI and the production capstone"]
```
