# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a collection of reusable AI agent blueprints (system prompts and configurations) for various tasks and domains. The repository contains markdown-based agent specifications that can be used with Claude, GPT-4, or other LLMs.

## Repository Structure

```
agents/
├── core/                      # General-purpose agents
│   ├── default-agent.md
│   └── research-agent.md
├── domain-specific/           # Specialized agents
│   └── solution-architect-agent.md
└── meta-agents/              # Agents that create/manage agents
    └── agent-creator.md

docs/                         # Documentation and guides
├── agent-to-cline-workflow.md    # Integration with Cline IDE
├── CLINE_BRIEF_TEMPLATE.md       # Template for implementation specs
├── CLINE_SETUP_GUIDE.md          # Cline configuration guide
├── RESEARCH-AGENT-GUIDE.md       # Research agent usage
└── SOLUTION-ARCHITECT-GUIDE.md   # Architecture agent usage

templates/                    # Reusable templates
└── agent-template.md         # Base template for new agents

schemas/                      # JSON validation schemas
└── agent-schema.json         # Validates agent blueprint structure

examples/                     # Example implementations
└── simple-chatbot/
```

## Agent Blueprint Format

All agent blueprints follow a standardized structure:

### YAML Frontmatter (Required)
```yaml
---
name: agent-name              # kebab-case, 3-50 chars
version: 1.0.0               # Semantic versioning
category: core|domain-specific|meta-agent|experimental
author: Author Name
tags: [tag1, tag2, tag3]     # lowercase, hyphenated
updated: YYYY-MM-DD
complexity: low|medium|high
dependencies: tool1, tool2   # Or "none"
---
```

### Required Sections
1. **Agent Name and Description**: One-paragraph overview
2. **Metadata**: Purpose, complexity, dependencies, use cases
3. **System Prompt**: Complete LLM instructions (the core content)
4. **Examples**: 3-5 usage examples demonstrating behavior
5. **Validation**: Test scenarios and success criteria
6. **Version History**: Change log for tracking iterations

## Working with Agent Blueprints

### Creating a New Agent

**Option 1 - Use the Agent Creator (Recommended)**
1. Read `agents/meta-agents/agent-creator.md`
2. Use that system prompt with an LLM to design your agent
3. The creator will guide you through the process

**Option 2 - Use the Template**
1. Copy `templates/agent-template.md` to appropriate directory:
   - `agents/core/` for general-purpose agents
   - `agents/domain-specific/` for specialized agents
   - `agents/experimental/` for beta/experimental agents
2. Fill in all required sections
3. Follow naming convention: `descriptive-purpose.md` (kebab-case)
4. Validate against `schemas/agent-schema.json`

### Modifying Existing Agents

When updating agents:
1. Read the full agent file first to understand current behavior
2. Update the `version` field following semantic versioning:
   - Patch (1.0.X): Bug fixes, clarifications
   - Minor (1.X.0): New features, backward compatible
   - Major (X.0.0): Breaking changes
3. Update the `updated` date field
4. Add entry to Version History section
5. Test thoroughly using the Validation section

### Quality Standards

**System Prompt Design:**
- Instructions must be specific and unambiguous
- Use conditional logic (if-then) for different scenarios
- Define explicit reasoning processes
- Include concrete examples within instructions
- Specify output formats clearly

**Citations and Sources:**
- Agent instructions should cite sources when claiming best practices
- Research agents must include proper URL citations
- Distinguish facts from opinions/recommendations

**Testing:**
- Every agent should have validation criteria
- Include both positive and negative test cases
- Test edge cases and ambiguous inputs
- Verify constraints are enforced

## Key Workflows

### Agent-to-Cline Development Pipeline

This repository supports a research → architecture → implementation workflow:

1. **Research Agent** (in AnythingLLM or Claude): Gathers information, best practices, technology comparisons
   - Output: `research-output.md`

2. **Solution Architect Agent**: Designs comprehensive architecture based on research
   - Output: `architecture.md`

3. **Create Implementation Brief**: Combine research + architecture
   - Output: `CLINE_BRIEF.md` (see `docs/CLINE_BRIEF_TEMPLATE.md`)

4. **Cline (VS Code extension)**: Actually implements the code
   - Input: `CLINE_BRIEF.md`
   - Output: Working application code

See `docs/agent-to-cline-workflow.md` for complete details.

### Variable Substitution

Agent blueprints use template variables that should be replaced before use:
- `{{CURRENT_DATE}}` → Today's date
- `{{WORKING_DIR}}` → Current working directory
- `{{TOOLS_LIST}}` → Available tools for the agent
- `{{USER_CONTEXT}}` → User-specific information

