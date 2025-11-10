# CLAUDE.md Template Guide

> **Navigation Hub** - This document links to detailed CLAUDE.md template documentation

## Quick Overview
CLAUDE.md configuration files provide project-specific instructions for Claude Code and Claude Flow. These files enable custom agent behavior, workflow automation, and project-specific best practices that override default behavior.

## Detailed Documentation
- [CLAUDE.md Specification](./guides/CLAUDE-MD-SPEC.md)
- [Template Library](./templates/CLAUDE-MD-TEMPLATES.md)
- [Configuration Guide](./guides/CLAUDE-MD-CONFIG.md)
- [Best Practices](./guides/CLAUDE-MD-BEST-PRACTICES.md)

## Quick Start

### Basic CLAUDE.md Structure

```markdown
# Project Name Configuration

## 🚨 CRITICAL RULES
[Absolute rules that MUST be followed]

## Project Overview
[Project description and context]

## Development Workflow
[Preferred workflows and methodologies]

## Code Style & Standards
[Coding standards and conventions]

## Available Tools & Commands
[Project-specific commands and tools]

## Agent Configuration
[Agent preferences and coordination patterns]

## Integration Tips
[Tips for working with the project]
```

### Template Categories

**Framework-Specific**
- React/Next.js projects
- Node.js/Express backends
- Python/FastAPI services
- Mobile development (React Native, Flutter)
- Machine learning projects

**Methodology-Specific**
- SPARC development
- TDD workflows
- Agile/Scrum projects
- Microservices architecture
- Monorepo management

**Team-Specific**
- Startup rapid development
- Enterprise compliance
- Open source projects
- Research projects
- Educational projects

### Common CLAUDE.md Patterns

**1. File Organization Rules**
```markdown
## 📁 File Organization
NEVER save to root folder. Use:
- `/src` - Source code
- `/tests` - Test files
- `/docs` - Documentation
- `/config` - Configuration
```

**2. Agent Coordination**
```markdown
## 🤖 Agent Configuration
Use mesh topology for this project.
Required agents: researcher, coder, tester, reviewer
Hooks: ALWAYS use pre-task and post-edit
Memory namespace: project-name
```

**3. Code Standards**
```markdown
## 💻 Code Style
- TypeScript strict mode required
- ESLint + Prettier formatting
- Jest for unit tests (>80% coverage)
- Conventional commits
- API documentation required
```

**4. Workflow Automation**
```markdown
## 🔄 Automated Workflows
On every commit:
1. Run linting (auto-fix)
2. Execute tests
3. Type checking
4. Format code
5. Update documentation
```

### Create Custom CLAUDE.md

```bash
# Generate template
npx claude-flow@alpha config generate --template react-fullstack

# Validate CLAUDE.md
npx claude-flow@alpha config validate

# Preview configuration
npx claude-flow@alpha config preview
```

### Template Variables

CLAUDE.md files support dynamic variables:

```markdown
## Project: {{PROJECT_NAME}}
Repository: {{REPO_URL}}
Version: {{VERSION}}
Environment: {{NODE_ENV}}

## Team
Lead: {{TECH_LEAD}}
Reviewers: {{CODE_REVIEWERS}}
```

### Integration with Claude Flow

**Automatic Loading**
- Claude Code reads CLAUDE.md on startup
- Instructions override default behavior
- Project-specific agents auto-configured

**Hooks Integration**
```bash
# CLAUDE.md configures hooks behavior
npx claude-flow@alpha hooks pre-task  # Reads CLAUDE.md rules
```

**Agent Spawning**
```javascript
// Agents follow CLAUDE.md configuration
Task("Coder", "Follow CLAUDE.md standards", "coder")
```

## Example Templates

### 1. Full-Stack Web Application
```markdown
# Full-Stack Application - CLAUDE.md

## Stack
- Frontend: React + TypeScript
- Backend: Node.js + Express
- Database: PostgreSQL
- Testing: Jest + Cypress

## Critical Rules
- NEVER commit secrets
- API versioning required (/api/v1/)
- Database migrations for all schema changes
- E2E tests for critical paths

## Agent Configuration
Topology: hierarchical
Agents: backend-dev, coder, tester, reviewer, api-docs
```

### 2. Machine Learning Project
```markdown
# ML Project - CLAUDE.md

## Stack
- Framework: PyTorch
- Data: Pandas + NumPy
- Visualization: Matplotlib
- Tracking: MLflow

## Critical Rules
- Data versioning with DVC
- Experiment tracking required
- Model versioning
- Reproducible seeds

## Agent Configuration
Agents: ml-developer, researcher, code-analyzer, tester
```

### 3. Microservices Architecture
```markdown
# Microservices - CLAUDE.md

## Architecture
- Services: 12 microservices
- Communication: gRPC + Kafka
- Orchestration: Kubernetes
- Service mesh: Istio

## Critical Rules
- Service independence
- Contract testing required
- Distributed tracing
- Circuit breakers

## Agent Configuration
Topology: mesh
Agents: backend-dev, system-architect, cicd-engineer, tester
```

## Best Practices

**DO:**
- Keep rules clear and concise
- Use hierarchical structure
- Include examples
- Document automation
- Version control CLAUDE.md

**DON'T:**
- Make rules too rigid
- Duplicate default behavior
- Include secrets
- Overcomplicate structure

## See Also
- [Configuration Guide](./CONFIGURATION.md)
- [Agent System](./AGENT-SYSTEM.md)
- [Hooks System](./HOOKS-SYSTEM.md)
- [Project Templates](./templates/PROJECT-TEMPLATES.md)
