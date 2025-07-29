---
# Agent Metadata
name: gcp-sre-agent
version: 1.0.0
category: sre
description: Specialized SRE agent for GCP environments with pre-configured gcloud CLI usage and guidance

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent for site reliability engineering tasks in Google Cloud Platform, leveraging a
  pre-authenticated and pre-configured gcloud CLI setup. It assists with incident response,
  monitoring, automation, and reliability improvements on GCP.

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  Invoke this agent by mentioning it in issues, comments, or pull requests when GCP-specific
  SRE guidance, CLI automation, or reliability reviews are needed.

# Inheritance Configuration
from: sre-base-agent

# Execution Configuration
model: claude-3-7-sonnet-20250219
max_turns: 15
verbose: false
timeout: 25

# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "pull_request_review"]

# Mention-based activation
mentions: "@gcp-sre,@gcp-sre-agent,@sre-gcp,@sre-gcp-agent"

# Priority (higher than base agent to run after base SRE tasks)
priority: 65

prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/sre/gcp-sre-agent.prompt.md

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  include_external_agents: ["sre-base-agent","developer-agent"]
  max_agents_in_context: 6
---
