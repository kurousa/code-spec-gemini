---
description: Show specification status and progress
allowed-tools: read_file, run_shell_command
---

# Specification Status

Show current status and progress for feature: **$ARGUMENTS**

## Spec Context (Instructions for the Agent)

To generate the report, the agent must read the following files from the `.kiro/specs/$ARGUMENTS/` directory:
- `spec.json` (for phase, approvals, and description)
- `requirements.md`
- `design.md`
- `tasks.md` (for progress calculation)

## Task: Generate Status Report

The agent will create a comprehensive status report for the specified feature.

### 1. Specification Overview
Display:
-   **Feature Name**: From `spec.json`
-   **Description**: From `spec.json`
-   **Current Phase**: From `spec.json` (e.g., `design-generated`)
-   **Approval Status**: Summarize the `approvals` object from `spec.json`.

### 2. Implementation Progress

#### Task Completion Tracking
-   **Read `tasks.md`**: The agent must read the content of `.kiro/specs/$ARGUMENTS/tasks.md`.
-   **Count Tasks**: 
    -   Count completed tasks by matching lines with `- [x]` (e.g., using regex `^\s*-\s*\[x\]`)
    -   Count total tasks by matching lines with either `- [x]` or `- [ ]` (e.g., using regex `^\s*-\s*\[[ x]\]`)
-   **Calculate Percentage**: Compute `(completed / total) * 100`.
-   **Display Progress**: Show the numbers and the calculated percentage.

    Example Output:
    -   **Tasks Progress**: ▓▓▓░░░░░░░ 3/10 (30%)

### 3. Phase Status & Next Steps
Based on the `phase` value in `spec.json`, provide a clear status and the next action for the user.

-   **If `phase` is `initialized`**:
    -   **Status**: Requirements need to be generated.
    -   **Next Step**: Run `kiro spec-requirements $ARGUMENTS`.

-   **If `phase` is `requirements-generated`**:
    -   **Status**: Requirements are generated and need to be reviewed.
    -   **Next Step**: Review `requirements.md`, then run `kiro spec-design $ARGUMENTS`.

-   **If `phase` is `design-generated`**:
    -   **Status**: Design is generated and needs to be reviewed.
    -   **Next Step**: Review `design.md`, then run `kiro spec-tasks $ARGUMENTS`.

-   **If `phase` is `tasks-generated`**:
    -   **Status**: Ready for implementation.
    -   **Next Step**: Start working on the tasks in `tasks.md`. Mark them as complete with `[x]` as you go.

## Instructions for the Agent

1.  **Read Spec Files**: Read `spec.json` and `tasks.md` from the `.kiro/specs/$ARGUMENTS/` directory.
2.  **Parse `spec.json`**: Extract the feature name, description, and current phase.
3.  **Parse `tasks.md`**: Read the file line by line. Use string matching or regex to count the total number of tasks (`- [ ]` and `- [x]`) and the number of completed tasks (`- [x]`).
4.  **Calculate Progress**: Compute the completion percentage.
5.  **Generate Report**: Present the information to the user in a clear, structured format as described above.
6.  **Provide Actionable Next Step**: Based on the current phase, tell the user exactly what to do next.
