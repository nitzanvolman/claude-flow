# Agent System Documentation

> **API Reference** - Complete reference for Claude Flow's multi-agent system

## Overview

Claude Flow provides 54+ specialized agent types organized into a modular, extensible architecture. Agents coordinate through memory sharing, hooks, and MCP tools to execute complex development workflows.

## Key Concepts

- **Agent Types** - Specialized roles (coder, tester, reviewer, etc.)
- **Swarm Topologies** - Coordination patterns (mesh, hierarchical, ring, star)
- **Memory Coordination** - Shared context and state management
- **Hook Integration** - Automated workflow orchestration
- **Dynamic Spawning** - On-demand agent creation based on task requirements
- **Neural Learning** - Pattern recognition and optimization from past executions

## Agent Categories

### Core Development Agents (5)

#### `coder`
Primary implementation agent for writing production code.

**Capabilities**:
- Multi-language support (JavaScript, TypeScript, Python, Go, Rust, etc.)
- Design pattern implementation (SOLID, DRY, KISS)
- Test-driven development
- Code refactoring and optimization

**API**:
```javascript
await mcp__claude-flow__agent_spawn({
  type: "coder",
  name: "backend-specialist",
  capabilities: ["nodejs", "express", "postgresql", "redis"]
});
```

**Use Cases**: Feature implementation, bug fixes, refactoring

---

#### `reviewer`
Code review and quality assurance specialist.

**Capabilities**:
- Code quality analysis
- Security vulnerability detection
- Performance review
- Best practices validation
- Architecture assessment

**API**:
```javascript
await mcp__claude-flow__agent_spawn({
  type: "reviewer",
  name: "security-reviewer",
  capabilities: ["security", "performance", "maintainability"]
});
```

**Use Cases**: PR reviews, security audits, code quality gates

---

#### `tester`
Comprehensive testing specialist.

**Capabilities**:
- Unit test generation (Jest, Mocha, Pytest, etc.)
- Integration test design
- End-to-end test automation (Cypress, Playwright)
- Test coverage analysis
- Performance testing

**API**:
```javascript
await mcp__claude-flow__agent_spawn({
  type: "tester",
  name: "qa-specialist",
  capabilities: ["jest", "cypress", "k6", "coverage-90%"]
});
```

**Use Cases**: Test suite creation, coverage improvement, regression testing

---

#### `planner`
Strategic planning and task decomposition expert.

**Capabilities**:
- Requirements analysis
- Task breakdown and prioritization
- Timeline estimation
- Dependency mapping
- Risk assessment

**API**:
```javascript
await mcp__claude-flow__agent_spawn({
  type: "planner",
  name: "sprint-planner",
  capabilities: ["agile", "estimation", "dependency-analysis"]
});
```

**Use Cases**: Sprint planning, project scoping, task organization

---

#### `researcher`
Research and analysis specialist.

**Capabilities**:
- Technology evaluation
- Best practices research
- Documentation analysis
- Competitive analysis
- Feasibility studies

**API**:
```javascript
await mcp__claude-flow__agent_spawn({
  type: "researcher",
  name: "tech-researcher",
  capabilities: ["framework-comparison", "api-design", "performance-analysis"]
});
```

**Use Cases**: Technology selection, architecture decisions, documentation

---

### Swarm Coordination Agents (5)

#### `hierarchical-coordinator`
Manages tree-based agent hierarchies with leader-follower patterns.

**Topology**: Hierarchical (tree structure)
**Best For**: Complex projects with clear ownership hierarchy

**API**:
```javascript
await mcp__claude-flow__swarm_init({
  topology: "hierarchical",
  maxAgents: 10,
  strategy: "specialized"
});

await mcp__claude-flow__agent_spawn({
  type: "coordinator",
  name: "hierarchical-coordinator"
});
```

---

#### `mesh-coordinator`
Peer-to-peer coordination with full agent interconnectivity.

**Topology**: Mesh (fully connected)
**Best For**: Collaborative tasks requiring frequent agent communication

