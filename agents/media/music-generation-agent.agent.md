---
# Agent Metadata
name: music-generation-agent
version: 1.0.0
category: media
description: Generates high-quality music and audio compositions from text prompts using advanced AI models like Lyria, MusicLM, and other MCP GenMedia audio services

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent when you need to:
  - Generate music compositions from text descriptions
  - Create background music for videos or presentations
  - Compose music in specific genres and styles
  - Generate instrumental tracks and soundscapes
  - Create custom audio content for projects
  - Integrate music generation into automated workflows

# Invocation Context (how to invoke it and when)
invocation_context: |
  This agent should be invoked when:
  - Someone mentions @music-generation or @music-gen in issues/comments
  - A request is made to create or generate music content
  - Background music or soundtracks are needed
  - Custom audio compositions are required
  - Automated music generation workflows need to be triggered

# Execution Configuration

max_turns: 10
verbose: false
timeout: 25
prompt_uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/media/music-generation-agent.prompt.md

# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "push"]

# Mention-based activation
mentions: "@music-generation,@music-gen,@generate-music,@create-music,@music-generation-agent"

# File patterns that might trigger this agent
paths:
  - "**/*.mp3"
  - "**/*.wav"
  - "**/*.flac"
  - "**/*.midi"
  - "**/*.mid"
  - "**/audio/**"
  - "**/music/**"
  - "**/sound/**"
  - "**/media/**"

# Priority (higher = runs first, media agents in 60-70 range)
priority: 63

# MCP Server Configuration
mcp_servers: ["filesystem", "memory", "mcp-lyria", "mcp-musiclm", "mcp-aiva"]

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  max_agents_in_context: 10
  coordination_instructions: |
    This agent coordinates with other media agents:
    - Provides soundtracks for video-generation-agent workflows
    - Works with speech-generation-agent for voice integration
    - Collaborates with video-editing-agent for audio synchronization
    - Integrates with all media agents for comprehensive content creation
---
