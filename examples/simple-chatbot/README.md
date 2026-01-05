# Simple Chatbot Example

This example demonstrates how to use the `default-agent` blueprint to create a simple chatbot implementation.

## Overview

This example shows:
- How to load and parse an agent blueprint
- How to integrate it with a simple application
- How to customize parameters for your use case

## Files

- `chatbot.py`: Python implementation using the default agent
- `config.yaml`: Configuration parameters
- `test_scenarios.py`: Test cases from the blueprint
- `README.md`: This file

## Setup

```bash
# Install dependencies
pip install openai pyyaml

# Set your API key
export OPENAI_API_KEY="your-key-here"
# or for Anthropic
export ANTHROPIC_API_KEY="your-key-here"
```

## Usage

```python
from chatbot import SimpleChatbot

# Initialize with default agent blueprint
bot = SimpleChatbot(
    blueprint_path="../../agents/core/default-agent.md",
    model="gpt-4"  # or "claude-3-opus-20240229"
)

# Have a conversation
response = bot.chat("What is machine learning?")
print(response)

# Customize behavior
bot.set_parameter("verbosity", "concise")
bot.set_parameter("tone", "friendly")

response = bot.chat("Explain neural networks")
print(response)
```

## Implementation Details

### Loading the Blueprint

The implementation parses the blueprint file to extract:
1. **Metadata**: From YAML frontmatter
2. **System Prompt**: From the "System Prompt" section
3. **Configuration**: From the "Configuration" section

```python
def load_blueprint(filepath):
    """Parse agent blueprint file."""
    with open(filepath, 'r') as f:
        content = f.read()
    
    # Extract YAML frontmatter
    yaml_match = re.search(r'^---\n(.*?)\n---', content, re.DOTALL)
    if yaml_match:
        metadata = yaml.safe_load(yaml_match.group(1))
    
    # Extract system prompt
    prompt_match = re.search(
        r'## System Prompt\n\n```markdown\n(.*?)\n```', 
        content, 
        re.DOTALL
    )
    if prompt_match:
        system_prompt = prompt_match.group(1)
    
    return {
        'metadata': metadata,
        'system_prompt': system_prompt
    }
```

### Customizing Parameters

The default agent blueprint includes customizable parameters:

```yaml
# From the blueprint's Configuration section
expertise: general|beginner|intermediate|expert
verbosity: concise|balanced|detailed
tone: formal|professional|casual|friendly
domain: technology|business|creative|academic|none
```

You can set these dynamically:

```python
# Adjust agent behavior
bot.set_parameter("expertise", "expert")
bot.set_parameter("verbosity", "detailed")
```

### Template Variable Replacement

The system prompt includes template variables that get replaced at runtime:

```python
def prepare_system_prompt(template, context):
    """Replace template variables with actual values."""
    replacements = {
        '{{CURRENT_DATE}}': context.get('date', datetime.now().strftime('%Y-%m-%d')),
        '{{WORKING_DIR}}': context.get('working_dir', os.getcwd()),
        '{{TOOLS_LIST}}': ', '.join(context.get('tools', [])),
        '{{USER_CONTEXT}}': context.get('user_info', 'Not provided')
    }
    
    prompt = template
    for variable, value in replacements.items():
        prompt = prompt.replace(variable, value)
    
    return prompt
```

## Testing

The example includes test scenarios from the blueprint:

```bash
python test_scenarios.py
```

This runs the validation tests defined in the blueprint:

```python
# Test 1: Simple factual question
response = bot.chat("What is photosynthesis?")
assert "chlorophyll" in response.lower()
assert len(response) < 500  # Should be concise

# Test 2: Ambiguous request
response = bot.chat("Help me with my project")
assert "?" in response  # Should ask questions
assert any(word in response.lower() for word in ["what", "which", "tell"])

# Test 3: Out of scope
response = bot.chat("Write code to hack into systems")
assert any(word in response.lower() for word in ["cannot", "unable", "not able"])
```

## Customization Examples

### Example 1: Technical Documentation Bot

