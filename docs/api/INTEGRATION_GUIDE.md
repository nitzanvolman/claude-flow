# Integration Guide

> **API Reference** - Complete guide for integrating Claude Flow into your projects

## Overview

This guide provides step-by-step instructions for integrating Claude Flow's multi-agent orchestration capabilities into your development workflow. Whether you're building a simple automation or complex distributed system, this guide covers all integration patterns.

## Key Concepts

- **Swarm Initialization** - Setting up agent coordination topologies
- **Agent Spawning** - Creating specialized agents for specific tasks
- **Task Orchestration** - Coordinating work across multiple agents
- **Memory Coordination** - Sharing context and state between agents
- **Hook Integration** - Automating workflows with pre/post operation hooks
- **MCP Tools** - Leveraging Model Context Protocol for advanced features

## Quick Start

### 1. Installation

```bash
# Install Claude Flow
npm install -g claude-flow@alpha

# Add MCP server (required)
claude mcp add claude-flow npx claude-flow@alpha mcp start

# Optional: Add enhanced coordination
claude mcp add ruv-swarm npx ruv-swarm mcp start

# Optional: Add cloud features
claude mcp add flow-nexus npx flow-nexus@latest mcp start
```

### 2. Basic Integration

```javascript
// Initialize a swarm
const swarm = await mcp__claude-flow__swarm_init({
  topology: "mesh",      // mesh, hierarchical, ring, star
  maxAgents: 8,
  strategy: "balanced"   // balanced, specialized, adaptive
});

// Spawn specialized agents
await mcp__claude-flow__agent_spawn({
  type: "coder",
  name: "backend-specialist",
  capabilities: ["nodejs", "express", "postgresql"]
});

// Orchestrate tasks
await mcp__claude-flow__task_orchestrate({
  task: "Build REST API with authentication",
  strategy: "parallel",
  priority: "high"
});
```

### 3. Using Hooks for Automation

```bash
# Pre-operation hooks
npx claude-flow@alpha hooks pre-task --description "Implement user authentication"
npx claude-flow@alpha hooks pre-edit --file "src/auth.js"

# Post-operation hooks
npx claude-flow@alpha hooks post-edit --file "src/auth.js" --memory-key "swarm/coder/auth"
npx claude-flow@alpha hooks post-task --task-id "auth-implementation"

# Session management
npx claude-flow@alpha hooks session-start --session-id "dev-session-1"
npx claude-flow@alpha hooks session-end --export-metrics true
```

## Integration Patterns

### Pattern 1: Single Agent Workflow

```javascript
// For simple tasks with one specialized agent
const result = await executeAgentWorkflow({
  agent: "coder",
  task: "Implement user login endpoint",
  hooks: {
    pre: ["validate", "prepare"],
    post: ["format", "test", "document"]
  }
});
```

### Pattern 2: Multi-Agent Collaboration

```javascript
// For complex tasks requiring multiple specialists
const swarm = await mcp__claude-flow__swarm_init({
  topology: "hierarchical",
  maxAgents: 5
});

// Spawn coordinated agents
await Promise.all([
  mcp__claude-flow__agent_spawn({ type: "researcher" }),
  mcp__claude-flow__agent_spawn({ type: "coder" }),
  mcp__claude-flow__agent_spawn({ type: "tester" }),
  mcp__claude-flow__agent_spawn({ type: "reviewer" })
]);

// Orchestrate with dependencies
await mcp__claude-flow__task_orchestrate({
  task: "Build complete authentication system",
  strategy: "adaptive",
  dependencies: {
    "research": [],
    "implement": ["research"],
    "test": ["implement"],
    "review": ["test"]
  }
});
```

### Pattern 3: Real-Time Coordination

```javascript
// Monitor swarm activity
const monitor = setInterval(async () => {
  const status = await mcp__claude-flow__swarm_status({
    swarmId: "swarm-123"
  });
  console.log(`Active agents: ${status.activeAgents}`);
  console.log(`Tasks completed: ${status.completedTasks}`);
}, 5000);

// Use memory for coordination
await mcp__claude-flow__memory_usage({
  action: "store",
  key: "swarm/shared/api-schema",
  namespace: "coordination",
  value: JSON.stringify({ endpoints: [...] })
});
```

### Pattern 4: GitHub Integration

