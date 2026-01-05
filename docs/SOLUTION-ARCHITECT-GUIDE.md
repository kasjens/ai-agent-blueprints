# Solution Architect Agent - Quick Reference Guide

## What This Agent Does

The Solution Architect Agent is an expert system architect that:
- **Analyzes requirements** and asks clarifying questions
- **Researches technologies** and evaluates options
- **Designs comprehensive architectures** with diagrams and documentation
- **Balances trade-offs** between technical excellence and business pragmatism
- **Considers all aspects**: scalability, security, cost, maintainability, team skills
- **Provides implementation roadmaps** with phases and milestones

## Key Capabilities

✅ **Systematic Architecture Methodology** - Discovery → Research → Design → Document → Risk Assessment  
✅ **Technology Evaluation** - Researches current options, compares alternatives, documents trade-offs  
✅ **Comprehensive Documentation** - Architecture diagrams, decision records, cost analysis, implementation roadmap  
✅ **Multi-Domain Expertise** - Cloud, microservices, databases, security, integration, scalability  
✅ **Cost-Conscious Design** - Balances features with budget constraints  
✅ **Risk Management** - Identifies risks, provides mitigation strategies

## Quick Start

### 1. Copy the System Prompt

Open the blueprint file and copy everything in the **System Prompt** section (starts with "# Role and Objective").

### 2. Set Up in AnythingLLM

1. Create workspace named "Solution Architect"
2. Click gear icon → Chat Settings tab
3. Paste system prompt in the Prompt field
4. Replace template variables:
   - `{{CURRENT_DATE}}` → Current date
   - `{{TOOLS_LIST}}` → `web-search, code-execution, file-creation`
   - `{{USER_CONTEXT}}` → Your company/project context
5. Enable **web-search** tool (for technology research)
6. Click "Update workspace"

### 3. Start Architecture Design

```
You: Design a microservices architecture for an e-commerce platform. 
Expected 50K daily active users, must integrate with existing inventory 
system, budget is $200K for initial build.

Agent: [Asks clarifying questions, then designs comprehensive architecture 
with diagrams, technology choices, cost analysis, implementation roadmap]
```

## Sample Architecture Requests

### New System Design
```
"Design a SaaS platform architecture for team collaboration. 
Target 10K users at launch, real-time features needed, 6-month timeline."
→ Complete architecture with tech stack, diagrams, cost analysis
```

### Legacy Modernization
```
"We have a 15-year-old PHP monolith. How should we modernize it? 
10K orders/day, 4 developers, can't do big-bang rewrite."
→ Phased modernization strategy with Strangler Fig pattern
```

### Integration Architecture
```
"Design integration layer for 5 third-party services: Salesforce, 
Stripe, SendGrid, Slack, Intercom"
→ Integration patterns, adapter design, error handling
```

### Cost-Constrained Design
```
"Design a SaaS platform with only $2K/month infrastructure budget"
→ Serverless-first architecture with cost optimization strategies
```

### Technology Evaluation
```
"Should we use PostgreSQL or MongoDB for our application? 
We need to store user profiles, orders, and product catalog."
→ Detailed comparison with recommendations based on your use case
```

## What Makes This Agent Powerful

### 1. Asks the Right Questions

**Before designing, clarifies**:
- Functional requirements (features, workflows)
- Non-functional requirements (performance, scale, security)
- Constraints (budget, timeline, team skills)
- Integration needs
- Compliance requirements

### 2. Research-Backed Technology Choices

**For each major decision**:
- Researches 2-3 current options
- Compares features, maturity, cost
- Documents trade-offs explicitly
- Provides rationale with evidence

Example:
> **PostgreSQL vs MongoDB**
> - ✅ PostgreSQL: ACID transactions, team expertise
> - ❌ PostgreSQL: Less flexible schema evolution
> - Chosen: PostgreSQL for order/payment consistency requirements

### 3. Comprehensive Documentation

**Every architecture includes**:
- High-level architecture diagram
- Component descriptions with technology choices
- Data architecture and flow
- Security architecture
- Scalability strategy
- Cost breakdown
- Risk assessment
- Implementation roadmap

### 4. Practical Trade-offs

**Balances**:
- Technical excellence vs. time-to-market
- Scalability vs. cost
- Flexibility vs. simplicity
- Innovation vs. proven tech
- Perfect vs. good enough

## Output Formats

### Complete Architecture Document

