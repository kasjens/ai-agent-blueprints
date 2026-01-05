# Cline Setup & Configuration Guide for Agent-Driven Development

Complete guide to installing, configuring, and optimizing Cline to work with your Research and Solution Architect agents.

## Table of Contents
1. [What is Cline?](#what-is-cline)
2. [Installation](#installation)
3. [API Configuration](#api-configuration)
4. [Custom Instructions Setup](#custom-instructions-setup)
5. [Project Structure for Cline](#project-structure)
6. [Optimal Prompting Strategies](#optimal-prompting)
7. [Advanced Configuration](#advanced-configuration)
8. [Troubleshooting](#troubleshooting)

---

## What is Cline?

**Cline** (formerly Claude Dev) is an autonomous AI coding agent that runs as a VS Code extension.

**What Cline Can Do**:
- ✅ Read and edit files in your project
- ✅ Execute terminal commands (npm install, git, etc.)
- ✅ Create entire project structures
- ✅ Write tests and documentation
- ✅ Debug and fix issues
- ✅ Use tools (file operations, terminal, browser automation)

**Key Difference from AnythingLLM**:
- **AnythingLLM**: Gives you guidance and documentation
- **Cline**: Actually writes code in your project

**Best Model for Agent-Driven Development**: Claude Sonnet 3.5/4 or GPT-4 (highest quality code generation)

---

## Installation

### Step 1: Install VS Code Extension

**Method 1: VS Code Marketplace**
```bash
1. Open VS Code
2. Press Ctrl+Shift+X (Windows/Linux) or Cmd+Shift+X (Mac)
3. Search for "Cline"
4. Click "Install"
5. Reload VS Code
```

**Method 2: Command Line**
```bash
code --install-extension saoudrizwan.claude-dev
```

### Step 2: Verify Installation

1. Look for Cline icon in the left sidebar (looks like a robot/assistant)
2. Or use Command Palette: `Ctrl+Shift+P` → type "Cline"
3. Should see "Cline: Open" option

### Step 3: First Launch

1. Click the Cline icon in sidebar
2. Cline panel opens
3. You'll see API configuration prompt

---

## API Configuration

Cline supports multiple LLM providers. Choose based on your preference:

### Option 1: Anthropic (Claude) - Recommended

**Why**: Best code generation quality, understands complex architectures

**Setup**:
```bash
1. Get API key from: https://console.anthropic.com/
2. In Cline settings, select "Anthropic"
3. Enter API key
4. Select model: Claude Sonnet 4 or Claude Sonnet 3.5
```

**Cost**: ~$3 per hour of active coding

**Configuration**:
```json
{
  "provider": "anthropic",
  "apiKey": "sk-ant-...",
  "model": "claude-sonnet-4-20250514",
  "maxTokens": 8192
}
```

### Option 2: OpenAI (GPT-4)

**Why**: Good alternative, widely available

**Setup**:
```bash
1. Get API key from: https://platform.openai.com/
2. In Cline settings, select "OpenAI"
3. Enter API key
4. Select model: gpt-4o or gpt-4-turbo
```

**Cost**: ~$2-4 per hour of active coding

**Configuration**:
```json
{
  "provider": "openai",
  "apiKey": "sk-...",
  "model": "gpt-4o",
  "temperature": 0.2
}
```

### Option 3: OpenAI-Compatible (Mistral via Le Chat)

**Why**: Cost-effective, you already have Mistral

**Setup**:
```bash
1. Get Mistral API key from: https://console.mistral.ai/
2. In Cline settings, select "OpenAI Compatible"
3. Base URL: https://api.mistral.ai/v1
4. API key: your Mistral key
5. Model: mistral-large-latest
```

**Cost**: ~$1-2 per hour of active coding

**Configuration**:
```json
{
  "provider": "openai-compatible",
  "baseUrl": "https://api.mistral.ai/v1",
  "apiKey": "your-mistral-key",
  "model": "mistral-large-latest"
}
```

### Option 4: Local Models (Ollama)

**Why**: Free, private, no API costs

**Setup**:
```bash
# Install Ollama
curl -fsSL https://ollama.com/install.sh | sh

# Pull a model
ollama pull deepseek-coder:33b

# In Cline settings
Provider: Ollama
Base URL: http://localhost:11434
Model: deepseek-coder:33b
```

**Trade-off**: Slower, lower quality than Claude/GPT-4

---

## Custom Instructions Setup

This is the KEY to making Cline work optimally with your agents!

### Access Custom Instructions

```bash
1. Open Cline panel
2. Click settings gear icon (top right)
3. Look for "Custom Instructions" or "System Prompt"
```

### Optimal Custom Instructions for Agent-Driven Development

**Copy this into Cline's Custom Instructions**:

```markdown
# Custom Instructions for Agent-Driven Development

You are Cline, an autonomous development assistant working from comprehensive architecture specifications.

## Your Role

You implement code based on detailed architecture documents created by specialized research and solution architect agents. Your job is to:
1. Follow architecture specifications EXACTLY
2. Maintain consistency with design decisions
3. Ask clarifying questions when specifications are ambiguous
4. Implement incrementally with approval at each phase

## Input Documents

You will frequently receive these documents:
- **CLINE_BRIEF.md**: Complete implementation specification
- **architecture.md**: High-level architecture and design decisions
- **research-output.md**: Technology research and best practices

When these documents are present, treat them as your primary source of truth.

## Implementation Principles

### 1. Specification Adherence
- Follow folder structure EXACTLY as specified
- Use technologies and versions specified in tech stack
- Implement APIs exactly as documented (endpoints, request/response formats)
- Match database schemas precisely
- Follow code patterns from examples provided

### 2. Quality Standards
- Write production-quality code (not prototypes)
- Include comprehensive error handling
- Add input validation on all user inputs
- Write tests as you implement (don't defer testing)
- Add meaningful comments for complex logic
- Follow TypeScript/language best practices

### 3. Security First
- Never hardcode secrets (use environment variables)
- Validate and sanitize all inputs
- Use parameterized queries (prevent SQL injection)
- Implement proper authentication/authorization
- Follow OWASP security guidelines

### 4. Incremental Development
- Implement one module/feature at a time
- Show your plan before starting each phase
- Request approval before moving to next phase
- Don't make assumptions - ask when unclear

### 5. Documentation
- Update README as you implement
- Add API documentation (Swagger/JSDoc)
- Document environment variables
- Include setup instructions

## When Reading Architecture Documents

Look for these key sections:
1. **Technology Stack**: Exact packages and versions to use
2. **Project Structure**: Folder organization to create
3. **Database Schema**: Tables/entities to implement
4. **API Specifications**: Endpoints with full details
5. **Implementation Phases**: Step-by-step plan to follow
6. **Success Criteria**: How to verify completion

## Response Format

When implementing, structure your work as:

1. **Phase Declaration**: "Implementing Phase X: [description]"
2. **Plan**: Show what you'll create/modify
3. **Implementation**: Create/edit files
4. **Verification**: Run tests, show it works
5. **Request Approval**: Ask before continuing

## Code Style

- Use modern language features (async/await, arrow functions)
- Prefer functional programming patterns where appropriate
- Use dependency injection for testability
- Keep functions small and focused (single responsibility)
- Name variables/functions descriptively
- Use TypeScript strict mode when applicable

## Testing Approach

- Write unit tests for business logic
- Write integration tests for APIs
- Write E2E tests for critical flows
- Mock external dependencies
- Aim for 80%+ code coverage
- Test error cases, not just happy paths

## Communication Style

- Be concise but thorough
- Show confidence in your implementations
- Ask specific questions when clarification needed
- Explain your reasoning for deviations from spec
- Proactively identify potential issues

## When Specifications Are Missing

If architecture documents don't specify something:
1. First, check if it's implied by related specifications
2. If truly ambiguous, ask the user for clarification
3. Suggest reasonable defaults based on best practices
4. Don't make major architectural decisions without approval

## Error Handling Pattern

Always implement proper error handling:
- Try-catch blocks for async operations
- Meaningful error messages
- Appropriate HTTP status codes for APIs
- Error logging (without exposing sensitive data)
- Graceful degradation where possible

## Performance Considerations

- Add database indexes for foreign keys and frequently queried fields
- Implement caching where specified
- Use connection pooling for databases
- Optimize N+1 query problems
- Lazy load where appropriate

Remember: You're implementing a well-researched, carefully architected system. Your job is faithful execution of the design, not re-architecting. When in doubt, stick to the specifications and ask questions.
```

---

## Project Structure for Cline

Organize your project to make it easy for Cline to find documentation.

### Recommended Structure

```
my-project/
├── .cline/                          # Cline-specific files
│   ├── instructions.md              # Project-specific instructions for Cline
│   └── progress.md                  # Track what's been implemented
├── docs/
│   ├── research-output.md           # From Research Agent
│   ├── architecture.md              # From Solution Architect Agent
│   └── CLINE_BRIEF.md              # Master implementation spec
├── src/                             # Cline creates this
├── tests/                           # Cline creates this
├── .env.example
├── README.md
├── package.json                     # Cline creates/updates
└── .gitignore
```

### Create .cline/instructions.md

This gives Cline project-specific context:

```markdown
# Project-Specific Instructions

## Project: [Your Project Name]

### Quick Reference
- Architecture: docs/architecture.md
- Implementation Spec: docs/CLINE_BRIEF.md
- Research: docs/research-output.md

### Tech Stack
[Paste from architecture]

### Key Decisions
1. [Decision 1 from architecture]
2. [Decision 2 from architecture]

### Current Phase
Phase [X]: [What you're currently implementing]

### Completed
- [x] Phase 1: Project setup
- [x] Phase 2: Authentication
- [ ] Phase 3: Core features (IN PROGRESS)

### Notes
- [Any deviations from architecture and why]
- [Issues encountered and solutions]
```

### Create .cline/progress.md

Track implementation progress:

```markdown
# Implementation Progress

## Completed Components
- [x] Project initialization
- [x] Database schema
- [x] Auth module (with tests)

## In Progress
- [ ] Tasks module (60% done)
  - [x] Controller
  - [x] Service
  - [ ] Tests

## Pending
- [ ] Teams module
- [ ] API documentation
- [ ] Docker setup

## Issues Resolved
1. TypeORM connection issue - fixed by adjusting config
2. JWT expiry handling - implemented refresh token rotation

## Questions for Next Session
1. Should we add rate limiting at this phase?
2. Confirm email validation regex pattern
```

---

## Optimal Prompting Strategies

### Initial Project Prompt

**When starting fresh**:

```
I need you to implement a project based on comprehensive architecture 
specifications.

Please read these documents in order:
1. docs/CLINE_BRIEF.md - Master implementation specification
2. docs/architecture.md - Architecture details
3. .cline/instructions.md - Project-specific context

After reading, please:
1. Summarize your understanding of what we're building
2. Confirm the tech stack
3. Show me your implementation plan (phases)
4. Ask any clarifying questions

Then implement Phase 1 and wait for my approval before continuing.

Ready to start?
```

### Continuing Work Prompt

**When resuming development**:

```
Continuing implementation of [Project Name].

Current state: Check .cline/progress.md

Next task: Implement Phase [X] from docs/CLINE_BRIEF.md

Please:
1. Review what's been completed
2. Show your plan for Phase [X]
3. Implement Phase [X]
4. Update progress.md when done

Follow all specifications in CLINE_BRIEF.md exactly.

Begin with Phase [X].
```

### Phase-Based Prompt Template

```
Phase [X]: [Phase Name]

Goal: [What this phase achieves]

From CLINE_BRIEF.md section [Y], please implement:
- [Specific item 1]
- [Specific item 2]
- [Specific item 3]

Requirements:
- Follow the exact folder structure in the architecture
- Use the technologies specified
- Include unit tests
- Update README with new features

Show me your plan first, then implement after I approve.
```

### Debugging/Fixing Prompt

```
Issue: [Describe the problem]

Context: [What you were trying to do]

Expected: [What should happen]

Actual: [What's happening]

Please:
1. Investigate the issue
2. Explain what's causing it
3. Propose a solution
4. Implement the fix
5. Verify with tests

Reference: [Relevant section in architecture if applicable]
```

### Refactoring Prompt

```
We need to refactor [component] to [reason].

Current implementation: src/[path]

Architecture guidance: docs/architecture.md section [X]

Requirements:
- Maintain backward compatibility
- Add tests for refactored code
- Update documentation
- Follow patterns from architecture

Show your refactoring plan first.
```

---

## Advanced Configuration

### Cline Settings Configuration

Access via: Cline panel → Settings gear → "Edit settings.json"

**Optimal Settings**:

```json
{
  // API Configuration
  "cline.provider": "anthropic",
  "cline.apiKey": "your-api-key",
  "cline.model": "claude-sonnet-4-20250514",
  
  // Behavior Settings
  "cline.autoApprove": false,                    // IMPORTANT: Keep false for review
  "cline.maxTokens": 8192,
  "cline.temperature": 0.2,                      // Lower = more consistent
  
  // File Operations
  "cline.maxFileSize": 1000000,                  // 1MB max file size to read
  "cline.excludePatterns": [
    "**/node_modules/**",
    "**/dist/**",
    "**/build/**",
    "**/.git/**"
  ],
  
  // Terminal
  "cline.allowTerminalCommands": true,
  "cline.terminalApprovalRequired": true,        // Review before executing
  
  // Memory
  "cline.maxHistoryMessages": 50,                // Keep context of last 50 messages
  
  // Custom Instructions
  "cline.customInstructions": "[Paste custom instructions from above]"
}
```

### VS Code Workspace Settings

Create `.vscode/settings.json`:

```json
{
  // Cline-specific
  "cline.projectContext": "docs/CLINE_BRIEF.md",
  
  // Editor settings
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll": true,
    "source.organizeImports": true
  },
  
  // TypeScript
  "typescript.preferences.importModuleSpecifier": "relative",
  "typescript.suggest.autoImports": true,
  
  // File associations
  "files.exclude": {
    "**/node_modules": true,
    "**/dist": true
  }
}
```

### Environment Configuration

Create `.env.cline`:

```bash
# API Configuration
CLINE_API_KEY=your-api-key
CLINE_MODEL=claude-sonnet-4-20250514

# Project Context
CLINE_PROJECT_DOCS=docs/CLINE_BRIEF.md
CLINE_ARCHITECTURE=docs/architecture.md
```

---

## Workflow: Agent → Cline Integration

### Complete Workflow with Commands

#### 1. Research Phase (AnythingLLM)

```
Workspace: Research Agent
Prompt: "Research Node.js API best practices 2025"
Output: Save as docs/research-output.md
```

#### 2. Architecture Phase (AnythingLLM)

```
Workspace: Solution Architect
Prompt: "Design API architecture based on research. [paste context]"
Output: Save as docs/architecture.md
```

#### 3. Create Implementation Brief

```bash
# Copy template
cp CLINE_BRIEF_TEMPLATE.md my-project/docs/CLINE_BRIEF.md

# Edit and fill in from architecture
code docs/CLINE_BRIEF.md
```

#### 4. Initialize Project Structure

```bash
mkdir my-project
cd my-project
mkdir -p docs .cline src tests

# Add architecture documents
mv ../docs/research-output.md docs/
mv ../docs/architecture.md docs/
mv ../docs/CLINE_BRIEF.md docs/

# Create Cline instructions
cat > .cline/instructions.md << 'EOF'
# Project Instructions
See docs/CLINE_BRIEF.md for complete specification.

Tech Stack: [From architecture]
Current Phase: Phase 1 - Setup
EOF
```

#### 5. Start Cline Implementation

```bash
# Open in VS Code
code .

# In VS Code:
# 1. Open Cline panel (click icon)
# 2. Paste initial prompt
```

**Initial Prompt**:
```
Please implement this project according to docs/CLINE_BRIEF.md.

Read the specification completely, then:
1. Initialize the project with the specified tech stack
2. Create the folder structure from the architecture
3. Implement Phase 1: [Foundation]

Show your plan before starting, then implement after I approve each step.
```

#### 6. Progressive Implementation

**For each phase**:

```
Cline: "Here's my plan for Phase 1: [shows plan]"
You: "Approved. Proceed."

Cline: [Implements Phase 1]
Cline: "Phase 1 complete. Tests passing. Ready for Phase 2?"

You: "Yes, proceed with Phase 2"

Cline: "Here's my plan for Phase 2: [shows plan]"
[Continue...]
```

---

## Best Practices

### ✅ Do This

**1. Keep Architecture Docs Updated**
```bash
# When architecture changes, update docs
# Cline will notice and adapt
```

**2. Review Before Approving**
```bash
# Don't blindly approve
# Check:
- Does it match specifications?
- Are there tests?
- Is error handling present?
```

**3. Use .cline/progress.md**
```bash
# Keep this updated so Cline knows state
# Especially useful when resuming work
```

**4. Commit Frequently**
```bash
git add .
git commit -m "Phase 1 complete: Project setup"
# Allows easy rollback if needed
```

**5. Test as You Go**
```bash
# After each phase:
npm test
npm run build
# Verify it works before continuing
```

### ❌ Avoid This

**1. Vague Prompts**
```bash
# Don't: "Build the API"
# Do: "Implement Phase 2 from CLINE_BRIEF.md: Auth module with JWT"
```

**2. No Architecture Reference**
```bash
# Don't: Let Cline make architectural decisions
# Do: "Follow architecture.md section 3.2 exactly"
```

**3. Auto-Approve Everything**
```bash
# Don't: Enable auto-approve in settings
# Do: Review each major change
```

**4. Skipping Phases**
```bash
# Don't: "Build everything at once"
# Do: "Complete Phase 1, then show results"
```

**5. No Documentation**
```bash
# Don't: Skip README and API docs
# Do: Include "Update documentation" in each phase
```

---

## Troubleshooting

### Problem: Cline Deviates from Architecture

**Solution**:
```
Stop. The architecture specifically requires [X], but you implemented [Y].

Please revert and implement according to docs/architecture.md section [Z].

Show me the relevant section of the architecture, confirm your 
understanding, then implement correctly.
```

### Problem: Cline Asks Too Many Questions

**Solution**: Make CLINE_BRIEF.md more detailed

```markdown
# Add to CLINE_BRIEF.md

## Implementation Details

### Auth Module
File: src/auth/auth.service.ts

```typescript
// Implement EXACTLY this interface
export class AuthService {
  async register(dto: RegisterDto): Promise<User> {
    // 1. Validate email uniqueness
    // 2. Hash password with bcrypt (12 rounds)
    // 3. Create user in database
    // 4. Return user (exclude password)
  }
}
```

Don't deviate from this structure.
```

### Problem: Cline Makes Breaking Changes

**Solution**: Use git commits as checkpoints

```bash
# Before each phase
git add .
git commit -m "Before Phase 3"

# If Cline breaks something
git reset --hard HEAD
# Start over with clearer instructions
```

### Problem: Performance Issues

**Solution 1**: Reduce Context
```bash
# In Cline settings
"cline.maxHistoryMessages": 25  # Reduce from 50
```

**Solution 2**: Exclude Large Files
```json
{
  "cline.excludePatterns": [
    "**/node_modules/**",
    "**/dist/**",
    "**/*.min.js",
    "**/package-lock.json"
  ]
}
```

**Solution 3**: Break Prompts Into Smaller Steps
```
Don't: "Implement the entire API"
Do: "Implement just the auth controller. Stop after that."
```

### Problem: API Rate Limits

**Solution**: Implement delays between phases

```
After completing each phase, I'll approve the next one.
This gives you time between API calls.

[Approve Phase 1]
[Wait 30 seconds]
[Approve Phase 2]
```

### Problem: Tests Failing

**Solution**: Dedicated testing phase

```
We have failing tests. Let's debug:

1. Run: npm test
2. Show me the error output
3. Identify the root cause
4. Fix ONLY the failing tests
5. Verify all tests pass

Don't change working code to fix tests - fix the tests.
```

---

## Optimization Tips

### 1. Leverage Cline's Strengths

**Cline is excellent at**:
- Boilerplate generation (setup, configs)
- Implementing well-specified components
- Following patterns from examples
- Writing tests based on specifications
- Debugging with clear error messages

**Use Cline for**:
- Initial project setup
- CRUD operations
- Test writing
- Documentation generation
- Refactoring for consistency

### 2. Human-in-the-Loop for Key Decisions

**You should decide**:
- Architecture changes
- Technology choices
- API contract changes
- Security implementations
- Performance optimizations

**Let Cline decide**:
- Variable naming
- Code organization within modules
- Test structure
- Documentation wording

### 3. Batch Related Changes

```
Implement the entire auth module in one session:
- auth.controller.ts
- auth.service.ts
- auth.module.ts
- dto/register.dto.ts
- dto/login.dto.ts
- auth.service.spec.ts

All in one phase, following the architecture pattern.
```

### 4. Use Templates for Repetitive Components

```markdown
# In CLINE_BRIEF.md

## Module Template

Every module should follow this structure:

[module-name]/
├── [module].controller.ts
├── [module].service.ts
├── [module].module.ts
├── entities/
│   └── [entity].entity.ts
├── dto/
│   ├── create-[entity].dto.ts
│   └── update-[entity].dto.ts
└── [module].service.spec.ts

When I say "Implement [X] module", use this template.
```

### 5. Progress Checkpoints

```
After every 3 phases:
1. Run full test suite
2. Verify build succeeds
3. Update progress.md
4. Commit to git
5. Brief summary of what's working

Then continue to next 3 phases.
```

---

## Example: Complete Session

### Setup (One-time)

```bash
# 1. Create project
mkdir task-api
cd task-api

# 2. Add architecture docs
mkdir -p docs .cline
cp ~/agent-blueprints/outputs/architecture.md docs/
cp ~/agent-blueprints/outputs/CLINE_BRIEF.md docs/

# 3. Initialize git
git init
git add docs/
git commit -m "Add architecture specifications"

# 4. Open in VS Code with Cline
code .
```

### Session 1: Foundation

**In Cline**:

```
You: Please implement this project according to docs/CLINE_BRIEF.md

Starting with Phase 1: Foundation (from section 8).

Read CLINE_BRIEF.md first, then show me your plan for Phase 1.

Cline: [Reads file, shows plan]
"I'll implement:
1. Initialize NestJS project
2. Install dependencies from tech stack
3. Set up TypeORM with PostgreSQL
4. Create basic folder structure
5. Configure environment variables

Ready to proceed?"

You: Approved. Implement Phase 1.

Cline: [Implements Phase 1]
[Creates project structure, installs packages, configures database]

Cline: "Phase 1 complete. Project initialized. Tests running. Ready for Phase 2?"

You: Show me the folder structure first.

Cline: [Shows structure]

You: Good. Commit this before continuing.

Cline: [Commits with message "Phase 1: Project foundation"]

You: Now proceed with Phase 2: Auth Module
```

### Session 2: Core Features

```
You: Continuing implementation. Check .cline/progress.md for status.

Implement Phase 3: Tasks Module from CLINE_BRIEF.md

Follow the exact structure and specifications.

Cline: [Reviews progress.md]
"I see Phase 1 and 2 are complete. Starting Phase 3: Tasks Module.

I'll implement:
- tasks.controller.ts with all endpoints
- tasks.service.ts with business logic
- task.entity.ts following User entity pattern
- DTOs for create/update operations
- Full test suite

Show plan first?"

You: Yes, show the API endpoints you'll create.

Cline: [Shows endpoint list matching CLINE_BRIEF.md]

You: Approved. Proceed.

[... implementation continues ...]
```

---

## Quick Reference Card

**Save this for easy access**:

```markdown
# Cline Quick Reference

## Starting New Phase
"Implement Phase [X] from docs/CLINE_BRIEF.md.
Show plan first, then implement after approval."

## Continuing Work
"Continue from .cline/progress.md.
Next task: [specific task]"

## Debugging
"Issue: [describe]
Expected: [X]
Actual: [Y]
Fix it."

## Reviewing Changes
"Show me what you changed in the last step"

## Confirming Understanding
"Summarize the architecture from docs/architecture.md"

## Resetting
"Revert the last change and try again following [spec]"

## Testing
"Run all tests and show results"

## Wrapping Up Phase
"Update progress.md with completed tasks"
```

---

## Summary

**Optimal Cline Setup**:
1. ✅ Claude Sonnet 4 or GPT-4o API
2. ✅ Custom instructions configured
3. ✅ Auto-approve disabled (manual review)
4. ✅ Project docs in standard locations
5. ✅ .cline/instructions.md for context
6. ✅ .cline/progress.md for state tracking

**Key Success Factors**:
- Detailed CLINE_BRIEF.md (from agent outputs)
- Phase-by-phase implementation
- Review and approve each phase
- Keep architecture docs updated
- Commit frequently

**Result**: Cline faithfully implements your well-architected system, saving you hours of coding while maintaining high quality! 🚀

---

**Next Steps**:
1. Install Cline in VS Code
2. Configure API with custom instructions
3. Try a small project (use blog platform example)
4. Refine your workflow
5. Scale to production projects

Happy autonomous coding!
