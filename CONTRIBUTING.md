# Contributing to Claude Flow

> **Welcome!** We're excited you want to contribute to Claude Flow's multi-agent orchestration system.

## Overview

Claude Flow is an open-source project that brings multi-agent coordination, neural learning, and distributed workflows to Claude Code. We welcome contributions of all types: bug fixes, features, documentation, examples, and more.

## Key Concepts

- **Community-Driven** - Built by developers, for developers
- **Quality First** - All contributions undergo review and testing
- **Documentation Matters** - Code without docs is incomplete
- **Test Coverage** - New features require tests
- **Backwards Compatibility** - Breaking changes require major version bump

## Quick Start

### 1. Fork and Clone

```bash
# Fork the repository on GitHub
# Clone your fork
git clone https://github.com/YOUR_USERNAME/claude-flow.git
cd claude-flow

# Add upstream remote
git remote add upstream https://github.com/ruvnet/claude-flow.git
```

### 2. Install Dependencies

```bash
# Install Node.js dependencies
npm install

# Build the project
npm run build

# Run tests
npm test
```

### 3. Create a Branch

```bash
# Create feature branch
git checkout -b feature/your-feature-name

# Or bug fix branch
git checkout -b fix/bug-description
```

### 4. Make Changes

```bash
# Make your changes
# Write tests
# Update documentation

# Format code
npm run lint

# Type check
npm run typecheck

# Run tests
npm test
```

### 5. Commit and Push

```bash
# Stage changes
git add .

# Commit with descriptive message
git commit -m "feat: add support for custom agent types

- Add CustomAgent base class
- Implement agent registration system
- Add tests for custom agents
- Update documentation"

# Push to your fork
git push origin feature/your-feature-name
```

### 6. Create Pull Request

1. Go to your fork on GitHub
2. Click "New Pull Request"
3. Fill out the PR template
4. Submit for review

---

## Contribution Types

### Bug Fixes

Found a bug? We'd love your help fixing it!

**Steps**:
1. Search existing issues to avoid duplicates
2. Create new issue with bug report template
3. Fork and create fix branch: `fix/issue-123-description`
4. Write test that reproduces bug
5. Fix bug
6. Ensure test passes
7. Submit PR referencing issue

**Example**:
```typescript
// Before: Bug causes swarm to crash
async initSwarm(topology: string) {
  const swarm = new Swarm(topology);  // Crashes if topology invalid
  return swarm;
}

// After: Proper validation
async initSwarm(topology: string) {
  if (!VALID_TOPOLOGIES.includes(topology)) {
    throw new Error(`Invalid topology: ${topology}`);
  }
  const swarm = new Swarm(topology);
  return swarm;
}

// Test
test('should throw error for invalid topology', () => {
  expect(() => initSwarm('invalid')).toThrow('Invalid topology');
});
```

---

### New Features

Adding a new capability? Follow these guidelines.

**Requirements**:
- Feature request issue approved by maintainers
- Design document for major features
- Comprehensive tests (>80% coverage)
- Documentation updates
- Example usage

**Process**:
1. Create feature request issue
2. Discuss design with maintainers
3. Get approval before implementing
4. Create feature branch
5. Implement with tests
6. Update documentation
7. Add examples
8. Submit PR

**Example - New Agent Type**:
```typescript
// 1. Implement agent
export class CustomAnalyzerAgent extends BaseAgent {
  constructor(config: AnalyzerConfig) {
    super({ type: 'custom-analyzer', ...config });
  }

  async analyze(code: string): Promise<AnalysisResult> {
    // Implementation
  }
}

// 2. Add tests
describe('CustomAnalyzerAgent', () => {
  test('should analyze code correctly', async () => {
    const agent = new CustomAnalyzerAgent({ rules: [...] });
    const result = await agent.analyze('function test() {}');
    expect(result.issues).toHaveLength(0);
  });
});

// 3. Update documentation
// docs/agents/custom-analyzer.md

// 4. Add example
// examples/custom-analyzer-usage.js
```

---

### Documentation

