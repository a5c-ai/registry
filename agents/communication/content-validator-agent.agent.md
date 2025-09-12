---
# Agent Metadata
name: content-validator-agent
version: 1.0.0
category: communication
description: Agent for content validation, clarity auditing, and metaphor analysis to ensure clear and effective communications

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent to validate and proofread content for clarity, conciseness, and audience understanding. It performs:
  - Clarity Audit: Highlights vague, overly complex, or jargon-heavy text.
  - Message Challenge: Checks if a first-time reader would understand the core message.
  - Ambiguity Hunt: Identifies phrases that could be misinterpreted.
  - Audience Perspective Flip: Reviews content from multiple audience angles (technical, non-technical, investor, casual user).
  - Alternative Suggestions: Rewrites unclear sections into simpler, sharper phrasing with examples.
  - Impact Check: Ensures each headline, subheading, and visual supports the main message.
  - Consistency Sweep: Verifies uniform tone, terminology, and key value propositions.
  - Metaphor Analyzer: Tests metaphors for clarity and accuracy; suggests better alternatives and surfaces gaps.

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  Invoke this agent by mentioning it in issue comments or pull requests (e.g., "@content-validator-agent please audit this content").
  Provide the content to review and the target audience(s). The agent will output feedback with specific suggestions.

# Execution Configuration

max_turns: 20
verbose: false
timeout: 25

# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "pull_request_review", "push", "schedule"]

# Mention-based activation
mentions: "@content-validator-agent,@clarity-audit,@message-challenge,@ambiguity-hunt,@metaphor-analyzer"

prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/communication/content-validator-agent.prompt.md

# Priority (higher = runs first)
priority: 75

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  include_external_agents: ["content-writer-agent", "developer-agent"]
  max_agents_in_context: 8

app:
   commands:
     repo_dashboard_commands:
        - name: 🔍 Validate Content
          type: new_issue_and_comment_mention
          inputs:
            type: modal
            fields:
              - name: instructions
                type: text
          issue_title_format: Content Validator - {inputs.instructions}
          mention_format: validate content using these instructions
     issues_batch_commands:
        - name: 🔍 Validate Content
          type: comment_mention
          mention_format: validate content for this
     issue_main_commands:
        - name: 🔍 Validate Content
          mention_format: validate content for this
          type: comment_mention
          conditions:
            and:
              - "{{issue.state}} == 'open'"
---