```markdown
# Solution Architecture: [Project Name]

## Executive Summary
[2-3 paragraph overview]

## 1. Requirements Overview
- Functional requirements
- Non-functional requirements (performance, scale, security)
- Constraints

## 2. High-Level Architecture
[Mermaid diagram showing system components]

## 3. Component Architecture
[Detailed description of each component]

## 4. Technology Stack
[Chosen technologies with rationale and trade-offs]

## 5. Data Architecture
[Database schema, caching strategy, backup/recovery]

## 6. Security Architecture
[Authentication, authorization, network security, compliance]

## 7. Scalability & Performance
[Scaling strategy, performance targets, optimizations]

## 8. Cost Analysis
[Monthly operating costs, build costs, optimization strategies]

## 9. Risk Assessment
[Technical and organizational risks with mitigation]

## 10. Implementation Roadmap
[Phased approach with milestones]
```

### Technology Evaluation

```markdown
# Technology Evaluation: [Category]

## Requirements
[What this technology must satisfy]

## Options Evaluated

### Option 1: [Technology A]
**Pros**: ...
**Cons**: ...
**Cost**: ...
**Fit Score**: X/10

### Option 2: [Technology B]
[Same structure]

## Recommendation
**Selected**: [Technology]
**Rationale**: [Why, with trade-offs]
```

### Quick Architecture Review

```markdown
# Architecture Review: [Component]

## Current Architecture
[Brief description]

## Assessment
**Strengths**: ...
**Concerns**: ...

## Recommendations
1. [Priority recommendation with rationale]
2. [Next priority]
```

## Architecture Principles

The agent follows these principles:

### 1. Scalability First
- Design for 10x current load
- Prefer horizontal scaling
- Implement caching strategically

### 2. Security by Design
- Defense in depth
- Least privilege access
- Encryption everywhere

### 3. Operational Excellence
- Observability from day one
- Automate everything
- Design for failure

### 4. Cost Optimization
- Right-size resources
- Use auto-scaling
- Monitor and optimize

### 5. Maintainability
- Keep it simple (KISS)
- Use proven patterns
- Document thoroughly

### 6. Pragmatic Trade-offs
- Perfect is the enemy of good
- Balance technical excellence with business needs
- Validate assumptions with PoCs

## Common Use Cases

### 🏗️ New System Design
```
"Design a [type] system for [purpose]"
→ Complete architecture from scratch
```

### 🔄 Legacy Modernization
```
"Modernize our [old system] - it's [pain points]"
→ Phased modernization strategy
```

### ☁️ Cloud Migration
```
"Plan migration from on-premises to AWS"
→ Migration strategy with phases and risks
```

### 🔌 Integration Design
```
"Integrate with [3rd party systems]"
→ Integration patterns and best practices
```

### 🔒 Security Architecture
```
"Design security architecture for [compliance]"
→ Comprehensive security controls
```

### 📈 Scalability Planning
```
"Current system can't handle growth - how to scale?"
→ Scalability strategy and optimizations
```

### 💰 Cost Optimization
```
"Our AWS bill is too high - how to optimize?"
→ Cost analysis and optimization recommendations
```

## Tips for Best Results

### ✅ Do This

**Provide Context**:
```
GOOD: "E-commerce platform, 50K users, $200K budget, 6-month timeline, 
team of 8 developers with Node.js experience"

BAD: "Design an e-commerce site"
```

**Be Honest About Constraints**:
- Real budget (not aspirational)
- Actual timeline (not hoped-for)
- True team skills (not planned training)

**Ask for Clarification**:
```
"What did you mean by 'highly available'? 99.9% or 99.99%?"
"When you say 'fast', what's the target response time?"
```

**Iterate and Refine**:
```
"Great architecture! Can you adjust for a smaller budget?"
"What if we drop real-time features for MVP?"
```

### ❌ Avoid This

**Too Vague**:
```
"Design something scalable and secure"
→ Everything is scalable and secure at different levels
```

**Hiding Constraints**:
```
"Design the perfect system" (but actually have $5K budget)
→ Agent will design expensive architecture
```

**Premature Optimization**:
```
"Design for 1 billion users" (when you have 0)
→ Over-engineered, expensive, complex
```

## Configuration Options

Customize behavior in system prompt:

```yaml
# Architecture style preference
default_style: microservices  # or monolith, serverless, hybrid

# Cloud provider
preferred_cloud: aws  # or azure, gcp, multi-cloud

# Cost sensitivity
cost_optimization: balanced  # aggressive, balanced, premium

# Technology stance
technology_stance: proven  # bleeding-edge, modern, proven, conservative

# Documentation level
documentation_level: comprehensive  # minimal, standard, comprehensive
```

## Integration with Other Agents

### Research → Architect → Implement Pipeline

```
1. Research Agent: "Research latest microservices frameworks"
   → Gathers information on options

2. Solution Architect Agent: "Design microservices architecture 
   using research findings"
   → Creates comprehensive architecture

3. (Developer): Implements based on architecture docs
```

### Architecture Review Workflow

```
1. Solution Architect Agent: Creates initial architecture
2. (Team Review): Provides feedback and constraints
3. Solution Architect Agent: "Refine architecture based on 
   feedback: [specific points]"
4. Final architecture ready for implementation
```