Great documentation is as valuable as great code!

**Areas**:
- API reference documentation
- Guides and tutorials
- Code examples
- Architecture documentation
- Troubleshooting guides
- Video tutorials

**Guidelines**:
- Clear and concise writing
- Code examples for all features
- Screenshots for UI/UX
- Keep docs in sync with code
- Test all code examples

**Example**:
```markdown
# Custom Agent Tutorial

This guide shows how to create a custom agent for specialized tasks.

## Overview
Custom agents extend BaseAgent to add specialized capabilities.

## Implementation

### Step 1: Define Agent Class
\`\`\`typescript
class MyCustomAgent extends BaseAgent {
  async execute(task: Task): Promise<Result> {
    // Your logic here
  }
}
\`\`\`

### Step 2: Register Agent
\`\`\`typescript
AgentRegistry.register('my-custom', MyCustomAgent);
\`\`\`

## Example Usage
[Full working example...]

## See Also
- [BaseAgent API](./base-agent.md)
- [Agent Registry](./agent-registry.md)
```

---

### Tests

Tests ensure reliability and prevent regressions.

**Types**:
- **Unit Tests**: Individual functions/classes
- **Integration Tests**: Multiple components working together
- **E2E Tests**: Complete workflows
- **Performance Tests**: Benchmarks and profiling

**Requirements**:
- 80%+ code coverage for new code
- All tests must pass
- No flaky tests
- Fast execution (<5s for unit tests)

**Example**:
```typescript
// Unit test
describe('AgentCoordinator', () => {
  test('should spawn agent with correct config', async () => {
    const coordinator = new AgentCoordinator();
    const agent = await coordinator.spawn({
      type: 'coder',
      capabilities: ['nodejs']
    });

    expect(agent.type).toBe('coder');
    expect(agent.capabilities).toContain('nodejs');
  });
});

// Integration test
describe('Swarm Integration', () => {
  test('should coordinate multiple agents', async () => {
    const swarm = await initSwarm({ topology: 'mesh' });
    await swarm.spawn({ type: 'coder' });
    await swarm.spawn({ type: 'tester' });

    const result = await swarm.orchestrate({
      task: 'Build and test feature'
    });

    expect(result.status).toBe('completed');
  });
});
```

---

### Examples

Examples help users understand how to use features.

**Types**:
- Basic usage examples
- Advanced patterns
- Integration examples
- Real-world use cases
- Performance optimization examples

**Structure**:
```
examples/
├── basic/
│   ├── simple-swarm.js
│   ├── agent-spawning.js
│   └── task-orchestration.js
├── advanced/
│   ├── custom-agents.js
│   ├── neural-training.js
│   └── distributed-execution.js
└── real-world/
    ├── fullstack-app/
    ├── code-review-automation/
    └── ci-cd-pipeline/
```

**Example**:
```javascript
// examples/basic/simple-swarm.js

/**
 * Simple Swarm Example
 *
 * This example shows how to:
 * 1. Initialize a swarm
 * 2. Spawn agents
 * 3. Orchestrate a task
 */

const { initSwarm, spawnAgent, orchestrateTask } = require('claude-flow');

async function main() {
  // 1. Initialize swarm with mesh topology
  const swarm = await initSwarm({
    topology: 'mesh',
    maxAgents: 5
  });

  console.log('Swarm initialized:', swarm.id);

  // 2. Spawn specialized agents
  const coder = await spawnAgent({
    type: 'coder',
    capabilities: ['javascript', 'react']
  });

  const tester = await spawnAgent({
    type: 'tester',
    capabilities: ['jest', 'cypress']
  });

  console.log('Agents spawned:', [coder.id, tester.id]);

  // 3. Orchestrate task
  const result = await orchestrateTask({
    task: 'Create React component with tests',
    strategy: 'adaptive'
  });

  console.log('Task completed:', result);
}

main().catch(console.error);
```

---

## Code Style

### TypeScript/JavaScript

We use ESLint and Prettier for consistent code style.