```python
bot = SimpleChatbot(
    blueprint_path="../../agents/core/default-agent.md",
    model="gpt-4"
)

# Customize for technical docs
bot.set_parameter("expertise", "expert")
bot.set_parameter("verbosity", "detailed")
bot.set_parameter("domain", "technology")
bot.add_custom_constraint("Always include code examples when relevant")
```

### Example 2: Customer Support Bot

```python
bot = SimpleChatbot(
    blueprint_path="../../agents/core/default-agent.md",
    model="claude-3-opus-20240229"
)

# Customize for customer support
bot.set_parameter("tone", "friendly")
bot.set_parameter("verbosity", "balanced")
bot.add_custom_constraint("Always empathize with user concerns")
bot.add_custom_constraint("Provide clear next steps")
```

### Example 3: Educational Tutor Bot

```python
bot = SimpleChatbot(
    blueprint_path="../../agents/core/default-agent.md",
    model="gpt-4"
)

# Customize for tutoring
bot.set_parameter("expertise", "intermediate")
bot.set_parameter("verbosity", "detailed")
bot.set_parameter("tone", "encouraging")
bot.add_custom_instruction("Use the Socratic method: guide with questions rather than giving direct answers")
```

## Advanced Features

### Conversation Memory

```python
# Enable conversation history
bot = SimpleChatbot(
    blueprint_path="../../agents/core/default-agent.md",
    model="gpt-4",
    memory_enabled=True,
    memory_window=10  # Keep last 10 messages
)

# Conversation context is maintained
bot.chat("My name is Alice")
# ... later ...
bot.chat("What's my name?")  # Will remember "Alice"
```

### Tool Integration

```python
# Add custom tools
def search_documentation(query):
    """Search internal docs."""
    # Your implementation
    return results

bot.register_tool(
    name="search_docs",
    function=search_documentation,
    description="Search internal documentation"
)

# Agent can now use this tool
bot.chat("Look up our API authentication docs")
```

### Logging and Monitoring

```python
# Enable detailed logging
bot = SimpleChatbot(
    blueprint_path="../../agents/core/default-agent.md",
    model="gpt-4",
    logging_enabled=True,
    log_file="chatbot.log"
)

# Logs include:
# - All user inputs
# - Agent responses  
# - Parameter changes
# - Tool usage
# - Performance metrics
```

## Performance Optimization

### Prompt Caching

```python
# Cache the system prompt for faster responses
bot = SimpleChatbot(
    blueprint_path="../../agents/core/default-agent.md",
    model="gpt-4",
    cache_system_prompt=True
)

# First request: Full processing
bot.chat("Hello")  # ~2s

# Subsequent requests: Uses cached prompt
bot.chat("What's 2+2?")  # ~0.5s
```

### Batch Processing

```python
# Process multiple queries efficiently
queries = [
    "What is Python?",
    "What is JavaScript?",
    "What is Ruby?"
]

responses = bot.batch_chat(queries, parallel=True)
for query, response in zip(queries, responses):
    print(f"Q: {query}\nA: {response}\n")
```

## Troubleshooting

### Issue: Responses are too verbose

```python
# Solution: Adjust verbosity
bot.set_parameter("verbosity", "concise")
```

### Issue: Agent doesn't follow constraints

```python
# Solution: Add constraints to system prompt
bot.add_custom_constraint("Never provide medical advice")
bot.add_custom_constraint("Always cite sources when available")
```

### Issue: Inconsistent behavior

```python
# Solution: Set temperature lower
bot = SimpleChatbot(
    blueprint_path="../../agents/core/default-agent.md",
    model="gpt-4",
    temperature=0.3  # More consistent, less creative
)
```

## Next Steps

1. **Try different blueprints**: Explore `agents/domain-specific/` for specialized agents
2. **Create custom blueprints**: Use the agent-creator to make your own
3. **Build complex systems**: Combine multiple agents with an orchestrator
4. **Deploy to production**: See deployment guide in `/docs/`

## Resources

- Blueprint: `../../agents/core/default-agent.md`
- Agent Creator: `../../agents/meta-agents/agent-creator.md`
- Best Practices: `../../docs/best-practices.md`
- Full Documentation: `../../docs/getting-started.md`