## Example Architecture Session

```
You: We need to design a real-time collaboration platform like Notion. 
Expected 5K users at launch, must support real-time editing, 
budget is $100K build + $5K/month operating.

Agent: I'll design a real-time collaboration architecture. First, let me 
clarify critical requirements:

**Questions**:
1. **Real-time Latency**: What's acceptable latency for seeing other users' 
   edits? <100ms, <500ms, or <1s?
2. **Concurrent Editors**: How many users editing same document simultaneously?
3. **Document Size**: Expected document size? (text-only, images, files?)
4. **Offline Support**: Must work offline with sync when reconnected?
5. **Data Residency**: Any geographic requirements for data storage?

You: <100ms latency critical, max 10 concurrent editors per document, 
text+images up to 10MB, offline nice-to-have but not required, US-only.

Agent: Perfect. I'll now design the architecture. Let me research current 
real-time collaboration patterns and technologies.

[Executes web searches]:
- "real-time collaboration architecture 2024"
- "operational transformation vs CRDT"
- "WebSocket scaling best practices"
- "Yjs collaborative editing"
- "Socket.io vs Pusher comparison"

# Solution Architecture: Real-Time Collaboration Platform

**Date**: January 5, 2025

## Executive Summary

This architecture delivers <100ms real-time collaboration using WebSockets, 
CRDTs (Yjs library) for conflict-free editing, and a serverless-first 
approach to minimize operating costs ($4.2K/month at 5K users).

Key decisions: Node.js + Socket.io for WebSocket layer, Yjs for CRDT, 
PostgreSQL + Redis for data persistence, AWS Lambda + ECS for compute.

[... complete 50+ page architecture document with diagrams, technology 
choices, cost analysis, security architecture, implementation roadmap ...]

---

You: Excellent! But can you adjust for a tighter budget - $3K/month operating?

Agent: Absolutely. Let me optimize for cost while maintaining real-time 
performance requirements.

**Cost Reduction Strategies**:

1. **Serverless WebSockets** (was: dedicated ECS)
   - Use AWS API Gateway WebSocket API
   - Savings: $800/month

2. **On-Demand Database** (was: provisioned)
   - DynamoDB on-demand instead of RDS
   - Savings: $400/month

3. **Aggressive Caching** (new)
   - Add CloudFront for document assets
   - Reduces compute and data transfer
   - Savings: $300/month

**Revised Monthly Cost**: $2,700 (vs original $4,200)

**Trade-offs**:
- ❌ Slightly higher latency on cold starts (WebSocket Lambda)
- ❌ Less query flexibility (DynamoDB vs PostgreSQL)
- ✅ Scales better with traffic (pay-per-use model)
- ✅ Lower operational complexity (fewer servers)

[... updated architecture reflecting cost optimizations ...]
```

## Troubleshooting

### Problem: Architecture seems over-engineered

**Solutions**:
- Specify: "Keep it simple for our current scale"
- Clarify: "We have 100 users, not 100K"
- Ask: "What's the minimal viable architecture?"

### Problem: Not enough detail

**Solutions**:
- Request: "Can you provide more detail on [component]?"
- Specify: "Include detailed data models"
- Ask: "What about [specific aspect]?"

### Problem: Technology choices don't match team skills

**Solutions**:
- Provide team context upfront: "Team knows Python and React"
- Request: "Adjust technology choices for a Python team"
- Ask: "What's the learning curve for [technology]?"

### Problem: Cost estimates seem unrealistic

**Solutions**:
- Clarify scale: "What assumptions are these costs based on?"
- Request: "Provide cost breakdown by component"
- Validate: "Can you research actual pricing for [service]?"

## Advanced Usage

### Multi-Stage Architecture

```
You: Design MVP architecture first, then show evolution path

Agent: [Provides Phase 1 simple architecture]
Agent: [Then shows Phase 2, 3 evolution as system grows]
```

### Architecture Comparison

```
You: Compare monolith vs microservices for our use case

Agent: [Provides side-by-side comparison with recommendations]
```

### Technology Deep Dive

```
You: You recommended PostgreSQL - can you provide detailed rationale?

Agent: [Researches and provides comprehensive analysis]
```

## Next Steps

1. **Set up the agent**: Follow Quick Start above
2. **Test with sample**: Try a simple architecture request
3. **Real project**: Use for actual architecture needs
4. **Iterate**: Refine based on team feedback
5. **Implement**: Use documentation to guide development

---

**Complete blueprint**: See `solution-architect-agent.md` for full system prompt and examples

**Integration guide**: See `agent-integration.md` in anythingllm-agent-setup repo

**Questions?** The agent works best with specific, detailed requirements!
