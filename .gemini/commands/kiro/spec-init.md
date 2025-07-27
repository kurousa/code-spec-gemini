---
description: Initialize a new specification with detailed project description and requirements
allowed-tools: run_shell_command, read_file, write_file
---

# Spec Initialization

Initialize a new specification based on the provided project description:

**Project Description**: $ARGUMENTS

## Steering Context Validation

### Check Steering Documents
The agent should read the following steering documents if they exist to gain context:
- `.kiro/steering/structure.md`
- `.kiro/steering/tech.md`
- `.kiro/steering/product.md`

### Verify Steering Exists
The agent should run a command to check if the steering directory exists, for example: `ls .kiro/steering` (or `dir .kiro/steering` on Windows).

**FLEXIBILITY**: For new features or empty projects, steering documents are recommended but not required. If steering documents are missing or empty, the agent may proceed directly to spec generation phase.

## Task: Initialize Specification Structure

**SCOPE**: This command initializes the directory structure and metadata based on the detailed project description provided.

### 1. Analyze Project Description
From the provided description ($ARGUMENTS), extract:
- Project purpose and goals
- Key features and functionality
- Target users or use cases
- Technical requirements or constraints
- Any specific implementation details mentioned

### 2. Generate Feature Name
Based on the analysis, create a concise, descriptive feature name that captures the essence of the project. This name should be filesystem-friendly (e.g., `user-authentication-flow`).

### 3. Create Spec Directory
Create a directory at `.kiro/specs/{generated-feature-name}/`. The agent will use file system tools to do this (e.g., `mkdir`).

### 4. Initialize spec.json Metadata
Create a file named `spec.json` inside the new directory with the following content. The agent must replace the placeholders.
```json
{
  "feature_name": "{generated-feature-name}",
  "project_description": "$ARGUMENTS",
  "created_at": "current_timestamp",
  "updated_at": "current_timestamp",
  "language": "japanese",
  "phase": "initialized",
  "approvals": {
    "requirements": {
      "generated": false,
      "approved": false
    },
    "design": {
      "generated": false,
      "approved": false
    },
    "tasks": {
      "generated": false,
      "approved": false
    }
  },
  "ready_for_implementation": false
}
```

### 5. Create Template Files
Create the following empty files inside the new spec directory.

#### requirements.md
```markdown
# Requirements Document

## Project Overview
{Brief summary of the project based on the provided description}

## Project Description (User Input)
$ARGUMENTS

## Requirements
<!-- Detailed user stories will be generated in the spec-requirements phase -->

---
**STATUS**: Ready for requirements generation
**NEXT STEP**: Run `kiro spec-requirements {feature-name}` to generate detailed requirements
```

#### design.md
```markdown
# Design Document

## Overview
<!-- Technical design will be generated after requirements approval -->

---
**STATUS**: Waiting for requirements approval
**NEXT STEP**: Complete and approve requirements first
```

#### tasks.md
```markdown
# Implementation Plan

<!-- Implementation tasks will be generated after design approval -->

---
**STATUS**: Waiting for design approval
**NEXT STEP**: Complete and approve design first
```

## Next Steps After Initialization

The agent will inform the user about the successful creation of the spec and provide the exact next command to run. The workflow continues as described in `GEMINI.md`.

## Instructions for the Agent

1.  **Parse project description**: Extract key information from the user's detailed description ($ARGUMENTS).
2.  **Generate feature name**: Create a concise, filesystem-friendly name.
3.  **Check for steering documents**: Read the files in `.kiro/steering/` if they exist. This is recommended but not required.
4.  **Create directory structure**: Use `run_shell_command` to create the directory `.kiro/specs/{generated-feature-name}`.
5.  **Create files**: Use the `write_file` tool to create `spec.json`, `requirements.md`, `design.md`, and `tasks.md` with the content specified above.
6.  **Provide clear next steps**: Inform the user that the initialization is complete and tell them the exact next command to run (e.g., `kiro spec-requirements {generated-feature-name}`).

## Output Format

After initialization, the agent must provide:
1. The generated feature name and the rationale behind it.
2. A brief summary of the project.
3. The paths to the created files.
4. The exact next command for the user to issue.
