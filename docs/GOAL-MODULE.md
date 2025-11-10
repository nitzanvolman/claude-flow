# GOAP Planning Guide

> **Navigation Hub** - This document links to detailed GOAP module documentation

## Quick Overview
Goal-Oriented Action Planning (GOAP) enables autonomous agents to dynamically plan and execute complex workflows. The system automatically generates action sequences to achieve goals, adapts to changing conditions, and optimizes paths using A* search.

## Detailed Documentation
- [GOAP Architecture](./architecture/GOAP-ARCHITECTURE.md)
- [Planning Algorithms](./guides/GOAP-PLANNING.md)
- [Action System](./api/GOAP-ACTIONS.md)
- [Integration Guide](./guides/GOAP-INTEGRATION.md)

## Quick Start

### GOAP Concepts

**Goals** - Desired world states to achieve
**Actions** - Operations that change world state
**Preconditions** - Requirements for action execution
**Effects** - Changes actions make to world state
**Planner** - A* search to find optimal action sequence

### Define Goals and Actions

```javascript
// Define a goal
const goal = {
  name: "deploy-application",
  conditions: {
    testsPass: true,
    buildComplete: true,
    deployed: true
  }
};

// Define actions
const actions = [
  {
    name: "run-tests",
    preconditions: { codeComplete: true },
    effects: { testsPass: true },
    cost: 2
  },
  {
    name: "build-project",
    preconditions: { testsPass: true },
    effects: { buildComplete: true },
    cost: 3
  },
  {
    name: "deploy-app",
    preconditions: { buildComplete: true },
    effects: { deployed: true },
    cost: 5
  }
];
```

### CLI Usage

```bash
# Create GOAP plan
npx claude-flow@alpha goap plan --goal deploy-application --world-state initial-state.json

# Execute GOAP workflow
npx claude-flow@alpha goap execute --plan plan.json

# Analyze plan efficiency
npx claude-flow@alpha goap analyze --plan plan.json
```

### Integration with Agents

```javascript
// Autonomous agent with GOAP planning
Task("GOAP Planner Agent", `
  Goal: Deploy application with zero downtime

  Available actions:
  - run-unit-tests
  - run-integration-tests
  - build-docker-image
  - push-to-registry
  - update-kubernetes-deployment
  - health-check-services
  - rollback-deployment

  World state:
  - code-changes: true
  - tests-pass: false
  - image-built: false
  - deployment-ready: false

  Use GOAP to plan and execute optimal deployment sequence.
  Adapt if any step fails (e.g., auto-rollback on health check failure).
`, "planner")
```

### GOAP with MCP Tools

```javascript
// Store GOAP state in memory
mcp__claude-flow__memory_usage {
  action: "store",
  key: "goap/world-state",
  namespace: "planning",
  value: JSON.stringify({
    currentState: { testsPass: true, buildComplete: false },
    plan: ["build-project", "deploy-app"],
    goalAchieved: false
  })
}

// Retrieve planning context
mcp__claude-flow__memory_usage {
  action: "retrieve",
  key: "goap/world-state",
  namespace: "planning"
}
```

## Advanced Features

### Dynamic Replanning
- Monitors world state changes
- Automatically replans when preconditions fail
- Adapts to unexpected conditions

### Multi-Agent GOAP
- Agents share world state
- Coordinate action execution
- Avoid conflicting operations

### Cost Optimization
- A* search for optimal paths
- Custom cost functions
- Heuristic-based planning

### Hierarchical Goals
- Break complex goals into subgoals
- Nested planning structures
- Incremental achievement tracking

## Use Cases

**DevOps Automation**
- Deployment pipelines
- Infrastructure provisioning
- Incident response

**Development Workflows**
- Feature implementation
- Bug fixing sequences
- Code refactoring

**Testing Strategies**
- Test execution order
- Test coverage optimization
- Regression testing

## See Also
- [Neural Module](./NEURAL-MODULE.md)
- [Agent System](./AGENT-SYSTEM.md)
- [DAA Autonomous Agents](./guides/DAA-AGENTS.md)
- [Workflow Automation](./guides/WORKFLOW-AUTOMATION.md)
