---
# Agent Metadata
name: sre-base-agent
version: 1.0.0
category: sre
description: Base agent for site reliability engineering tasks, providing core SRE functionalities and best practices

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent as the foundation for site reliability engineering tasks across different cloud environments.
  Provides core SRE best practices, including incident response, monitoring, performance optimization,
  and reliability engineering principles.

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  Invoke this agent by mentioning it in issues, comments, or pull requests when SRE guidance,
  automation, or reviews are required for cloud infrastructure and reliability engineering.

# Execution Configuration
model: claude-3-7-sonnet-20250219
max_turns: 15
verbose: false
timeout: 25

# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "pull_request_review"]

# Mention-based activation
mentions: "@sre-base,@sre-agent,@sre-base-agent"

# Priority (higher = runs first)
priority: 60

prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/sre/sre-base-agent.prompt.md

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  max_agents_in_context: 8
---
