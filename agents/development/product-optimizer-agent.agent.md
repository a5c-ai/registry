---
# Agent Metadata
name: product-optimizer-agent
version: 1.0.0
category: development
description: Product-focused agent that compares implementation and product flow with specs, identifies gaps in functionality/usability, and opens actionable GitHub issues (creates specs definition issue if docs/specs/README.md is missing)
from: producer-agent

# Usage Context
usage_context: |
  Use this agent to optimize product flow and usability:
  - Compare repo implementation and user flows against specs in docs/specs/README.md
  - Identify missing or suboptimal flow, functionality, and usability
  - Analyze implementation and PR history to determine project phase
  - Open well-scoped GitHub issues for decoupled tasks
  - If docs/specs/README.md is missing, open an issue to define specs comprehensively

# Invocation Context
invocation_context: |
  Invoke via mention in issues/PRs/comments (e.g., "@product-optimizer-agent" or "@product-optimizer").
  Provide repository context, target areas (flows, features, UX), and any constraints or priorities.

# Execution Configuration
max_turns: 20
verbose: false
timeout: 25

# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "push", "issue_opened", "pull_request_review", "schedule"]
mentions: "@product-optimizer-agent,@product-optimizer,@flow-optimizer,@usability-optimizer,@specs-optimizer"
activation_cron: "0 9,21 * * *"

# Prompt reference
prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/development/product-optimizer-agent.prompt.md

# Priority (higher runs first)
priority: 76

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  max_agents_in_context: 8

app:
   commands:
     repo_dashboard_commands:
        - name: 📦 Optimizer Product
          type: new_issue_and_comment_mention
          inputs:
            type: modal
            fields:
              - name: instructions
                type: text
          issue_title_format: Product Optimizer - {inputs.instructions}
          mention_format: optimize product flow and usability using these instructions
---
