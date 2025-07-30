# A5C GitHub Action

A flexible GitHub Action for automated agent-based code operations using various CLI tools like Claude, Aider, and Cursor.

## Features

- **Unified Resource Handler**: Robust loading of prompts, agents, and configurations from local files, HTTP/HTTPS URLs, and file:// URIs with caching and retry logic
- **Multiple CLI Tool Support**: Configurable templates for Claude, Aider, Cursor, and custom tools
- **Agent Discovery**: Automatic agent detection and routing based on events and mentions
- **Remote Agent Support**: Load agents from remote repositories and individual URLs
- **Built-in MCP Servers**: Filesystem, memory, time, search, and GitHub integration built into the action
- **Schedule-based Activation**: Cron-based agent triggering for automated workflows
- **MCP Server Integration**: Support for Model Context Protocol servers with configurable server selection
- **Flexible Configuration**: Hierarchical configuration with built-in defaults and user overrides
- **Mention-based Triggering**: Agents triggered by specific mentions in comments (serial execution by appearance order)
- **Event-based Triggering**: Agents triggered by GitHub events (execution by priority)
- **Structured Output Processing**: Intelligent extraction of structured data from agent responses

## Quick Start

1. **Create the directory structure**:
   ```bash
   mkdir -p .a5c/agents
   ```

2. **Create a configuration file** (`.a5c/config.yml`):
   ```yaml
   defaults:
     cli_command: "cat {{prompt_path}} | claude {{#if mcp_config}}--mcp-config {{mcp_config}}{{/if}} -p 'fulfill the request'"
     
   file_processing:
     include_patterns:
       - "*.js"
       - "*.ts"
       - "*.py"
     exclude_patterns:
       - "node_modules/**"
       - "*.test.js"
   
   # Optional: Remote agents configuration
   remote_agents:
     enabled: true
     cache_timeout: 120     # Cache timeout in minutes (2 hours)
     retry_attempts: 5      # Number of retry attempts
     retry_delay: 2000      # Delay between retries in milliseconds
     sources:
       individual:
         - uri: "https://raw.githubusercontent.com/myorg/agents/main/security-scanner.agent.md"
           alias: "remote-security"
         - uri: "https://raw.githubusercontent.com/myorg/private-agents/main/proprietary-scanner.agent.md"
           alias: "private-scanner"
       repositories:
         - uri: "https://github.com/myorg/shared-agents"
           pattern: "agents/**/*.agent.md"
         - uri: "https://github.com/myorg/private-agents"
           pattern: ".a5c/agents/**/*.agent.md"
   ```

3. **Optional: Create additional MCP servers config** (`.a5c/mcps.json`):
   ```json
   {
     "mcpServers": {
       "database": {
         "command": "npx",
         "args": ["-y", "@myorg/mcp-server-database"],
         "env": {
           "DATABASE_URL": "${DATABASE_URL}"
         }
       },
       "slack": {
         "command": "npx", 
         "args": ["-y", "@modelcontextprotocol/server-slack"],
         "env": {
           "SLACK_BOT_TOKEN": "${SLACK_BOT_TOKEN}"
         }
       }
     }
   }
   ```

4. **Create an agent** (`.a5c/agents/code-reviewer.agent.md`):
   ```markdown
   ---
   # Agent Metadata
   name: code-reviewer
   version: 1.0.0
   category: code-review
   description: AI-powered code review agent
   
   # Usage Context
   usage_context: |
     Use for comprehensive code reviews on pull requests and significant changes.
     Performs security analysis, quality assessment, and best practices validation.
   
   # Invocation Context
   invocation_context: |
     Invoke with pull request context, changed files, and diff information.
     Needs repository access and GitHub API permissions.
   
   # Execution Configuration
   max_turns: 10
   timeout: 15
   
   # MCP Server Configuration
   mcp_servers: ["filesystem", "memory", "github"]
   
   # Mention Activation
   mentions: "@code-reviewer,@review,@code-review"
   
   # Priority
   priority: 10
   ---
   
   Please review this code for:
   - Code quality and best practices
   - Security vulnerabilities
   - Performance issues
   - Documentation completeness
   ```

