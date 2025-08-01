# Technology Stack

## Architecture

A documentation-driven framework built on the Gemini CLI. The architecture consists of two main layers:

1.  **Command Layer**: Markdown-based command definitions that instruct the Gemini agent.
2.  **Knowledge Layer**: Structured markdown documents (`.kiro/`) that provide persistent project context.

## Core Technologies

### Gemini CLI Platform
- **Base Platform**: [Gemini CLI](https://github.com/google/gemini-cli)
- **Model**: Google's Gemini models.
- **Extension System**: Custom command definitions in the `.gemini/commands/` directory.

### Command System
- **Definition Format**: Markdown files that describe the command's purpose and provide instructions for the AI agent.
- **Execution**: The Gemini CLI agent interprets these files to execute tasks using its available tools.

## Development Environment

### Required Tools
- **Gemini CLI**: The latest version.
- **Git**: For version control.
- **A Text Editor**: For reviewing and editing the generated markdown documents.

### Project Structure
```
.gemini/
└── commands/
    └── kiro/                  # Command definitions

.kiro/
├── steering/                  # Project knowledge documents
│   ├── product.md
│   ├── tech.md
│   └── structure.md
└── specs/                     # Feature specifications
    └── [feature-name]/
        ├── spec.json
        ├── requirements.md
        ├── design.md
        └── tasks.md
```

## Common Commands

### Core Workflow Commands
```bash
# Steering management
/kiro:steering                    # Smartly creates or updates steering documents

# Specification workflow
/kiro:spec-init "[description]"   # Initializes a new specification
/kiro:spec-requirements [name]    # Generates the requirements document
/kiro:spec-design [name]          # Generates the technical design
/kiro:spec-tasks [name]           # Generates implementation tasks
/kiro:spec-status [name]          # Checks progress and compliance
```

### Manual Operations
```bash
# Project setup (one-time)
cp -r .gemini/ /path/to/your-project/
cp GEMINI.md /path/to/your-project/

# Manual phase approval (if needed)
# Edit .kiro/specs/[feature-name]/spec.json to set approval flags:
# "requirements_approved": true, "design_approved": true
```

## Integration Points

### Git Integration
- All steering and specification documents are stored in Git, allowing for version control and collaboration.
- Commit messages can be standardized to reference specification tasks.

### Documentation Systems
- The framework generates standard markdown documents, which are compatible with most documentation systems, wikis, and viewers.
