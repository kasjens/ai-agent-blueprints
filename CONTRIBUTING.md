# Contributing to Agent Blueprints

Thank you for your interest in contributing! This guide will help you add new agent blueprints, improve existing ones, and maintain the quality of the repository.

## Table of Contents

1. [Getting Started](#getting-started)
2. [Contribution Types](#contribution-types)
3. [Blueprint Standards](#blueprint-standards)
4. [Submission Process](#submission-process)
5. [Review Criteria](#review-criteria)
6. [Community Guidelines](#community-guidelines)

---

## Getting Started

### Prerequisites

1. **Fork the repository**:
   ```bash
   # Click "Fork" on GitHub, then:
   git clone https://github.com/your-username/agent-blueprints.git
   cd agent-blueprints
   ```

2. **Create a branch**:
   ```bash
   git checkout -b feature/my-new-agent
   ```

3. **Make your changes** following the guidelines below

4. **Test thoroughly** using the validation checklist

5. **Submit a pull request** with a clear description

---

## Contribution Types

### 1. New Agent Blueprints

**Best candidates for new agents**:
- Solve a specific, well-defined problem
- Fill a gap in existing agents
- Represent proven patterns from production use
- Have clear use cases and examples

**Not ideal**:
- Agents that are too similar to existing ones
- Overly general "do everything" agents
- Agents without clear validation criteria
- Experimental ideas without testing

### 2. Improvements to Existing Agents

**Valuable improvements**:
- Better examples covering more scenarios
- Clearer instructions reducing ambiguity
- Fixed bugs or inconsistencies
- Performance optimizations
- Better error handling
- Enhanced documentation

### 3. Documentation

**Helpful contributions**:
- Additional usage examples
- Troubleshooting guides
- Tutorial content
- Translation to other languages
- Clarification of confusing sections

### 4. Tooling and Infrastructure

**Useful additions**:
- Validation scripts
- Testing frameworks
- Blueprint generators
- Conversion utilities
- CI/CD improvements

---

## Blueprint Standards

### Required Sections

Every agent blueprint MUST include:

```yaml
---
# Metadata (YAML frontmatter)
name: agent-name
version: 1.0.0
category: core|domain-specific|meta-agent
author: Your Name
tags: [tag1, tag2]
updated: YYYY-MM-DD
complexity: low|medium|high
dependencies: tool1, tool2
---

# Agent Name
[Description]

## Metadata
[Purpose, complexity, use cases]

## System Prompt
[Complete prompt with all sections]

## Tool Requirements
[If applicable]

## Configuration
[Customizable parameters]

## Examples
[At least 3, preferably 5]

## Validation
[Test scenarios and criteria]

## Version History
[Change log]

## Related Agents
[Links to similar agents]

## Notes
[Additional context]
```

### Quality Standards

#### 1. Clarity
- Instructions must be unambiguous
- Technical terms must be defined
- Examples must be self-explanatory

#### 2. Completeness
- All scenarios covered (happy path, edge cases, errors)
- Constraints clearly stated
- Success criteria measurable

#### 3. Testability
- Validation criteria must be checkable
- Test scenarios must be reproducible
- Expected behaviors must be specific

#### 4. Maintainability
- Code follows consistent structure
- Changes are documented
- Version history is maintained

### Naming Conventions

**Files**:
- Use kebab-case: `data-analyst-agent.md`
- Be descriptive but concise
- Avoid version numbers in filename

**Agents**:
- Name format: `descriptive-purpose`
- Examples: `code-reviewer`, `research-assistant`, `sql-query-helper`

**Tags**:
- Use lowercase
- Use hyphens for multi-word tags
- Be specific: `python-code-review` not just `code`

---

## Submission Process

### Step 1: Prepare Your Contribution

**For New Agents**:
1. Use the agent-creator or template
2. Fill in all required sections
3. Add 5+ diverse examples
4. Create validation tests
5. Test thoroughly

**For Improvements**:
1. Identify the specific improvement
2. Make targeted changes
3. Verify no regressions
4. Update version history
5. Test the modified agent

### Step 2: Self-Review Checklist

Before submitting, verify:

**Structure**:
- [ ] YAML frontmatter is valid
- [ ] All required sections present
- [ ] Markdown formatting is correct
- [ ] No broken links

**Content**:
- [ ] Instructions are clear and specific
- [ ] No conflicting directives
- [ ] Examples match instructions
- [ ] Constraints are enforced
- [ ] Edge cases addressed

**Quality**:
- [ ] Spelling and grammar checked
- [ ] Technical accuracy verified
- [ ] Examples tested and working
- [ ] Documentation is complete

**Testing**:
- [ ] All test scenarios pass
- [ ] Edge cases handled
- [ ] No security issues
- [ ] Performance acceptable

### Step 3: Commit Your Changes

```bash
# Stage your changes
git add agents/domain-specific/my-new-agent.md

# Commit with descriptive message
git commit -m "Add SQL query optimization agent

- Focused on PostgreSQL query analysis
- Includes performance benchmarking
- Covers indexing strategies and query plans
- 7 examples covering common scenarios
- Validation tests included"

# Push to your fork
git push origin feature/my-new-agent
```

### Step 4: Create Pull Request

1. Go to the original repository on GitHub
2. Click "New Pull Request"
3. Select your branch
4. Fill in the PR template:

```markdown
## Description
[Brief description of your contribution]

## Type of Change
- [ ] New agent blueprint
- [ ] Improvement to existing agent
- [ ] Documentation update
- [ ] Bug fix
- [ ] Other: [describe]

## Agent Category
- [ ] Core
- [ ] Domain-Specific
- [ ] Meta-Agent
- [ ] Experimental

## Testing
[Describe how you tested this]

## Checklist
- [ ] Follows blueprint standards
- [ ] All required sections included
- [ ] Examples are tested and working
- [ ] Documentation is clear
- [ ] Validation criteria defined
- [ ] Version history updated

## Related Issues
[Link any related issues]
```

---

## Review Criteria

Submissions will be evaluated on:

### 1. Functionality (40%)
- Does the agent work as described?
- Are use cases clearly defined?
- Is the scope appropriate?

### 2. Quality (30%)
- Are instructions clear and specific?
- Are examples comprehensive?
- Is error handling adequate?

### 3. Documentation (20%)
- Is documentation complete?
- Are examples well-explained?
- Is validation criteria clear?

### 4. Best Practices (10%)
- Follows established patterns?
- Avoids known anti-patterns?
- Maintainable and extensible?

### Review Process

1. **Automated Checks**: Schema validation, formatting
2. **Maintainer Review**: Quality and standards compliance
3. **Community Feedback**: Optional discussion period
4. **Final Approval**: Merge or request changes

### Response Time

- Initial review: 3-5 business days
- Follow-up reviews: 1-2 business days
- Complex changes: May take longer

---

## Community Guidelines

### Code of Conduct

We are committed to providing a welcoming environment:

**Be Respectful**:
- Treat all contributors with respect
- Be open to different perspectives
- Assume good intentions

**Be Constructive**:
- Provide helpful, actionable feedback
- Focus on improving the work, not criticizing the person
- Offer alternatives when pointing out issues

**Be Collaborative**:
- Work together to improve the repository
- Share knowledge and experience
- Help newcomers get started

### Communication Channels

- **GitHub Issues**: Bug reports, feature requests
- **Pull Requests**: Code submissions and reviews
- **Discussions**: General questions and ideas

### Attribution

Contributors will be credited in:
- Agent metadata (author field)
- CONTRIBUTORS.md file
- Release notes

---

## Examples of Good Contributions

### Example 1: New Agent with Clear Scope

```markdown
---
name: email-classifier
version: 1.0.0
category: domain-specific
author: Jane Smith
tags: [email, classification, productivity]
updated: 2025-01-05
complexity: medium
dependencies: none
---

# Email Classifier

Categorizes emails into predefined buckets (urgent, important, 
information, spam) based on content, sender, and context.

[Complete blueprint follows...]
```

**Why this is good**:
- Specific, well-defined purpose
- Clear use case
- Appropriate complexity level
- Follows template structure

### Example 2: Improvement to Existing Agent

```
commit: Improve code-reviewer edge case handling

Changes:
- Added handling for empty file submissions
- Enhanced security check for credential detection  
- Improved error messages for malformed code
- Added 3 new examples covering these scenarios

Tested with 15 additional test cases. All pass.
```

**Why this is good**:
- Specific improvements listed
- Maintains existing functionality
- Adds tests for changes
- Clear commit message

---

## Getting Help

### Questions?

- Check existing documentation first
- Look at similar blueprints for examples
- Open a GitHub Discussion
- Tag maintainers in complex cases

### Stuck?

Use the agent-creator meta-agent to help design your blueprint:

```bash
# Load the agent-creator
cat agents/meta-agents/agent-creator.md

# Use it to guide your design process
```

---

## Recognition

Outstanding contributors may be:
- Featured in README
- Invited to maintainer team
- Credited in releases
- Given special badges

---

## Thank You!

Your contributions make this repository valuable for everyone. Whether you're submitting your first agent or your fiftieth improvement, we appreciate your effort to help the community build better AI agents.

**Happy contributing!** 🚀