5. **Add the workflow** (`.github/workflows/a5c.yml`):
   ```yaml
   name: A5C Agent System
   on:
     pull_request:
       types: [opened, synchronize]
     issue_comment:
       types: [created]
   
   jobs:
     run-agents:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v3
         - name: Run A5C Agents
           uses: ./path/to/a5c-githubaction
           with:
             github_token: ${{ secrets.GITHUB_TOKEN }}
             config_file: ".a5c/config.yml"
   ```

   **Using Remote Configuration and Agents:**
   ```yaml
   name: A5C Agent System with Remote Config and Agents
   on:
     pull_request:
       types: [opened, synchronize]
     issue_comment:
       types: [created]
   
   jobs:
     run-agents:
       runs-on: ubuntu-latest
       permissions:
         contents: read
         issues: write
         pull-requests: write
         # For private repositories containing agents:
         actions: read
         metadata: read
       steps:
         - uses: actions/checkout@v3
         - name: Run A5C Agents with Remote Config and Agents
           uses: ./path/to/a5c-githubaction
           with:
             github_token: ${{ secrets.GITHUB_TOKEN }}
             config_uri: "https://raw.githubusercontent.com/myorg/shared-config/main/a5c-config.yml"
   ```

   **Note:** For private repositories containing agents, ensure your `GITHUB_TOKEN` has the `repo` scope. The default `GITHUB_TOKEN` in GitHub Actions has sufficient permissions for public repositories but may need additional permissions for private repositories.

## Architecture

The system has been refactored into focused modules:

### Core Components

- **Resource Handler** (`src/resource-handler.js`): Unified resource loading with caching and retry logic
- **Agent Router** (`agent-router.js`): Agent discovery and routing logic
- **Configuration Manager** (`src/config.js`): Hierarchical configuration merging
- **Prompt Engine** (`src/prompt.js`): Template-based prompt generation
- **Agent Execution** (`src/agent-execution.js`): CLI tool execution and response handling
- **Output Processor** (`src/output-processor.js`): Structured data extraction and formatting
- **MCP Manager** (`src/mcp-manager.js`): Built-in and user-defined MCP server management
- **Utilities** (`src/utils.js`): Common utility functions and helpers

### Configuration System

The configuration system uses a hierarchical approach:
1. Built-in defaults (`default-config.yml`)
2. User configuration (`.a5c/config.yml` or remote URI)
3. Agent-specific configuration (frontmatter in agent files)

#### Remote Configuration

Configuration files can be loaded from remote repositories, including private repositories with proper authentication:

```yaml
# .github/workflows/a5c.yml
- name: Run A5C with Remote Config
  uses: ./
  with:
    config_uri: "https://raw.githubusercontent.com/myorg/shared-config/main/a5c-config.yml"
    github_token: ${{ secrets.GITHUB_TOKEN }}
```

**Supported URI formats:**
- `https://raw.githubusercontent.com/org/repo/branch/path/config.yml` - GitHub raw files
- `https://github.com/org/repo/raw/branch/path/config.yml` - GitHub raw files (alternative)
- `https://api.github.com/repos/org/repo/contents/path/config.yml` - GitHub API (auto-decoded)
- `https://your-domain.com/path/config.yml` - Any HTTPS URL
- `file:///absolute/path/config.yml` - Local file paths

**Authentication:**
- **GitHub repositories**: Automatic authentication using `GITHUB_TOKEN`
- **Private repositories**: Requires `GITHUB_TOKEN` with appropriate permissions
- **GitHub Enterprise**: Supported with proper token configuration
- **Custom domains**: No authentication (public URLs only)

**Features:**
- **Caching**: Remote configs are cached to reduce API calls
- **Retry logic**: Automatic retry on failures with exponential backoff
- **Fallback**: Falls back to local config if remote loading fails

### Agent Discovery

The system automatically discovers agents from:
- **Local agents**: `.a5c/agents/` directory (including subdirectories)
- **Remote agents**: Individual URLs or entire repositories
- **Pattern matching**: All `*.agent.md` files are automatically detected

