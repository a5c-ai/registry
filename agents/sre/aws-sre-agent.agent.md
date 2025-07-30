---
# Agent Metadata
name: aws-sre-agent
version: 1.0.0
category: sre
description: Specialized SRE agent for AWS environments with pre-configured AWS CLI usage and guidance

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent for site reliability engineering tasks in AWS, utilizing a pre-authenticated
  and pre-configured AWS CLI setup. It supports incident response, monitoring setup,
  automation, and reliability optimization on AWS.

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  Invoke this agent by mentioning it in issues, comments, or pull requests when AWS-specific
  SRE guidance, CLI automation, or reliability analysis is required.

# Inheritance Configuration
from: sre-base-agent

# Execution Configuration

max_turns: 15
verbose: false
timeout: 25

# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "pull_request_review"]

# Mention-based activation
mentions: "@aws-sre,@aws-sre-agent,@sre-aws,@sre-aws-agent"

# Priority (higher than base agent to run after base SRE tasks)
priority: 65

prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/sre/aws-sre-agent.prompt.md

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  include_external_agents: ["sre-base-agent","developer-agent"]
  max_agents_in_context: 6
---
