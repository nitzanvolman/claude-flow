# MCP Tools Reference

> **API Reference** - Complete catalog of Model Context Protocol (MCP) tools for Claude Flow

## Overview

Claude Flow provides 150+ MCP tools across three server implementations:
- **claude-flow** (Core): 70+ essential tools for swarm orchestration
- **ruv-swarm** (Enhanced): 40+ advanced coordination tools
- **flow-nexus** (Cloud): 70+ cloud-based tools for distributed systems

## Key Concepts

- **MCP Servers** - Protocol servers exposing specialized tools
- **Tool Categories** - Organized by functionality (coordination, monitoring, etc.)
- **Parameter Types** - Typed parameters with validation
- **Return Values** - Structured responses with metadata
- **Rate Limits** - Usage quotas and throttling
- **Authentication** - API key and session-based auth

## Installation

### Claude Flow (Required)

```bash
# Install globally
npm install -g claude-flow@alpha

# Add MCP server to Claude Code
claude mcp add claude-flow npx claude-flow@alpha mcp start
```

### Ruv-Swarm (Optional - Enhanced Coordination)

```bash
# Install globally
npm install -g ruv-swarm

# Add MCP server
claude mcp add ruv-swarm npx ruv-swarm mcp start
```

### Flow-Nexus (Optional - Cloud Features)

```bash
# Add MCP server (no installation required)
claude mcp add flow-nexus npx flow-nexus@latest mcp start

# Register account
npx flow-nexus@latest register

# Login
npx flow-nexus@latest login
```

---

## Core Tools (claude-flow)

### Swarm Management

#### `swarm_init`
Initialize swarm with specified topology.

**Parameters**:
```typescript
{
  topology: "mesh" | "hierarchical" | "ring" | "star",
  maxAgents?: number,  // default: 8
  strategy?: "auto" | "balanced" | "specialized" | "adaptive"  // default: "auto"
}
```

**Returns**:
```typescript
{
  swarmId: string,
  topology: string,
  maxAgents: number,
  strategy: string,
  created: string
}
```

**Example**:
```javascript
const swarm = await mcp__claude-flow__swarm_init({
  topology: "mesh",
  maxAgents: 10,
  strategy: "adaptive"
});
// Returns: { swarmId: "swarm_123...", topology: "mesh", ... }
```

---

#### `swarm_status`
Get current swarm status and metrics.

**Parameters**:
```typescript
{
  swarmId?: string  // Optional, uses active swarm if not provided
}
```

**Returns**:
```typescript
{
  swarmId: string,
  topology: string,
  activeAgents: number,
  maxAgents: number,
  status: "active" | "idle" | "destroyed",
  uptime: number,
  tasksCompleted: number,
  metrics: {
    cpu: number,
    memory: number,
    throughput: number
  }
}
```

---

#### `swarm_monitor`
Real-time swarm monitoring.

**Parameters**:
```typescript
{
  swarmId?: string,
  interval?: number  // seconds, default: 5
}
```

---

#### `swarm_scale`
Scale swarm up or down.

**Parameters**:
```typescript
{
  swarmId?: string,
  targetSize: number  // 1-100
}
```

---

#### `swarm_destroy`
Gracefully shutdown and cleanup swarm.

**Parameters**:
```typescript
{
  swarmId: string
}
```

---

### Agent Management

#### `agent_spawn`
Create specialized agent in swarm.

**Parameters**:
```typescript
{
  type: "coordinator" | "analyst" | "optimizer" | "documenter" |
        "monitor" | "specialist" | "architect" | "task-orchestrator" |
        "code-analyzer" | "perf-analyzer" | "api-docs" |
        "performance-benchmarker" | "system-architect" | "researcher" |
        "coder" | "tester" | "reviewer",
  name?: string,
  swarmId?: string,
  capabilities?: string[]
}
```

**Returns**:
```typescript
{
  agentId: string,
  type: string,
  name: string,
  swarmId: string,
  status: "active",
  capabilities: string[]
}
```

**Example**:
```javascript
const agent = await mcp__claude-flow__agent_spawn({
  type: "coder",
  name: "backend-specialist",
  capabilities: ["nodejs", "postgresql", "redis"]
});
```

---

#### `agent_list`
List all active agents and their capabilities.

**Parameters**:
```typescript
{
  swarmId?: string
}
```

**Returns**:
```typescript
{
  agents: Array<{
    agentId: string,
    type: string,
    name: string,
    status: string,
    capabilities: string[]
  }>
}
```

---

#### `agent_metrics`
Get performance metrics for specific agent.

**Parameters**:
```typescript
{
  agentId: string
}
```

