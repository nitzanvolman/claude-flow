# Memory System Documentation

## Overview

Claude Flow features a hybrid memory system combining **AgentDB** (96x-164x faster vector search) with **ReasoningBank** (persistent SQLite storage) for optimal performance and reliability.

## Architecture

### Hybrid Memory Approach

```
┌─────────────────────────────────────────┐
│         Memory System (Hybrid)          │
├─────────────────────────────────────────┤
│  AgentDB (Primary - Vector Search)      │
│  • 96x-164x faster queries              │
│  • HNSW indexing (O(log n))             │
│  • 9 RL algorithms                      │
│  • Semantic understanding               │
├─────────────────────────────────────────┤
│  ReasoningBank (Fallback - SQLite)      │
│  • 2-3ms pattern search                 │
│  • Persistent storage (.swarm/memory.db)│
│  • 100% backward compatible             │
│  • No API keys required                 │
└─────────────────────────────────────────┘
```

## Quick Start

### AgentDB (Recommended)

```bash
# Install AgentDB integration
npm install agentdb@1.3.9

# Semantic vector search
npx claude-flow@alpha memory vector-search "user authentication flow" \
  --k 10 --threshold 0.7 --namespace backend

# Store with vector embedding
npx claude-flow@alpha memory store-vector api_design "REST endpoints" \
  --namespace backend --metadata '{"version":"v2"}'

# Check AgentDB status
npx claude-flow@alpha memory agentdb-info
```

### ReasoningBank (Legacy)

```bash
# Store memories
npx claude-flow@alpha memory store api_key "REST API configuration" \
  --namespace backend --reasoningbank

# Query with pattern search
npx claude-flow@alpha memory query "API config" \
  --namespace backend --reasoningbank

# List all memories
npx claude-flow@alpha memory list --namespace backend --reasoningbank
```

## AgentDB Features

### Performance Improvements

- **Vector Search**: 96x faster (9.6ms → <0.1ms)
- **Batch Operations**: 125x faster
- **Large Queries**: 164x faster
- **Memory Usage**: 4-32x reduction via quantization

### Advanced Capabilities

1. **Semantic Vector Search**: HNSW indexing with O(log n) complexity
2. **9 RL Algorithms**: Q-Learning, PPO, MCTS, Decision Transformer, etc.
3. **Reflexion Memory**: Learn from past experiences
4. **Skill Library**: Auto-consolidate successful patterns
5. **Causal Reasoning**: Understand cause-effect relationships
6. **Quantization**: Binary (32x), Scalar (4x), Product (8-16x) reduction

### Usage Examples

```bash
# Semantic search with threshold
npx claude-flow@alpha memory vector-search "authentication" \
  --k 5 --threshold 0.8

# Store with metadata
npx claude-flow@alpha memory store-vector user_auth "JWT implementation" \
  --namespace security --metadata '{"lang":"typescript","version":"v2"}'

# Batch operations
npx claude-flow@alpha memory batch-store \
  --file ./memories.json --namespace project
```

## ReasoningBank Features

### Core Capabilities

1. **Persistent Storage**: SQLite database (.swarm/memory.db)
2. **Pattern Matching**: LIKE-based search with similarity scoring
3. **Namespace Isolation**: Organize memories by domain
4. **Fast Queries**: 2-3ms average latency
5. **No API Keys**: Hash-based embeddings (1024 dimensions)

### Usage Examples

```bash
# Store with namespace
npx claude-flow@alpha memory store config "API settings" \
  --namespace backend --reasoningbank

# Query recent memories
npx claude-flow@alpha memory query "API" --recent --reasoningbank

# List all namespaces
npx claude-flow@alpha memory list-namespaces --reasoningbank

# Check status
npx claude-flow@alpha memory status --reasoningbank
```

## CLI Commands Reference

### Storage Commands

