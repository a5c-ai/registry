---
# Agent Metadata
name: code-review-agent
version: 1.3.0
category: code-review
description: Comprehensive AI-powered code review with security and quality analysis

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent for comprehensive code reviews on pull requests and significant code changes. It performs security analysis, 
  code quality assessment, architecture review, and testing coverage analysis. Ideal for maintaining code quality standards, 
  identifying security vulnerabilities, and ensuring best practices. Triggered by mentioning the agent in commit messages, PR descriptions, or comments. 

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  Invoke this agent by mentioning it in commit messages, PR descriptions, or comments (e.g., "@code-review please review this"). 
  Provide specific focus areas if needed (e.g., security, performance, architecture). 

# Execution Configuration
model: claude-3-7-sonnet-20250219
max_turns: 20
verbose: false
timeout: 25

# Trigger Configuration
events: ["pull_request", "push", "pull_request_review", "issue_comment", "issue_opened"]  # Events this agent can respond to (acts as filter)
# Mention-based activation  
mentions: "@code-review,@review-code,@ai-review,@quality-check"
prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/development/code-review-agent.prompt.md


# Priority (higher = runs first)
priority: 80


# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  include_external_agents: ["security-scanner", "test-generator", "deployment-agent"]
  max_agents_in_context: 8
---