**Returns**:
```typescript
{
  agentId: string,
  cpu: number,
  memory: number,
  tasksCompleted: number,
  averageTaskTime: number,
  successRate: number
}
```

---

### Task Orchestration

#### `task_orchestrate`
Orchestrate complex task workflows across agents.

**Parameters**:
```typescript
{
  task: string,  // Task description
  strategy?: "parallel" | "sequential" | "adaptive" | "balanced",
  priority?: "low" | "medium" | "high" | "critical",
  dependencies?: Record<string, string[]>
}
```

**Returns**:
```typescript
{
  taskId: string,
  status: "queued",
  assignedAgents: string[],
  estimatedTime: number
}
```

**Example**:
```javascript
const task = await mcp__claude-flow__task_orchestrate({
  task: "Implement user authentication with JWT tokens",
  strategy: "adaptive",
  priority: "high",
  dependencies: {
    "implement": ["research"],
    "test": ["implement"],
    "review": ["test"]
  }
});
```

---

#### `task_status`
Check progress of running tasks.

**Parameters**:
```typescript
{
  taskId: string
}
```

**Returns**:
```typescript
{
  taskId: string,
  status: "queued" | "in_progress" | "completed" | "failed",
  progress: number,  // 0-100
  assignedAgents: string[],
  startTime: string,
  estimatedCompletion: string
}
```

---

#### `task_results`
Get results from completed tasks.

**Parameters**:
```typescript
{
  taskId: string
}
```

**Returns**:
```typescript
{
  taskId: string,
  status: "completed" | "failed",
  result: any,
  metrics: {
    duration: number,
    agentsUsed: number,
    tokensUsed: number
  },
  artifacts: string[]  // Files created/modified
}
```

---

### Memory Management

#### `memory_usage`
Store/retrieve persistent memory with TTL and namespacing.

**Parameters**:
```typescript
{
  action: "store" | "retrieve" | "list" | "delete" | "search",
  key?: string,
  value?: string,
  namespace?: string,  // default: "default"
  ttl?: number  // seconds
}
```

**Examples**:
```javascript
// Store
await mcp__claude-flow__memory_usage({
  action: "store",
  key: "swarm/architecture/decisions",
  namespace: "coordination",
  value: JSON.stringify({ framework: "express", db: "postgresql" }),
  ttl: 3600
});

// Retrieve
const data = await mcp__claude-flow__memory_usage({
  action: "retrieve",
  key: "swarm/architecture/decisions",
  namespace: "coordination"
});

// List
const keys = await mcp__claude-flow__memory_usage({
  action: "list",
  namespace: "coordination"
});

// Delete
await mcp__claude-flow__memory_usage({
  action: "delete",
  key: "swarm/old-data",
  namespace: "coordination"
});
```

---

#### `memory_search`
Search memory with patterns.

**Parameters**:
```typescript
{
  pattern: string,  // Supports wildcards: "swarm/*", "*/decisions"
  namespace?: string,
  limit?: number  // default: 10
}
```

**Returns**:
```typescript
{
  matches: Array<{
    key: string,
    value: string,
    namespace: string,
    timestamp: string
  }>
}
```

---

### Neural Features

#### `neural_status`
Check neural network status.

**Parameters**:
```typescript
{
  modelId?: string
}
```

---

#### `neural_train`
Train neural patterns with WASM SIMD acceleration.

**Parameters**:
```typescript
{
  pattern_type: "coordination" | "optimization" | "prediction",
  training_data: string,  // JSON string
  epochs?: number  // default: 50
}
```

**Example**:
```javascript
await mcp__claude-flow__neural_train({
  pattern_type: "coordination",
  training_data: JSON.stringify({
    operation: "swarm-coordination",
    outcome: "success",
    metrics: { time: 120, quality: 0.95 }
  }),
  epochs: 100
});
```

---

#### `neural_patterns`
Analyze cognitive patterns.

**Parameters**:
```typescript
{
  action: "analyze" | "learn" | "predict",
  operation?: string,
  outcome?: string,
  metadata?: Record<string, any>
}
```

---

#### `neural_predict`
Make AI predictions.

**Parameters**:
```typescript
{
  modelId: string,
  input: string
}
```

---

### Performance Analysis

#### `benchmark_run`
Execute performance benchmarks with real-time metrics.

**Parameters**:
```typescript
{
  suite?: "full" | "wasm" | "swarm" | "agent" | "task",
  iterations?: number  // default: 10
}
```

**Returns**:
```typescript
{
  suite: string,
  iterations: number,
  results: {
    avgTime: number,
    minTime: number,
    maxTime: number,
    throughput: number
  }
}
```

