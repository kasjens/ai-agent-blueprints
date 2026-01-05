# Cline Quick Reference Card

**Print this and keep it near your desk!**

---

## Essential Prompts

### Starting New Project
```
Implement this project according to docs/CLINE_BRIEF.md

Read all docs, then show your implementation plan.
After I approve, implement Phase 1 and stop.
```

### Starting a Phase
```
Phase [X]: [Name]

From docs/CLINE_BRIEF.md section [Y], implement:
- [Item 1]
- [Item 2]

Show plan first, then implement after my approval.
```

### Continuing Work
```
Continue from .cline/progress.md

Next: Implement [specific feature]
Follow specs in docs/CLINE_BRIEF.md exactly.
```

### Debugging
```
Issue: [What's wrong]
Expected: [What should happen]
Actual: [What's happening]

Investigate and fix. Show me the root cause.
```

### Reviewing
```
Show me what changed in the last step
```

### Testing
```
Run all tests and show results.
If any fail, fix them.
```

### Correcting Course
```
Stop. You deviated from the architecture.

Architecture requires [X] (docs/architecture.md section [Y])
You implemented [Z]

Revert and implement correctly per specification.
```

---

## Project Setup Checklist

```
my-project/
├── docs/
│   ├── research-output.md       ✓ From Research Agent
│   ├── architecture.md          ✓ From Solution Architect
│   └── CLINE_BRIEF.md          ✓ Implementation spec
├── .cline/
│   ├── instructions.md          ✓ Project context
│   └── progress.md             ✓ Track completion
├── src/                         ← Cline creates
├── tests/                       ← Cline creates
├── README.md
└── .gitignore
```

---

## Custom Instructions (Paste in Cline Settings)

```markdown
You implement code from detailed architecture specs.

Key Principles:
1. Follow CLINE_BRIEF.md EXACTLY
2. Implement incrementally with approval
3. Write production-quality code with tests
4. Include error handling and validation
5. Update documentation as you go

When specifications exist:
- Stick to specified tech stack and versions
- Follow exact folder structure
- Match API endpoints precisely
- Use patterns from provided examples

Ask clarifying questions if specifications are ambiguous.
Never make architectural decisions without approval.

Show plan before implementing each phase.
```

---

## Optimal Settings

```json
{
  "cline.autoApprove": false,
  "cline.temperature": 0.2,
  "cline.maxHistoryMessages": 50,
  "cline.terminalApprovalRequired": true,
  "cline.model": "claude-sonnet-4-20250514"
}
```

---

## Git Workflow

```bash
# Before each phase
git add .
git commit -m "Before Phase [X]"

# After phase completes
git add .
git commit -m "Phase [X] complete: [description]"

# If something breaks
git reset --hard HEAD  # Rollback
```

---

## Common Issues & Fixes

### Issue: Cline makes changes not in spec
**Fix**: 
```
Stop. Revert last change.
Implement according to docs/architecture.md section [X]
```

### Issue: Tests failing
**Fix**:
```
Run: npm test
Show errors
Fix ONLY the failing tests
Verify all pass
```

### Issue: API rate limit
**Fix**: Slow down approvals (wait 30s between phases)

### Issue: Cline asks too many questions
**Fix**: Make CLINE_BRIEF.md more detailed with examples

---

## Quality Checklist (After Each Phase)

- [ ] Code matches architecture specification
- [ ] Tests written and passing
- [ ] Error handling present
- [ ] Documentation updated
- [ ] No hardcoded secrets
- [ ] git commit created
- [ ] progress.md updated

---

## Emergency Commands

### Stop Everything
```
Stop. Don't proceed further.
```

### Show Current State
```
Show me:
1. What files you've changed
2. What's currently working
3. What's not implemented yet
```

### Reset Last Action
```
Undo the last change you made.
Show me what you're reverting.
```

### Verify Everything
```
Run these checks:
1. npm run build
2. npm test
3. npm run lint
Show results for each.
```

---

## Pro Tips

✅ **Review each phase** - Don't auto-approve blindly
✅ **Commit frequently** - Easy rollback if needed
✅ **Keep docs updated** - Cline uses them as reference
✅ **Start small** - One module at a time
✅ **Test as you go** - Don't defer testing

❌ **Don't skip phases** - Follow order in CLINE_BRIEF
❌ **Don't change specs mid-stream** - Update docs first
❌ **Don't let Cline decide architecture** - That's your job
❌ **Don't enable auto-approve** - Quality > speed

---

## Phase Template

```markdown
Phase [X]: [Name] (Day/Week [Y])

Goal: [What this achieves]

Tasks:
- [ ] [Task 1]
- [ ] [Task 2]
- [ ] [Task 3]

Deliverables:
- [Deliverable 1]
- [Deliverable 2]

Success Criteria:
- [How to verify]
```

---

## Daily Workflow

**Morning**:
1. Check `.cline/progress.md`
2. Review what's completed
3. Decide on today's phases
4. Tell Cline what to implement

**During**:
5. Approve phases as Cline completes them
6. Review code quality
7. Run tests after each phase
8. Commit to git

**Evening**:
9. Update progress.md
10. Push to git
11. Plan tomorrow's work

---

## Useful VS Code Commands

```
Ctrl/Cmd + Shift + P → Cline: Open
Ctrl/Cmd + Shift + P → Cline: Clear History
Ctrl/Cmd + Shift + P → Cline: Export Conversation
```

---

## Agent → Cline Flow (One Page)

```
┌─────────────────────────────────────────┐
│ 1. Research Agent (AnythingLLM)         │
│    "Research [topic] best practices"    │
│    Output: research-output.md           │
└─────────────────┬───────────────────────┘
                  ↓
┌─────────────────────────────────────────┐
│ 2. Solution Architect (AnythingLLM)     │
│    "Design architecture for [project]"  │
│    Output: architecture.md              │
└─────────────────┬───────────────────────┘
                  ↓
┌─────────────────────────────────────────┐
│ 3. Create Implementation Brief          │
│    Combine research + architecture      │
│    Output: CLINE_BRIEF.md              │
└─────────────────┬───────────────────────┘
                  ↓
┌─────────────────────────────────────────┐
│ 4. Cline (VS Code)                      │
│    "Implement per CLINE_BRIEF.md"      │
│    Output: Working code + tests         │
└─────────────────────────────────────────┘
```

---

## Model Recommendations

| Provider | Model | Best For | Cost/Hour |
|----------|-------|----------|-----------|
| Anthropic | Claude Sonnet 4 | Best quality | ~$3 |
| Anthropic | Claude Sonnet 3.5 | Great quality | ~$2 |
| OpenAI | GPT-4o | Good alternative | ~$2-3 |
| Mistral | mistral-large-latest | Budget option | ~$1-2 |
| Ollama | deepseek-coder:33b | Local/Free | $0 |

**Recommendation**: Claude Sonnet 4 for complex architectures

---

## When to Intervene

**Cline's Plan Looks Good** ✅:
- Matches architecture specifications
- Includes tests
- Has error handling
- Follows patterns from examples
→ **Approve and let it proceed**

**Cline's Plan Has Issues** ❌:
- Deviates from specs
- Missing tests or error handling
- Wrong technology choice
- Unclear about something
→ **Stop, correct, clarify, then approve**

---

## Remember

**Cline is your implementation assistant**, not your architect.

**You design** (via Research + Solution Architect agents)
**Cline implements** (faithfully executing your design)

**Best results** = Detailed specs + Incremental approval + Regular review

---

**Questions?** See CLINE_SETUP_GUIDE.md for detailed documentation.

**Happy Coding!** 🚀
