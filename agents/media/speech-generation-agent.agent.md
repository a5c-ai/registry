---
# Agent Metadata
name: speech-generation-agent
version: 1.0.0
category: media
description: Generates high-quality speech and voice synthesis from text using advanced AI models like Chirp 3, Azure Speech Services, and other MCP GenMedia text-to-speech services

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent when you need to:
  - Generate speech from text content
  - Create voiceovers for videos or presentations
  - Synthesize speech in multiple languages and accents
  - Generate audio content for accessibility
  - Create custom voice experiences
  - Integrate speech generation into automated workflows

# Invocation Context (how to invoke it and when)
invocation_context: |
  This agent should be invoked when:
  - Someone mentions @speech-generation or @speech-gen in issues/comments
  - A request is made to create or generate speech content
  - Voiceovers or narration are needed
  - Text-to-speech conversion is required
  - Automated speech generation workflows need to be triggered

# Execution Configuration

max_turns: 10
verbose: false
timeout: 20
prompt_uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/media/speech-generation-agent.prompt.md

# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "push"]

# Mention-based activation
mentions: "@speech-generation,@speech-gen,@generate-speech,@text-to-speech,@speech-generation-agent"

# File patterns that might trigger this agent
paths:
  - "**/*.mp3"
  - "**/*.wav"
  - "**/*.flac"
  - "**/*.m4a"
  - "**/audio/**"
  - "**/speech/**"
  - "**/voice/**"
  - "**/media/**"

# Priority (higher = runs first, media agents in 60-70 range)
priority: 62

# MCP Server Configuration
mcp_servers: ["filesystem", "memory", "mcp-chirp", "mcp-azure-speech", "mcp-elevenlabs"]

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  max_agents_in_context: 10
  coordination_instructions: |
    This agent coordinates with other media agents:
    - Provides voiceovers for video-generation-agent workflows
    - Works with music-generation-agent for voice integration
    - Collaborates with video-editing-agent for dubbing and synchronization
    - Integrates with all media agents for comprehensive audio content creation
---
