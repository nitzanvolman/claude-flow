# MCP Tools Overview

> **Navigation Hub** - This document links to detailed MCP tools documentation

## Quick Overview
Model Context Protocol (MCP) tools provide advanced coordination capabilities for Claude Flow. Three MCP servers are available: claude-flow (required), ruv-swarm (enhanced coordination), and flow-nexus (cloud orchestration with 70+ tools).

## Detailed Documentation
- [MCP Architecture](./architecture/MCP-ARCHITECTURE.md)
- [Tool Reference](./api/MCP-TOOLS-REFERENCE.md)
- [Integration Guide](./guides/MCP-INTEGRATION.md)
- [Troubleshooting](./troubleshooting/MCP-ISSUES.md)

## Quick Start

### Setup MCP Servers
```bash
# Required: Core coordination
claude mcp add claude-flow npx claude-flow@alpha mcp start

# Optional: Enhanced swarm features
claude mcp add ruv-swarm npx ruv-swarm mcp start

# Optional: Cloud orchestration (requires registration)
claude mcp add flow-nexus npx flow-nexus@latest mcp start
```

### Core MCP Tool Categories

**Swarm Coordination**
- `mcp__claude-flow__swarm_init` - Initialize swarm topology
- `mcp__claude-flow__agent_spawn` - Define agent types
- `mcp__claude-flow__task_orchestrate` - Orchestrate workflows

**Memory Management**
- `mcp__claude-flow__memory_usage` - Store/retrieve coordination data
- `mcp__claude-flow__memory_search` - Search memory patterns
- `mcp__claude-flow__memory_persist` - Cross-session persistence

**Neural Features**
- `mcp__claude-flow__neural_train` - Train neural patterns
- `mcp__claude-flow__neural_patterns` - Analyze cognitive patterns
- `mcp__claude-flow__neural_predict` - Make AI predictions

**Performance Monitoring**
- `mcp__claude-flow__performance_report` - Generate metrics reports
- `mcp__claude-flow__bottleneck_analyze` - Identify bottlenecks
- `mcp__claude-flow__benchmark_run` - Execute benchmarks

**GitHub Integration**
- `mcp__claude-flow__github_repo_analyze` - Repository analysis
- `mcp__claude-flow__github_pr_manage` - Pull request management
- `mcp__claude-flow__github_code_review` - Automated code review

### Flow-Nexus MCP Tools (70+ Advanced Features)
```bash
# Authentication required
npx flow-nexus@latest register
npx flow-nexus@latest login

# Cloud sandboxes for code execution
mcp__flow-nexus__sandbox_create
mcp__flow-nexus__sandbox_execute

# Neural AI with distributed training
mcp__flow-nexus__neural_cluster_init
mcp__flow-nexus__neural_train_distributed

# Real-time monitoring
mcp__flow-nexus__execution_stream_subscribe
mcp__flow-nexus__realtime_subscribe
```

## Key Distinctions

**Claude Code vs MCP Tools**
- **Claude Code**: Handles ALL execution (file ops, bash, implementation)
- **MCP Tools**: Coordinates strategy (topology, memory, orchestration)

**Pattern**: MCP coordinates → Claude Code's Task tool executes

## See Also
- [Agent System Guide](./AGENT-SYSTEM.md)
- [Neural Module](./NEURAL-MODULE.md)
- [GitHub Integration](./GITHUB-INTEGRATION.md)
- [API Reference](./api/MCP-TOOLS-REFERENCE.md)
