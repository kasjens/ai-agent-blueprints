# Agent Blueprints Repository

A collection of reusable AI agent templates and configurations for various tasks and domains.

## 🏗️ Repository Structure

```
agent-blueprints/
├── agents/                      # Agent blueprint definitions
│   ├── core/                    # Essential, general-purpose agents
│   │   ├── default-agent.md     # Standard conversational agent
│   │   ├── research-agent.md    # Research and analysis
│   │   └── task-executor.md     # Task execution specialist
│   ├── domain-specific/         # Specialized domain agents
│   │   ├── code-reviewer.md
│   │   ├── data-analyst.md
│   │   └── content-writer.md
│   ├── meta-agents/             # Agents that manage/create other agents
│   │   ├── agent-creator.md     # Creates new agent blueprints
│   │   └── agent-orchestrator.md # Coordinates multiple agents
│   └── experimental/            # Experimental or beta agents
├── templates/                   # Reusable templates
│   ├── agent-template.md        # Base agent structure
│   ├── tool-definition.yaml     # Tool schema template
│   └── workflow-template.md     # Multi-step workflow template
├── schemas/                     # JSON schemas for validation
│   ├── agent-schema.json        # Agent configuration schema
│   └── tool-schema.json         # Tool definition schema
├── examples/                    # Example implementations
│   ├── simple-chatbot/
│   └── research-assistant/
├── tests/                       # Test cases and validation
│   ├── test-scenarios.md
│   └── evaluation-criteria.md
└── docs/                        # Documentation
    ├── getting-started.md
    ├── best-practices.md
    └── troubleshooting.md
```

## 🚀 Quick Start

### Using an Agent Blueprint

1. **Browse available agents** in the `agents/` directory
2. **Copy the blueprint** you need
3. **Customize** the parameters for your use case
4. **Deploy** using your preferred AI platform (Claude, GPT-4, etc.)

### Creating a New Agent

Use the `agent-creator.md` meta-agent to generate new blueprints:

```bash
# 1. Review the agent-creator blueprint
cat agents/meta-agents/agent-creator.md

# 2. Use it to generate a new agent for your specific task
# Provide task description, domain, and constraints
```

## 📋 Agent Blueprint Format

Each agent blueprint follows this structure:

```yaml
---
name: agent-name
version: 1.0.0
category: core|domain-specific|meta-agent
author: Your Name
tags: [tag1, tag2, tag3]
updated: YYYY-MM-DD
---

# Agent Name

Brief description of what this agent does.

## Metadata
- **Purpose**: One-line purpose statement
- **Complexity**: Low|Medium|High
- **Dependencies**: Required tools/APIs
- **Use Cases**: Primary scenarios

## System Prompt
[Full system prompt with all instructions]

## Tool Requirements
[Required tools and schemas]

## Configuration
[Customizable parameters]

## Examples
[Usage examples]

## Validation
[How to test this agent]
```

## 🎯 Agent Categories

### Core Agents
General-purpose agents suitable for common tasks:
- **default-agent**: Standard conversational interface
- **research-agent**: Information gathering and analysis
- **task-executor**: Execute specific tasks with verification

### Domain-Specific Agents
Specialized agents for particular domains:
- **solution-architect-agent**: System design and architecture planning
- **code-reviewer**: Code analysis and feedback
- **data-analyst**: Data processing and insights
- **content-writer**: Content creation with style guidelines

### Meta-Agents
Agents that work with other agents:
- **agent-creator**: Generate new agent blueprints
- **agent-orchestrator**: Coordinate multiple agents

## 🛠️ Customization Guide

### Basic Customization
1. Update the `Role and Objective` section
2. Modify `Instructions` for your specific needs
3. Add or remove tools from `Tool Requirements`
4. Adjust `Output Format` specifications

### Advanced Customization
1. Add custom reasoning steps
2. Define domain-specific constraints
3. Create specialized tool schemas
4. Implement multi-stage workflows

## 📊 Validation and Testing

Each agent should be validated against:
- **Functional Tests**: Does it perform the intended task?
- **Edge Cases**: How does it handle unusual inputs?
- **Safety**: Are constraints properly enforced?
- **Performance**: Response quality and speed

See `tests/` directory for test scenarios.

## 🤝 Contributing

### Adding a New Agent Blueprint

1. Use the template in `templates/agent-template.md`
2. Follow the naming convention: `descriptive-name.md`
3. Include all required sections
4. Add examples and test cases
5. Update this README with your agent in the appropriate category

### Improving Existing Agents

1. Test the agent thoroughly
2. Document your changes
3. Update version number
4. Add migration notes if breaking changes

## 📚 Resources

- **Best Practices**: See `docs/best-practices.md`
- **Getting Started**: See `docs/getting-started.md`
- **Troubleshooting**: See `docs/troubleshooting.md`

## 📄 License

[Your chosen license]

## 🙏 Acknowledgments

Built on research from:
- Anthropic's Claude Skills patterns
- OpenAI's agent design guides
- Community best practices from awesome-claude-skills
- AGENTS.md industry standard

---

**Version**: 1.0.0  
**Last Updated**: 2025-01-05