**Agent Discovery Features:**
- **Cross-agent context**: Agents can discover and reference other agents in their prompts
- **Local + Remote support**: Discovery works across both local and remote agents
- **Category-based discovery**: Agents from the same category are automatically included
- **Explicit inclusion**: Agents can explicitly include specific other agents by ID
- **Configurable limits**: Maximum number of agents in discovery context is configurable

**Directory Structure:**
```
your-repo/
├── .a5c/
│   ├── config.yml
│   ├── mcps.json                    # Optional: Additional MCP servers
│   └── agents/
│       ├── code-reviewer.agent.md
│       ├── security/
│       │   ├── security-scanner.agent.md
│       │   └── vulnerability-checker.agent.md
│       └── deployment/
│           └── deployment-agent.agent.md
└── .github/
    └── workflows/
        └── a5c.yml
```

### Agent Configuration

Agents are configured using YAML frontmatter in `.agent.md` files:

### Agent Inheritance

A5C supports agent inheritance, allowing you to create specialized agents that inherit from base agents. This enables code reuse and hierarchical agent organization.

#### Basic Inheritance

Use the `from` field to specify the base agent:

```yaml
---
# Child agent configuration
name: security-reviewer
version: 1.0.0
from: base-reviewer  # Inherits from base-reviewer agent
category: security
description: Security-focused code review agent
priority: 80
mentions: "@security-review,@sec-review"
---

{{base-prompt}}

## Additional Security Analysis

As a security-focused reviewer, I will also examine:
- Security vulnerabilities and exploits
- Dependency security issues
- Authentication and authorization flaws
```

#### Multi-level Inheritance

Agents can inherit from other agents that also inherit, creating inheritance chains:

```yaml
---
# Advanced agent inheriting from security-reviewer
name: advanced-security-reviewer
version: 1.0.0
from: security-reviewer  # Which inherits from base-reviewer
category: security
priority: 100
mentions: "@advanced-security,@threat-analysis"
max_turns: 20
timeout: 30
---

{{base-prompt}}

## Advanced Threat Analysis

I will additionally perform:
- AI-powered threat detection
- Zero-day vulnerability analysis
- Supply chain security assessment
```

#### Inheritance Features

1. **Field Overriding**: Child agents can override any field from parent agents
2. **Array Merging**: Array fields (like `mcp_servers`, `events`) are merged, not overridden
3. **Base Prompt Variable**: Use `{{base-prompt}}` in child prompts to include the resolved parent prompt
4. **Multi-level Support**: Inheritance works across multiple levels (A inherits from B which inherits from C)
5. **Circular Detection**: System prevents circular inheritance loops
6. **Remote Inheritance**: Agents can inherit from remote agents using URIs

#### Supported Inheritance Sources

- **Agent ID**: `from: base-reviewer` (searches in `.a5c/agents/` directories)
- **File Path**: `from: ./agents/base-reviewer.agent.md`
- **Remote URI**: `from: https://example.com/agents/base-reviewer.agent.md`
- **Agent URI**: `from: agent://base-reviewer`

#### Example Inheritance Chain

```yaml
# Base agent (.a5c/agents/base-reviewer.agent.md)
---
name: base-reviewer
max_turns: 10
mentions: "@base-review"
mcp_servers: ["filesystem", "github"]
events: ["pull_request"]
---

Basic code review prompt...

# Security-focused agent (.a5c/agents/security-reviewer.agent.md)
---
name: security-reviewer
from: base-reviewer
category: security
priority: 80
mentions: "@security-review"
mcp_servers: ["filesystem", "github", "search"]
events: ["pull_request", "push"]
labels: ["security", "critical"]
---

{{base-prompt}}

Additional security analysis...

# Advanced security agent (.a5c/agents/advanced-security-reviewer.agent.md)
---
name: advanced-security-reviewer
from: security-reviewer
priority: 100
mentions: "@advanced-security"
mcp_servers: ["filesystem", "github", "search", "memory"]
max_turns: 20
timeout: 30
---

{{base-prompt}}

Advanced threat analysis...
```

