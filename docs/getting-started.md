# Getting Started with Agent Blueprints

This guide will help you start using and creating agent blueprints for your AI projects.

## Table of Contents

1. [Quick Start](#quick-start)
2. [Understanding Agent Blueprints](#understanding-agent-blueprints)
3. [Using an Existing Blueprint](#using-an-existing-blueprint)
4. [Creating a New Blueprint](#creating-a-new-blueprint)
5. [Testing Your Agent](#testing-your-agent)
6. [Best Practices](#best-practices)
7. [Troubleshooting](#troubleshooting)

---

## Quick Start

### 5-Minute Setup

1. **Clone the repository**:
   ```bash
   git clone https://github.com/your-org/agent-blueprints.git
   cd agent-blueprints
   ```

2. **Browse available agents**:
   ```bash
   ls agents/core/          # General-purpose agents
   ls agents/domain-specific/   # Specialized agents
   ls agents/meta-agents/   # Agents that work with other agents
   ```

3. **Pick an agent and read its blueprint**:
   ```bash
   cat agents/core/default-agent.md
   ```

4. **Use the blueprint** by copying its system prompt into your AI platform (Claude, GPT-4, etc.)

---

## Understanding Agent Blueprints

### What is an Agent Blueprint?

An agent blueprint is a complete specification for an AI agent that includes:

- **Role Definition**: What the agent is and what expertise it has
- **System Prompt**: Detailed instructions for agent behavior
- **Tool Requirements**: External capabilities the agent needs
- **Examples**: Demonstrations of ideal agent behavior
- **Validation Criteria**: How to test if the agent works correctly

### Blueprint Structure

Every blueprint follows this format:

```markdown
---
name: agent-name           # Unique identifier
version: 1.0.0            # Semantic versioning
category: core            # Classification
author: Your Name         # Creator
tags: [conversational]    # Search tags
updated: 2025-01-05       # Last modified
complexity: low           # Difficulty level
dependencies: none        # Required tools
---

# Agent Name
[Description]

## System Prompt
[Complete instructions for the agent]

## Examples
[Usage demonstrations]

## Validation
[Testing criteria]
```

### Blueprint Categories

| Category | Purpose | Examples |
|----------|---------|----------|
| **core** | General-purpose agents for common tasks | default-agent, research-agent |
| **domain-specific** | Specialized agents for particular fields | code-reviewer, data-analyst |
| **meta-agents** | Agents that create or manage other agents | agent-creator, agent-orchestrator |
| **experimental** | Beta or cutting-edge agents | new-architecture-tests |

---

## Using an Existing Blueprint

### Step 1: Choose the Right Agent

Ask yourself:
- What task do I need to accomplish?
- How complex is the task?
- Do I need specialized domain knowledge?
- Are there existing agents that do something similar?

**Decision Tree**:

```
Need something generic? 
→ Start with: agents/core/default-agent.md

Need domain expertise?
→ Check: agents/domain-specific/

Need to create new agents?
→ Use: agents/meta-agents/agent-creator.md

Need multiple agents working together?
→ Use: agents/meta-agents/agent-orchestrator.md
```

### Step 2: Read the Blueprint

Open the blueprint file and review:
1. **Overview**: Understand what the agent does
2. **System Prompt**: This is what you'll give to your AI
3. **Tool Requirements**: Check if you have access to needed tools
4. **Examples**: See how the agent should behave
5. **Configuration**: Identify customization options

### Step 3: Deploy the Agent

#### For Claude (claude.ai)

1. Start a new conversation or project
2. Go to project settings or use "Custom Instructions"
3. Copy the entire **System Prompt** section from the blueprint
4. Replace any `{{VARIABLES}}` with actual values:
   - `{{CURRENT_DATE}}` → Today's date
   - `{{WORKING_DIR}}` → Your working directory
   - `{{TOOLS_LIST}}` → Available tools
   - `{{USER_CONTEXT}}` → Your info/preferences

#### For OpenAI API

```python
import openai

# Load blueprint system prompt
with open('agents/core/default-agent.md', 'r') as f:
    content = f.read()
    # Extract system prompt section
    system_prompt = extract_system_prompt(content)

# Use in API call
response = openai.ChatCompletion.create(
    model="gpt-4",
    messages=[
        {"role": "system", "content": system_prompt},
        {"role": "user", "content": "Your question here"}
    ]
)
```

#### For Custom Applications

1. Parse the blueprint file (YAML + Markdown)
2. Extract the system prompt
3. Replace template variables
4. Inject into your agent framework

### Step 4: Test the Agent

Use the test scenarios from the blueprint's **Validation** section:

```markdown
Test 1: Simple factual question
Input: "What is photosynthesis?"
Expected: Clear, accurate explanation

Test 2: Ambiguous request
Input: "Help me with my project"
Expected: Asks clarifying questions

Test 3: Edge case
Input: [Complex or unusual request]
Expected: [Specific handling]
```

---

## Creating a New Blueprint

### Option 1: Use the Agent Creator (Recommended)

The fastest way to create a new agent is to use our meta-agent:

1. **Load the Agent Creator**:
   ```bash
   cat agents/meta-agents/agent-creator.md
   ```

2. **Use it to generate your agent**:
   
   Start a conversation with Claude or your AI using the agent-creator system prompt, then describe your needs:
   
   ```
   You: I need an agent that reviews academic papers for logical fallacies
   
   Agent Creator: Great! Let me gather requirements...
   1. What field? (Philosophy, Science, General)
   2. Output format? (Inline comments, summary report)
   3. Severity levels? (Minor, major, critical)
   ...
   ```

3. **Refine the generated blueprint**:
   
   The Agent Creator will produce a complete blueprint. Review and customize it for your specific needs.

### Option 2: Manual Creation

1. **Copy the template**:
   ```bash
   cp templates/agent-template.md agents/domain-specific/my-new-agent.md
   ```

2. **Fill in the sections**:

   Start with metadata:
   ```yaml
   ---
   name: my-new-agent
   version: 1.0.0
   category: domain-specific
   author: Your Name
   tags: [relevant, tags]
   updated: 2025-01-05
   complexity: medium
   dependencies: tool1, tool2
   ---
   ```

3. **Write the system prompt**:

   Follow the proven structure:
   ```markdown
   # Role and Objective
   [Define who the agent is]

   ## Environment
   [Set context]

   ## Core Instructions
   [Detailed behaviors]

   ## Reasoning Process
   [How to think]

   ## Tool Usage
   [When and how to use tools]

   ## Output Format
   [Structure of responses]

   ## Constraints
   [Boundaries and safety]

   ## Examples
   [Demonstrations]
   ```

4. **Add diverse examples**:
   
   Include at least:
   - Happy path (typical use)
   - Edge case (unusual input)
   - Error handling (problematic request)
   - Multi-step workflow (complex task)
   - Constraint testing (boundary check)

5. **Define validation criteria**:
   
   Create testable requirements:
   ```markdown
   ## Validation
   
   **Functional Tests**:
   - [ ] Agent correctly identifies X
   - [ ] Agent properly formats Y
   - [ ] Agent handles Z edge case
   
   **Quality Metrics**:
   - [ ] Responses are accurate
   - [ ] Output follows template
   - [ ] Tone is consistent
   ```

6. **Validate against schema**:
   ```bash
   # If you have a validator tool
   validate-blueprint agents/domain-specific/my-new-agent.md
   ```

### Framework Selection Guide

Choose the right framework for your agent:

**CO-STAR** (for creative/generative agents):
- Content creation agents
- Writing assistants
- Ideation helpers
- Recommendation engines

**RISEN** (for operational/task agents):
- Data analysis agents
- Code reviewers
- System administrators
- Process automation

**Hybrid** (for complex agents):
- Research assistants
- Multi-capability agents
- Agents with both creative and analytical tasks

---

## Testing Your Agent

### Phase 1: Functional Testing

Test that the agent does what it's supposed to do:

```markdown
Test: Basic Capability
Input: [Standard request]
Expected: [Correct response]
Result: ✅ Pass / ❌ Fail
Notes: [Observations]
```

### Phase 2: Edge Case Testing

Test unusual or boundary conditions:

```markdown
Test: Ambiguous Input
Input: [Vague or unclear request]
Expected: [Asks clarifying questions]
Result: ✅ Pass / ❌ Fail

Test: Out of Scope
Input: [Request outside agent's domain]
Expected: [Politely declines or redirects]
Result: ✅ Pass / ❌ Fail
```

### Phase 3: Constraint Testing

Verify that safety boundaries are enforced:

```markdown
Test: Prohibited Action
Input: [Request that violates constraints]
Expected: [Refuses appropriately]
Result: ✅ Pass / ❌ Fail
```

### Phase 4: Performance Testing

Evaluate quality and efficiency:

- Response quality (accuracy, relevance)
- Response time
- Resource usage (token count, API calls)
- Consistency across similar inputs

### Testing Checklist

Use this for every new blueprint:

```markdown
[ ] Functional requirements met
[ ] Edge cases handled gracefully
[ ] Constraints properly enforced
[ ] Examples match actual behavior
[ ] Documentation is clear
[ ] Performance is acceptable
[ ] No security issues
[ ] User experience is positive
```

---

## Best Practices

### DO

✅ **Start simple**: Begin with core functionality, add complexity only when needed

✅ **Use examples**: Include 3-5 diverse examples showing different scenarios

✅ **Be specific**: "Analyze data for trends" → "Calculate month-over-month percentage changes and identify values exceeding 2 standard deviations"

✅ **Test thoroughly**: Use the validation checklist before deploying

✅ **Version your blueprints**: Use semantic versioning (1.0.0, 1.1.0, 2.0.0)

✅ **Document changes**: Keep version history updated

✅ **Consider reusability**: Design agents that others can customize

### DON'T

❌ **Overload with tools**: 5-7 distinct tools max; more creates confusion

❌ **Use vague instructions**: "Be helpful" is not actionable

❌ **Skip edge cases**: Always define error handling

❌ **Create conflicting rules**: Review for consistency

❌ **Forget constraints**: Always include safety boundaries

❌ **Assume knowledge**: Explain specialized terms

❌ **Deploy untested**: Always validate before production use

### Common Patterns

**Pattern: Progressive Enhancement**
```
v1.0.0: Core functionality only
v1.1.0: Add common edge cases
v1.2.0: Add advanced features
v2.0.0: Major architecture change
```

**Pattern: Modular Tools**
```
Instead of: One agent with 15 tools
Do: Three specialized agents with 5 tools each
     + One orchestrator agent
```

**Pattern: Clear Escalation**
```
Agent knows when to:
1. Handle directly
2. Ask for clarification
3. Escalate to human
```

---

## Troubleshooting

### Problem: Agent gives irrelevant responses

**Diagnosis**: Instructions may be too vague or conflicting

**Solution**:
1. Review the "Role and Objective" section - is it specific?
2. Check for conflicting instructions
3. Add more explicit examples
4. Use conditional logic: "If X, then do Y. If Z, then do W."

---

### Problem: Agent refuses reasonable requests

**Diagnosis**: Constraints may be too strict

**Solution**:
1. Review the "Constraints and Prohibitions" section
2. Check if the constraint is necessary
3. Make constraints more specific with conditions
4. Add examples of acceptable similar requests

---

### Problem: Agent doesn't use tools correctly

**Diagnosis**: Tool definitions may be unclear

**Solution**:
1. Add detailed tool descriptions
2. Include clear "when to use" criteria
3. Provide concrete examples of tool usage
4. Add output handling instructions

---

### Problem: Inconsistent behavior

**Diagnosis**: Ambiguous instructions or missing examples

**Solution**:
1. Make instructions more explicit
2. Add examples covering edge cases
3. Define a clear reasoning process
4. Test with multiple similar inputs

---

### Problem: Too verbose or too terse

**Diagnosis**: Output format not well-defined

**Solution**:
1. Add specific output format templates
2. Include length guidelines
3. Provide examples of ideal response length
4. Use configuration parameters for verbosity

---

## Next Steps

Now that you understand the basics:

1. **Explore examples**: Check the `examples/` directory for complete implementations

2. **Read best practices**: See `docs/best-practices.md` for advanced techniques

3. **Join the community**: Contribute your own blueprints!

4. **Experiment**: Modify existing blueprints and see what happens

5. **Share feedback**: Help improve blueprints by reporting issues

---

## Resources

- **Templates**: `/templates/` - Base templates to start from
- **Schemas**: `/schemas/` - Validation schemas
- **Examples**: `/examples/` - Complete example implementations
- **Tests**: `/tests/` - Test scenarios and criteria

## Get Help

- Check `/docs/troubleshooting.md` for common issues
- Review existing blueprints for examples
- Use the agent-creator to help design new agents

---

**Happy agent building!** 🚀