**API**:
```javascript
await mcp__claude-flow__swarm_init({
  topology: "mesh",
  maxAgents: 8,
  strategy: "balanced"
});
```

---

#### `adaptive-coordinator`
Dynamic topology optimization based on task characteristics.

**Capabilities**:
- Real-time topology switching
- Performance-based optimization
- Load balancing
- Fault tolerance

**API**:
```javascript
await mcp__claude-flow__swarm_init({
  topology: "mesh",
  strategy: "adaptive",
  maxAgents: 12
});

await mcp__claude-flow__agent_spawn({
  type: "coordinator",
  name: "adaptive-coordinator"
});
```

---

#### `collective-intelligence-coordinator`
Emergent behavior and swarm intelligence orchestrator.

**Capabilities**:
- Collective decision making
- Emergent pattern recognition
- Distributed problem solving
- Knowledge synthesis

---

#### `swarm-memory-manager`
Manages shared memory and state across agent swarm.

**Capabilities**:
- Cross-agent state synchronization
- Memory persistence and restoration
- Cache management
- Context sharing

**API**:
```javascript
await mcp__claude-flow__memory_usage({
  action: "store",
  key: "swarm/shared/architecture",
  namespace: "coordination",
  value: JSON.stringify({ decisions: {...} }),
  ttl: 3600
});
```

---

### Consensus & Distributed Agents (7)

#### `byzantine-coordinator`
Byzantine fault tolerance for adversarial scenarios.

**Use Cases**: Multi-party validation, untrusted environments

---

#### `raft-manager`
Raft consensus protocol implementation.

**Use Cases**: Leader election, distributed state machines

---

#### `gossip-coordinator`
Gossip protocol for eventual consistency.

**Use Cases**: Large swarms, distributed updates

---

#### `consensus-builder`
Multi-algorithm consensus orchestrator.

**Capabilities**:
- Quorum management
- Vote aggregation
- Conflict resolution

---

#### `crdt-synchronizer`
Conflict-free replicated data types for distributed state.

**Use Cases**: Real-time collaboration, offline-first applications

---

#### `quorum-manager`
Quorum-based decision making.

**Use Cases**: Critical decisions, distributed voting

---

#### `security-manager`
Security policy enforcement and audit.

**Capabilities**:
- Access control
- Encryption management
- Audit logging
- Threat detection

---

### Performance & Optimization Agents (4)

#### `perf-analyzer`
Performance analysis and profiling.

**Capabilities**:
- CPU profiling
- Memory analysis
- Bottleneck detection
- Performance regression testing

**API**:
```javascript
await mcp__claude-flow__benchmark_run({
  suite: "full"
});

await mcp__claude-flow__bottleneck_analyze({
  component: "api-server",
  metrics: ["response-time", "memory-usage", "cpu-usage"]
});
```

---

#### `performance-benchmarker`
Systematic performance benchmarking.

**Use Cases**: Performance testing, optimization validation

---

#### `task-orchestrator`
Advanced task scheduling and execution.

**Capabilities**:
- Dependency resolution
- Parallel execution
- Load balancing
- Retry logic

---

#### `memory-coordinator`
Memory optimization and management.

**Use Cases**: Large-scale applications, memory-constrained environments

---

### GitHub & Repository Agents (9)

#### `github-modes`
GitHub operations orchestrator.

**Capabilities**:
- Repository management
- Branch operations
- Tag and release management

---

#### `pr-manager`
Pull request lifecycle management.

**API**:
```javascript
await mcp__claude-flow__github_pr_manage({
  repo: "owner/repo",
  pr_number: 123,
  action: "review"  // review, merge, close
});
```

---

#### `code-review-swarm`
Distributed code review with multiple reviewers.

**Capabilities**:
- Parallel review execution
- Consensus-based approval
- Automated feedback aggregation

---

#### `issue-tracker`
Issue triage and management.