This creates a three-level inheritance chain where `advanced-security-reviewer` inherits from `security-reviewer` which inherits from `base-reviewer`.

### Standard Agent Configuration

For agents without inheritance, use the standard configuration format:

```yaml
---
# Agent Metadata
name: security-scanner
version: 1.0.0
category: security
description: Security vulnerability scanner and analysis agent

# Usage Context
usage_context: |
  Use for security analysis, vulnerability scanning, and compliance checks.
  Performs automated security audits and identifies potential threats.

# Invocation Context
invocation_context: |
  Invoke with code changes, dependency updates, or security-related events.
  Requires repository access and security scanning tools.

# Execution Configuration
max_turns: 15
timeout: 20

# MCP Server Configuration
mcp_servers: ["filesystem", "memory", "github", "search"]

# Trigger Configuration

# Mention-based activation
mentions: "@security-scan,@sec-check,@security,@vuln-scan"

# Label-based activation (when labels are added/present)
labels: "security,critical,vulnerability"

# Branch-based activation (supports patterns)
branches: "feature/*,hotfix/*,security/*"

# File path-based activation (supports glob patterns)
paths: "src/**/*.js,lib/**/*.ts,security/**/*"

# Scheduled activation
activation_cron: "0 2 * * 1"  # Monday at 2 AM

# Priority (higher = runs first)
priority: 100

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  include_external_agents: ["code-review-agent", "deployment-agent"]
  max_agents_in_context: 6
---

Agent prompt content goes here...
```

### Agent Discovery Configuration

Each agent can be configured to discover and reference other agents in their prompts. This enables cross-agent collaboration and context sharing:

```yaml
agent_discovery:
  enabled: true                    # Enable/disable agent discovery
  include_same_directory: true     # Include agents from same category/source
  include_external_agents:         # Explicitly include specific agents
    - "code-review-agent"
    - "security-scanner"
    - "deployment-agent"
  max_agents_in_context: 6        # Maximum number of agents in discovery context
```

**Agent Discovery Behavior:**
- **Same Directory/Category**: When `include_same_directory: true`, agents from the same category or source are automatically included
- **External Agents**: Specific agents can be explicitly included by their ID, regardless of category
- **Local + Remote**: Discovery works across both local and remote agents seamlessly
- **Deduplication**: Duplicate agents are automatically removed from the discovery context
- **Limits**: The `max_agents_in_context` setting prevents the context from becoming too large

**Usage in Prompts:**
The discovered agents are available in the prompt template as `{{availableAgents}}` and can be referenced by the AI agent for collaboration:

```markdown
Available agents for collaboration:
{{#each availableAgents}}
- **{{name}}** ({{id}}): {{description}}
  - Invoke with: {{mentions}}
  - Use for: {{usage_context}}
{{/each}}
```

### Built-in MCP Servers

The action includes several built-in MCP servers that are always available:

| Server | Description | Usage |
|--------|-------------|-------|
| `agent-reporter` | Agent status reporting | Real-time status updates and communication with the execution process |
| `filesystem` | File system access | Reading/writing files, directory operations |
| `memory` | Persistent memory | Maintaining context across interactions |
| `time` | Time and date utilities | Current time, date formatting, scheduling |
| `search` | Web search via Brave | Research and information gathering |
| `github` | GitHub API integration | Repository, issue, and PR operations |

**No setup required** - these servers are embedded in the action and automatically available to all agents.

### User-defined MCP Servers

Add custom MCP servers via `.a5c/mcps.json`:

```json
{
  "mcpServers": {
    "database": {
      "command": "npx",
      "args": ["-y", "@myorg/mcp-server-database"],
      "env": {
        "DATABASE_URL": "${DATABASE_URL}"
      }
    },
    "slack": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-slack"],
      "env": {
        "SLACK_BOT_TOKEN": "${SLACK_BOT_TOKEN}"
      }
    }
  }
}
```

### Resource Loading

