---
# Agent Metadata
name: build-fixer-agent
version: 1.0.0
category: development
description: Specialized agent for analyzing and fixing failed CI/CD pipeline runs and build failures

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent when:
  - CI/CD pipeline runs are failing
  - Build processes are failing
  - Tests are failing in automated workflows
  - You need to diagnose and fix build infrastructure issues
  
  This agent analyzes failed GitHub Actions runs, diagnoses the root cause of failures, and takes appropriate corrective action by:
  1. Fixing project build errors with pull requests
  2. Fixing test framework or build infrastructure issues with pull requests
  3. Opening GitHub issues for failing unit or e2e tests (grouping related failures)

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  This agent is primarily triggered automatically on failed GitHub Actions workflow runs.
  It can also be manually invoked by mentioning it in issues, PRs, or comments (e.g., "@build-fixer please analyze this failing build").
  
  For manual invocation, provide:
  - The link to the failing workflow run
  - Any context about what changed since the last successful build
  - Specific failures you want prioritized

# Execution Configuration
model: claude-3-7-sonnet-20250219
max_turns: 30
verbose: false
timeout: 30

# Trigger Configuration
events: ["workflow_run", "workflow_job", "check_run", "check_suite", "issues", "issue_comment", "pull_request", "pull_request_review", "commit_comment"]


# Mention-based activation  
mentions: "@build-fixer,@build-fix,@fix-build,@pipeline-fixer,@ci-fix,@test-fix,@build-fixer-agent"

# Priority (higher = runs first)
priority: 75
prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/development/build-fixer-agent.prompt.md

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  include_external_agents: ["developer-agent"]
  max_agents_in_context: 8
---