**API**:
```javascript
await mcp__claude-flow__github_issue_track({
  repo: "owner/repo",
  action: "triage"  // triage, prioritize, assign, close
});
```

---

#### `release-manager`
Release coordination and versioning.

**API**:
```javascript
await mcp__claude-flow__github_release_coord({
  repo: "owner/repo",
  version: "2.1.0"
});
```

---

#### `workflow-automation`
GitHub Actions workflow management.

**API**:
```javascript
await mcp__claude-flow__github_workflow_auto({
  repo: "owner/repo",
  workflow: {
    on: ["push", "pull_request"],
    jobs: ["test", "build", "deploy"]
  }
});
```

---

#### `project-board-sync`
Project board synchronization.

**Use Cases**: Sprint management, roadmap tracking

---

#### `repo-architect`
Repository structure and organization.

**Use Cases**: Monorepo management, architecture decisions

---

#### `multi-repo-swarm`
Cross-repository coordination.

**API**:
```javascript
await mcp__claude-flow__github_sync_coord({
  repos: ["owner/repo1", "owner/repo2", "owner/repo3"]
});
```

---

### SPARC Methodology Agents (6)

#### `sparc-coord`
SPARC workflow orchestrator.

**Phases**: Specification → Pseudocode → Architecture → Refinement → Completion

---

#### `specification`
Requirements specification.

**CLI**:
```bash
npx claude-flow sparc run spec-pseudocode "Build user authentication"
```

---

#### `pseudocode`
Algorithm design in pseudocode.

---

#### `architecture`
System architecture design.

**CLI**:
```bash
npx claude-flow sparc run architect "Design microservices architecture"
```

---

#### `refinement`
Implementation refinement through TDD.

**CLI**:
```bash
npx claude-flow sparc tdd "User authentication feature"
```

---

### Specialized Development Agents (8)

#### `backend-dev`
Backend system specialist.

**Capabilities**:
- API design (REST, GraphQL, gRPC)
- Database design
- Authentication/authorization
- Caching strategies
- Message queues

---

#### `mobile-dev`
Mobile application specialist.

**Platforms**: iOS, Android, React Native, Flutter

---

#### `ml-developer`
Machine learning and AI specialist.

**Capabilities**:
- Model training
- Feature engineering
- Model deployment
- Performance optimization

---

#### `cicd-engineer`
CI/CD pipeline specialist.

**Capabilities**:
- Pipeline design (GitHub Actions, Jenkins, CircleCI)
- Docker and Kubernetes
- Deployment automation
- Infrastructure as Code

---

#### `api-docs`
API documentation specialist.

**Capabilities**:
- OpenAPI/Swagger generation
- Interactive documentation
- Code examples
- Integration guides

---

#### `system-architect`
System architecture specialist.

**Capabilities**:
- Architecture design
- Technology selection
- Scalability planning
- Security architecture

---

#### `code-analyzer`
Static analysis and code intelligence.

**Capabilities**:
- AST analysis
- Dependency graphs
- Code metrics
- Refactoring suggestions

---

#### `base-template-generator`
Project scaffolding and templates.

**Use Cases**: New project setup, boilerplate generation

---

### Testing & Validation Agents (2)

#### `tdd-london-swarm`
London school TDD (mockist) approach.

**Focus**: Isolated unit tests with heavy mocking

---

#### `production-validator`
Production readiness validation.

**Checks**:
- Security vulnerabilities
- Performance benchmarks
- Scalability tests
- Monitoring setup
- Documentation completeness

---

### Migration & Planning Agents (2)

#### `migration-planner`
Large-scale migration planning.

**Use Cases**:
- Framework migrations
- Language migrations
- Cloud migrations
- Database migrations

---

#### `swarm-init`
Swarm initialization and setup.

**API**:
```javascript
await mcp__claude-flow__swarm_init({
  topology: "mesh",      // mesh, hierarchical, ring, star
  maxAgents: 8,
  strategy: "balanced"   // balanced, specialized, adaptive
});
```

---

