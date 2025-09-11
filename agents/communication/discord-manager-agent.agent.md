---
# Agent Metadata
name: discord-manager-agent
version: 1.0.0
category: communication
description: Manages communication between Discord and A5C agents, enabling seamless interaction through Discord channels and direct messages

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent when you need to:
  - Interact with Discord users through A5C agents
  - Listen for and respond to Discord commands and messages
  - Route Discord requests to appropriate A5C agents
  - Relay agent responses back to Discord channels
  - Manage Discord server settings and configurations
  - Handle Discord events and notifications
  - Create a bot-like presence in Discord communities
  - Automate Discord-based workflows and responses

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  This agent should be invoked when:
  - Someone mentions @discord-manager or @discord-bot in issues/comments
  - A request is made to interact with Discord channels or users
  - Discord integration setup or configuration is needed
  - A project needs to establish Discord communication capabilities
  - Teams need to coordinate activities through Discord channels

# Execution Configuration

max_turns: 10
verbose: false
timeout: 15
schedule: 
  - cron: "0 */3 * * *"
# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "push", "issue_opened", "scheduled"]

# Mention-based activation
mentions: "@discord-manager,@discord-bot,@discord-integration,@discord-connector,@discord-manager-agent"
prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/communication/discord-manager-agent.prompt.md

# Priority (higher = runs first)
priority: 75

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  max_agents_in_context: 8
  coordination_instructions: |
    This agent coordinates with all other agents by:
    - Routing Discord messages to appropriate agents based on content and mentions
    - Relaying agent responses back to Discord channels
    - Facilitating agent collaboration through Discord threads and channels
    - Managing permissions for which Discord users can access which agents

app:
   commands:
     repo_dashboard_commands:
        - name: Discord Task
          type: new_issue_and_comment_mention
          inputs:
            type: modal
            fields:
              - name: instructions
                type: text
          issue_title_format: Discord - {inputs.instructions}
          mention_format: do your scan or fulfill the instructions

---
