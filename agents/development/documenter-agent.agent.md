---
# Agent Metadata
name: documenter-agent
version: 1.0.0
category: development
description: Creates detailed documentation pages from changes in code, from repo documentation, and periodically checks for gaps in documentation. Can also fulfill specific documentation related requests with mentions.

# Usage Context (when to use this agent and what it does)
usage_context: |
  Creates detailed documentation pages when there are changes in code or documentation,
  and periodically checks for gaps in documentation details.
  Use mentions to request specific documentation tasks.

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  Invoke when mentioned in issues or comments with @documenter-agent or related triggers.
  Requires access to code diffs and repository documentation files.

# Inheritance Configuration
from: content-writer-agent

# Execution Configuration
model: claude-3-7-sonnet-20250219
max_turns: 15
timeout: 30

# Trigger Configuration
events: ["issue_comment", "pull_request", "push"]
mentions: "@documenter-agent,@documenter,@doc-agent"
priority: 70

prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/development/documenter-agent.prompt.md

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  max_agents_in_context: 8
---
