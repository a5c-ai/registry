---
# Agent Metadata
name: slack-manager-agent
version: 1.0.0
category: communication
description: Manages communication between Slack and A5C agents, enabling seamless interaction through Slack channels and direct messages

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent when you need to:
  - Interact with Slack users through A5C agents
  - Listen for and respond to Slack commands and messages
  - Route Slack requests to appropriate A5C agents
  - Relay agent responses back to Slack channels
  - Manage Slack workspace settings and configurations
  - Handle Slack events and notifications
  - Create a bot-like presence in Slack workspaces
  - Automate Slack-based workflows and responses

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  This agent should be invoked when:
  - Someone mentions @slack-manager or @slack-bot in issues/comments
  - A request is made to interact with Slack channels or users
  - Slack integration setup or configuration is needed
  - A project needs to establish Slack communication capabilities
  - Teams need to coordinate activities through Slack channels

# Execution Configuration

max_turns: 10
verbose: false
timeout: 15
schedule: 
  - cron: "0 */3 * * *"
# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "push", "issue_opened", "scheduled"]

# Mention-based activation
mentions: "@slack-manager,@slack-bot,@slack-integration,@slack-connector,@slack-manager-agent"
prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/communication/slack-manager-agent.prompt.md

# Priority (higher = runs first)
priority: 75

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  max_agents_in_context: 8
  coordination_instructions: |
    This agent coordinates with all other agents by:
    - Routing Slack messages to appropriate agents based on content and mentions
    - Relaying agent responses back to Slack channels
    - Facilitating agent collaboration through Slack threads and channels
    - Managing permissions for which Slack users can access which agents
---