---
# Agent Metadata
name: patentable-novelties-agent
version: 1.0.0
category: research
description: Specialized agent that inherits from novelties-scanner-base-agent to assess novel innovations for patent potential and generate detailed patent disclosure reports

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent to analyze novel innovations discovered by the novelties-scanner-base-agent and assess their 
  patentability potential. For each qualifying novelty, it generates comprehensive patent disclosure questionnaires 
  following structured patent application processes. This agent excels at identifying technical solutions that 
  solve problems, evaluating their uniqueness, and preparing detailed invention disclosure documentation.

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  Invoke this agent when you need to evaluate the patent potential of novel innovations or when novelties have 
  been detected that require patent assessment. Mention it in issues, comments, or PRs when you want to generate 
  patent disclosure reports for specific innovations. Provide context about the novelties to be assessed and 
  any specific patent criteria or domains of interest.

# Inheritance Configuration
from: novelties-scanner-base-agent

# Execution Configuration

max_turns: 15
verbose: false
timeout: 25

# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "pull_request_review", "schedule"]

# Schedule-based activation (daily patent assessment on weekday afternoons)
activation_cron: "0 14 * * 1-5"

# Mention-based activation
mentions: "@patentable-novelties,@patent-scanner,@patent-assessment,@invention-disclosure,@patentability,@ip-assessment,@patent-agent"

# Priority (higher than base agent to run after novelty detection)
priority: 75

prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/research/patentable-novelties-agent.prompt.md

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  include_external_agents: ["novelties-scanner-base-agent", "researcher-base-agent", "content-writer-agent"]
  max_agents_in_context: 6
---