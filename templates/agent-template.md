---
name: agent-name
version: 1.0.0
category: core|domain-specific|meta-agent|experimental
author: Your Name
tags: [tag1, tag2, tag3]
updated: YYYY-MM-DD
complexity: low|medium|high
dependencies: tool1, tool2, none
---

# Agent Name

Brief one-paragraph description of what this agent does and who it's for.

## Metadata

- **Purpose**: One-sentence description of primary objective
- **Complexity**: Low|Medium|High
- **Dependencies**: List of required tools, APIs, or integrations
- **Use Cases**: 
  - Primary use case 1
  - Primary use case 2
  - Primary use case 3

## System Prompt

```markdown
# Role and Objective

[Define who the agent is and what its primary goal is. Be specific about expertise level and domain.]

Example:
"You are a Senior Data Analyst specializing in business intelligence. Your objective is to analyze datasets, identify trends, and provide actionable insights to business stakeholders."

## Environment

- Current Date: {{CURRENT_DATE}}
- Working Directory: {{WORKING_DIR}}
- Available Tools: {{TOOLS_LIST}}
- User Context: {{USER_CONTEXT}}

## Core Instructions

[Organize instructions by category. Each category should have clear, actionable directives.]

### [Category 1: e.g., Data Analysis Process]
1. [Specific instruction with clear logic]
2. [Specific instruction with clear logic]
3. [Specific instruction with clear logic]

### [Category 2: e.g., Communication Guidelines]
- [Instruction about how to communicate findings]
- [Instruction about visualizations or formats]
- [Instruction about handling uncertainty]

### [Category 3: e.g., Quality Assurance]
- [Instruction about validation]
- [Instruction about error checking]
- [Instruction about edge cases]

## Reasoning Process

[Define the step-by-step thinking process the agent should follow]

For each task:
1. **Understand**: [What to analyze about the request]
2. **Plan**: [How to structure the approach]
3. **Execute**: [How to carry out the work]
4. **Verify**: [How to validate the results]
5. **Communicate**: [How to present findings]

## Tool Usage

[Define each tool the agent can use with clear examples]

### tool_name_1
**Purpose**: [What this tool does]
**When to Use**: [Conditions for using this tool]
**Parameters**:
- param1 (type): Description
- param2 (type): Description

**Example**:
```
tool_name_1(param1="value", param2="value")
```

**Output Handling**: [How to interpret and use the results]

### tool_name_2
[Same structure as above]

## Output Format

[Specify exactly how responses should be structured]

**For [Scenario Type 1]**:
```
[Template or example structure]
```

**For [Scenario Type 2]**:
```
[Template or example structure]
```

## Constraints and Prohibitions

**Do NOT:**
- [Specific thing to avoid]
- [Specific thing to avoid]
- [Specific thing to avoid]

**Always:**
- [Required behavior]
- [Required behavior]
- [Required behavior]

## Tone and Style

- **[Style Attribute 1]**: [Description]
- **[Style Attribute 2]**: [Description]
- **[Style Attribute 3]**: [Description]

## Examples

### Example 1: [Scenario Name - Happy Path]

**User**: [Example user input]

**Agent**: [Complete example response showing ideal behavior]

---

### Example 2: [Scenario Name - Edge Case]

**User**: [Example user input with unusual characteristics]

**Agent**: [Example showing how to handle the edge case]

---

### Example 3: [Scenario Name - Error Handling]

**User**: [Example problematic input]

**Agent**: [Example showing graceful error handling]

---

### Example 4: [Scenario Name - Complex Workflow]

**User**: [Multi-step request]

**Agent**: [Example showing how to break down and handle complexity]

---

### Example 5: [Scenario Name - Boundary Testing]

**User**: [Request that tests constraints]

**Agent**: [Example showing how constraints are enforced]

---

## Validation Checklist

Use this to verify the agent is working correctly:

**Functional Requirements**:
- [ ] [Specific capability 1 works correctly]
- [ ] [Specific capability 2 works correctly]
- [ ] [Specific capability 3 works correctly]

**Quality Metrics**:
- [ ] Responses are accurate and relevant
- [ ] Output format matches specifications
- [ ] Tone and style are consistent
- [ ] Examples cover edge cases

**Safety and Constraints**:
- [ ] Prohibitions are enforced
- [ ] Required behaviors are present
- [ ] Error handling is graceful
- [ ] Boundaries are respected

**Performance**:
- [ ] Response time is acceptable
- [ ] Resource usage is efficient
- [ ] Tool calls are optimized

## Configuration

[Define customizable parameters]

```yaml
# Core Parameters
parameter_1: default_value  # Description
parameter_2: default_value  # Description

# Behavior Modifiers
modifier_1: true|false  # Description
modifier_2: value  # Description

# Advanced Options
option_1: value  # Description
```

## Testing Scenarios

Test this agent with these scenarios:

1. **[Test Category 1]**: "[Example test input]"
   - Expected: [Expected behavior]
   
2. **[Test Category 2]**: "[Example test input]"
   - Expected: [Expected behavior]

3. **[Test Category 3]**: "[Example test input]"
   - Expected: [Expected behavior]

## Version History

- **1.0.0** (YYYY-MM-DD): Initial release
  - [Feature or change]
  - [Feature or change]

## Related Agents

- **agent-name.md**: [Relationship and why it's related]
- **agent-name.md**: [Relationship and why it's related]

## Notes

[Any additional context, implementation guidance, known limitations, or future enhancements]

### Implementation Tips
- [Tip 1]
- [Tip 2]

### Known Limitations
- [Limitation 1]
- [Limitation 2]

### Future Enhancements
- [Potential improvement 1]
- [Potential improvement 2]
```

## Usage Instructions

1. **Copy this template** to create a new agent blueprint
2. **Fill in all sections** - don't skip placeholders
3. **Replace {{VARIABLES}}** with actual values or keep as dynamic
4. **Add 3-5 diverse examples** covering different scenarios
5. **Test thoroughly** using the validation checklist
6. **Document changes** in version history

## Template Variables

Use these variables in your system prompt:
- `{{CURRENT_DATE}}`: Inserts current date
- `{{WORKING_DIR}}`: Current working directory
- `{{TOOLS_LIST}}`: Available tools
- `{{USER_CONTEXT}}`: User information and preferences
- `{{AUTHOR}}`: Blueprint author name
- `{{DATE}}`: Creation/update date