**Key Rules**:
- Use TypeScript for all new code
- Prefer `const` over `let`, avoid `var`
- Use async/await over callbacks
- Descriptive variable names
- JSDoc comments for public APIs
- Maximum line length: 100 characters
- 2 spaces for indentation

**Example**:
```typescript
/**
 * Spawns a new agent in the swarm with specified capabilities.
 *
 * @param config - Agent configuration
 * @param config.type - Agent type (coder, tester, etc.)
 * @param config.capabilities - Array of agent capabilities
 * @returns Promise resolving to spawned agent
 * @throws {ValidationError} If config is invalid
 *
 * @example
 * const agent = await spawnAgent({
 *   type: 'coder',
 *   capabilities: ['nodejs', 'typescript']
 * });
 */
export async function spawnAgent(
  config: AgentConfig
): Promise<Agent> {
  // Validate config
  if (!config.type) {
    throw new ValidationError('Agent type is required');
  }

  // Create agent
  const agent = new Agent(config);
  await agent.initialize();

  return agent;
}
```

---

### Commit Messages

We follow [Conventional Commits](https://www.conventionalcommits.org/).

**Format**:
```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types**:
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation only
- `style`: Formatting, missing semicolons, etc.
- `refactor`: Code change that neither fixes a bug nor adds a feature
- `perf`: Performance improvement
- `test`: Adding missing tests
- `chore`: Updating build tasks, package manager configs, etc.

**Examples**:
```bash
# Feature
feat(agents): add custom agent registration system

Allow users to register custom agent types with AgentRegistry.
This enables extensibility for specialized use cases.

Closes #123

# Bug fix
fix(swarm): prevent crash on invalid topology

Add validation for topology parameter before initializing swarm.
Throw descriptive error for invalid values.

Fixes #456

# Documentation
docs(api): add examples for agent spawning

Add code examples and usage patterns for spawning agents
in different topologies.
```

---

## Pull Request Process

### PR Template

When creating a PR, fill out the template:

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix (non-breaking change which fixes an issue)
- [ ] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to change)
- [ ] Documentation update

## Testing
- [ ] Unit tests added/updated
- [ ] Integration tests added/updated
- [ ] All tests pass locally
- [ ] Test coverage maintained/improved

## Documentation
- [ ] README updated
- [ ] API documentation updated
- [ ] Examples added/updated
- [ ] CHANGELOG updated

## Checklist
- [ ] Code follows project style guidelines
- [ ] Self-review completed
- [ ] Comments added for complex logic
- [ ] No new warnings generated
- [ ] Dependent changes merged

## Related Issues
Fixes #123
Relates to #456

## Screenshots (if applicable)
[Add screenshots]

## Additional Notes
[Any additional information]
```

---

### Review Process

1. **Automated Checks**: CI runs tests, linting, type checking
2. **Code Review**: Maintainer reviews code quality and design
3. **Discussion**: Address feedback and questions
4. **Approval**: Get approval from at least one maintainer
5. **Merge**: Maintainer merges PR

**Review Criteria**:
- Code quality and style
- Test coverage
- Documentation completeness
- Performance impact
- Breaking changes justified
- Security considerations

---

## Development Workflow

### Setting Up Development Environment

```bash
# Clone repository
git clone https://github.com/ruvnet/claude-flow.git
cd claude-flow

# Install dependencies
npm install

# Build project
npm run build

# Watch mode for development
npm run dev

# Run tests
npm test

# Run tests in watch mode
npm run test:watch

# Run linting
npm run lint

# Fix linting issues
npm run lint:fix

# Type checking
npm run typecheck
```

---

### Testing Locally

```bash
# Build project
npm run build

# Link for local testing
npm link

# In another project
npm link claude-flow

# Test with Claude Code
claude mcp add claude-flow-local /path/to/claude-flow/dist/mcp.js
```

---

### Debugging

```bash
# Enable debug logging
export DEBUG=claude-flow:*

# Run with verbose output
npx claude-flow --verbose

# Debug specific module
export DEBUG=claude-flow:swarm

# Debug MCP server
npx claude-flow mcp start --debug
```

---

## Project Structure

```
claude-flow/
├── src/
│   ├── agents/          # Agent implementations
│   ├── coordination/    # Swarm coordination logic
│   ├── memory/          # Memory management
│   ├── neural/          # Neural features
│   ├── hooks/           # Hook system
│   ├── mcp/             # MCP server implementation
│   └── utils/           # Utility functions
├── tests/
│   ├── unit/            # Unit tests
│   ├── integration/     # Integration tests
│   └── e2e/             # End-to-end tests
├── docs/
│   ├── api/             # API documentation
│   ├── guides/          # User guides
│   └── examples/        # Code examples
├── examples/            # Example projects
├── scripts/             # Build and development scripts
└── .claude-flow/        # Claude Flow configuration
```

---

## Release Process

### Version Numbering

We use [Semantic Versioning](https://semver.org/):
- **MAJOR**: Breaking changes
- **MINOR**: New features (backwards compatible)
- **PATCH**: Bug fixes (backwards compatible)

### Release Checklist

- [ ] All tests pass
- [ ] Documentation updated
- [ ] CHANGELOG updated
- [ ] Version bumped in package.json
- [ ] Git tag created
- [ ] NPM package published
- [ ] GitHub release created
- [ ] Release notes published

---

## Communication

### Channels

- **GitHub Issues**: Bug reports, feature requests
- **GitHub Discussions**: Questions, ideas, showcases
- **Pull Requests**: Code contributions
- **Discord** (coming soon): Real-time chat

### Guidelines

- Be respectful and professional
- Search before posting
- Provide context and examples
- Follow up on your issues/PRs
- Help others when you can

---

## Getting Help

### Resources

- **Documentation**: https://github.com/ruvnet/claude-flow/tree/main/docs
- **Examples**: https://github.com/ruvnet/claude-flow/tree/main/examples
- **API Reference**: https://github.com/ruvnet/claude-flow/tree/main/docs/api
- **Issues**: https://github.com/ruvnet/claude-flow/issues
- **Discussions**: https://github.com/ruvnet/claude-flow/discussions

### Questions?

- Check documentation first
- Search existing issues/discussions
- Create new discussion for questions
- Create issue only for bugs/features

---

## Recognition

### Contributors

All contributors are recognized in:
- README.md contributors section
- GitHub contributors page
- Release notes

### Hall of Fame

Outstanding contributors may be invited to:
- Become project maintainers
- Join core team discussions
- Shape project roadmap

---

## Code of Conduct

### Our Pledge

We pledge to make participation in our project a harassment-free experience for everyone, regardless of age, body size, disability, ethnicity, gender identity and expression, level of experience, nationality, personal appearance, race, religion, or sexual identity and orientation.

### Our Standards

**Positive Behavior**:
- Using welcoming and inclusive language
- Being respectful of differing viewpoints
- Gracefully accepting constructive criticism
- Focusing on what is best for the community
- Showing empathy towards others

**Unacceptable Behavior**:
- Trolling, insulting/derogatory comments
- Public or private harassment
- Publishing others' private information
- Other conduct which could reasonably be considered inappropriate

### Enforcement

Violations may result in:
1. Warning
2. Temporary ban
3. Permanent ban

Report violations to: conduct@ruv.io

---

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

## See Also

- [Integration Guide](./docs/api/INTEGRATION_GUIDE.md) - How to use Claude Flow
- [Agent System Documentation](./docs/api/agent-system-documentation.md) - Agent architecture
- [MCP Tools Reference](./docs/api/mcp-tools-reference.md) - MCP tools catalog
- [Architecture Overview](./docs/ARCHITECTURE.md) - System design

---

## Thank You!

Thank you for contributing to Claude Flow! Your contributions help make multi-agent orchestration accessible to everyone.

**Questions?** Open a discussion: https://github.com/ruvnet/claude-flow/discussions

**Found a bug?** Open an issue: https://github.com/ruvnet/claude-flow/issues

**Ready to contribute?** Fork and submit a PR!

---

Built with ❤️ by the Claude Flow community
