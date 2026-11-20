---
name: teach
description: Teach a concept step-by-step within this workspace.
disable-model-invocation: true
argument-hint: "What would you like to learn about?"
---

# Teaching Workspace

Guide the user through multi-session learning grounded in the workspace state.

## Workspace State

- `docs/mission.md`: The guiding compass and user goals. Ground all teaching here. See [MISSION-FORMAT.md](./MISSION-FORMAT.md).
- `docs/lessons/`: Sequential lessons (`NNNN-<slug>.md`). Maintained in `docs/lessons/index.md`.
- `docs/cheatsheet/`: Compressed commands, annotations, and quick references.
- `docs/debugging/`: Diagnostic playbooks with failure sequence diagrams.
- `docs/interview/`: Senior technical and system design question bank.
- `docs/references/`: Official sources (`resources.md`), glossary (`glossary.md`), and reference index (`index.md`).
- `learning-records/`: ADR-style records of demonstrated user understanding (`NNNN-<slug>.md`). See [LEARNING-RECORD-FORMAT.md](./LEARNING-RECORD-FORMAT.md).
- `NOTES.md`: Scratchpad for learner profile and working notes.

## Core Rules

1. **Ground in Mission**: Align every lesson with `docs/mission.md`. If unclear, interview the user first.
2. **High-Trust Knowledge**: Source facts from `docs/references/resources.md`. Verify facts before explaining.
3. **Storage Strength**: Build retention through active recall, desirable difficulty, and hands-on exercises.

## Authoring Lessons

1. **File Location**: Save self-contained lessons to `docs/lessons/NNNN-<slug>.md`.
2. **Catalog Updates**: Check off and link every new lesson in `docs/lessons/index.md`.
3. **Sidebar Rule**: Expose only top-level section roots in `zensical.toml` `nav` (e.g. `{ "Lessons" = ["lessons/index.md"] }`). Keep individual lessons cataloged inside `docs/lessons/index.md`.
4. **Bottom Pagination**: Include navigation linking `Previous Lesson | All Lessons (index.md) | Next Lesson`. Update the previous lesson's "Next" link when adding a lesson.
5. **Visual Diagrams**: Include vertical Mermaid diagrams in every lesson and debugging guide.
6. **Zensical Styling**: Use admonitions (`!!! note`, `!!! tip`), code annotations, and copy buttons.

## Authoring Reference & Debugging Guides

- Cheatsheets: `docs/cheatsheet/`
- Debugging Playbooks: `docs/debugging/` (include failure sequence diagrams)
- Interview Questions: `docs/interview/`
- Catalog all guides in their section `index.md` with bottom pagination tables.

## Mermaid Standards & Verification

### Layout Standards
- **Orientation**: Default to `flowchart TD` (top-to-bottom).
- **Subgraphs**: Stack parallel architectures vertically (`SubA ~~~ SubB`) to maintain readable node widths.
- **Quoted Labels**: Quote node labels with special characters (e.g., `Node["Item (Details)"]`).

### Verification Steps
Run automated verification before completing your turn:

1. Validate diagrams with the local renderer (must report 0 errors):
   ```bash
   uv run python .agents/skills/teach/scripts/validate_mermaid.py
   ```
   Successful renders are cached by content and validator/dependency versions. Unchanged diagrams skip Node and browser startup. Append edited Markdown paths for a focused check; use `--force` to re-render all selected diagrams. Dependencies are installed once during setup; never use `npx` or install tools during validation.
2. Run a whole-site link checker when the project supplies one, so renamed or deleted targets still invalidate incoming links. Run example tests only if executable example code changed.
3. Validate the documentation build once after all edits, using the incremental command:
   ```bash
   uv run zensical build
   ```
4. Report completion summary:
   - Number of Mermaid diagrams checked, newly rendered, and reused from cache (0 errors).
   - Zensical build status.

Use a clean build for initial setup or publishing. Do not rebuild the entire site or rerun unrelated scripts after each individual edit.