```javascript
// Analyze repository
await mcp__claude-flow__github_repo_analyze({
  repo: "owner/repository",
  analysis_type: "code_quality"
});

// Manage pull requests
await mcp__claude-flow__github_pr_manage({
  repo: "owner/repository",
  pr_number: 42,
  action: "review"
});

// Automate workflows
await mcp__claude-flow__github_workflow_auto({
  repo: "owner/repository",
  workflow: {
    on: ["push", "pull_request"],
    jobs: ["test", "build", "deploy"]
  }
});
```

## API Reference

### Core MCP Tools

| Tool | Purpose | Documentation |
|------|---------|---------------|
| `swarm_init` | Initialize swarm topology | [Agent System Docs](./agent-system-documentation.md) |
| `agent_spawn` | Create specialized agents | [Agent System Docs](./agent-system-documentation.md) |
| `task_orchestrate` | Coordinate multi-agent tasks | [MCP Tools Reference](./mcp-tools-reference.md) |
| `memory_usage` | Manage shared state | [MCP Tools Reference](./mcp-tools-reference.md) |
| `neural_train` | Train AI patterns | [MCP Tools Reference](./mcp-tools-reference.md) |

### Hook Commands

| Hook | Usage | When to Use |
|------|-------|-------------|
| `pre-task` | Before starting work | Setup, validation, preparation |
| `post-task` | After completing work | Cleanup, reporting, metrics |
| `pre-edit` | Before file changes | Backup, analysis, validation |
| `post-edit` | After file changes | Format, test, documentation |
| `session-start` | Begin new session | Context restoration, setup |
| `session-end` | End session | Metrics export, cleanup |

## Advanced Features

### Neural Pattern Training

```javascript
// Train from successful operations
await mcp__claude-flow__neural_train({
  pattern_type: "coordination",
  training_data: "successful-swarm-execution.json",
  epochs: 50
});

// Use learned patterns
const patterns = await mcp__claude-flow__neural_patterns({
  action: "predict",
  operation: "optimize-swarm-topology"
});
```

### Performance Optimization

```javascript
// Run benchmarks
const metrics = await mcp__claude-flow__benchmark_run({
  suite: "full",
  iterations: 10
});

// Identify bottlenecks
const bottlenecks = await mcp__claude-flow__bottleneck_analyze({
  component: "swarm-coordinator",
  metrics: ["response-time", "memory-usage", "agent-utilization"]
});

// Generate reports
const report = await mcp__claude-flow__performance_report({
  format: "detailed",
  timeframe: "7d"
});
```

### Cross-Session Persistence

```bash
# Save session state
npx claude-flow@alpha hooks session-end --export-metrics true

# Restore previous session
npx claude-flow@alpha hooks session-restore --session-id "session-abc123"

# Export workflow definition
npx claude-flow@alpha hooks export-workflow --output "workflow.json"
```

## Best Practices

### 1. Always Use Hooks

```bash
# Wrap all agent operations with hooks
npx claude-flow@alpha hooks pre-task --description "Your task"
# ... do work ...
npx claude-flow@alpha hooks post-task --task-id "your-task"
```

### 2. Batch Operations

```javascript
// ✅ CORRECT: All operations in one message
await Promise.all([
  mcp__claude-flow__agent_spawn({ type: "coder" }),
  mcp__claude-flow__agent_spawn({ type: "tester" }),
  mcp__claude-flow__task_orchestrate({ task: "Build feature" })
]);

// ❌ WRONG: Sequential operations across messages
await mcp__claude-flow__agent_spawn({ type: "coder" });
// wait for response...
await mcp__claude-flow__agent_spawn({ type: "tester" });
```

### 3. Use Memory for Coordination

```javascript
// Store decisions for other agents
await mcp__claude-flow__memory_usage({
  action: "store",
  key: "swarm/architecture/decisions",
  namespace: "coordination",
  value: JSON.stringify({
    framework: "express",
    database: "postgresql",
    authentication: "jwt"
  })
});

// Retrieve shared context
const decisions = await mcp__claude-flow__memory_usage({
  action: "retrieve",
  key: "swarm/architecture/decisions",
  namespace: "coordination"
});
```

### 4. Monitor Performance