---

#### `bottleneck_analyze`
Identify performance bottlenecks.

**Parameters**:
```typescript
{
  component?: string,
  metrics?: string[]  // ["cpu", "memory", "io", "network"]
}
```

**Returns**:
```typescript
{
  bottlenecks: Array<{
    component: string,
    metric: string,
    severity: "low" | "medium" | "high" | "critical",
    recommendation: string
  }>
}
```

---

#### `performance_report`
Generate performance reports.

**Parameters**:
```typescript
{
  format?: "summary" | "detailed" | "json",
  timeframe?: "24h" | "7d" | "30d"
}
```

---

#### `token_usage`
Analyze token consumption.

**Parameters**:
```typescript
{
  operation?: string,
  timeframe?: string  // "1h", "24h", "7d"
}
```

---

### GitHub Integration

#### `github_repo_analyze`
Repository analysis.

**Parameters**:
```typescript
{
  repo: string,  // "owner/repository"
  analysis_type?: "code_quality" | "performance" | "security"
}
```

---

#### `github_pr_manage`
Pull request management.

**Parameters**:
```typescript
{
  repo: string,
  pr_number?: number,
  action: "review" | "merge" | "close"
}
```

---

#### `github_issue_track`
Issue tracking and triage.

**Parameters**:
```typescript
{
  repo: string,
  action: "triage" | "prioritize" | "assign" | "close"
}
```

---

#### `github_release_coord`
Release coordination.

**Parameters**:
```typescript
{
  repo: string,
  version: string
}
```

---

#### `github_workflow_auto`
Workflow automation.

**Parameters**:
```typescript
{
  repo: string,
  workflow: {
    on: string[],
    jobs: string[]
  }
}
```

---

### Advanced Coordination

#### `coordination_sync`
Sync agent coordination.

---

#### `topology_optimize`
Auto-optimize swarm topology.

---

#### `load_balance`
Distribute tasks efficiently.

**Parameters**:
```typescript
{
  swarmId?: string,
  tasks: string[]
}
```

---

### Workflow Management

#### `workflow_create`
Create custom workflows.

**Parameters**:
```typescript
{
  name: string,
  steps: Array<{
    name: string,
    agent: string,
    action: string
  }>,
  triggers?: string[]
}
```

---

#### `workflow_execute`
Run predefined workflows.

**Parameters**:
```typescript
{
  workflowId: string,
  params?: Record<string, any>
}
```

---

### DAA (Decentralized Autonomous Agents)

#### `daa_agent_create`
Create dynamic agents.

**Parameters**:
```typescript
{
  agent_type: string,
  capabilities?: string[],
  resources?: Record<string, any>
}
```

---

#### `daa_capability_match`
Match capabilities to tasks.

**Parameters**:
```typescript
{
  task_requirements: string[],
  available_agents?: string[]
}
```

---

## Enhanced Tools (ruv-swarm)

### Advanced Swarm Features

#### `swarm_init` (Enhanced)
No-timeout version with additional features.

**Parameters**: Same as claude-flow, plus:
```typescript
{
  enableCoordination?: boolean,
  persistenceMode?: "auto" | "memory" | "disk"
}
```

---

#### `agents_spawn_parallel`
Spawn multiple agents in parallel (10-20x faster).

**Parameters**:
```typescript
{
  agents: Array<{
    type: string,
    name: string,
    capabilities?: string[],
    priority?: "low" | "medium" | "high" | "critical"
  }>,
  maxConcurrency?: number,  // default: 5
  batchSize?: number  // default: 3
}
```

**Example**:
```javascript
await mcp__ruv-swarm__agents_spawn_parallel({
  agents: [
    { type: "researcher", name: "tech-research" },
    { type: "coder", name: "backend-dev" },
    { type: "coder", name: "frontend-dev" },
    { type: "tester", name: "qa-engineer" },
    { type: "reviewer", name: "code-reviewer" }
  ],
  maxConcurrency: 5
});
```

---

### DAA Features

#### `daa_init`
Initialize decentralized autonomous agents.

**Parameters**:
```typescript
{
  enableCoordination?: boolean,
  enableLearning?: boolean,
  persistenceMode?: "auto" | "memory" | "disk"
}
```

---

#### `daa_agent_create`
Create autonomous agent with learning.

**Parameters**:
```typescript
{
  id: string,
  capabilities?: string[],
  cognitivePattern?: "convergent" | "divergent" | "lateral" |
                     "systems" | "critical" | "adaptive",
  enableMemory?: boolean,
  learningRate?: number  // 0-1
}
```

---

#### `daa_agent_adapt`
Trigger agent adaptation based on feedback.