## Swarm Topologies

### Mesh (Peer-to-Peer)
**Structure**: Fully connected network
**Best For**: Collaborative tasks, high communication needs
**Pros**: High redundancy, no single point of failure
**Cons**: High coordination overhead

```javascript
await mcp__claude-flow__swarm_init({ topology: "mesh" });
```

---

### Hierarchical (Tree)
**Structure**: Leader-follower hierarchy
**Best For**: Clear ownership, cascading tasks
**Pros**: Clear authority, efficient communication
**Cons**: Leader bottleneck, single point of failure

```javascript
await mcp__claude-flow__swarm_init({ topology: "hierarchical" });
```

---

### Ring (Circular)
**Structure**: Circular agent chain
**Best For**: Pipeline processing, sequential workflows
**Pros**: Predictable flow, simple coordination
**Cons**: Limited parallelism, sequential dependencies

```javascript
await mcp__claude-flow__swarm_init({ topology: "ring" });
```

---

### Star (Hub-and-Spoke)
**Structure**: Central coordinator with peripheral agents
**Best For**: Centralized control, independent tasks
**Pros**: Simple coordination, good for independent tasks
**Cons**: Central coordinator bottleneck

```javascript
await mcp__claude-flow__swarm_init({ topology: "star" });
```

---

## Agent Lifecycle

### 1. Spawning

```javascript
// Spawn single agent
await mcp__claude-flow__agent_spawn({
  type: "coder",
  name: "feature-developer",
  capabilities: ["react", "typescript", "graphql"]
});

// Spawn multiple agents
await Promise.all([
  mcp__claude-flow__agent_spawn({ type: "coder" }),
  mcp__claude-flow__agent_spawn({ type: "tester" }),
  mcp__claude-flow__agent_spawn({ type: "reviewer" })
]);
```

### 2. Task Assignment

```javascript
await mcp__claude-flow__task_orchestrate({
  task: "Implement user authentication with JWT",
  strategy: "adaptive",  // parallel, sequential, adaptive
  priority: "high",      // low, medium, high, critical
  maxAgents: 5
});
```

### 3. Monitoring

```javascript
// Get swarm status
const status = await mcp__claude-flow__swarm_status({
  swarmId: "swarm-123"
});

// List active agents
const agents = await mcp__claude-flow__agent_list({
  filter: "active"  // all, active, idle, busy
});

// Get agent metrics
const metrics = await mcp__claude-flow__agent_metrics({
  agentId: "coder-1"
});
```

### 4. Coordination

```bash
# Hooks for agent coordination
npx claude-flow@alpha hooks pre-task --description "Task description"
npx claude-flow@alpha hooks post-task --task-id "task-123"

# Memory coordination
npx claude-flow@alpha hooks post-edit --file "src/auth.js" --memory-key "swarm/coder/auth"
```

### 5. Cleanup

```javascript
// Scale down swarm
await mcp__claude-flow__swarm_scale({
  swarmId: "swarm-123",
  targetSize: 3
});

// Destroy swarm
await mcp__claude-flow__swarm_destroy({
  swarmId: "swarm-123"
});
```

---

## Memory Coordination

### Store Data

```javascript
await mcp__claude-flow__memory_usage({
  action: "store",
  key: "swarm/shared/api-schema",
  namespace: "coordination",
  value: JSON.stringify({
    endpoints: ["/users", "/posts", "/comments"],
    authentication: "jwt"
  }),
  ttl: 3600  // Optional: time-to-live in seconds
});
```

### Retrieve Data

```javascript
const data = await mcp__claude-flow__memory_usage({
  action: "retrieve",
  key: "swarm/shared/api-schema",
  namespace: "coordination"
});
```

### Search Memory

```javascript
const results = await mcp__claude-flow__memory_search({
  pattern: "swarm/coder/*",
  namespace: "coordination",
  limit: 10
});
```

### List Keys

```javascript
const keys = await mcp__claude-flow__memory_usage({
  action: "list",
  namespace: "coordination"
});
```

