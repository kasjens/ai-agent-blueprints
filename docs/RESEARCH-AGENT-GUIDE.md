# Research Agent - Quick Reference Guide

## What This Agent Does

The Research Agent is a highly capable specialist that:
- **Conducts systematic research** using web search tools
- **Evaluates source credibility** and cross-references claims
- **Synthesizes findings** into structured, actionable insights
- **Provides proper citations** for all claims
- **Handles complex scenarios** like contradictory information or limited data

## Key Capabilities

✅ **Systematic Research Methodology** - 6-step process from understanding → searching → evaluating → synthesizing → presenting  
✅ **Source Credibility Assessment** - Prioritizes peer-reviewed, official, and authoritative sources  
✅ **Multi-Perspective Analysis** - Presents different viewpoints when they exist  
✅ **Proper Citations** - Every claim linked to source with URL  
✅ **Adaptive Depth** - Adjusts from quick (5-10 min) to comprehensive (30+ min) research  
✅ **Edge Case Handling** - Manages contradictions, limited info, and breaking news

## Quick Start

### 1. Copy the System Prompt

Open the blueprint file and copy everything in the **System Prompt** section (starts with "# Role and Objective").

### 2. Set Up in AnythingLLM

1. Create workspace named "Research Assistant"
2. Click gear icon → Chat Settings tab
3. Paste system prompt in the Prompt field
4. Replace template variables:
   - `{{CURRENT_DATE}}` → Current date
   - `{{TOOLS_LIST}}` → `web-search, web-browsing`
   - `{{USER_CONTEXT}}` → Your info
5. Enable **web-search** tool in workspace settings
6. Click "Update workspace"

### 3. Start Researching

```
You: Research the latest developments in quantum computing

Agent: [Conducts systematic research with 6-8 sources, provides structured report with citations]
```

## Sample Research Requests

### Quick Overview
```
"Give me a quick overview of Large Language Models"
→ 3-5 sources, key points, 5-10 minutes
```

### Standard Research
```
"Research the current state of electric vehicle adoption in Europe"
→ 5-7 sources, structured findings, 15-20 minutes
```

### Comprehensive Deep Dive
```
"Comprehensive research on AI agent frameworks: compare architectures, 
enterprise adoption, pros/cons, and recommendations"
→ 10+ sources, detailed analysis, 30+ minutes
```

### Specific Focus
```
"Research AI safety alignment - focus on technical approaches 
being developed in 2024-2025"
→ Targeted research on specific aspect
```

## What Makes This Agent Powerful

### 1. Systematic Search Strategy
Instead of one search, executes multiple targeted searches:
```
1. "quantum computing" (broad overview)
2. "quantum computing applications 2024" (current specific)
3. "quantum computing healthcare drug discovery" (niche application)
```

### 2. Source Evaluation
Automatically prioritizes:
- ✅ Peer-reviewed journals
- ✅ Official documentation
- ✅ Established news outlets
- ✅ Expert opinions with credentials
- ⚠️ Blogs (verifies claims)
- ❌ Content farms, biased sources

### 3. Handling Contradictions
When sources disagree (e.g., "Is X good or bad?"):
- Presents both perspectives
- Explains areas of agreement vs. debate
- Cites quality of evidence for each side
- Provides nuanced conclusion

### 4. Proper Citations
Every factual claim includes:
- Source name
- Clickable URL
- Publication date
- Author/organization (when relevant)

Example:
> "CrewAI has 30,500+ GitHub stars and 1M+ monthly downloads [CrewAI Documentation](https://docs.crewai.com/)"

## Output Formats

### Standard Research Report
```markdown
# Research: [Topic]

## Executive Summary
[2-3 sentence overview]

## Background & Context
[Why this matters]

## Key Findings
### [Theme 1]
- Finding with [Source](URL)

### [Theme 2]  
- Finding with [Source](URL)

## Analysis & Insights
[Patterns, trends, implications]

## Recommendations
[Actionable next steps]

## Sources
[Full list with URLs and dates]
```

### Quick Summary (for simple queries)
```markdown
**Quick Research Summary**: [Topic]

**Key Findings**:
- Finding 1 ([Source](URL))
- Finding 2 ([Source](URL))

**Bottom Line**: [Key insight]
```

## Configuration Options

Customize behavior by modifying these in the system prompt:

```yaml
# Research depth
default_depth: standard  # quick | standard | comprehensive

# Source requirements  
minimum_sources: 5       # Minimum sources to consult
prefer_recent: true      # Prioritize recent sources

# Citation style
citation_format: inline  # How to present citations

# Tone
formality: professional  # casual | professional | academic
```

## Advanced Usage

### Multi-Part Research
```
You: Research quantum computing (Part 1: technical overview)

[Agent provides overview]

You: Now focus on practical applications in drug discovery (Part 2)

[Agent provides targeted deep dive]
```

### Iterative Refinement
```
You: Research AI frameworks

[Agent provides report]

You: Great! Now compare just CrewAI and LangGraph in detail

[Agent provides focused comparison]
```