The unified resource handler supports:
- Local file paths: `config.yml`, `./.a5c/agents/my-agent.md`
- File URLs: `file:///absolute/path/to/file`
- HTTP/HTTPS URLs: `https://example.com/prompt.md`
- Caching with configurable TTL
- Retry logic with exponential backoff

### CLI Command Templates

Each agent specifies its CLI command as a complete template string using Handlebars syntax:

**Built-in Template Variables:**
- `{{prompt}}` - The full prompt text
- `{{prompt_path}}` - Path to temporary prompt file
- `{{mcp_config}}` - Path to MCP configuration file
- `{{model}}` - Model configuration
- `{{max_turns}}` - Maximum conversation turns
- `{{verbose}}` - Verbose flag
- `{{files}}` - Array of changed files

**Example CLI Commands:**

```yaml
# Claude Code with MCP support
cli_command: "cat {{prompt_path}} | claude {{#if mcp_config}}--mcp-config {{mcp_config}}{{/if}} -p 'fulfill the request'"

```

## Advanced Features

### Remote Agents

Load agents from remote repositories or individual URLs with full support for private repositories:

```yaml
remote_agents:
  enabled: true
  cache_timeout: 120       # Cache timeout in minutes (2 hours)
  retry_attempts: 5        # Number of retry attempts
  retry_delay: 2000        # Delay between retries in milliseconds
  sources:
    # Individual agent files
    individual:
      - uri: "https://raw.githubusercontent.com/myorg/agents/main/security-scanner.agent.md"
        alias: "remote-security"
      - uri: "https://raw.githubusercontent.com/myorg/private-agents/main/proprietary-scanner.agent.md"
        alias: "private-scanner"
      - uri: "https://example.com/agents/code-reviewer.agent.md"
        alias: "external-reviewer"
    
    # Entire repositories
    repositories:
      - uri: "https://github.com/myorg/shared-agents"
        pattern: "agents/**/*.agent.md"
      - uri: "https://github.com/myorg/private-agents"
        pattern: ".a5c/agents/**/*.agent.md"
      - uri: "https://github.com/anotherorg/public-agents"
        pattern: "**/*.agent.md"
```

**Repository Scanning Features:**
- Automatic discovery of agent files in remote repositories using GitHub API
- Pattern-based filtering with full glob pattern support (`**/*.agent.md`, `agents/**/*.agent.md`, etc.)
- Caching of remote content with configurable TTL to reduce API calls
- Robust retry logic with exponential backoff for failed requests
- Full support for private GitHub repositories using `GITHUB_TOKEN`
- Authentication automatically handled for GitHub repositories
- Branch-specific loading support (defaults to `main` branch)

**Authentication for Private Repositories:**
- **GitHub Token**: Automatically uses `GITHUB_TOKEN` environment variable
- **Private Repository Access**: Requires token with `repo` scope for private repositories
- **Public Repository Access**: Works without authentication for public repositories
- **Rate Limiting**: Respects GitHub API rate limits with proper retry logic

**Supported Repository URI Formats:**
- `https://github.com/owner/repo` - Main branch
- `https://github.com/owner/repo/tree/branch` - Specific branch
- `https://github.com/owner/repo.git` - Git URL format
- `git@github.com:owner/repo.git` - SSH URL format (converted to HTTPS)

**Individual Agent URI Formats:**
- `https://raw.githubusercontent.com/owner/repo/branch/path/agent.agent.md` - GitHub raw files
- `https://github.com/owner/repo/raw/branch/path/agent.agent.md` - GitHub raw files (alternative)
- `https://api.github.com/repos/owner/repo/contents/path/agent.agent.md` - GitHub API (auto-decoded)
- `https://your-domain.com/path/agent.agent.md` - Any HTTPS URL

### Schedule-based Activation

Agents can be triggered on a schedule using cron expressions:

```yaml
---
name: "Daily Security Scan"
activation_cron: "0 9 * * 1-5"  # Weekdays at 9 AM
events: []
cli_command: "cat {{prompt_path}} | claude -p 'fulfill the request'"
---
```

