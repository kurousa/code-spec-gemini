---
description: Create custom Kiro steering documents for specialized project contexts
allowed-tools: read_file, write_file
---

# Kiro Custom Steering Creation

**Goal**: Create a new, custom steering document in `.kiro/steering/` based on user input.

## Task: Create Custom Steering Document

This is an interactive command. The agent will ask the user a series of questions to gather the necessary information to create the new steering file.

### Common Custom Steering Types
-   API Standards (`api-standards.md`)
-   Testing Approach (`testing-approach.md`)
-   Code Style Guidelines (`code-style.md`)
-   Security Policies (`security.md`)
-   Deployment Workflow (`deployment.md`)

### Instructions for the Agent

1.  **Ask for Filename**: First, ask the user for the desired filename (e.g., `api-standards.md`). The filename must end in `.md`.

2.  **Ask for Purpose**: Ask the user to describe the purpose of this new steering document. What topics should it cover? (e.g., "It should define our REST API conventions, including versioning and error handling.")

3.  **Ask for Key Content Points**: Ask the user to provide the key guidelines, rules, or content points that should be in the document. The user can provide a bulleted list or a rough draft.

4.  **Generate Document Content**: Based on the user's answers, generate the content for the new steering file. The content should be well-structured with clear headings, lists, and code examples where appropriate.

    **Example Structure**:
    ```markdown
    # [Document Title]

    ## 1. Purpose
    [Purpose provided by the user]

    ## 2. Guidelines
    [Key content points provided by the user, formatted nicely]

    ### 2.1. [Guideline A]
    [Details and code examples]

    ### 2.2. [Guideline B]
    [Details and code examples]
    ```

5.  **Write the File**: Use the `write_file` tool to save the generated content to `.kiro/steering/{filename}`.

6.  **Confirm Creation**: Report back to the user that the file has been created successfully and show them the path to the new file.

### Security and Quality Guidelines

-   **No Sensitive Data**: Remind the user not to include secrets like API keys or passwords in the content.
-   **Single Responsibility**: The document should focus on a single, specific area.
-   **Actionable Guidance**: The content should provide clear, actionable guidelines.
