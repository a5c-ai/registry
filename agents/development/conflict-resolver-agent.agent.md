---
# Agent Metadata
name: conflict-resolver-agent
version: 1.0.0
category: development
description: AI-powered agent for resolving merge conflicts in pull requests by working directly on the PR branch

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent when:
  - Pull requests have merge conflicts that need to be resolved
  - PR branches are behind the base branch and need conflict resolution
  - Automated merges are failing due to conflicts
  - Manual intervention is needed to reconcile conflicting changes
  
  This agent analyzes merge conflicts, understands the context from the PR and related issues, and resolves conflicts by:
  1. Working directly on the PR branch (not creating new PRs)
  2. Analyzing the nature of the conflicts and understanding the intended changes
  3. Researching the PR context, related issues, and project specifications
  4. Resolving conflicts intelligently while preserving the intent of both changes
  5. Committing and pushing the resolved changes directly to the PR branch

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  This agent is primarily triggered when:
  - Pull requests have merge conflicts (detected via GitHub events)
  - Manually invoked by mentioning it in PR comments or issues (e.g., "@conflict-resolver please resolve conflicts")
  - Called by other agents when conflicts are detected during automated workflows
  
  For manual invocation, provide:
  - The PR number or link where conflicts exist
  - Any specific context about the intended changes
  - Priority guidance if certain changes should take precedence
  - Links to related issues or specifications for additional context

# Execution Configuration
model: claude-3-7-sonnet-20250219
max_turns: 40
verbose: false
timeout: 45

# Trigger Configuration
events: ["pull_request", "pull_request_target", "pull_request_review", "issue_comment", "commit_comment"]

# Mention-based activation  
mentions: "@conflict-resolver,@resolve-conflicts,@fix-conflicts,@merge-conflicts,@conflict-resolver-agent"

# Priority (higher = runs first)
priority: 80
prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/development/conflict-resolver-agent.prompt.md

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  include_external_agents: ["developer-agent", "build-fixer-agent"]
  max_agents_in_context: 8
---