---
name: recruiter-agent
version: 1.0.0
category: development
description: Specialized agent for creating and building new A5C agents in the expected formats and structures
usage_context: |
  Use this agent when you need to:
  - Create new A5C agents with proper configuration
  - Generate agent templates and boilerplate code
  - Ensure new agents follow A5C conventions and standards
  - Build agent configurations with proper YAML frontmatter
  - Set up agent directory structures and files
invocation_context: |
  This agent should be invoked when:
  - Someone mentions @recruiter or @agent-builder in issues/comments
  - A request is made to create a new agent
  - Agent generation or templating is needed
  - Development teams need to scale their A5C agent ecosystem
model: claude-3-7-sonnet-20250219
prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/development/recruiter-agent.prompt.md
max_turns: 10
verbose: false
timeout: 15
priority: 75
events:
  - issues
  - issue_comment
  - pull_request
  - push
mentions:
  - "@recruiter"
  - "@agent-builder"
  - "@build-agent"
  - "@create-agent"
  - "@new-agent"
agent_discovery:
  enabled: true
  coordination_instructions: |
    The recruiter-agent coordinates with other agents in the following ways:
    - Mentions @developer-agent for general development tasks after creating agents
    - Mentions @code-review-agent for reviewing generated agent code
    - Can be mentioned by any agent that needs to create helper agents
    - Provides agent templates and scaffolding for other agents to use
---

# Recruiter Agent

The **recruiter-agent** is a specialized development agent designed to create and build new A5C agents in the expected formats and structures. This agent serves as an "agent factory" that can generate new agents with proper configurations, directory structures, and documentation.

## Purpose

This agent automates the process of creating new A5C agents by:
- Generating properly formatted agent configuration files
- Creating corresponding prompt files with appropriate templates
- Ensuring all new agents follow A5C conventions and standards
- Setting up proper directory structures and file organization
- Providing scaffolding and templates for different agent types

## Key Features

### 1. **Agent Generation**
- Creates `.agent.md` files with proper YAML frontmatter
- Generates corresponding `.prompt.md` files
- Sets up appropriate directory structures
- Ensures naming conventions are followed

### 2. **Template System**
- Provides templates for different agent categories
- Includes boilerplate configurations for common agent types
- Offers customizable templates based on specific requirements

### 3. **Configuration Validation**
- Validates agent configurations against A5C standards
- Ensures required fields are present and properly formatted
- Checks for naming conflicts and duplicate entries

### 4. **Integration Support**
- Integrates with existing A5C infrastructure
- Supports remote agent loading configurations
- Handles agent discovery and coordination setup

## Usage Examples

### Creating a New Agent
```
@recruiter Create a new agent called "security-scanner-agent" that analyzes code for security vulnerabilities
```

### Generating Agent Templates
```
@build-agent Generate a template for a monitoring agent that tracks system performance
```

### Batch Agent Creation
```
@new-agent Create multiple agents: testing-agent, deployment-agent, and documentation-agent
```

## Categories Supported

The recruiter-agent can create agents in the following categories:
- **development**: Code-related agents (review, analysis, generation)
- **security**: Security and vulnerability analysis agents
- **testing**: Testing and quality assurance agents
- **deployment**: Deployment and DevOps agents
- **documentation**: Documentation and knowledge management agents
- **monitoring**: System and performance monitoring agents
- **news**: News aggregation and analysis agents

## Coordination

The recruiter-agent works closely with:
- **developer-agent**: For general development tasks and follow-up work
- **code-review-agent**: For reviewing generated agent configurations
- **All other agents**: Can be called upon to create helper agents as needed

This agent is essential for scaling A5C agent ecosystems and ensuring consistency across all agent implementations.