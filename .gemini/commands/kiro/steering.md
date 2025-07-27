---
description: Create or update Kiro steering documents intelligently based on project state
allowed-tools: run_shell_command, read_file, write_file, glob
---

# Kiro Steering Management

**Goal**: Intelligently create or update steering documents in `.kiro/steering/`.

The agent will analyze the project to generate `product.md`, `tech.md`, and `structure.md`. It will create them if they don't exist, or update them intelligently if they do.

## 1. Project Analysis (Instructions for the Agent)

To build context, the agent must perform a comprehensive analysis of the project:

-   **Analyze File Structure**: Use the `glob` tool with patterns like `**/*` to understand the overall directory structure.
-   **Analyze Source Code**: Use `glob` to find source files (e.g., `**/*.js`, `**/*.py`, `**/*.ts`). Read a representative sample of these files using `read_many_files` to understand coding patterns, frameworks, and dependencies.
-   **Analyze Config Files**: Use `glob` to find configuration files (e.g., `package.json`, `requirements.txt`, `tsconfig.json`, `pom.xml`). Read their contents to determine the exact technology stack and dependencies.
-   **Analyze Documentation**: Read existing documentation like `README.md` to understand the project's stated purpose and usage.

## 2. Smart Create/Update Strategy

-   **For each core steering file (`product.md`, `tech.md`, `structure.md`)**:
    1.  **Check for Existence**: Use `read_file` to see if the file already exists. A file not found error means it needs to be created.
    2.  **If it EXISTS**: Read the current content. Generate an updated version that merges new findings from the project analysis while preserving user-added sections and comments. The agent should act like a collaborator, adding to the document rather than replacing it wholesale.
    3.  **If it does NOT EXIST**: Generate a comprehensive initial version of the document from scratch based on the project analysis.
    4.  **Write the result**: Use `write_file` to save the new or updated content.

## 3. Document Content Generation

### `product.md` (Product Overview)
-   **Content**: Should describe the product's purpose, core features, target users, and value proposition.
-   **Source of Information**: `README.md`, existing documentation, and inferences from the codebase.

### `tech.md` (Technology Stack)
-   **Content**: Should detail the architecture, frontend/backend frameworks, languages, databases, development environment, and common commands.
-   **Source of Information**: `package.json`, `requirements.txt`, `tsconfig.json`, etc. The agent must list specific libraries and their versions.

### `structure.md` (Project Structure)
-   **Content**: Should outline the codebase organization, key directory structures, file naming conventions, and architectural patterns.
-   **Source of Information**: The agent's analysis of the file system via the `glob` tool.

## 4. Preservation of Custom Content

**CRITICAL**: When updating an existing file, the agent must preserve user customizations. This means:
-   Keeping sections or comments that don't fit the standard template.
-   Updating factual information (like a dependency list) while leaving narrative sections intact.
-   Maintaining the existing formatting and style.

## Instructions for the Agent

1.  **Create Directory**: First, ensure the `.kiro/steering/` directory exists. Use `run_shell_command` with `mkdir -p .kiro/steering` (or equivalent).
2.  **Analyze Project**: Perform the project analysis described in Step 1 using `glob` and `read_many_files`.
3.  **Process Each Steering File**: For `product.md`, `tech.md`, and `structure.md`, execute the "Smart Create/Update Strategy" from Step 2.
4.  **Generate Content**: Generate the markdown content for each file based on your analysis.
5.  **Write Files**: Use `write_file` to save the results.
6.  **Inform User**: Report back to the user on which files were created and/or updated.
