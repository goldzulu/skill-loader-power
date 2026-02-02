---
inclusion: manual
---

# Skill Loader Quick Start

Get up and running with the Skill Loader in 5 minutes.

## What is the Skill Loader?

The Skill Loader helps you discover and import Claude skills from [skills.sh](https://skills.sh) into Kiro. Claude skills are pre-built workflows and capabilities you can use immediately.

## Prerequisites

- **Node.js 18+**: Check with `node --version`
- **Internet connection**: For accessing skills.sh and GitHub
- **Kiro**: This power works with Kiro's MCP integration

## Quick Start Steps

### 1. Verify Installation

The Skill Loader should already be installed. Test it:

```
List the top 5 Claude skills
```

You should see a list of popular skills. If you get an error, check the main POWER.md for troubleshooting.

### 2. Browse Available Skills

See what's available:

```
Show me the trending skills from the last 24 hours
```

Or search for something specific:

```
Search for React skills
```

### 3. Import Your First Skill

Let's import a popular skill:

```
Import pdf-extractor as a steering file
```

This will:
- Fetch the skill from GitHub
- Validate it for security issues
- Convert it to Kiro format
- Save it to `.kiro/steering/pdf-extractor.md`

### 4. Use the Skill

Now you can use it:

```
Extract text from my-document.pdf
```

Kiro will automatically use the imported skill to help with the task.

## Common Commands

**Discovery**:
```
List all skills
Search for [keyword] skills
Show me the top 10 skills
What are the trending skills?
```

**Importing**:
```
Import [skill-name] as a steering file
Import [skill-name] as a power
```

**Validation**:
```
Fetch [skill-name]
Validate [skill-name]
```

## Steering Files vs Powers

**Steering Files** (`.kiro/steering/`):
- Temporary context for specific tasks
- Project-specific
- Easy to add and remove
- Great for experimenting

**Powers** (`~/.kiro/powers/`):
- Permanent integration
- Available globally
- Persist across sessions
- Great for frequently used skills

**When to use each**:
- Use **steering files** for one-off tasks or trying out skills
- Use **powers** for skills you'll use regularly

## Popular Skills to Try

Here are some popular skills to get started:

1. **pdf-extractor** - Extract text from PDF files
   ```
   Import pdf-extractor as a steering file
   ```

2. **web-scraper** - Extract data from websites
   ```
   Import web-scraper as a steering file
   ```

3. **api-tester** - Test REST APIs
   ```
   Import api-tester as a power
   ```

4. **code-reviewer** - Review code for issues
   ```
   Import code-reviewer as a power
   ```

5. **react-component-builder** - Build React components
   ```
   Import react-component-builder as a power
   ```

## Next Steps

1. **Explore the catalog**: Browse all available skills
2. **Import skills for your workflow**: Find skills that match your needs
3. **Read the full documentation**: Check POWER.md for detailed information
4. **Create your own skills**: Learn at [agentskills.io](https://agentskills.io)

## Troubleshooting

**Problem: "Skill not found"**
- Check spelling (use hyphens, not underscores)
- Search for the skill first: `Search for [keyword]`

**Problem: "Network error"**
- Check internet connection
- Try again in a few seconds

**Problem: "Security validation failed"**
- Review the security issues
- Only proceed if you trust the skill

## Getting Help

- **Full documentation**: See POWER.md in this power
- **Troubleshooting**: Check the Troubleshooting section in POWER.md
- **Community**: Ask in the Kiro community forum
- **Issues**: Report bugs on GitHub

## Summary

You now know how to:
- ✓ Browse and search for skills
- ✓ Import skills as steering files or powers
- ✓ Use imported skills in your work
- ✓ Understand the difference between formats

Happy skill loading! 🚀

