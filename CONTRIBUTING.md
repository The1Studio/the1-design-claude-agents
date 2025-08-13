# Contributing to The1 Design Claude Agents

Thank you for your interest in contributing to The1 Design Claude Agents! This document provides guidelines and instructions for contributing to our collection of specialized Claude sub-agents focused on design and visual analysis.

## 🎯 Our Mission

We aim to build the most comprehensive, high-quality collection of Claude sub-agents that enhance design analysis, visual processing, and creative workflows. Every contribution helps make Claude Code more powerful for designers and developers working with visual content.

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How to Contribute](#how-to-contribute)
- [Creating New Agents](#creating-new-agents)
- [Improving Existing Agents](#improving-existing-agents)
- [Reporting Issues](#reporting-issues)
- [Pull Request Process](#pull-request-process)
- [Agent Quality Standards](#agent-quality-standards)
- [Testing Guidelines](#testing-guidelines)

## 📜 Code of Conduct

We are committed to providing a welcoming and inclusive environment. Please:

- Be respectful and constructive in all interactions
- Welcome newcomers and help them get started
- Focus on what is best for the community
- Show empathy towards other community members

## 🤝 How to Contribute

### 1. Fork and Clone

```bash
# Fork the repository on GitHub, then:
git clone https://github.com/YOUR_USERNAME/the1-design-claude-agents.git
cd the1-design-claude-agents
git remote add upstream https://github.com/the1studio/the1-design-claude-agents.git
```

### 2. Create a Branch

```bash
git checkout -b feature/agent-name
# or
git checkout -b fix/issue-description
```

### 3. Make Your Changes

Follow our guidelines below for creating or improving agents.

### 4. Test Your Changes

Ensure your agent works correctly with Claude Code before submitting.

### 5. Commit Your Changes

```bash
git add .
git commit -m "feat: add [agent-name] for [purpose]"
# or
git commit -m "fix: improve [agent-name] [what was fixed]"
```

Follow [Conventional Commits](https://www.conventionalcommits.org/) format.

### 6. Push and Create PR

```bash
git push origin feature/agent-name
```

Then create a Pull Request on GitHub.

## 🆕 Creating New Agents

### Agent File Structure

Place your agent in the appropriate category:
```
agents/
├── core/
│   ├── visual-analysis/
│   ├── pattern-detection/
│   └── ...
├── orchestrators/
├── python/
├── specialized/
│   ├── defense/
│   ├── puzzle/
│   └── ...
└── universal/
```

### Agent Format

```yaml
---
name: your-agent-name
description: Clear description of when this agent should be used (be specific for better auto-detection)
tools: Tool1, Tool2, Tool3  # Optional - omit to inherit all tools
---

# Agent Name - Specialist in [Domain]

You are an expert [role] specializing in [specific area]. Your primary responsibilities include:

## Core Expertise
- [Visual analysis expertise]
- [Design pattern recognition]
- [Creative workflow optimization]

## Working Principles
1. [Design-focused principle 1]
2. [Visual analysis principle 2]
3. [User experience principle 3]

## Task Approach
When given a task, you:
1. [Analyze visual/design requirements]
2. [Apply design principles]
3. [Provide actionable insights]

## Best Practices
- [Design best practice 1]
- [Visual analysis best practice 2]
- [Creative workflow best practice 3]

## Common Patterns
[Include design-specific patterns, frameworks, or methodologies]

## Quality Standards
[Define what constitutes quality work in this design domain]
```

### Agent Naming Convention

- Use lowercase with hyphens: `visual-style-matcher`
- Be specific: `level-difficulty-visualizer` not just `game-analyzer`
- Include the domain: `pattern-learning-agent`, `screenshot-analyzer`

### Required Documentation

For each new agent, create:

1. **Agent file**: `agents/category/subcategory/agent-name.md`
2. **Example usage**: `examples/agent-name-example.md`
3. **Update README**: Add your agent to the appropriate section

## 🔧 Improving Existing Agents

### Enhancement Guidelines

- Test extensively before modifying core behavior
- Maintain backward compatibility
- Document what was changed and why
- Update examples if behavior changes

### Common Improvements

- Adding new visual analysis capabilities
- Enhancing design pattern recognition
- Improving task detection for design workflows
- Adding error handling for image processing
- Updating for new design tools and frameworks

## 🐛 Reporting Issues

### Before Reporting

1. Check existing issues to avoid duplicates
2. Test with the latest version of Claude Code
3. Verify the issue is with the agent, not Claude Code itself

### Issue Template

```markdown
**Agent Name**: [agent-name]
**Issue Type**: Bug / Enhancement / Feature Request
**Claude Code Version**: [version]

**Description**:
[Clear description of the issue]

**Steps to Reproduce**:
1. [Step 1]
2. [Step 2]

**Expected Behavior**:
[What should happen]

**Actual Behavior**:
[What actually happens]

**Additional Context**:
[Any other relevant information, including sample images if relevant]
```

## 🔄 Pull Request Process

### PR Title Format
- `feat: add [agent-name] agent for [purpose]`
- `fix: correct [issue] in [agent-name]`
- `docs: update [what] for [agent-name]`
- `refactor: improve [what] in [agent-name]`

### PR Description Template

```markdown
## Description
[Describe your changes]

## Type of Change
- [ ] New agent
- [ ] Bug fix
- [ ] Enhancement
- [ ] Documentation update

## Testing
- [ ] Tested with Claude Code locally
- [ ] Added/updated examples
- [ ] Updated documentation
- [ ] Tested with sample design assets

## Checklist
- [ ] Follows agent format guidelines
- [ ] Includes meaningful examples
- [ ] Tools are appropriate for the task
- [ ] No sensitive information included
- [ ] Commits follow conventional format

## Related Issues
Closes #[issue-number]
```

## ✅ Agent Quality Standards

### Essential Requirements

1. **Clear Purpose**: Agent must have a well-defined, specific design purpose
2. **Appropriate Tools**: Only request necessary tools
3. **Professional Tone**: Maintain design expertise while being helpful
4. **Error Handling**: Include guidance for common design issues
5. **Best Practices**: Incorporate design industry standards
6. **Visual Awareness**: Understand visual design principles

### Quality Checklist

- [ ] Agent name follows naming convention
- [ ] Description enables good auto-detection
- [ ] System prompt is comprehensive but focused
- [ ] Examples demonstrate real-world design usage
- [ ] No typos or grammatical errors
- [ ] Tools are minimal but sufficient
- [ ] Includes design-specific best practices

### Anti-Patterns to Avoid

- ❌ Overly broad agents ("general-designer")
- ❌ Requesting all tools when only a few are needed
- ❌ Vague or generic system prompts
- ❌ Missing concrete design examples
- ❌ Duplicating existing agents
- ❌ Including user-specific information

## 🧪 Testing Guidelines

### Local Testing

1. **Install your agent locally**:
   ```bash
   cp agents/category/your-agent.md ~/.claude/agents/
   ```

2. **Test auto-invocation**:
   ```bash
   claude "Design task that should trigger your agent"
   ```

3. **Test explicit invocation**:
   ```bash
   claude "Use the your-agent to analyze this design"
   ```

### Test Scenarios

Create test cases for:
- Common design use cases
- Visual analysis edge cases
- Error scenarios with invalid images
- Integration with design tools
- Performance with large image files

## 🎉 Recognition

Contributors will be:
- Listed in our [Contributors](CONTRIBUTORS.md) file
- Credited in agent metadata
- Mentioned in release notes
- Eligible for "Top Contributor" badges

## 💡 Tips for Success

1. **Study existing agents**: Learn from well-rated design agents
2. **Be specific**: Focused design agents perform better than general ones
3. **Test thoroughly**: Real-world testing with design assets prevents issues
4. **Document well**: Good examples help users understand design capabilities
5. **Iterate**: Start simple and enhance based on design feedback

## 📞 Getting Help

- **GitHub Discussions**: Use GitHub Discussions for questions
- **Issues**: Report bugs via GitHub Issues
- **The1Studio**: Contact us for design-specific guidance

---

Thank you for contributing to The1 Design Claude Agents! Your design expertise helps make Claude Code more powerful for creative professionals. 🎨