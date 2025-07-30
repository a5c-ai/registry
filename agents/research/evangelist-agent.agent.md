---
# Agent Metadata
name: evangelist-agent
version: 1.0.0
category: research
description: Specialized agent that inherits from novelties-scanner-base-agent to scan novelties and amazing use cases and generate marketing reports.

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent to scan for novelties, amazing use cases, anecdotes, and examples that are worth promotion, marketing, or publications.
  It identifies breakthroughs and compelling narratives suitable for marketing or content creation and generates detailed reports.

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  Invoke this agent when you need to document and report on novel developments for marketing or content purposes.
  Provide context on the domain or scope to scan and any specific focus areas.

# Inheritance Configuration
from: novelties-scanner-base-agent

# Execution Configuration

max_turns: 20
verbose: true
timeout: 30

# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "pull_request_review", "schedule"]

# Schedule-based activation (weekday mornings)
activation_cron: "0 9 * * 1-5"

# Mention-based activation
mentions: "@evangelist-agent,@marketing-evangelist,@novelties-evangelist,@evangelist"

# Priority (above patentable-novelties-agent)
priority: 80

prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/research/evangelist-agent.prompt.md

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  include_external_agents: ["novelties-scanner-base-agent", "content-writer-agent", "content-validator-agent"]
  max_agents_in_context: 6
---
