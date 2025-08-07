---
# Agent Metadata
name: content-writer-agent
version: 1.0.0
category: communication
description: Base agent for creating clear, engaging content for non-technical audiences across various channels

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent when you need to:
  - Translate technical information into clear, engaging copy
  - Create content tailored to specific channels and audiences
  - Develop content with business value propositions and storytelling
  - Maintain consistent brand voice and style across communications
  - Create content for mixed or non-technical audiences (executives, customers, press)

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  This agent should be invoked when:
  - Technical content needs translation for non-technical audiences
  - Content needs to be created for specific channels (blog, sales deck, social media)
  - Brand messaging needs to be consistent and value-focused
  - Complex information needs to be conveyed with analogies and storytelling
  
  Provide clear details about:
  - Target audience (executives, customers, general public)
  - Desired content format or channel
  - Key technical concepts that need translation
  - Brand voice and style guidelines to follow

# Execution Configuration
max_turns: 15
verbose: false
timeout: 20

# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "pull_request_review", "push", "schedule"]

# Mention-based activation
mentions: "@content-writer,@writer,@content-creator,@copywriter,@content-writer-agent"

# Priority (higher = runs first)
priority: 70

prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/communication/content-writer-agent.prompt.md

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  include_external_agents: ["researcher-base-agent", "documentation-agent"]
  max_agents_in_context: 8
  coordination_instructions: |
    This agent coordinates with other agents by:
    - Requesting research from researcher-base-agent for accurate content
    - Collaborating with documentation-agent to maintain consistent messaging
    - Receiving technical details from developer agents to ensure accuracy
    - Providing content suggestions to media generation agents for visual alignment
---