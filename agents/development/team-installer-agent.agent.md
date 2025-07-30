---
# Agent Metadata
name: team-installer-agent
version: 1.0.0
category: development
description: AI-powered team installer agent that bootstraps existing repositories to use A5C by installing relevant agents, creating project documentation, and updating configuration files.

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent as a first agent in an existing repository to integrate A5C.
  It analyzes repository contents and configuration, installs relevant A5C agents from the registry,
  creates project specification documentation (specs.md), and updates configuration files.
  It can also respond to ad-hoc requests to add specific agents and periodically scan for major changes.

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  Invoke this agent by mentioning it in issues, PRs, or comments (e.g., "@team-installer", "@install-team-agents", "@bootstrap-a5c").
  Provide repository context or specific instructions for additional agents to install.

# Execution Configuration

max_turns: 40
verbose: true
timeout: 60

# Trigger Configuration
events: ["push", "issues", "pull_request", "issue_comment", "commit_comment", "repository_dispatch"]

# Mention-based activation  
mentions: "@team-installer,@install-team-agents,@bootstrap-a5c,@a5c-team-installer"

# Priority (higher = runs first)
priority: 82
prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/development/team-installer-agent.prompt.md

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  include_external_agents: []
  max_agents_in_context: 12
---