```bash
# Store memory
npx claude-flow@alpha memory store <key> <value> \
  [--namespace <ns>] [--reasoningbank|--agentdb]

# Store with vector embedding (AgentDB only)
npx claude-flow@alpha memory store-vector <key> <value> \
  [--namespace <ns>] [--metadata <json>]

# Batch store from file
npx claude-flow@alpha memory batch-store \
  --file <path> --namespace <ns>
```

### Query Commands

```bash
# Query memories (pattern search)
npx claude-flow@alpha memory query <query> \
  [--namespace <ns>] [--recent] [--reasoningbank]

# Vector search (semantic understanding)
npx claude-flow@alpha memory vector-search <query> \
  [--k <num>] [--threshold <0-1>] [--namespace <ns>]

# List all memories
npx claude-flow@alpha memory list \
  [--namespace <ns>] [--reasoningbank]
```

### Management Commands

```bash
# Check status
npx claude-flow@alpha memory status [--reasoningbank|--agentdb]

# Get AgentDB info
npx claude-flow@alpha memory agentdb-info

# List namespaces
npx claude-flow@alpha memory list-namespaces

# Clear namespace
npx claude-flow@alpha memory clear --namespace <ns>
```

## MCP Tool Integration

### Memory Tools

```javascript
// Store memory
mcp__claude-flow__memory_usage {
  action: "store",
  key: "project/config",
  namespace: "backend",
  value: JSON.stringify({ apiVersion: "v2" }),
  ttl: 3600000
}

// Retrieve memory
mcp__claude-flow__memory_usage {
  action: "retrieve",
  key: "project/config",
  namespace: "backend"
}

// Search memories
mcp__claude-flow__memory_search {
  pattern: "config",
  namespace: "backend",
  limit: 10
}
```

## Performance Comparison

| Feature | AgentDB | ReasoningBank |
|---------|---------|---------------|
| **Vector Search** | 96x faster | N/A |
| **Query Latency** | <0.1ms | 2-3ms |
| **Semantic Understanding** | ✅ Yes | ❌ Pattern matching only |
| **Memory Reduction** | 4-32x | Standard |
| **API Keys Required** | Optional | ❌ No |
| **Storage** | In-memory + SQLite | SQLite only |
| **Backward Compatible** | ✅ 100% | ✅ Native |

## Best Practices

### When to Use AgentDB

- Semantic search required
- Large-scale memory queries
- Performance-critical applications
- Machine learning integration
- Complex pattern recognition

### When to Use ReasoningBank

- Simple pattern matching
- No external dependencies
- Offline environments
- Legacy compatibility
- Quick prototyping

## Documentation Links

- **[AgentDB Production Guide](./agentdb/PRODUCTION_READINESS.md)** - Deployment guide
- **[AgentDB Implementation](./agentdb/SWARM_IMPLEMENTATION_COMPLETE.md)** - Technical details
- **[Backward Compatibility](./agentdb/BACKWARD_COMPATIBILITY_GUARANTEE.md)** - Compatibility guarantee
- **[ReasoningBank Guide](./guides/REASONINGBANK.md)** - Legacy system documentation

## Troubleshooting

### Common Issues

**Issue**: AgentDB not installed
```bash
# Solution: Install AgentDB
npm install agentdb@1.3.9
```

**Issue**: Memory not persisting
```bash
# Solution: Check database location
ls -la .swarm/memory.db
npx claude-flow@alpha memory status
```

**Issue**: Vector search returns 0 results
```bash
# Solution: Check namespace and threshold
npx claude-flow@alpha memory vector-search "query" \
  --namespace correct-namespace --threshold 0.5
```

## Additional Resources

- **[MCP Tools Reference](./MCP-TOOLS.md)** - Memory tool specifications
- **[Agent System](./AGENT-SYSTEM.md)** - Agent memory coordination
- **[Performance Metrics](./performance/PERFORMANCE-METRICS-GUIDE.md)** - Memory performance tracking