## Architecture Principles

### Agent Design Philosophy

**Systematic Processes**: Agents define step-by-step processes rather than vague instructions. Example: Research Agent defines 6-step methodology (Understand → Develop Strategy → Execute → Evaluate → Synthesize → Present).

**Role-Based Identity**: Each agent has a specific expertise (e.g., "Senior Research Analyst", "Solution Architect"). This anchors behavior and decision-making.

**Tool Integration**: Agents specify exact tool usage patterns with parameters, examples, and output handling.

**Quality Constraints**: Explicit "Always" and "Never" rules that define boundaries.

**Progressive Disclosure**: Instructions organized from general principles to specific scenarios.

### Blueprint vs Implementation

- **Blueprints** (this repo): Reusable system prompts and configurations
- **Implementation**: Actual deployment in Claude Projects, API calls, or IDE extensions
- Blueprints are platform-agnostic and can be used with any LLM that supports system prompts

### Meta-Agents Pattern

The `meta-agents/` directory contains agents that work with other agents:
- `agent-creator.md`: Generates new agent blueprints
- Future: agent-orchestrator, agent-validator, etc.

This enables programmatic agent creation and management.

## Validation and Schema

### Validating Agent Blueprints

Agents should validate against `schemas/agent-schema.json`:

**Required Fields (YAML frontmatter):**
- `name`: kebab-case, 3-50 characters, pattern: `^[a-z][a-z0-9-]*[a-z0-9]$`
- `version`: Semantic version, pattern: `^\d+\.\d+\.\d+$`
- `category`: One of: core, domain-specific, meta-agent, experimental
- `author`: 2-100 characters
- `tags`: Array of lowercase hyphenated tags (1-10 items)
- `updated`: Date in YYYY-MM-DD format
- `complexity`: low, medium, or high
- `dependencies`: Comma-separated list or "none"

**Content Requirements:**
- System prompt must be substantial (minimum guidelines in schema)
- Examples section must include diverse use cases
- Validation criteria must be testable and specific

## Common Tasks

### Adding a New Core Agent
```bash
# Copy template
cp templates/agent-template.md agents/core/my-agent.md

# Edit all required sections
# Validate structure matches schema

# Update README.md to list the new agent
# Commit with clear message describing the agent's purpose
```

### Testing an Agent Blueprint
1. Read the agent's Validation section
2. Use the system prompt with Claude or GPT-4
3. Run each test scenario from the Validation section
4. Verify expected behaviors occur
5. Check that constraints are enforced
6. Document any deviations or issues

### Using Research Agent for Development
1. Copy system prompt from `agents/core/research-agent.md`
2. Paste into Claude or LLM interface
3. Provide research query
4. Agent will execute systematic 6-step research process
5. Output includes structured findings with citations
6. Save output as `research-output.md` for later use

### Creating Implementation Specs for Cline
1. Use Research Agent to gather information
2. Use Solution Architect Agent to design architecture
3. Copy `docs/CLINE_BRIEF_TEMPLATE.md`
4. Fill in tech stack, structure, and implementation details
5. Reference both research and architecture outputs
6. Use with Cline VS Code extension for autonomous implementation

## Git Workflow

### Branch Strategy
- `main`: Stable, tested agent blueprints
- Feature branches for new agents or major changes

### Commit Guidelines
Follow conventional commits for agent changes:
- `feat(agent-name): Add new capability`
- `fix(agent-name): Correct behavior`
- `docs: Update guidelines`
- `refactor(agent-name): Improve clarity without changing behavior`

### Modified Files Detection
Git status shows several modified docs files. When working on documentation:
- Ensure cross-references between files remain accurate
- Update dates in YAML frontmatter when modifying agents
- Keep version numbers synchronized

## Contributing

See `CONTRIBUTING.md` for detailed guidelines:
- Blueprint standards and required sections
- Quality standards for clarity, completeness, testability
- Naming conventions for files and agents
- Self-review checklist before submission
- Review criteria (functionality 40%, quality 30%, documentation 20%, best practices 10%)

## References

- **Templates**: `templates/agent-template.md` for structure
- **Best Practices**: `docs/best-practices.md` for design principles
- **Getting Started**: `docs/getting-started.md` for beginners
- **Quick Start**: `QUICK-START.md` for 5-minute overview
- **Cline Integration**: `docs/agent-to-cline-workflow.md` for implementation pipeline
