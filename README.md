# LLM Templates - Quick Start Guide

<https://github.com/doitian/llm-templates>

## Installation

```bash
# Install LLM tool
pip install llm

# Set up your API key (for OpenAI)
llm keys set openai
```

## Template Installation

1. **Find your templates directory:**
   ```bash
   llm templates path
   ```

2. **Copy the YAML files to that directory**

3. **Verify installation:**
   ```bash
   llm templates
   ```

Or use [llm-templates-github](https://github.com/simonw/llm-templates-github).

## Common Usage Patterns

### 1. Text Summarization
```bash
# Basic summary
cat article.txt | llm -t summary

# Bullet-point summary
echo "Long text here..." | llm -t bullet-summary

# Title generation
cat document.txt | llm -t summarize-title
```

### 2. Text Editing & Improvement
```bash
# General polish
echo "Rough draft text" | llm -t polish

# Polish for specific audience
echo "Technical content" | llm -t polish-for -p audience "middle school students"

# Chinese editing
echo "中文文本" | llm -t polish-chinese
```

### 3. Development Tasks
```bash
# Git commit messages
git diff | llm -t git-commit

# Code explanation
cat script.py | llm -t explain-code

# Release notes
cat CHANGELOG.md | llm -t release-notes -p project "MyApp"
```

### 4. Academic Writing
```bash
# Generate essay topics
llm -t essay-topics -p input "climate change"

# Create essay outline
llm -t essay-outline -p topic "AI in Education" -p genre "research paper"

# Write full essay
echo "Outline: 1. Introduction 2. Main points..." | llm -t essay-writing -p audience "academic"

# Generate citations
llm -t essay-citation-sources -p input "machine learning ethics"
```

### 5. Translation
```bash
# To English
echo "Bonjour le monde" | llm -t translate-to-english

# To Chinese
echo "Hello world" | llm -t translate-to-chinese
```

### 6. Utility Tasks
```bash
# Generate conversation starters
llm -t conversation-starter

# Create mindmap
llm -t mindmap -p input "Project Management"

# Generate tags
cat blog-post.md | llm -t tag

# Build vocabulary
echo "serendipity, ephemeral, ubiquitous" | llm -t vocabulary-builder
```

## Advanced Usage

### Chaining Templates
```bash
# Summarize then create bullet points
curl -s "https://example.com/article" | \
  llm -t summary | \
  llm -t bullet-summary
```

### Using Different Models
```bash
# Use GPT-4 for complex tasks
cat research-paper.pdf | llm -t academic-research -m gpt-4

# Use faster model for simple tasks
echo "Quick text" | llm -t summary -m gpt-3.5-turbo
```

### Processing Files
```bash
# Process multiple files
for file in *.txt; do
  echo "=== $file ===" 
  cat "$file" | llm -t summary
done
```

### Custom Variables
```bash
# Essay writing with custom parameters
llm -t essay-writing -p audience "high school students" -p input "Topic: Solar Energy
Outline:
1. What is solar energy
2. Benefits and drawbacks
3. Future prospects"
```

## Template Customization

### Editing Templates
```bash
# Edit existing template
llm templates edit summary

# Or edit directly
nano ~/.local/share/llm/templates/summary.yaml
```

### Adding New Variables
```yaml
# Example: Add a tone variable to polish template
system: You are an expert editor focused on clarity, coherence, and conciseness.
prompt: |
  Edit the following text with a $tone tone while preserving its original meaning.
  
  Text: """
  $input
  """
defaults:
  tone: professional
```

## Troubleshooting

### Common Issues

1. **Template not found**
   ```bash
   # Check template directory
   llm templates path
   # List available templates
   llm templates
   ```

2. **Variable errors**
   ```bash
   # Provide all required variables
   llm -t polish-for -p audience "students" -p input "text here"
   ```

3. **API key issues**
   ```bash
   # Set API key
   llm keys set openai
   # Test with simple prompt
   echo "test" | llm "summarize this"
   ```

## Best Practices

1. **Start Simple**: Begin with basic templates like `summary` or `polish`

2. **Use Pipes**: Combine with other command-line tools:
   ```bash
   curl -s "url" | html2text | llm -t summary
   ```

3. **Save Outputs**: Redirect results to files:
   ```bash
   cat document.txt | llm -t bullet-summary > summary.md
   ```

4. **Test Variables**: Check what variables a template uses:
   ```bash
   cat ~/.local/share/llm/templates/polish-for.yaml
   ```

5. **Model Selection**: Use appropriate models for task complexity:
   - Simple tasks: `gpt-3.5-turbo`
   - Complex analysis: `gpt-4`
   - Code tasks: `claude-3-sonnet`

## Integration Examples

### With Git Workflow
```bash
# Add to git alias
git config --global alias.auto-commit '!git add -A && git diff --cached | llm -t git-commit | git commit -F -'
```

### With Text Processing Pipeline
```bash
#!/bin/bash
# process-article.sh
curl -s "$1" | \
  html2text | \
  llm -t summary | \
  llm -t bullet-summary | \
  llm -t tag > processed-article.md
```

### With Academic Workflow
```bash
# research-helper.sh
echo "$1" | llm -t essay-citation-sources > sources.md
echo "$1" | llm -t essay-outline > outline.md
echo "$1" | llm -t essay-topics > topics.md
```

---

*Ready to start using your converted LLM templates! 🚀*