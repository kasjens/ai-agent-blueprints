# Agent Blueprints - Quick Reference

## 📁 Repository Structure

```
agent-blueprints/
├── README.md                    ← Start here
├── LICENSE                      ← MIT License
├── CONTRIBUTING.md              ← How to contribute
├── .gitignore                   ← Git ignore rules
│
├── agents/                      ← Agent blueprints
│   ├── core/                    ← General-purpose agents
│   │   └── default-agent.md     ← Standard conversational agent
│   ├── domain-specific/         ← Specialized agents (empty, ready for your agents)
│   ├── meta-agents/             ← Agents that create/manage agents
│   │   └── agent-creator.md     ← Creates new agent blueprints
│   └── experimental/            ← Beta/experimental agents
│
├── templates/                   ← Reusable templates
│   └── agent-template.md        ← Base template for new agents
│
├── schemas/                     ← Validation schemas
│   └── agent-schema.json        ← JSON schema for validation
│
├── examples/                    ← Example implementations
│   └── simple-chatbot/          ← Python chatbot example
│       └── README.md
│
├── tests/                       ← Test cases (empty, ready for tests)
│
└── docs/                        ← Documentation
    ├── getting-started.md       ← Beginner's guide
    └── best-practices.md        ← Design best practices
```

## 🚀 Quick Start (5 Minutes)

### 1. Browse Available Agents
```bash
cd agent-blueprints/agents/core
cat default-agent.md          # General conversational agent
```

### 2. Use an Agent Blueprint
Copy the "System Prompt" section from any blueprint and use it with:
- Claude (claude.ai) in Project instructions
- OpenAI API as system message
- Any other LLM that supports system prompts

### 3. Create a New Agent

**Option A: Use the Agent Creator (Recommended)**
```bash
cat agents/meta-agents/agent-creator.md
# Copy this system prompt to Claude/GPT-4
# Then: "Create an agent that [your requirements]"
```

**Option B: Manual Creation**
```bash
cp templates/agent-template.md agents/domain-specific/my-agent.md
# Fill in all sections
# Test thoroughly
```

## 📋 Blueprint Anatomy

Every blueprint has this structure:

```yaml
---
name: agent-name              # Unique ID (kebab-case)
version: 1.0.0               # Semantic versioning
category: core               # core|domain-specific|meta-agent
author: Your Name            # Creator
tags: [tag1, tag2]          # Descriptive tags
updated: 2025-01-05         # Last modified date
complexity: low             # low|medium|high
dependencies: none          # Required tools/APIs
---

# Agent Name
Description of what the agent does

## System Prompt
The complete instructions for the AI
(This is what you copy and use)

## Examples  
Usage demonstrations

## Validation
How to test the agent
```

## 🎯 Use Cases by Agent Type

| Need | Use This | Location |
|------|----------|----------|
| General conversation | default-agent | agents/core/ |
| Create new agents | agent-creator | agents/meta-agents/ |
| Custom domain | Create your own | Use template |
| Multiple agents | agent-orchestrator | agents/meta-agents/ (to be created) |

## ⚙️ Customization Quick Tips

### Adjust Behavior
Most agents have customizable parameters:
```yaml
expertise: general|beginner|intermediate|expert
verbosity: concise|balanced|detailed  
tone: formal|professional|casual|friendly
domain: your-domain-here
```

### Replace Template Variables
Before using, replace these in the system prompt:
- `{{CURRENT_DATE}}` → Today's date
- `{{WORKING_DIR}}` → Your working directory  
- `{{TOOLS_LIST}}` → Available tools
- `{{USER_CONTEXT}}` → Your information

### Add Constraints
Append to the "Constraints" section:
```markdown
**Additional Constraints**:
- Never share personal data
- Always cite sources
- Use metric units
```

## 🧪 Testing Your Agent

Use the blueprint's validation section:

```markdown
## Quick Test Checklist
□ Test a normal request
□ Test an ambiguous request  
□ Test an out-of-scope request
□ Test an edge case
□ Verify constraints are enforced
```

## 🏗️ Creating Your First Agent

**5-Step Process:**

1. **Define Purpose**: "This agent should..."
2. **Use Agent Creator**: Let it guide you through design
3. **Generate Blueprint**: Get complete configuration
4. **Test Thoroughly**: Use validation checklist
5. **Refine & Deploy**: Iterate based on results

## 📚 Key Documents

| Document | When to Read |
|----------|-------------|
| README.md | First time using the repo |
| getting-started.md | Before creating your first agent |
| best-practices.md | Before creating complex agents |
| CONTRIBUTING.md | Before submitting changes |
| agent-template.md | When manually creating agents |
| agent-creator.md | When you need help designing agents |

## 🔧 Common Tasks

### Task: Use Default Agent with Claude
1. Open `agents/core/default-agent.md`
2. Copy everything in "System Prompt" section
3. Go to claude.ai → Project → Custom Instructions
4. Paste the system prompt
5. Replace `{{VARIABLES}}` with actual values
6. Start chatting!

### Task: Create a Domain-Specific Agent
1. Load `agents/meta-agents/agent-creator.md` into Claude
2. Say: "Create an agent for [your domain/task]"
3. Answer the creator's questions
4. Review and customize the generated blueprint
5. Save to `agents/domain-specific/your-agent.md`

### Task: Test an Agent
1. Read the "Validation" section of the blueprint
2. Run each test scenario
3. Verify expected behaviors
4. Check constraints are enforced
5. Document any issues

## 💡 Pro Tips

1. **Start Simple**: Use default-agent as base, customize gradually
2. **Use Examples**: The more examples in your blueprint, the better
3. **Be Specific**: Vague instructions = inconsistent behavior  
4. **Test Edge Cases**: Don't just test happy paths
5. **Version Everything**: Use semantic versioning (1.0.0 → 1.1.0 → 2.0.0)
6. **Document Changes**: Update version history with every change

## 🚨 Common Mistakes to Avoid

❌ Too many tools (>10)
❌ Vague instructions
❌ No examples
❌ Skipping validation
❌ Conflicting constraints
❌ No error handling

✅ 5-7 focused tools
✅ Specific, actionable instructions  
✅ 3-5 diverse examples
✅ Thorough testing
✅ Clear, consistent rules
✅ Graceful error handling

## 🎓 Learning Path

**Beginner** (1-2 hours):
1. Read main README
2. Study default-agent.md
3. Use it in Claude/GPT-4
4. Customize one parameter

**Intermediate** (2-4 hours):
1. Read getting-started.md
2. Use agent-creator to make an agent
3. Test your agent thoroughly
4. Review best-practices.md

**Advanced** (4+ hours):
1. Create agents manually from template
2. Build multi-agent systems
3. Contribute to repository
4. Optimize for production

## 📞 Getting Help

1. **Check docs first**: Most questions answered in docs/
2. **Look at examples**: See examples/ for working code
3. **Use agent-creator**: It can guide you through design
4. **Ask community**: Open GitHub discussion

## 🎉 Success Indicators

You're ready to create great agents when you can:
- [ ] Explain what makes instructions clear vs. vague
- [ ] Identify anti-patterns in agent design
- [ ] Create 5+ diverse test scenarios
- [ ] Write specific, measurable validation criteria
- [ ] Design appropriate tool schemas
- [ ] Structure agents for maintainability

---

**Ready to build?** Start with `docs/getting-started.md` for detailed guidance!

**Need inspiration?** Check out the research report on best practices!

**Want to contribute?** See `CONTRIBUTING.md` for guidelines!
