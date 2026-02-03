# Release v2.0.0 - Documentation-Only Kiro Power

## 🎉 First Release

This is the initial release of the Skill Loader Power - a comprehensive documentation-only Kiro Power that guides users on using the Skill Loader MCP Server.

## ✨ Features

### Comprehensive Documentation
- ✅ 2,368 lines of detailed documentation in POWER.md
- ✅ All 9 MCP tools documented with examples
- ✅ 4 common workflows with step-by-step guides
- ✅ Security validation guide
- ✅ 12+ complete usage examples
- ✅ Troubleshooting guide
- ✅ Best practices and tips

### Included Files
- **POWER.md** - Main documentation (2,368 lines)
- **mcp.json** - MCP server configuration
- **README.md** - Quick reference guide
- **steering/** - Optional quick-start and advanced guides

## 📦 Installation

### Option 1: Manual Installation
```bash
# Clone the repository
git clone https://github.com/goldzulu/skill-loader-power.git

# Copy to Kiro powers directory
cp -r skill-loader-power ~/.kiro/powers/skill-loader
```

### Option 2: Direct Download
Download and extract to `~/.kiro/powers/skill-loader`

## 🚀 Prerequisites

This power requires the Skill Loader MCP Server to be installed:

```bash
npm install -g @goldzulu/skill-loader-mcp-server
```

Then configure it in your MCP settings (`.kiro/settings/mcp.json`):

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

## 📚 Documentation Highlights

### Tool Documentation
Complete documentation for all 9 tools:
- list-skills
- search-skills
- get-leaderboard
- fetch-skill
- validate-skill
- convert-to-power
- convert-to-steering
- import-skill
- get-skill-stats

### Workflows
4 common workflows with examples:
1. Discovering and browsing skills
2. Importing a skill as a Power
3. Importing a skill as a steering file
4. Validating skill security

### Examples
12+ complete examples covering:
- Basic skill discovery
- Advanced search with filters
- Security validation
- Batch operations
- Error handling
- And more!

## 🔗 Links

- **GitHub**: https://github.com/goldzulu/skill-loader-power
- **MCP Server**: https://github.com/goldzulu/skill-loader-mcp-server
- **npm Package**: https://www.npmjs.com/package/@goldzulu/skill-loader-mcp-server
- **Issues**: https://github.com/goldzulu/skill-loader-power/issues

## 🙏 Acknowledgments

This power provides documentation for the Skill Loader MCP Server, which integrates with:
- [skills.sh](https://skills.sh) - Claude skills repository
- [Kiro](https://kiro.ai) - AI-powered IDE
- [Model Context Protocol](https://modelcontextprotocol.io)

## 📝 License

MIT License - see [LICENSE](LICENSE) for details

---

**Full Changelog**: https://github.com/goldzulu/skill-loader-power/commits/v2.0.0
