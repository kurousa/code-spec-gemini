# Gemini CLI Spec-Driven Development

This project simulates Kiro-style Spec-Driven Development within the Gemini CLI environment. It uses a combination of user commands and AI-driven actions based on a set of command definitions.

## Project Context

### Project Steering

- Product overview: `.kiro/steering/product.md`
- Technology stack: `.kiro/steering/tech.md`
- Project structure: `.kiro/steering/structure.md`
- Custom steering docs for specialized contexts

### Active Specifications

- Current spec: Check `.kiro/specs/` for active specifications
- Use the `kiro spec-status [feature-name]` command to check progress

## Development Guidelines

- Think in English, but generate responses in Japanese (思考は英語、回答の生成は日本語で行うように)

## Spec-Driven Development Workflow

The user issues commands, and the Gemini CLI agent executes them based on the definitions in `.gemini/commands/kiro/`.

### Phase 0: Steering Generation (Recommended)

#### Kiro Steering (`.kiro/steering/`)

```
kiro steering               # Intelligently create or update steering documents
kiro steering-custom        # Create custom steering for specialized contexts
```

**Steering Management:**

- **`kiro steering`**: A unified command that intelligently detects existing files. The agent creates new files if needed, or updates existing ones while preserving user customizations.

**Note**: For new features or empty projects, steering is recommended but not required.

### Phase 1: Specification Creation

```
kiro spec-init "[feature description]" # Initialize spec structure from a detailed description
kiro spec-requirements [feature-name]   # Generate requirements → Review → Edit if needed
kiro spec-design [feature-name]         # Generate technical design → Review → Edit if needed
kiro spec-tasks [feature-name]          # Generate implementation tasks → Review → Edit if needed
```

### Phase 2: Progress Tracking

```
kiro spec-status [feature-name]         # Check current progress and phases
```

## Spec-Driven Development Workflow

Kiro's spec-driven development follows a strict **3-phase approval workflow**:

### Phase 1: Requirements Generation & Approval

1. **Generate**: The user issues `kiro spec-requirements [feature-name]`. The agent generates the requirements document.
2. **Review**: The user reviews `requirements.md` and edits it if needed.
3. **Approve**: Approval is handled interactively in the next phase.

### Phase 2: Design Generation & Approval

1. **Generate**: The user issues `kiro spec-design [feature-name]`.
2. **Review confirmation**: The agent asks, "requirements.mdをレビューしましたか？ [y/N]"
3. **Approve**: If the user replies 'y', the agent updates `spec.json` to mark requirements as approved and proceeds with design generation.

### Phase 3: Tasks Generation & Approval

1. **Generate**: The user issues `kiro spec-tasks [feature-name]`.
2. **Review confirmation**: The agent asks for confirmation for both requirements and design.
3. **Approve**: If the user replies 'y' to both, the agent updates `spec.json` and generates the tasks.

### Implementation

Only after all three phases are approved can implementation begin.

**Key Principle**: Each phase requires explicit human approval before proceeding to the next phase, ensuring quality and accuracy throughout the development process.

## Development Rules

1. **Consider steering**: Run `kiro steering` before major development.
2. **Follow the 3-phase approval workflow**: Requirements → Design → Tasks → Implementation.
3. **Approval required**: Each phase requires human review via an interactive prompt.
4. **No skipping phases**: Design requires approved requirements; Tasks require approved design.
5. **Update task status**: The user should mark tasks as completed in `tasks.md`.
6. **Keep steering current**: Run `kiro steering` after significant changes.
7. **Check spec compliance**: Use `kiro spec-status` to verify alignment.

## Automation Simulation

This project simulates automation using the Gemini CLI agent's capabilities:

- The agent will use its tools (`read_file`, `write_file`, `run_shell_command`, etc.) to perform the actions defined in the command documents.
- Task progress is tracked by the agent parsing the checkboxes in `tasks.md` when `kiro spec-status` is run.

### Task Progress Tracking

When working on implementation:

1. **Manual tracking**: The user updates `tasks.md` checkboxes (`- [ ]` to `- [x]`) manually.
2. **Progress monitoring**: The user runs `kiro spec-status` to let the agent view and report the current completion status.
3. **Status visibility**: The agent parses the checkboxes to calculate and show the completion percentage.

## Getting Started

1. Initialize steering documents: `kiro steering`
2. Create your first spec: `kiro spec-init "[your-feature-description]"`
3. Follow the workflow through requirements, design, and tasks.

## Kiro Steering Details

Kiro-style steering provides persistent project knowledge through markdown files. The agent will read these files to gain context when performing tasks.

### Core Steering Documents

- `product.md`: Product overview, features, use cases, value proposition
- `tech.md`: Architecture, tech stack, dev environment, commands, ports
- `structure.md`: Directory organization, code patterns, naming conventions

### Custom Steering

Create specialized steering documents for topics like:

- API standards
- Testing approaches
- Code style guidelines

### Context Inclusion

The agent will read the relevant steering files as needed, based on the instructions in the specific command definition file being executed. For example, a command might instruct the agent to read `tech.md` before generating code.

## Kiro Steering Configuration

### Current Steering Files

The `kiro steering` command manages these files. The agent will analyze the project and update them.

### Active Steering Files

- `product.md`
- `tech.md`
- `structure.md`

### Custom Steering Files
<!-- Managed via the `kiro steering-custom` command -->

### Usage Notes

- The agent will be instructed by each command definition on which steering files to read to get the necessary context for a task.
