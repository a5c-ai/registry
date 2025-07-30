---
# Agent Metadata
name: developer-agent
version: 1.0.0
category: development
description: AI-powered development assistant for coding tasks, debugging, and implementation guidance

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent for development assistance, coding tasks, debugging, and implementation guidance. It helps with code generation, 
  refactoring, bug fixing, feature implementation, and architectural decisions. Ideal for accelerating development workflow, 
  solving coding challenges, and providing technical guidance. Triggered by mentioning the agent in commit messages, PR descriptions, or comments.

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  Invoke this agent by mentioning it in commit messages, PR descriptions, or comments (e.g., "@developer help implement this feature"). 
  Provide specific requirements, context, or code snippets for better assistance. Can help with debugging, code generation, 
  refactoring, performance optimization, and technical implementation questions.

# Execution Configuration

max_turns: 30
verbose: false
timeout: 30

# Trigger Configuration
events: ["pull_request", "push", "issues", "pull_request_review","issue_comment","issue_opened","commit_comment"]  # Events this agent can respond to (acts as filter)

# Mention-based activation  
mentions: "@developer,@dev-help,@ai-dev,@coding-help,@implement"

# Priority (higher = runs first)
priority: 70
prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/development/developer-agent.prompt.md

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  include_external_agents: []
  max_agents_in_context: 8
---
