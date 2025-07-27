---
description: Generate implementation tasks for a specification
allowed-tools: run_shell_command, read_file, write_file
---

# Implementation Tasks

Generate detailed implementation tasks for feature: **$ARGUMENTS**

## Interactive Approval: Requirements & Design Review

**CRITICAL**: Tasks can only be generated after the agent confirms that the user has reviewed and approved both the requirements and the design.

### Interactive Review Process (Instructions for the Agent)
1.  **Check for Files**: Verify that both `requirements.md` and `design.md` exist in `.kiro/specs/$ARGUMENTS/`.
2.  **Prompt for Requirements Review**: Ask the user: "`requirements.md`をレビューしましたか？ [y/N]"
    *   If 'N', stop and instruct the user to review the file.
3.  **Prompt for Design Review**: If the first answer was 'y', then ask the user: "`design.md`をレビューしましたか？ [y/N]"
    *   If 'N', stop and instruct the user to review the file.
4.  **If both are 'y' (yes)**: Proceed with task generation. First, update `spec.json` to mark both requirements and design as approved.

**JSON update for `spec.json` on approval**:
```json
{
  "approvals": {
    "requirements": {
      "generated": true,
      "approved": true
    },
    "design": {
      "generated": true,
      "approved": true
    }
  },
  "phase": "design-approved"
}
```

## Context Analysis

### Complete Spec Context (APPROVED)
The agent must read and fully understand the approved versions of:
-   `.kiro/specs/$ARGUMENTS/requirements.md`
-   `.kiro/specs/$ARGUMENTS/design.md`

### Steering Context
The agent should also read the following steering documents if they exist:
-   `.kiro/steering/structure.md`
-   `.kiro/steering/tech.md`

## Task: Generate Implementation Tasks

**CRITICAL**: Convert the approved design into a granular, step-by-step checklist of coding tasks. The tasks should be structured as prompts for a code-generation agent, prioritizing a test-driven approach.

### 1. Task Document Generation
Generate the content for `tasks.md`. The agent should check the `language` field in `spec.json` and write the document in that language.

```markdown
# Implementation Plan

This plan is a checklist of coding tasks to be executed. Each item represents a prompt for a code-generation agent.

- [ ] **Phase 1: Setup & Foundation**
  - [ ] 1.1. Set up the initial project structure (directories for models, services, controllers) based on `design.md`.
  - [ ] 1.2. Add and configure necessary testing libraries (e.g., Jest, pytest).

- [ ] **Phase 2: Data Models & Persistence (Test-Driven)**
  - [ ] 2.1. Write tests for the `[Primary Domain]` model's validation and business logic.
  - [ ] 2.2. Implement the `[Primary Domain]` model to pass the tests.
  - [ ] 2.3. Write tests for the data access layer (repository/DAO) for the `[Primary Domain]` model.
  - [ ] 2.4. Implement the data access layer to pass the tests.

- [ ] **Phase 3: Business Logic & Services (Test-Driven)**
  - [ ] 3.1. Write tests for the core business logic in the `[Primary Domain]Service`.
  - [ ] 3.2. Implement the `[Primary Domain]Service` to pass the tests.

- [ ] **Phase 4: API / Endpoints (Test-Driven)**
  - [ ] 4.1. Write integration tests for the `[Primary Domain]` API endpoints (CRUD operations).
  - [ ] 4.2. Implement the API controllers/routers and connect them to the service layer to pass the tests.
  - [ ] 4.3. Implement authentication/authorization middleware for the API as specified in `design.md`.

- [ ] **Phase 5: Frontend Components (Test-Driven)**
  - [ ] 5.1. Write tests for reusable, basic UI components (e.g., Button, Input).
  - [ ] 5.2. Implement the basic UI components to pass the tests.
  - [ ] 5.3. Write tests for the main feature component that displays `[Primary Domain]` data.
  - [ ] 5.4. Implement the main feature component, connecting it to the API.

- [ ] **Phase 6: Final Integration**
  - [ ] 6.1. Write end-to-end tests for the complete user workflow.
  - [ ] 6.2. Ensure all parts are correctly integrated and pass the E2E tests.
```

### 2. Update Metadata
After writing the tasks file, the agent must update `spec.json`:
```json
{
  "phase": "tasks-generated",
  "approvals": {
    "tasks": {
      "generated": true,
      "approved": true
    }
  },
  "ready_for_implementation": true,
  "updated_at": "current_timestamp"
}
```

---

## Instructions for the Agent

1.  **Confirm Approvals**: Ask the user for approval of `requirements.md`, then for `design.md`. Do not proceed if either is 'N'.
2.  **Update `spec.json` for Approvals**: After getting two 'y' responses, read, then update `spec.json` to mark both `requirements` and `design` as approved.
3.  **Read Context**: Read the approved `requirements.md`, `design.md`, and relevant steering files.
4.  **Generate Tasks**: Based on the design, generate a granular checklist of coding and testing tasks. The list should be broken down into phases and follow a test-driven methodology.
5.  **Write to File**: Save the checklist to `.kiro/specs/$ARGUMENTS/tasks.md`.
6.  **Update Metadata for Tasks**: Read and update `spec.json` again to set the phase to `tasks-generated`, mark tasks as approved, and set `ready_for_implementation` to `true`.
7.  **Inform User**: Tell the user that all phases are approved, the implementation tasks are generated in `tasks.md`, and development can now begin.
