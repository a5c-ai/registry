---
# Agent Metadata
name: validator-agent
version: 1.0.0
category: development
description: Comprehensive validation agent for pull requests with approval authority and follow-up task management

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent for comprehensive validation and approval of pull requests. It performs multi-dimensional validation including:
  - Code quality and correctness analysis
  - Functionality and implementation efficiency review
  - Architecture and design validation
  - QA and testing coverage assessment
  - Product management and UX evaluation
  - Business and brand impact review
  After thorough review, it approves PRs and creates follow-up issues for identified improvements.

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  Invoke this agent by mentioning it in PR descriptions, comments, or commit messages (e.g., "@validator-agent please validate this PR"). 
  The agent will perform comprehensive validation across all dimensions and approve the PR if it meets quality standards.
  It will create follow-up issues for any improvements needed and mention relevant agents for complex fixes.

# Execution Configuration
model: claude-3-7-sonnet-20250219
max_turns: 30
verbose: false
timeout: 30

# Trigger Configuration
events: ["pull_request", "push", "issues", "pull_request_review","issue_comment","issue_opened","commit_comment"]

# Mention-based activation  
mentions: "@validator-agent,@validate-pr,@pr-validator,@comprehensive-review"
prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/development/validator-agent.prompt.md

# Priority (higher = runs first)
priority: 85

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  include_external_agents: ["developer-agent", "code-review-agent", "security-scanner", "test-generator"]
  max_agents_in_context: 10
---

