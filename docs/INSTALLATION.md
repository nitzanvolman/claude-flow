# Installation Guide

> **Navigation Hub** - This document links to detailed installation documentation

## Quick Overview
Claude Flow is an advanced multi-agent orchestration system for AI-powered development. Installation supports npm, npx, and optional MCP server configurations for enhanced coordination capabilities.

## Detailed Documentation
- [Quick Start Guide](../README.md#quick-start)
- [MCP Server Setup](./MCP-TOOLS.md)
- [Configuration Options](./CONFIGURATION.md)
- [Troubleshooting Guide](./troubleshooting/INSTALLATION-ISSUES.md)

## Quick Start

### Basic Installation (npx - No Install Required)
```bash
# Run directly without installation
npx claude-flow@alpha --help
npx claude-flow@alpha sparc modes
npx claude-flow@alpha sparc tdd "feature description"
```

### Global Installation (npm)
```bash
# Install globally for persistent access
npm install -g claude-flow@alpha

# Verify installation
claude-flow --version
```

### MCP Server Setup (Optional - Enhanced Features)
```bash
# Add Claude Flow MCP server (required for coordination)
claude mcp add claude-flow npx claude-flow@alpha mcp start

# Optional: Enhanced swarm coordination
claude mcp add ruv-swarm npx ruv-swarm mcp start

# Optional: Cloud-based orchestration (70+ tools)
claude mcp add flow-nexus npx flow-nexus@latest mcp start
```

### Verify Installation
```bash
# Check version
claude-flow --version

# List available modes
claude-flow sparc modes

# Test hooks system
claude-flow hooks pre-task --description "test"
```

## Installation Requirements
- **Node.js**: v18.0.0 or higher
- **npm**: v9.0.0 or higher
- **Claude Desktop**: Latest version (for MCP features)
- **Git**: For repository integration

## Platform Support
- Linux (tested)
- macOS (tested)
- Windows (via WSL recommended)

## See Also
- [Getting Started Guide](./GETTING-STARTED.md)
- [Configuration Guide](./CONFIGURATION.md)
- [MCP Tools Overview](./MCP-TOOLS.md)
- [Architecture Documentation](./ARCHITECTURE.md)