**Parameters**:
```typescript
{
  agentId: string,
  feedback?: string,
  performanceScore?: number,  // 0-1
  suggestions?: string[]
}
```

---

#### `daa_workflow_create`
Create autonomous workflow.

**Parameters**:
```typescript
{
  id: string,
  name: string,
  steps?: Array<{
    name: string,
    agent: string,
    action: string
  }>,
  strategy?: "parallel" | "sequential" | "adaptive",
  dependencies?: Record<string, string[]>
}
```

---

#### `daa_knowledge_share`
Share knowledge between agents.

**Parameters**:
```typescript
{
  sourceAgentId: string,
  targetAgentIds: string[],
  knowledgeDomain?: string,
  knowledgeContent?: Record<string, any>
}
```

---

### Query Control

#### `query_control`
Control running queries (pause, resume, terminate).

**Parameters**:
```typescript
{
  action: "pause" | "resume" | "terminate" | "change_model" |
          "change_permissions" | "execute_command",
  queryId: string,
  model?: "claude-3-5-sonnet-20241022" | "claude-3-5-haiku-20241022" |
          "claude-3-opus-20240229",
  permissionMode?: "default" | "acceptEdits" | "bypassPermissions" | "plan",
  command?: string
}
```

---

#### `query_list`
List all active queries.

**Parameters**:
```typescript
{
  includeHistory?: boolean  // default: false
}
```

---

## Cloud Tools (flow-nexus)

### Sandbox Management

#### `sandbox_create`
Create code execution sandbox with environment variables.

**Parameters**:
```typescript
{
  template: "node" | "python" | "react" | "nextjs" | "vanilla" |
            "base" | "claude-code",
  name?: string,
  timeout?: number,  // seconds, default: 3600
  env_vars?: Record<string, string>,
  anthropic_key?: string,
  install_packages?: string[],
  startup_script?: string,
  metadata?: Record<string, any>,
  api_key?: string  // Custom E2B API key
}
```

**Example**:
```javascript
const sandbox = await mcp__flow-nexus__sandbox_create({
  template: "node",
  name: "api-server",
  timeout: 7200,
  env_vars: {
    "DATABASE_URL": "postgresql://...",
    "REDIS_URL": "redis://..."
  },
  install_packages: ["express", "pg", "redis"]
});
```

---

#### `sandbox_execute`
Execute code in sandbox.

**Parameters**:
```typescript
{
  sandbox_id: string,
  code: string,
  language?: string,  // default: "javascript"
  timeout?: number,  // default: 60
  env_vars?: Record<string, string>,
  working_dir?: string,
  capture_output?: boolean  // default: true
}
```

---

#### `sandbox_configure`
Configure sandbox environment.

**Parameters**:
```typescript
{
  sandbox_id: string,
  env_vars?: Record<string, string>,
  anthropic_key?: string,
  install_packages?: string[],
  run_commands?: string[]
}
```

---

#### `sandbox_upload`
Upload file to sandbox.

**Parameters**:
```typescript
{
  sandbox_id: string,
  file_path: string,
  content: string
}
```

---

### Templates

#### `template_list`
List available deployment templates.

**Parameters**:
```typescript
{
  category?: string,
  featured?: boolean,
  template_type?: string,
  limit?: number  // default: 20
}
```

---

#### `template_deploy`
Deploy template with variables.

**Parameters**:
```typescript
{
  template_id?: string,
  template_name?: string,
  deployment_name?: string,
  variables?: Record<string, any>,
  env_vars?: Record<string, any>
}
```

---

### Neural AI (Cloud)

#### `neural_train` (Cloud)
Train neural network in distributed E2B sandboxes.

**Parameters**:
```typescript
{
  config: {
    architecture: {
      type: "feedforward" | "lstm" | "gan" | "autoencoder" | "transformer",
      layers: Array<any>
    },
    training: {
      epochs: number,
      batch_size: number,
      learning_rate: number,
      optimizer: string
    },
    divergent?: {
      enabled: boolean,
      pattern: "lateral" | "quantum" | "chaotic" | "associative" | "evolutionary",
      factor: number
    }
  },
  tier?: "nano" | "mini" | "small" | "medium" | "large",
  user_id?: string
}
```

---

#### `neural_cluster_init`
Initialize distributed neural cluster.

**Parameters**:
```typescript
{
  name: string,
  architecture?: "transformer" | "cnn" | "rnn" | "gnn" | "hybrid",
  topology?: "mesh" | "ring" | "star" | "hierarchical",
  consensus?: "proof-of-learning" | "byzantine" | "raft" | "gossip",
  daaEnabled?: boolean,
  wasmOptimization?: boolean
}
```

