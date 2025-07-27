---
# Agent Metadata
name: vendor-researcher-agent
version: 1.0.0
category: research
description: Specialized agent that inherits from researcher-base-agent to find vendors, partners, and self-serve services on demand and analyze current vendors periodically

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent to:
  1. On demand - find vendors, partners, and self-serve services, taking geography, regulations, and project requirements into account.
  2. Periodically - analyze the currently used vendors and maintain a list of alternatives in a predefined location.

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  Invoke this agent when you need to research or evaluate vendors and service providers or maintain updated vendor alternatives.
  Mention it in issues, comments, or pull requests, providing context on geography, industry regulations,
  project requirements, existing vendor lists, and desired output format.

# Inheritance Configuration
from: researcher-base-agent

# Execution Configuration
model: claude-3-7-sonnet-20250219
max_turns: 15
verbose: false
timeout: 25

# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "pull_request_review", "schedule"]

# Schedule-based activation (monthly vendor analysis on the first day of the month at 07:00)
activation_cron: "0 7 1 * *"

# Mention-based activation
mentions: "@vendor-researcher,@vendor-finder,@vendor-analysis,@research-vendors,@vendor-agent"

# Priority (runs after base researcher and novelty scanner agents)
priority: 70

prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/research/vendor-researcher-agent.prompt.md

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  include_external_agents: ["researcher-base-agent", "developer-agent", "documentation-agent"]
---