### Contradictory Info Investigation
```
You: I'm seeing conflicting information about whether coffee 
is healthy. Can you research both perspectives?

[Agent presents balanced analysis of both sides with evidence]
```

## Common Use Cases

### 📊 Market Research
```
"Research the competitive landscape for [product category]"
→ Competitors, market size, trends, opportunities
```

### 🔬 Technical Investigation
```
"Research the technical architecture of [technology]"
→ How it works, alternatives, trade-offs, use cases
```

### 📈 Trend Analysis
```
"What are the emerging trends in [industry] for 2025?"
→ Trends with evidence, expert opinions, forecasts
```

### 🏢 Company/Product Research
```
"Research [Company Name]: funding, products, market position"
→ Comprehensive company profile with citations
```

### 📚 Academic Research
```
"Research recent academic papers on [topic]"
→ Summary of recent research, key findings, consensus
```

### ⚖️ Policy/Regulatory Research
```
"Research current regulations on [topic] in [region]"
→ Current policies, recent changes, expert analysis
```

## Tips for Best Results

### ✅ Do This
- **Be specific**: "AI agent frameworks" > "AI"
- **Specify depth**: Tell the agent if you need quick vs. comprehensive
- **Provide context**: "I'm evaluating tools for my startup" helps tailor focus
- **Ask follow-ups**: "Can you dive deeper into X?" or "Compare Y and Z"

### ❌ Avoid This
- **Too vague**: "Tell me about technology"
- **Asking without search**: Agent needs web-search tool enabled
- **Expecting instant**: Comprehensive research takes time
- **One source is enough**: Agent always uses multiple sources

## Troubleshooting

### Problem: Agent isn't searching the web

**Solution**: 
- Ensure `web-search` tool is enabled in workspace
- Verify Mistral API or LLM is configured
- Check the system prompt includes tool instructions

### Problem: Research seems shallow

**Solution**:
- Explicitly request comprehensive depth: "Do comprehensive research on..."
- Ask for more sources: "Can you consult additional sources?"
- Request specific angles: "Also research the criticism and limitations"

### Problem: Too many citations, hard to read

**Solution**:
- Request summary first: "Give me a quick summary with top 3-5 findings"
- Ask for executive summary only: "Just the executive summary please"

### Problem: Information seems outdated

**Solution**:
- Specify recency: "Research developments in 2024-2025"
- Ask for latest: "What are the most recent updates?"
- Agent automatically includes publication dates in citations

## Integration with Other Agents

### Research → Analysis → Report Pipeline

1. **Research Agent**: Gathers information
   ```
   Research: quantum computing applications
   → Produces comprehensive research report
   ```

2. **Analysis Agent**: Analyzes findings
   ```
   Analyze these findings for business opportunities
   → Produces strategic analysis
   ```

3. **Writer Agent**: Creates deliverable
   ```
   Create executive presentation from this analysis
   → Produces final report/presentation
   ```

See the **research-pipeline.md** example in the anythingllm-agent-setup repository.

## Example Research Session

```
You: I need to research AI coding assistants for our development team. 
We're deciding between GitHub Copilot, Cursor, and Cody.

Agent: I'll conduct comprehensive research on AI coding assistants, 
focusing on GitHub Copilot, Cursor, and Cody for team evaluation.

[Executes 8-10 targeted searches]
[Consults official docs, reviews, comparisons, pricing]
[Cross-references claims across sources]
[Evaluates for enterprise use cases]

# Research: AI Coding Assistants Comparison

## Executive Summary

GitHub Copilot leads in market share and IDE integration; Cursor offers 
the most advanced multi-file editing; Cody excels at codebase understanding. 
Choice depends on: team IDE preference (VS Code vs. dedicated), whether 
multi-file edits are priority, and budget considerations.

[... detailed comparison with 15+ citations ...]

## Recommendations for Your Team

Based on development team context:

1. **Try Cursor** if: Team values cutting-edge features, comfortable 
   switching IDEs, needs advanced multi-file refactoring
   
2. **Choose Copilot** if: Team heavily invested in VS Code/JetBrains, 
   wants most mature/stable option, GitHub Enterprise customers
   
3. **Consider Cody** if: Need strong codebase context understanding, 
   want flexible LLM provider, budget is constrained

## Sources
[15 sources with URLs, dates, and context]

---

You: Thanks! Can you now focus specifically on pricing for a team of 20 developers?

Agent: I'll research detailed pricing for all three options for a 20-person team.

[Executes targeted pricing searches]
[Calculates comparative costs]
[Notes any volume discounts or enterprise offerings]

**Pricing Comparison - 20 Developers**

[Detailed pricing breakdown with sources]
```

## Next Steps

1. **Try it**: Set up the research agent in AnythingLLM
2. **Test it**: Run 3-5 research queries on different topics
3. **Customize**: Adjust depth, formality, or focus for your needs
4. **Integrate**: Combine with analysis and writing agents for full workflows
5. **Share feedback**: Let us know what works and what could be better

---

**Questions?** Check the full blueprint for detailed methodology and 5 complete examples.

**Need help?** See the agent-integration.md guide in anythingllm-agent-setup repository.