---

### Seraphina AI Chat

#### `seraphina_chat`
Seek guidance from Queen Seraphina AI assistant.

**Parameters**:
```typescript
{
  message: string,
  conversation_history?: Array<{
    role: "user" | "assistant",
    content: string
  }>,
  enable_tools?: boolean  // default: false
}
```

**Example**:
```javascript
const response = await mcp__flow-nexus__seraphina_chat({
  message: "What's the best swarm topology for building a microservices API?",
  enable_tools: false
});
```

---

### Authentication

#### `user_register`
Register new user account.

**Parameters**:
```typescript
{
  email: string,
  password: string,
  username?: string,
  full_name?: string
}
```

---

#### `user_login`
Login user and create session.

**Parameters**:
```typescript
{
  email: string,
  password: string
}
```

---

#### `auth_status`
Check authentication status.

**Parameters**:
```typescript
{
  detailed?: boolean
}
```

---

### Payments

#### `check_balance`
Check credit balance and auto-refill status.

---

#### `create_payment_link`
Create secure payment link.

**Parameters**:
```typescript
{
  amount: number  // USD, minimum $10
}
```

---

#### `configure_auto_refill`
Configure automatic credit refill.

**Parameters**:
```typescript
{
  enabled: boolean,
  threshold?: number,
  amount?: number
}
```

---

## Tool Categories Summary

### Core (claude-flow) - 70+ tools
- ✅ Swarm management (6 tools)
- ✅ Agent management (3 tools)
- ✅ Task orchestration (3 tools)
- ✅ Memory management (2 tools)
- ✅ Neural features (5 tools)
- ✅ Performance analysis (4 tools)
- ✅ GitHub integration (5 tools)
- ✅ Workflow management (2 tools)
- ✅ DAA features (2 tools)

### Enhanced (ruv-swarm) - 40+ tools
- ✅ Advanced swarm (8 tools)
- ✅ DAA coordination (7 tools)
- ✅ Query control (2 tools)
- ✅ Neural patterns (4 tools)
- ✅ Memory management (5 tools)

### Cloud (flow-nexus) - 70+ tools
- ✅ Sandbox management (9 tools)
- ✅ Templates (3 tools)
- ✅ Neural AI (10 tools)
- ✅ Distributed neural (7 tools)
- ✅ Authentication (8 tools)
- ✅ Payments (4 tools)
- ✅ Real-time features (4 tools)
- ✅ Storage (4 tools)
- ✅ Seraphina chat (1 tool)

---

## Rate Limits

### claude-flow & ruv-swarm
- No rate limits (local execution)

### flow-nexus
- **Free Tier**: 1000 requests/day
- **Pro Tier**: 10,000 requests/day
- **Enterprise**: Unlimited

---

## Best Practices

### 1. Use Appropriate MCP Server

```javascript
// Core coordination → claude-flow
await mcp__claude-flow__swarm_init({ topology: "mesh" });

// Advanced coordination → ruv-swarm
await mcp__ruv-swarm__agents_spawn_parallel({ agents: [...] });

// Cloud execution → flow-nexus
await mcp__flow-nexus__sandbox_create({ template: "node" });
```

### 2. Batch Operations

```javascript
// ✅ CORRECT: Parallel execution
await Promise.all([
  mcp__claude-flow__agent_spawn({ type: "coder" }),
  mcp__claude-flow__agent_spawn({ type: "tester" }),
  mcp__claude-flow__agent_spawn({ type: "reviewer" })
]);
```

### 3. Handle Errors

```javascript
try {
  const result = await mcp__claude-flow__task_orchestrate({
    task: "Complex task",
    strategy: "adaptive"
  });
} catch (error) {
  console.error("Task failed:", error);
  // Retry or fallback logic
}
```

### 4. Monitor Performance

```javascript
// Regular performance checks
const metrics = await mcp__claude-flow__performance_report({
  format: "summary",
  timeframe: "24h"
});

if (metrics.avgResponseTime > 1000) {
  // Optimize or scale
  await mcp__claude-flow__swarm_scale({ targetSize: 10 });
}
```

---

## See Also

- [Agent System Documentation](./agent-system-documentation.md) - Agent types and capabilities
- [Integration Guide](./INTEGRATION_GUIDE.md) - Step-by-step integration
- [CONTRIBUTING.md](../../CONTRIBUTING.md) - How to contribute
- [GitHub Integration Guide](../GITHUB_INTEGRATION.md) - GitHub workflows

---

**Next Steps**: Review the [Integration Guide](./INTEGRATION_GUIDE.md) for practical examples.