### Delete Data

```javascript
await mcp__claude-flow__memory_usage({
  action: "delete",
  key: "swarm/shared/old-data",
  namespace: "coordination"
});
```

---

## Neural Features

### Pattern Recognition

```javascript
// Analyze patterns
const patterns = await mcp__claude-flow__neural_patterns({
  action: "analyze",
  operation: "swarm-coordination",
  metadata: { topology: "mesh", agents: 5 }
});
```

### Learning

```javascript
// Train from successful operations
await mcp__claude-flow__neural_train({
  pattern_type: "coordination",
  training_data: JSON.stringify({
    operation: "feature-implementation",
    outcome: "success",
    metrics: { time: 120, quality: 0.95 }
  }),
  epochs: 50
});
```

### Prediction

```javascript
// Predict optimal configuration
const prediction = await mcp__claude-flow__neural_patterns({
  action: "predict",
  operation: "optimize-swarm",
  metadata: { task_complexity: "high", agents: 8 }
});
```

---

## Performance Monitoring

### Benchmarks

```javascript
const benchmarks = await mcp__claude-flow__benchmark_run({
  suite: "full",      // full, wasm, swarm, agent, task
  iterations: 10
});
```

### Bottleneck Analysis

```javascript
const bottlenecks = await mcp__claude-flow__bottleneck_analyze({
  component: "swarm-coordinator",
  metrics: ["response-time", "memory-usage", "cpu-usage"]
});
```

### Performance Reports

```javascript
const report = await mcp__claude-flow__performance_report({
  format: "detailed",     // summary, detailed, json
  timeframe: "7d"         // 24h, 7d, 30d
});
```

### Token Usage

```javascript
const usage = await mcp__claude-flow__token_usage({
  operation: "swarm-execution",
  timeframe: "24h"
});
```

---

## Best Practices

### 1. Choose Right Topology

```javascript
// Simple independent tasks → Star
await mcp__claude-flow__swarm_init({ topology: "star" });

// Collaborative work → Mesh
await mcp__claude-flow__swarm_init({ topology: "mesh" });

// Clear hierarchy → Hierarchical
await mcp__claude-flow__swarm_init({ topology: "hierarchical" });

// Sequential pipeline → Ring
await mcp__claude-flow__swarm_init({ topology: "ring" });
```

### 2. Use Appropriate Strategy

```javascript
// Balanced: General purpose
strategy: "balanced"

// Specialized: Domain-specific tasks
strategy: "specialized"

// Adaptive: Dynamic optimization
strategy: "adaptive"
```

### 3. Coordinate via Memory

```javascript
// Store decisions
await mcp__claude-flow__memory_usage({
  action: "store",
  key: "swarm/decisions/architecture",
  value: JSON.stringify({ framework: "express" })
});

// Other agents retrieve
const decisions = await mcp__claude-flow__memory_usage({
  action: "retrieve",
  key: "swarm/decisions/architecture"
});
```

### 4. Monitor Performance

```javascript
// Regular health checks
setInterval(async () => {
  const status = await mcp__claude-flow__swarm_status();
  if (status.activeAgents < 3) {
    await mcp__claude-flow__swarm_scale({ targetSize: 5 });
  }
}, 30000);
```

### 5. Use Hooks Consistently

```bash
# Always wrap operations
npx claude-flow@alpha hooks pre-task --description "Task"
# ... do work ...
npx claude-flow@alpha hooks post-task --task-id "task-id"
```

---

## See Also

- [MCP Tools Reference](./mcp-tools-reference.md) - Complete MCP tool catalog
- [Integration Guide](./INTEGRATION_GUIDE.md) - Step-by-step integration
- [CONTRIBUTING.md](../../CONTRIBUTING.md) - How to contribute
- [Architecture Documentation](../ARCHITECTURE.md) - System design

---

**Next Steps**: Explore the [MCP Tools Reference](./mcp-tools-reference.md) for complete tool documentation.
