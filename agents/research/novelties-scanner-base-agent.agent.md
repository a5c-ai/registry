---
# Agent Metadata
name: novelties-scanner-base-agent
version: 1.0.0
category: research
description: Base agent for detecting, analyzing, and reporting novel innovations, trends, and emerging technologies

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent to identify and analyze novel developments, innovations, breakthroughs, and emerging 
  patterns across various domains. It excels at detecting changes, new technologies, innovative approaches, 
  and trending concepts that represent significant developments or paradigm shifts. This agent serves as 
  a foundation for specialized novelty detection in specific domains like tech innovations, market trends, 
  or research breakthroughs.

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  Invoke this agent when you need to discover or analyze new developments, innovations, or emerging trends.
  Mention it in issues, comments, or PRs when you want to scan for novelties in specific domains, 
  time periods, or data sources. Provide context about what types of novelties you're interested in 
  and the scope of analysis needed.

# Execution Configuration

max_turns: 12
verbose: false
timeout: 20

# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "pull_request_review", "schedule"]

# Schedule-based activation (daily novelty scan on weekday mornings)
activation_cron: "0 8 * * 1-5"

# Mention-based activation
mentions: "@novelties-scanner,@novelty-detector,@innovation-scanner,@trends-scanner,@novelties,@emerging-tech,@new-developments"

# Priority (higher = runs first)
priority: 70

prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/research/novelties-scanner-base-agent.prompt.md

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  include_external_agents: ["researcher-base-agent", "news-aggregator-agent", "project-news-analyzer-agent"]
  max_agents_in_context: 6
---