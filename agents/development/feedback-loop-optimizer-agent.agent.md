---
# Agent Metadata
name: feedback-loop-optimizer-agent
version: 1.0.0
category: development
description: Periodic auditor that strengthens automated feedback loops (pre-commit, e2e, CI, lint, coverage, monitoring/alerts) and opens actionable issues; prefers open-source/free solutions. Inherits task generation style from producer.

# Usage Context
usage_context: |
  Use this agent to proactively improve repository feedback loops by:
  - Auditing commit hygiene and pre-commit hooks
  - Ensuring end-to-end/smoke tests exist and run in CI
  - Hardening CI workflows (build, test, lint, type-check, coverage gates)
  - Enforcing linting and formatting across languages
  - Adding coverage reporting and thresholds
  - Proposing monitoring, tracing, logging, and alerting with OSS tools
  - Establishing on-call/incident triggers and escalation paths

# Invocation Context
invocation_context: |
  Invoke via mention in issues/PRs/comments (e.g., "@feedback-loop-optimizer-agent" or "@feedback-loop-optimizer").
  The agent also runs on a schedule to surface opportunities without manual prompts.

# Inheritance Configuration
from: producer-agent

# Execution Configuration
max_turns: 20
verbose: false
timeout: 25

# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "push", "issue_opened", "pull_request_review", "schedule"]
mentions: "@feedback-loop-optimizer-agent,@feedback-loop-optimizer,@feedback-optimizer,@feedback-loops"
activation_cron: "0 9,21 * * *"

# Prompt reference
prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/development/feedback-loop-optimizer-agent.prompt.md

# Priority (align with product-optimizer)
priority: 76

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  max_agents_in_context: 8
---

