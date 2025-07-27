---
description: Generate comprehensive requirements for a specification
allowed-tools: run_shell_command, read_file, write_file
---

# Requirements Generation

Generate comprehensive requirements for feature: **$ARGUMENTS**

## Context Validation

### Steering Context
The agent should read the following steering documents if they exist to gain context:
- `.kiro/steering/structure.md`
- `.kiro/steering/tech.md`
- `.kiro/steering/product.md`

### Existing Spec Context
The agent should read the following files for the current specification:
- The `spec.json` file at `.kiro/specs/$ARGUMENTS/spec.json` to understand the project description and language.
- The (potentially empty) `requirements.md` file at `.kiro/specs/$ARGUMENTS/requirements.md`.

## Task: Generate Initial Requirements

The agent will generate an initial set of requirements in EARS format based on the feature idea, then iterate with the user to refine them until they are complete and accurate.

The focus is on writing requirements, not code exploration.

### Requirements Generation Guidelines
1.  **Focus on Core Functionality**: Start with the essential features from the user's idea.
2.  **Use EARS Format**: All acceptance criteria must use proper EARS syntax.
3.  **Generate First, Then Iterate**: Generate an initial version first, then refine based on user feedback.
4.  **Keep It Manageable**: Create a solid foundation that can be expanded.

### 1. EARS Format Requirements

**EARS (Easy Approach to Requirements Syntax)** is the mandatory format for acceptance criteria:

- **WHEN** [event/condition] **THEN** [system] **SHALL** [response]
- **IF** [precondition/state] **THEN** [system] **SHALL** [response]
- **WHILE** [ongoing condition] **THE SYSTEM SHALL** [continuous behavior]
- **WHERE** [location/context] **THE SYSTEM SHALL** [contextual behavior]

### 2. Requirements Document Structure
Generate the content for `requirements.md`. The agent should check the `language` field in `spec.json` and write the document in that language.

```markdown
# Requirements Document

## Introduction
[Clear introduction summarizing the feature and its business value]

## Requirements

### Requirement 1: [Major Feature Area]
**User Story:** As a [role], I want [feature], so that [benefit]

#### Acceptance Criteria
This section must contain EARS requirements.

1.  WHEN [event] THEN [system] SHALL [response]
2.  IF [precondition] THEN [system] SHALL [response]

### Requirement 2: [Next Major Feature Area]
**User Story:** As a [role], I want [feature], so that [benefit]

1.  WHEN [event] THEN [system] SHALL [response]

[... continue for all major functional areas ...]
```

### 3. Update Metadata
After writing the requirements file, the agent must update `spec.json` with the following changes:
```json
{
  "phase": "requirements-generated",
  "approvals": {
    "requirements": {
      "generated": true,
      "approved": false
    }
  },
  "updated_at": "current_timestamp"
}
```

### 4. Document Generation Only
The agent should only generate the content for the `requirements.md` file. No review or approval instructions should be in the file itself.

---

## INTERACTIVE APPROVAL (Agent's Internal Note)

The following describes the process, it is not to be included in any generated files.

### Next Phase Uses Interactive Approval
After `requirements.md` is generated, the next command the user issues will be `kiro spec-design $ARGUMENTS`. This next step requires interactive approval.

The agent will ask: "requirements.mdをレビューしましたか？ [y/N]"
- If 'y': The agent will auto-approve the requirements in `spec.json` and then generate the design.
- If 'N': The agent will stop and instruct the user to review the file.

### Review Checklist (for user reference):
- [ ] Requirements are clear and complete.
- [ ] User stories cover all necessary functionality.
- [ ] Acceptance criteria are testable.
- [ ] Requirements align with project goals.

## Instructions for the Agent

1.  **Read Context**: Read `spec.json` to get the project description and target language. Read steering files for broader context.
2.  **Generate Requirements**: Based on the project description, generate the content for `requirements.md`.
3.  **Apply EARS format**: Use proper EARS syntax for all acceptance criteria.
4.  **Structure Clearly**: Group related functionality into logical requirement areas with User Stories.
5.  **Write to File**: Use the `write_file` or `replace` tool to save the content to `.kiro/specs/$ARGUMENTS/requirements.md`.
6.  **Update Metadata**: Read `spec.json`, update the `phase` and `approvals.requirements.generated` fields, and write the file back.
7.  **Inform User**: Tell the user that the requirements have been generated and that they should review the file before proceeding to the next step (`kiro spec-design $ARGUMENTS`).