### Label-based Activation

Agents can be triggered when specific labels are added to issues or pull requests:

```yaml
---
name: "Security Scanner"
labels: "security,critical,vulnerability"
events: ["issues", "pull_request", "pull_request_target"]
cli_command: "cat {{prompt_path}} | claude -p 'fulfill the request'"
---
```

**Supported Events:**
- `issues` - When labels are added to issues
- `pull_request` - When labels are added to pull requests
- `pull_request_target` - When labels are added to pull requests from forks

### Branch-based Activation

Agents can be triggered based on branch name patterns:

```yaml
---
name: "Feature Branch CI"
branches: "feature/*,hotfix/*,release/*"
events: ["push", "pull_request"]
cli_command: "cat {{prompt_path}} | claude -p 'fulfill the request'"
---
```

**Pattern Support:**
- `feature/*` - Matches branches starting with "feature/"
- `*-hotfix` - Matches branches ending with "-hotfix"
- `*staging*` - Matches branches containing "staging"
- `main` - Exact match for "main" branch

### File Path-based Activation

Agents can be triggered when specific files or directories are modified:

```yaml
---
name: "Frontend Changes"
paths: "src/**/*.js,src/**/*.ts,components/**/*"
events: ["push", "pull_request"]
cli_command: "cat {{prompt_path}} | claude -p 'fulfill the request'"
---
```

**Pattern Support:**
- `src/**/*.js` - All JavaScript files in src directory and subdirectories
- `*.md` - All Markdown files in root directory
- `docs/` - All files in docs directory
- `security/**/*` - All files in security directory and subdirectories

### Trigger Combination

Agents can combine multiple trigger types:

```yaml
---
name: "Security Analysis"
events: ["pull_request", "push"]
labels: "security,critical"
branches: "main,develop,feature/*"
paths: "src/**/*.js,lib/**/*.ts,security/**/*"
mentions: "@security-scan,@vuln-check"
activation_cron: "0 2 * * 1"  # Also run weekly
priority: 100
---
```

**Trigger Logic:**
- **ANY** trigger condition can activate the agent
- Multiple conditions of the same type are OR'd together
- Different trigger types are OR'd together
- Higher priority agents run first when multiple agents are triggered

### MCP Server Integration

Agents can specify which MCP servers to use (built-in + user-defined):

```yaml
---
name: "Database Agent"
mcp_servers: ["filesystem", "memory", "database", "slack"]
cli_command: "cat {{prompt_path}} | claude {{#if mcp_config}}--mcp-config {{mcp_config}}{{/if}} -p 'fulfill the request'"
---
```

### File Processing

Configure which files are included in agent context:

```yaml
file_processing:
  include_patterns:
    - "src/**/*.js"
    - "src/**/*.ts"
    - "**/*.md"
  exclude_patterns:
    - "node_modules/**"
    - "*.test.js"
    - "dist/**"
```

### Structured Output

The output processor extracts structured data from agent responses:

```yaml
# Agent response can include:
PR Title: Fix authentication bug
Labels: bug, security, urgent
Severity: high
Summary: Fixed critical authentication vulnerability
Action Items:
- Update tests
- Deploy to staging
```

## Development

### Project Structure

```
a5c-githubaction/
├── src/
│   ├── resource-handler.js    # Unified resource loading
│   ├── config.js              # Configuration management
│   ├── prompt.js              # Prompt processing
│   ├── agent-execution.js     # CLI execution
│   ├── output-processor.js    # Output processing
│   ├── mcp-manager.js         # MCP server management
│   ├── utils.js               # Common utilities
│   └── agent-router.js        # Routing handlers
├── agent-router.js            # Main agent routing logic
├── index.js                   # Main entry point
├── default-config.yml         # Built-in defaults
├── package.json               # Dependencies
└── action.yml                 # GitHub Action definition
```

### Testing

```bash
# Install dependencies
npm ci

# Run tests
npm test

# Run linting
npm run lint
```

### Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests for new functionality
5. Submit a pull request

## License

MIT License - see LICENSE file for details. 