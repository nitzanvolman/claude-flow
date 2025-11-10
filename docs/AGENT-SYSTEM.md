# Agent System Guide

> **Navigation Hub** - This document links to detailed agent system documentation

## Quick Overview
Claude Flow's agent system provides 54+ specialized agents for development workflows. Agents coordinate through hooks, memory, and swarm topologies to execute complex multi-agent tasks with autonomous collaboration.

## Detailed Documentation
- [Agent Architecture](./architecture/AGENT-ARCHITECTURE.md)
- [Agent Types Reference](./api/AGENT-TYPES.md)
- [Coordination Protocols](./guides/AGENT-COORDINATION.md)
- [Custom Agent Creation](./guides/CUSTOM-AGENTS.md)

## Quick Start

### Available Agent Categories (54 Total)

**Core Development**
- `coder` - Implementation and code generation
- `reviewer` - Code review and quality assurance
- `tester` - Test creation and validation
- `planner` - Task breakdown and planning
- `researcher` - Requirements analysis and research

**Swarm Coordination**
- `hierarchical-coordinator` - Tree-based coordination
- `mesh-coordinator` - Peer-to-peer coordination
- `adaptive-coordinator` - Dynamic topology switching
- `collective-intelligence-coordinator` - Distributed decision-making
- `swarm-memory-manager` - Shared memory coordination

**Consensus & Distributed**
- `byzantine-coordinator` - Byzantine fault tolerance
- `raft-manager` - Raft consensus protocol
- `gossip-coordinator` - Gossip protocol coordination
- `consensus-builder` - Multi-agent consensus
- `crdt-synchronizer` - Conflict-free replication
- `quorum-manager` - Quorum-based decisions
- `security-manager` - Security validation

**Performance & Optimization**
- `perf-analyzer` - Performance analysis
- `performance-benchmarker` - Benchmark execution
- `task-orchestrator` - Task orchestration
- `memory-coordinator` - Memory optimization
- `smart-agent` - Autonomous agent behavior

**GitHub & Repository**
- `github-modes` - GitHub workflow automation
- `pr-manager` - Pull request management
- `code-review-swarm` - Multi-agent code review
- `issue-tracker` - Issue tracking and triage
- `release-manager` - Release coordination
- `workflow-automation` - CI/CD automation
- `project-board-sync` - Project board management
- `repo-architect` - Repository architecture
- `multi-repo-swarm` - Multi-repository coordination

**SPARC Methodology**
- `sparc-coord` - SPARC workflow coordination
- `sparc-coder` - SPARC-based implementation
- `specification` - Requirements specification
- `pseudocode` - Algorithm design
- `architecture` - System architecture
- `refinement` - TDD refinement

**Specialized Development**
- `backend-dev` - Backend development
- `mobile-dev` - Mobile development
- `ml-developer` - Machine learning development
- `cicd-engineer` - CI/CD pipeline engineering
- `api-docs` - API documentation
- `system-architect` - System architecture design
- `code-analyzer` - Code analysis and metrics
- `base-template-generator` - Template generation

**Testing & Validation**
- `tdd-london-swarm` - London-style TDD
- `production-validator` - Production validation

**Migration & Planning**
- `migration-planner` - Migration planning
- `swarm-init` - Swarm initialization

### Spawning Agents with Claude Code Task Tool

```javascript
// Single message with parallel agent execution
[Parallel Execution]:
  Task("Research agent", "Analyze API requirements", "researcher")
  Task("Architect agent", "Design system architecture", "system-architect")
  Task("Coder agent", "Implement backend services", "backend-dev")
  Task("Tester agent", "Create test suite", "tester")
  Task("Reviewer agent", "Review code quality", "reviewer")
```

### Agent Coordination Protocol

**Every agent MUST execute hooks:**

```bash
# Before work
npx claude-flow@alpha hooks pre-task --description "task"
npx claude-flow@alpha hooks session-restore --session-id "swarm-id"

# During work
npx claude-flow@alpha hooks post-edit --file "file.js" --memory-key "swarm/agent/step"
npx claude-flow@alpha hooks notify --message "progress update"

# After work
npx claude-flow@alpha hooks post-task --task-id "task"
npx claude-flow@alpha hooks session-end --export-metrics true
```

## Swarm Topologies

**Hierarchical** - Tree structure with coordinators
**Mesh** - Peer-to-peer collaboration
**Ring** - Circular message passing
**Star** - Central coordinator with workers

## See Also
- [Swarm Coordination](./guides/SWARM-COORDINATION.md)
- [Hooks System](./HOOKS-SYSTEM.md)
- [Memory Management](./guides/MEMORY-MANAGEMENT.md)
- [Neural Module](./NEURAL-MODULE.md)
