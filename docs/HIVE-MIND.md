# Hive Mind System Hub

> **Navigation Hub** - This document links to detailed Hive Mind documentation

## Quick Overview
The Hive Mind system enables collective intelligence coordination with queen-led hierarchies, consensus mechanisms, and persistent memory. Multiple hives can operate independently or collaborate, with agents sharing knowledge and making distributed decisions.

## Detailed Documentation
- [Hive Mind Architecture](./architecture/HIVE-MIND-ARCHITECTURE.md)
- [Queen Agent System](./guides/QUEEN-AGENTS.md)
- [Consensus Mechanisms](./guides/CONSENSUS-MECHANISMS.md)
- [Collective Memory](./guides/COLLECTIVE-MEMORY.md)

## Quick Start

### Hive Mind Commands

```bash
# Create new hive with queen
npx claude-flow@alpha hive-mind init --name research-hive --queen-role coordinator

# List active hives
npx claude-flow@alpha hive-mind list

# Get hive status
npx claude-flow@alpha hive-mind status --hive-id hive-123

# Stop hive
npx claude-flow@alpha hive-mind stop --hive-id hive-123

# Resume hive
npx claude-flow@alpha hive-mind resume --hive-id hive-123

# Interactive setup wizard
npx claude-flow@alpha hive-mind wizard
```

### Hive Mind Slash Commands

```bash
# Initialize hive mind
/hive-mind

# Setup wizard
/hive-mind-wizard

# List all sessions
/hive-mind-sessions

# Stop specific hive
/hive-mind-stop <hive-id>

# Resume hive
/hive-mind-resume <hive-id>
```

### Hive Architecture

**Queen Agent** - Central coordinator and decision maker
**Worker Agents** - Specialized task executors
**Consensus Layer** - Distributed agreement system
**Collective Memory** - Shared knowledge store
**Communication Bus** - Inter-agent messaging

### Create Hive with Queen

```javascript
// Initialize hive with queen agent
Task("Queen Coordinator", `
  Role: Hive mind queen coordinator

  Responsibilities:
  - Coordinate worker agents
  - Make strategic decisions
  - Maintain collective memory
  - Facilitate consensus
  - Monitor hive health

  Initialize hive with 5 worker agents:
  - Research specialist
  - Code implementation
  - Testing validation
  - Documentation
  - Performance optimization

  Use consensus for major decisions.
  Store all decisions in collective memory.
`, "collective-intelligence-coordinator")
```

### Consensus Mechanisms

**Byzantine Fault Tolerance**
- Tolerates malicious agents
- 3f+1 agents required for f failures
- Cryptographic verification

**Raft Consensus**
- Leader election
- Log replication
- Strong consistency guarantees

**Gossip Protocol**
- Epidemic information spread
- Eventually consistent
- High scalability

**Quorum-Based**
- Majority voting
- Fast decisions
- Trade-off consistency

### Collective Memory System

```bash
# Store in collective memory
npx claude-flow@alpha hooks post-edit \
  --file "feature.js" \
  --memory-key "hive/collective/feature-implementation"

# Query collective memory
npx claude-flow@alpha memory search \
  --pattern "hive/collective/*" \
  --namespace "coordination"
```

### MCP Integration

```javascript
// Initialize hive coordination
mcp__claude-flow__swarm_init {
  topology: "hierarchical",
  maxAgents: 10,
  strategy: "collective-intelligence"
}

// Spawn queen coordinator
mcp__claude-flow__agent_spawn {
  type: "collective-intelligence-coordinator",
  name: "queen-agent",
  capabilities: ["decision-making", "consensus", "coordination"]
}

// Orchestrate collective task
mcp__claude-flow__task_orchestrate {
  task: "complex-feature-development",
  strategy: "adaptive",
  priority: "high"
}
```

## Advanced Features

### Multi-Hive Collaboration
- Cross-hive communication
- Resource sharing
- Knowledge transfer
- Coordinated execution

### Autonomous Decision Making
- Queen agent autonomy
- Worker specialization
- Dynamic role assignment
- Self-organization

### Persistent Memory
- Cross-session continuity
- Knowledge accumulation
- Pattern recognition
- Historical analysis

### Health Monitoring
- Agent performance tracking
- Consensus health metrics
- Memory usage optimization
- Automatic recovery

## Use Cases

**Large-Scale Development**
- Multiple feature teams
- Cross-component coordination
- Shared architecture decisions

**Research Projects**
- Distributed investigation
- Knowledge synthesis
- Collective analysis

**Complex Workflows**
- Multi-stage pipelines
- Parallel execution paths
- Dependency management

## See Also
- [Agent System](./AGENT-SYSTEM.md)
- [Consensus Protocols](./guides/CONSENSUS-PROTOCOLS.md)
- [Byzantine Coordination](./guides/BYZANTINE-COORDINATION.md)
- [Swarm Orchestration](./guides/SWARM-ORCHESTRATION.md)