```javascript
// Track metrics continuously
setInterval(async () => {
  const metrics = await mcp__claude-flow__agent_metrics({
    agentId: "coder-1"
  });

  if (metrics.cpuUsage > 80) {
    await mcp__claude-flow__swarm_scale({
      swarmId: "current",
      targetSize: metrics.activeAgents + 2
    });
  }
}, 30000);
```

## Examples

### Example 1: Full-Stack Application

```javascript
// Initialize development swarm
const swarm = await mcp__claude-flow__swarm_init({
  topology: "hierarchical",
  maxAgents: 8,
  strategy: "specialized"
});

// Spawn full-stack team
await Promise.all([
  mcp__claude-flow__agent_spawn({
    type: "backend-dev",
    capabilities: ["nodejs", "postgresql", "redis"]
  }),
  mcp__claude-flow__agent_spawn({
    type: "coder",
    name: "frontend-dev",
    capabilities: ["react", "typescript", "tailwind"]
  }),
  mcp__claude-flow__agent_spawn({
    type: "code-analyzer",
    name: "database-architect"
  }),
  mcp__claude-flow__agent_spawn({
    type: "tester",
    capabilities: ["jest", "cypress"]
  }),
  mcp__claude-flow__agent_spawn({
    type: "cicd-engineer"
  })
]);

// Orchestrate development
await mcp__claude-flow__task_orchestrate({
  task: "Build e-commerce platform with authentication, product catalog, and payment processing",
  strategy: "adaptive",
  priority: "high"
});
```

### Example 2: Code Review Automation

```javascript
// Setup review swarm
await mcp__claude-flow__swarm_init({
  topology: "star",
  maxAgents: 5
});

// GitHub integration
await mcp__claude-flow__github_code_review({
  repo: "myorg/myrepo",
  pr: 123
});

// Get review results
const results = await mcp__claude-flow__task_results({
  taskId: "review-pr-123"
});
```

### Example 3: Migration Project

```javascript
// Large-scale codebase migration
const swarm = await mcp__claude-flow__swarm_init({
  topology: "mesh",
  maxAgents: 12,
  strategy: "adaptive"
});

// Spawn specialized migration team
await Promise.all([
  mcp__claude-flow__agent_spawn({ type: "migration-planner" }),
  mcp__claude-flow__agent_spawn({ type: "code-analyzer" }),
  mcp__claude-flow__agent_spawn({ type: "coder", name: "refactor-specialist" }),
  mcp__claude-flow__agent_spawn({ type: "tester" }),
  mcp__claude-flow__agent_spawn({ type: "reviewer" }),
  mcp__claude-flow__agent_spawn({ type: "production-validator" })
]);

// Execute migration
await mcp__claude-flow__task_orchestrate({
  task: "Migrate from JavaScript to TypeScript with full type coverage",
  strategy: "sequential",
  priority: "critical"
});
```

## Troubleshooting

### Common Issues

**Issue**: Agents not coordinating properly
```bash
# Solution: Check swarm status
npx claude-flow@alpha hooks system-check

# Reset coordination
npx claude-flow@alpha hooks coordination-sync
```

**Issue**: Memory not persisting
```bash
# Solution: Verify session management
npx claude-flow@alpha hooks session-status

# Force session save
npx claude-flow@alpha hooks session-end --export-metrics true
```

**Issue**: Performance degradation
```bash
# Solution: Run diagnostics
npx claude-flow@alpha hooks performance-report

# Identify bottlenecks
npx claude-flow@alpha hooks bottleneck-detect
```

## See Also

- [Agent System Documentation](./agent-system-documentation.md) - Deep dive into agent architecture
- [MCP Tools Reference](./mcp-tools-reference.md) - Complete MCP tool catalog
- [CONTRIBUTING.md](../../CONTRIBUTING.md) - How to contribute to Claude Flow
- [GitHub Integration Guide](../GITHUB_INTEGRATION.md) - GitHub-specific workflows
- [Architecture Overview](../ARCHITECTURE.md) - System design and patterns

## Support

- **Documentation**: https://github.com/ruvnet/claude-flow
- **Issues**: https://github.com/ruvnet/claude-flow/issues
- **Discussions**: https://github.com/ruvnet/claude-flow/discussions
- **Flow-Nexus Platform**: https://flow-nexus.ruv.io (cloud features)

---

**Next Steps**: Explore the [Agent System Documentation](./agent-system-documentation.md) to understand agent specializations and coordination patterns.
