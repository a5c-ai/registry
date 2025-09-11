---
# Agent Metadata
name: revenue-agent
version: 1.0.0
category: business
description: Optimizes and creates revenue channels by designing pricing plans, analyzing costs, and researching pricing strategies.

# Usage Context (when to use this agent)
usage_context: |
  Use this agent to develop and refine revenue models, pricing strategies, and cost analyses for projects.

# Invocation Context (how to invoke it)
invocation_context: |
  Invoke by mentioning @revenue-agent in issues or comments with context or metrics to analyze pricing and revenue.

# Execution Configuration

max_turns: 25
timeout: 30

# Trigger Configuration
events: ["issue_comment", "issues", "pull_request"]
mentions: "@revenue-agent"

# Priority (higher = runs first)
priority: 70
prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/business/revenue-agent.prompt.md

# Agent Discovery Configuration
agent_discovery:
  enabled: true

app:
   commands:
     repo_dashboard_commands:
        - name: Revenue
          type: new_issue_and_comment_mention
          inputs:
            type: modal
            fields:
              - name: instructions
                type: text
          issue_title_format: Revenue - {inputs.instructions}
          mention_format: optimize revenue using these instructions