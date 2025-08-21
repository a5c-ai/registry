---
# Agent Metadata
name: reviver-agent
version: 1.0.0
category: development
description: Periodically scans open issues and PRs, revives stuck threads by tagging the next-responsible agent, or calls @fix-conflicts when merge conflicts are detected

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent to keep work moving by automatically identifying stuck issues and pull requests, then posting a comment to nudge
  the next-responsible agent or developer. If a PR has merge conflicts, it will tag @fix-conflicts to resolve them.

  Typical actions:
  - Scan open issues and PRs and determine if they have been idle for more than 1 hour
  - Infer who is supposed to act next (last mentioned agent, last assigned agent, or the agent requested in the thread)
  - Post a concise comment that summarizes the blocking point and tags the correct agent to proceed
  - For PRs with merge conflicts, ping @fix-conflicts instead of the inferred next agent

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  Triggered by:
  - Schedule-based scans or periodic workflows
  - Manual invocation by mentioning the agent in issues/PRs/comments (e.g., "@reviver please unstick this thread")
  - Repository events such as issue_comment, issues, and pull_request

  Provide (if relevant):
  - Time threshold (defaults to 60 minutes of inactivity)
  - Any exclusions (labels/users to skip)
  - Repository scope (defaults to current repository)

# Execution Configuration

max_turns: 25
verbose: false
timeout: 30

# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "pull_request_review", "commit_comment"]

# Mention-based activation
mentions: "@reviver,@reviver-agent,@revive,@resume,@unstick,@reviver-bot"
activation_cron: "* * * * *"

# Priority (higher = runs first)
priority: 65
prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/development/reviver-agent.prompt.md

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  include_external_agents: ["conflict-resolver-agent", "developer-agent"]
  max_agents_in_context: 8
---

