# Skill Loader Power

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Kiro Power](https://img.shields.io/badge/Kiro-Power-blue.svg)](https://kiro.dev)

A documentation-only Kiro power that guides you on using the Skill Loader MCP Server to discover, fetch, and convert Claude skills from [skills.sh](https://skills.sh) and GitHub repositories.

## What is This?

This is a **Guided MCP Power** - it provides comprehensive documentation for using the Skill Loader MCP Server. The power itself contains no executable code; all functionality is provided by the `@kiro/skill-loader-mcp-server` npm package.

## Features

- 🔍 **Skill Discovery**: Browse and search Claude skills from skills.sh marketplace
- 📥 **Multi-Source Support**: Import from skills.sh, anthropics/skills, vercel-labs/agent-skills, and any GitHub repo
- 🔄 **Dual Output**: Convert to steering files (temporary) or standalone powers (permanent)
- 🔒 **Security Validation**: Multi-layer security checks before content injection
- 📝 **Content Preservation**: Maintains all markdown formatting, code blocks, and metadata
- ⚡ **Complete Workflow**: Import skills with a single command

## Installation

### Prerequisites

- **Node.js 18+**: Required to run the MCP server
- **Kiro**: This power works with Kiro's MCP integration

### Install the Power

1. **Copy to Kiro powers directory**:
   ```bash
   mkdir -p ~/.kiro/powers
   cp -r skill-loader ~/.kiro/powers/skill-loader
   ```

2. **Verify installation**:
   Open Kiro and try:
   ```
   List the top 5 Claude skills
   ```

The MCP server will be automatically installed via npx on first use.

### Manual MCP Server Installation (Optional)

If you prefer to install the MCP server globally:

```bash
npm install -g @kiro/skill-loader-mcp-server
```

Then update `mcp.json` to use `skill-loader-mcp-server` instead of `npx`.

## Quick Start

Try these commands to get started:

```
# Browse top skills
List the top Claude skills

# Search for specific skills
Search for PDF skills

# Import a skill as steering file
Import pdf-extractor as a steering file

# View trending skills
Show me the trending skills from the last 24 hours
```

## Documentation

See **[POWER.md](./POWER.md)** for complete documentation including:

- Installation and setup
- All 9 available tools
- Common workflows
- Security validation
- 12+ detailed examples
- Troubleshooting guide
- Technical details
- References and resources

## Quick Reference

### Discovery Tools
- `list_skills` - List all available skills
- `search_skills` - Search by keyword
- `get_leaderboard` - View trending skills

### Fetching Tools
- `fetch_skill` - Download skill content
- `validate_skill` - Check for security issues

### Conversion Tools
- `convert_to_steering` - Create steering file
- `convert_to_power` - Create power

### Workflow Tools
- `import_skill` - Complete import workflow (fetch + validate + convert)

## Structure

```
skill-loader/
├── POWER.md              # Complete documentation
├── mcp.json              # MCP server configuration
├── README.md             # This file
└── steering/             # Optional guides
    ├── quick-start.md    # 5-minute quick start
    └── advanced.md       # Advanced usage patterns
```

## MCP Server

This power uses the **Skill Loader MCP Server**:

- **Package**: `@kiro/skill-loader-mcp-server`
- **Repository**: [github.com/goldzulu/skill-loader-mcp-server](https://github.com/goldzulu/skill-loader-mcp-server)
- **Protocol**: MCP (Model Context Protocol)
- **Installation**: Automatic via npx

## Support

- **Documentation**: See [POWER.md](./POWER.md)
- **Troubleshooting**: Check the Troubleshooting section in POWER.md
- **Issues**: [GitHub Issues](https://github.com/goldzulu/skill-loader-power/issues)
- **MCP Server Issues**: [MCP Server GitHub](https://github.com/goldzulu/skill-loader-mcp-server/issues)

## Version

- **Power Version**: 2.0.0
- **MCP Server Version**: 1.0.0

## License

MIT

---

**Note**: This is version 2.0 of the Skill Loader Power, redesigned as a documentation-only power following the Guided MCP Power pattern. Version 1.0 (with embedded code) is deprecated.

