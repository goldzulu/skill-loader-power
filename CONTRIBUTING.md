# Contributing to Skill Loader Power

Thank you for your interest in contributing to the Skill Loader Power! This document provides guidelines for contributing to the documentation.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [How to Contribute](#how-to-contribute)
- [Documentation Standards](#documentation-standards)
- [Submitting Changes](#submitting-changes)
- [Reporting Issues](#reporting-issues)

## Code of Conduct

This project adheres to a Code of Conduct that all contributors are expected to follow. Please read [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) before contributing.

## Getting Started

1. Fork the repository
2. Clone your fork: `git clone https://github.com/YOUR_USERNAME/skill-loader-power.git`
3. Add upstream remote: `git remote add upstream https://github.com/goldzulu/skill-loader-power.git`
4. Create a new branch: `git checkout -b docs/your-improvement`

## How to Contribute

### Types of Contributions

We welcome various types of contributions:

- **Documentation improvements**: Fix typos, clarify instructions, add examples
- **New examples**: Add usage examples for different scenarios
- **Troubleshooting guides**: Help others solve common problems
- **Translations**: Translate documentation to other languages
- **Steering files**: Add new quick-start or advanced guides

### Before You Start

1. Check existing [issues](https://github.com/goldzulu/skill-loader-power/issues) and [pull requests](https://github.com/goldzulu/skill-loader-power/pulls)
2. For major changes, open an issue first to discuss your proposal
3. For minor fixes (typos, formatting), feel free to submit a PR directly

## Documentation Standards

### File Structure

```
skill-loader/
├── POWER.md              # Main documentation (DO NOT edit structure)
├── README.md             # Quick reference
├── mcp.json              # MCP configuration
└── steering/             # Optional guides
    ├── quick-start.md
    └── advanced.md
```

### Writing Style

- **Clear and concise**: Use simple language
- **Action-oriented**: Start with verbs (e.g., "Install", "Configure", "Run")
- **Examples**: Include code examples for all instructions
- **Formatting**: Use proper markdown formatting
- **Links**: Use relative links for internal references

### Markdown Guidelines

```markdown
# Use H1 for main sections
## Use H2 for subsections
### Use H3 for sub-subsections

**Bold** for emphasis
`code` for inline code
```code blocks``` for multi-line code

- Bullet points for lists
1. Numbered lists for steps
```

### Code Examples

- Use proper syntax highlighting
- Include comments for clarity
- Test all code examples before submitting
- Show both input and expected output

Example:
```json
{
  "mcpServers": {
    "skill-loader": {
      "command": "npx",
      "args": ["-y", "@goldzulu/skill-loader-mcp-server"]
    }
  }
}
```

## Submitting Changes

### Pull Request Process

1. **Update your fork**:
   ```bash
   git fetch upstream
   git rebase upstream/main
   ```

2. **Make your changes**:
   - Edit documentation files
   - Add examples if needed
   - Test all instructions

3. **Preview your changes**:
   - Read through your changes
   - Check markdown rendering
   - Verify all links work

4. **Push to your fork**:
   ```bash
   git push origin docs/your-improvement
   ```

5. **Create a Pull Request**:
   - Use a clear, descriptive title
   - Explain what you changed and why
   - Reference related issues

### Commit Message Format

```
docs(section): brief description

Longer explanation if needed
```

**Examples**:
```
docs(examples): add batch import example

docs(readme): fix installation instructions

docs(troubleshooting): add common error solutions
```

### Pull Request Checklist

- [ ] Documentation is clear and accurate
- [ ] All code examples are tested
- [ ] Links are working
- [ ] Markdown formatting is correct
- [ ] No typos or grammatical errors
- [ ] Changes are relevant to the project

## Reporting Issues

### Documentation Issues

Use the [Documentation Issue template](.github/ISSUE_TEMPLATE/documentation.md) for:

- Typos or grammatical errors
- Unclear instructions
- Missing information
- Broken links
- Outdated examples

### Questions

Use the [Question template](.github/ISSUE_TEMPLATE/question.md) for:

- How to use specific features
- Clarification on documentation
- General questions about the power

## Improving Examples

### Adding New Examples

When adding new examples:

1. **Identify the use case**: What problem does this solve?
2. **Write clear steps**: Break down the process
3. **Include code**: Show actual commands and configuration
4. **Explain the output**: What should users expect?
5. **Add context**: When would someone use this?

### Example Template

```markdown
### Example: [Title]

**Use Case**: [When to use this]

**Steps**:
1. [First step]
2. [Second step]
3. [Third step]

**Code**:
```json
[Configuration or command]
```

**Expected Output**:
```
[What users should see]
```

**Notes**:
- [Important point 1]
- [Important point 2]
```

## Steering Files

### Adding New Steering Files

Steering files provide focused guides for specific workflows:

1. Create a new `.md` file in the `steering/` directory
2. Use a descriptive filename (e.g., `batch-operations.md`)
3. Follow the existing structure
4. Include practical examples
5. Keep it focused on one topic

### Steering File Template

```markdown
# [Title]

## Overview

Brief description of what this guide covers.

## Prerequisites

- Requirement 1
- Requirement 2

## Steps

### Step 1: [Action]

Detailed instructions...

### Step 2: [Action]

Detailed instructions...

## Examples

Practical examples...

## Troubleshooting

Common issues and solutions...

## Next Steps

What to do after completing this guide...
```

## Getting Help

- **Questions**: Open a [discussion](https://github.com/goldzulu/skill-loader-power/discussions) or issue
- **Documentation**: Check the main [POWER.md](POWER.md)
- **MCP Server**: See [skill-loader-mcp-server](https://github.com/goldzulu/skill-loader-mcp-server)

## Recognition

Contributors will be:
- Listed in the project README
- Mentioned in release notes
- Credited for their improvements

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

Thank you for helping improve the Skill Loader Power documentation! 📚
