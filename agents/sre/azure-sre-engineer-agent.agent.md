---
# Agent Metadata
name: azure-sre-engineer-agent
version: 1.0.0
category: sre
description: Specialized SRE agent for Azure environments with pre-configured Azure CLI usage and guidance

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent for SRE tasks specific to Azure cloud environments, leveraging a pre-authenticated and
  pre-configured Azure CLI setup. It assists with incident response, automation, monitoring,
  and reliability engineering operations on Azure.

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  Invoke this agent by mentioning it in issues, comments, or pull requests when Azure-specific
  SRE guidance, CLI automation, or reliability reviews are needed.

# Inheritance Configuration
from: sre-base-agent

# Execution Configuration

max_turns: 15
verbose: false
timeout: 25

# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "pull_request_review"]

# Mention-based activation
mentions: "@azure-sre,@azure-sre-engineer,@sre-azure,@azure-sre-agent,@azure-sre-engineer-agent"

# Priority (higher than base agent to run after base SRE tasks)
priority: 65

prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/sre/azure-sre-engineer-agent.prompt.md

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  include_external_agents: ["sre-base-agent","developer-agent"]
  max_agents_in_context: 6

app:
   commands:
     repo_dashboard_commands:
        - name: 🛠️ DevOps/SRE
          type: new_issue_and_comment_mention
          inputs:
            type: modal
            fields:
              - name: instructions
                type: text                
          issue_title_format: DevOps/SRE - {inputs.instructions}
          mention_format: do it
---
