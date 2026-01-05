# Agent Blueprint Best Practices

A comprehensive guide to designing high-quality AI agents based on industry research and production deployments.

## Table of Contents

1. [Instruction Design Principles](#instruction-design-principles)
2. [System Prompt Architecture](#system-prompt-architecture)
3. [Tool Integration](#tool-integration)
4. [Example Creation](#example-creation)
5. [Testing and Validation](#testing-and-validation)
6. [Common Anti-Patterns](#common-anti-patterns)
7. [Performance Optimization](#performance-optimization)
8. [Production Readiness](#production-readiness)

---

## Instruction Design Principles

### Principle 1: Specificity Over Generality

**Bad**: "Be helpful and answer questions accurately"

**Good**: 
```markdown
When answering factual questions:
1. Verify the information is within your knowledge base
2. If certain, provide a direct answer in 1-2 paragraphs
3. If uncertain, acknowledge uncertainty and explain why
4. If beyond your knowledge cutoff, recommend current sources
```

**Why**: Specific instructions reduce ambiguity and improve consistency.

### Principle 2: Progressive Disclosure

Structure instructions from general to specific:

```markdown
## Core Behavior
[High-level principles]

### Scenario A: Simple Queries
[Specific instructions for simple cases]

### Scenario B: Complex Analysis
[Specific instructions for complex cases]

### Scenario C: Error Conditions
[Specific instructions for errors]
```

**Why**: Agents can quickly find relevant instructions without processing irrelevant details.

### Principle 3: Explicit Reasoning

Always define HOW the agent should think:

```markdown
## Reasoning Process

For each request:
1. **Classify**: Is this a question, task, or conversation?
2. **Assess**: What information/tools do I need?
3. **Plan**: What's the best approach?
4. **Execute**: Carry out the plan step by step
5. **Verify**: Does the output meet requirements?
6. **Communicate**: Present results clearly
```

**Why**: Explicit reasoning improves output quality and makes behavior predictable.

### Principle 4: Conditional Logic

Use if-then structures for clarity:

```markdown
## Response Strategy

If user asks about recent events:
→ Acknowledge knowledge cutoff and suggest current sources

If user provides code for review:
→ Analyze for: correctness, style, performance, security
→ Provide specific feedback with examples

If request is ambiguous:
→ Ask 2-3 clarifying questions before proceeding
```

**Why**: Conditional logic handles different scenarios without conflicting instructions.

---

## System Prompt Architecture

### Optimal Structure (Proven in Production)

```markdown
# 1. Role and Identity (50-100 words)
Clear definition of expertise and accountability

# 2. Environment Context (50-100 words)
Current state, available tools, user information

# 3. Core Instructions (300-800 words)
Main behavioral guidelines organized by category

# 4. Reasoning Process (100-200 words)
Step-by-step thinking approach

# 5. Tool Usage (100-300 words per tool)
When and how to use each capability

# 6. Output Format (100-200 words)
Specific templates and structure

# 7. Constraints (100-200 words)
Clear boundaries and prohibitions

# 8. Examples (200-500 words)
Diverse demonstrations

# 9. Final Reminder (20-50 words)
One critical instruction to reinforce
```

### Section-by-Section Guidelines

#### Role and Identity
```markdown
# Good Example
You are a Senior Software Engineer specializing in Python backend development. 
Your expertise includes API design, database optimization, and security best 
practices. You provide code reviews that balance correctness, maintainability, 
and performance.

# Bad Example
You are a helpful coding assistant.
```

#### Environment Context
```markdown
# Good Example
## Environment
- Current Date: 2025-01-05
- Language: Python 3.11
- Framework: FastAPI
- Database: PostgreSQL 14
- User Expertise: Mid-level engineer
- Review Focus: Production-readiness

# Bad Example
## Environment
You have access to various tools.
```

#### Core Instructions
Organize by category, not by random order:

```markdown
## Code Review Process
[Instructions about how to review]

## Feedback Communication
[Instructions about how to communicate findings]

## Security Considerations
[Instructions about security checks]
```

---

## Tool Integration

### Rule 1: One Tool, One Purpose

Each tool should have a single, clear purpose:

```yaml
# Good
search_academic_papers:
  purpose: "Search academic databases for peer-reviewed papers"
  
get_paper_metadata:
  purpose: "Extract metadata from a specific paper"

# Bad  
research_tool:
  purpose: "Search for papers, get metadata, analyze citations, and generate summaries"
```

### Rule 2: Clear Triggering Conditions

Define WHEN to use each tool:

```markdown
## Tool: web_search

**Use when:**
- User asks about events after your knowledge cutoff
- User requests current data (prices, weather, news)
- Verification of factual claims is needed

**Do NOT use when:**
- Question is about well-established historical facts
- User is asking for creative content
- Information is in your training data with high confidence
```

### Rule 3: Example-Driven Documentation

Every tool needs examples:

```markdown
## Tool: analyze_data

**Parameters**:
- data: CSV string or file path
- operation: "summarize" | "visualize" | "correlate"

**Example 1: Summarization**
```python
analyze_data(
    data="sales_data.csv",
    operation="summarize"
)
```
→ Returns: mean, median, std dev, outliers

**Example 2: Correlation**
```python
analyze_data(
    data="sales_data.csv", 
    operation="correlate",
    variables=["sales", "marketing_spend"]
)
```
→ Returns: correlation coefficient, p-value, scatter plot
```

### Rule 4: Output Handling Instructions

Always explain what to do with tool results:

```markdown
## Handling Search Results

When web_search returns results:
1. Scan all results for relevance
2. Identify the 2-3 most authoritative sources
3. Cross-reference information across sources
4. If sources conflict, present both perspectives
5. Synthesize findings in your own words (never copy verbatim)
6. Cite sources using the provided URL format
```

---

## Example Creation

### The 5 Example Rule

Every agent should have at least 5 examples covering:

1. **Happy Path**: Typical, straightforward use case
2. **Edge Case**: Unusual or boundary condition
3. **Error Handling**: Invalid or problematic input
4. **Multi-Step**: Complex workflow requiring multiple steps
5. **Constraint Testing**: Request that tests safety boundaries

### Example Structure

```markdown
### Example X: [Scenario Name]

**Context**: [Setup information]

**User**: [Exact user input]

**Agent**: [Complete agent response showing ideal behavior]

**Notes**: [Why this example matters, what it demonstrates]

---
```

### Example Quality Checklist

Each example should:
- [ ] Demonstrate a specific aspect of agent behavior
- [ ] Show complete input and output (no truncation)
- [ ] Represent realistic usage
- [ ] Illustrate best practices
- [ ] Cover edge cases, not just happy paths

### Example: Good vs Bad Examples

❌ **Bad Example** (too vague):
```markdown
User: Help me
Agent: Sure! I can help with many things.
```

✅ **Good Example** (specific and instructive):
```markdown
### Example 2: Handling Ambiguous Requests

**User**: Help me with my Python project

**Agent**: I'd be happy to help with your Python project! To provide the 
most useful assistance, could you tell me:

1. What type of project is it? (web app, data analysis, automation, etc.)
2. What specific issue or question do you have?
3. What have you tried so far?

Meanwhile, I can help with common Python tasks like debugging errors, 
reviewing code, explaining concepts, or suggesting libraries.

**Notes**: This example demonstrates how the agent handles vague requests by
asking clarifying questions while remaining helpful.
```

---

## Testing and Validation

### Test-Driven Agent Development

Write test scenarios BEFORE finalizing the agent:

```markdown
## Test Suite for Data Analyst Agent

### Test 1: Basic Analysis
Input: "Analyze this sales data: [CSV]"
Expected: Statistical summary with key insights
Pass Criteria: Includes mean, median, trends, outliers

### Test 2: Ambiguous Request
Input: "Look at the data"
Expected: Asks what type of analysis is needed
Pass Criteria: Asks 2-3 clarifying questions

### Test 3: Invalid Data
Input: [Malformed CSV]
Expected: Identifies data issues and explains
Pass Criteria: Specific error message, doesn't crash

### Test 4: Complex Analysis
Input: "Compare Q1 vs Q2 sales across regions"
Expected: Multi-step analysis with comparisons
Pass Criteria: Correct calculations, clear visualizations

### Test 5: Out of Scope
Input: "Predict next year's revenue"
Expected: Explains limitations, offers alternatives
Pass Criteria: Honest about capabilities
```

### Validation Layers

Use multiple validation approaches:

**Layer 1: Structural Validation**
- [ ] All required sections present
- [ ] Follows schema format
- [ ] No syntax errors

**Layer 2: Logical Validation**
- [ ] No conflicting instructions
- [ ] Constraints are enforced
- [ ] Reasoning process makes sense

**Layer 3: Functional Validation**
- [ ] Agent performs intended tasks
- [ ] Examples match actual behavior
- [ ] Tools are used correctly

**Layer 4: Quality Validation**
- [ ] Responses are high quality
- [ ] Tone and style are consistent
- [ ] Edge cases handled gracefully

---

## Common Anti-Patterns

### Anti-Pattern 1: The Kitchen Sink Agent

❌ **Problem**: One agent trying to do everything

```markdown
Agent: General Purpose Assistant
Capabilities: Code, writing, analysis, research, math, 
creative, translation, tutoring, advice, ...
Tools: 23 different tools
```

✅ **Solution**: Specialized agents or hierarchical architecture

```markdown
Agent 1: Code Specialist (5 code-related tools)
Agent 2: Research Specialist (5 research-related tools)  
Agent 3: Writing Specialist (5 writing-related tools)
Meta-Agent: Routes requests to appropriate specialist
```

### Anti-Pattern 2: Implicit Expectations

❌ **Problem**: Assuming the agent "just knows" what to do

```markdown
"Be professional and provide good answers."
```

✅ **Solution**: Explicit behavioral instructions

```markdown
## Professional Communication

- Use formal language appropriate for business context
- Structure responses with clear headings
- Support claims with evidence or reasoning
- Acknowledge limitations honestly
- Provide actionable recommendations
```

### Anti-Pattern 3: Example-Free Instructions

❌ **Problem**: No concrete demonstrations

```markdown
"Analyze data and provide insights"
```

✅ **Solution**: Always include examples

```markdown
"Analyze data and provide insights"

Example:
Input: Monthly sales: [Jan: $10k, Feb: $12k, Mar: $9k]
Output: 
"**Trend Analysis**: 20% increase Jan→Feb, followed by 25% 
decrease Feb→Mar, suggesting volatility. Average: $10.3k/month.

**Concern**: March decline warrants investigation. Possible 
seasonal effect or operational issue.

**Recommendation**: Compare with prior year March; analyze by 
product category to identify source of decline."
```

### Anti-Pattern 4: Vague Constraints

❌ **Problem**: Unclear boundaries

```markdown
"Don't provide harmful information"
```

✅ **Solution**: Specific, testable constraints

```markdown
## Prohibited Actions

Do NOT:
- Provide instructions for illegal activities
- Generate content that could harm minors
- Create misleading or deceptive content
- Share private or confidential information
- Bypass security measures or authentication

If a request falls into these categories:
1. Decline politely
2. Explain why you can't help
3. Offer alternative approaches if applicable
```

### Anti-Pattern 5: No Reasoning Process

❌ **Problem**: Agent jumps to answers without thinking

```markdown
[No reasoning section defined]
```

✅ **Solution**: Explicit step-by-step reasoning

```markdown
## Reasoning Process

Before responding:
1. **Understand**: What is being asked? What's the context?
2. **Classify**: What type of request is this?
3. **Assess**: What information or tools do I need?
4. **Plan**: What's my approach? What steps are involved?
5. **Execute**: Follow the plan methodically
6. **Verify**: Does my response address the request fully?
7. **Refine**: How can I make the response clearer?
```

### Anti-Pattern 6: Conflicting Instructions

❌ **Problem**: Instructions that contradict each other

```markdown
"Always provide detailed, comprehensive explanations"
...
"Keep responses concise and brief"
```

✅ **Solution**: Conditional clarity

```markdown
## Response Length Guidelines

For simple factual questions:
- Provide concise, direct answers (1-2 paragraphs)

For complex topics requiring explanation:
- Provide comprehensive coverage with clear structure
- Use headings and bullet points for scannability

For tutorial/instructional content:
- Balance detail with readability
- Include examples but don't overwhelm
```

---

## Performance Optimization

### Optimization 1: Token Efficiency

**Techniques**:
- Remove redundant instructions
- Use structured formats (YAML, JSON) for configuration
- Reference external resources instead of embedding long lists
- Use progressive disclosure (don't load everything upfront)

**Example**:
```markdown
# Inefficient (1000 tokens)
[Lists 100 specific domain terms with definitions inline]

# Efficient (50 tokens)
Refer to the domain glossary at /resources/terminology.md
when encountering specialized terms.
```

### Optimization 2: Caching Strategies

Structure prompts for optimal caching:

```markdown
# Cacheable Section (rarely changes)
## Role and Core Instructions
[Stable content here]

# Dynamic Section (changes per request)
## Current Context
- Date: {{CURRENT_DATE}}
- User Request: {{USER_INPUT}}
- Relevant History: {{RECENT_MESSAGES}}
```

### Optimization 3: Lazy Tool Loading

Don't define all tools upfront:

```markdown
# Instead of defining 20 tools in the initial prompt...

## Available Tool Categories
- Data Analysis Tools (see /tools/data/)
- Web Research Tools (see /tools/web/)
- Code Tools (see /tools/code/)

Load specific tool definitions only when needed.
```

---

## Production Readiness

### Pre-Production Checklist

Before deploying an agent to production:

#### Functionality
- [ ] Agent performs all intended tasks correctly
- [ ] Edge cases are handled gracefully
- [ ] Error messages are helpful and actionable
- [ ] Performance meets requirements

#### Safety
- [ ] Constraints are enforced consistently
- [ ] No harmful outputs in testing
- [ ] PII handling follows privacy guidelines
- [ ] Security boundaries are respected

#### Quality
- [ ] Responses are accurate and relevant
- [ ] Tone and style are consistent
- [ ] Output format meets specifications
- [ ] Documentation is complete

#### Monitoring
- [ ] Logging is configured
- [ ] Metrics are tracked
- [ ] Alerts are set up
- [ ] Feedback mechanism exists

### Deployment Strategy

**Phase 1: Canary** (1% of traffic)
- Monitor for critical issues
- Collect initial performance data
- Duration: 24-48 hours

**Phase 2: Limited** (10% of traffic)
- Validate at scale
- Compare with baseline
- Duration: 3-7 days

**Phase 3: Expansion** (50% of traffic)
- Broader validation
- Identify rare edge cases
- Duration: 1-2 weeks

**Phase 4: Full** (100% of traffic)
- Complete rollout
- Continue monitoring
- Iterate based on feedback

### Monitoring and Iteration

**Key Metrics**:
- Response accuracy rate
- Constraint violation rate
- Average response time
- User satisfaction score
- Error rate by type

**Continuous Improvement**:
1. Collect user feedback
2. Analyze failure cases
3. Update examples and instructions
4. Test changes
5. Deploy improvements
6. Monitor impact

---

## Summary: The 10 Commandments of Agent Design

1. **Be Specific**: Vague instructions create inconsistent behavior
2. **Use Examples**: Show, don't just tell
3. **Define Reasoning**: Explicit thinking processes improve quality
4. **Test Thoroughly**: Cover happy paths, edge cases, and errors
5. **Limit Scope**: Specialized agents outperform generalists
6. **Make Tools Clear**: Each tool needs purpose, parameters, and examples
7. **Enforce Constraints**: Safety boundaries must be explicit
8. **Structure for Clarity**: Use headings, sections, and hierarchies
9. **Iterate Based on Data**: Monitor, analyze, improve
10. **Document Everything**: Future you will thank present you

---

**Remember**: Great agents aren't built in a day. Start simple, test thoroughly, and iterate based on real-world usage.
