---
# Agent Metadata
name: producer-agent
version: 1.0.1
category: development
description: Specialized agent for comparing project implementation with specifications and generating actionable development tasks

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent when you need to:
  - Compare current project implementation with specifications in docs/specs/README.md
  - Identify gaps between current implementation and requirements
  - Generate actionable coding tasks that can be decoupled and assigned
  - Analyze project implementation phase and development history
  - Create GitHub issues for missing features or components
  - Ensure project stays aligned with documented specifications

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  This agent should be invoked when:
  - Someone mentions @producer-agent in issues/comments
  - Project specification alignment is needed
  - Development gap analysis is required
  - Planning and task generation is needed for project development
  - Regular project assessment and planning cycles

# Execution Configuration

max_turns: 20
verbose: false
timeout: 25
activation_cron: "0 9,21 * * *"

# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "push", "issue_opened", "pull_request_review"]  # Events this agent can respond to (acts as filter)

# Mention-based activation
mentions: "@producer-agent,@producer,@gap-analysis,@project-analysis,@specs-check,@task-generator"

prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/development/producer-agent.prompt.md

# Priority (higher = runs first)
priority: 75

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  max_agents_in_context: 8

app:
   commands:
     repo_dashboard_commands:
        - name: 🚀 Advance Project
          type: new_issue_and_comment_mention
          inputs:
            type: modal
          issue_title_format: Producer Generic Scan - {inputs.title}
          mention_format: do a generic scan (not under a specific issue)
        - name: ⭐ Produce Something
          type: new_issue_and_comment_mention
          inputs:
            type: modal
            fields:
              - name: title
                type: text
          issue_title_format: Producer - {inputs.title}
          mention_format: produce this - {inputs.title}
        - name: 🔍 Tech Debt Scan
          type: new_issue_and_comment_mention
          inputs:
            type: modal
          issue_title_format: Producer Tech Debt Scan - {inputs.title}
          mention_format: do a tech debt scan
     issues_batch_commands:
        - name: ⭐ Produce
          type: comment_mention
          mention_format: produce this
     issue_main_commands:
        - name: ⭐ Produce
          mention_format: produce this
          type: comment_mention
          conditions:
            and:
              - "{{issue.state}} == 'open'"
     pr_batch_commands:
        - name: ⭐ Produce
          type: comment_mention
          mention_format: produce this
     pr_main_commands:
        - name: ⭐ Produce
          type: comment_mention
          mention_format: produce this
---
