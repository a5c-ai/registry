---
# Agent Metadata
name: music-generation-agent
version: 1.1.0
category: media
description: Generates high-quality music and audio compositions from text prompts using advanced AI models like Lyria, MusicLM, AIVA, Soundraw, and other MCP GenMedia audio services

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent when you need to:
  - Generate music compositions from text descriptions
  - Create background music for videos or presentations
  - Compose music in specific genres and styles
  - Generate instrumental tracks and soundscapes
  - Create custom audio content for projects
  - Integrate music generation into automated workflows
  - Produce royalty-free music for commercial use
  - Generate mood-specific music for different contexts
  - Create adaptive music for interactive media
  - Provide music stems for flexible mixing

# Invocation Context (how to invoke it and when)
invocation_context: |
  This agent should be invoked when:
  - Someone mentions @music-generation, @music-gen, or @music-generation-agent in issues/comments
  - A request is made to create or generate music content
  - Background music or soundtracks are needed
  - Custom audio compositions are required
  - Automated music generation workflows need to be triggered
  - Music is needed for video or media projects
  - Project requires original soundtrack or audio elements
  - Audio generation tasks require AI assistance

# Execution Configuration
model: claude-3-7-sonnet-20250219
max_turns: 10
verbose: false
timeout: 25
prompt_uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/media/music-generation-agent.prompt.md

# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "push"]

# Mention-based activation
mentions: "@music-generation,@music-gen,@generate-music,@create-music,@music-generation-agent,@soundtrack,@audio-generation"

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
mcp_servers: ["filesystem", "memory", "mcp-lyria", "mcp-musiclm", "mcp-aiva", "mcp-soundraw", "mcp-mubert", "mcp-amper"]

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
    - Integrates with image-generation-agent for audio-visual projects
    - Coordinates with content-writer-agent for lyric creation
    - Supports project-seeder-agent for initializing media projects
    - Integrates with all media agents for comprehensive content creation
    
    Workflow coordination patterns:
    - Video production: @music-generation-agent creates soundtrack → @video-editing-agent synchronizes
    - Multimedia: @image-generation-agent creates visuals → @music-generation-agent adds audio
    - Content creation: @content-writer-agent writes lyrics → @music-generation-agent composes music
---
