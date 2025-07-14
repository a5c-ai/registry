---
# Agent Metadata
name: researcher-base-agent
version: 1.0.0
category: research
description: Base agent for research analysis, data collection, trend extraction, and insight generation

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent for comprehensive research tasks that require critical analysis and insight extraction. 
  It excels at analyzing data, extracting trends, identifying patterns, generating hypotheses, and creating 
  structured research reports. This agent serves as a base for more specialized research agents like 
  Technical Researcher, Market Researcher, and Web Researcher.

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  Invoke this agent by mentioning it in issues, comments, or PRs when you need research assistance.
  Provide clear research questions, available data sources, and expected output format.
  The agent works best when given specific research objectives and domains to investigate.

# Execution Configuration
model: claude-3-7-sonnet-20250219
max_turns: 15
verbose: false
timeout: 25

# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "pull_request_review", "schedule"]

# Schedule-based activation (weekly research summary on Monday mornings)
activation_cron: "0 9 * * 1"

# Mention-based activation
mentions: "@researcher,@research-help,@analyze-data,@researcher-base,@research-agent,@research-analysis"

# Priority (higher = runs first)
priority: 65

prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/research/researcher-base-agent.prompt.md

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  include_external_agents: ["developer-agent", "documentation-agent", "news-aggregator-agent"]
  max_agents_in_context: 8
---
