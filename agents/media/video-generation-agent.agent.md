---
# Agent Metadata
name: video-generation-agent
version: 1.0.0
category: media
description: Generates high-quality videos from text prompts, images, or video clips using advanced AI models like Veo 2/3, Luma AI, and other MCP GenMedia services

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent when you need to:
  - Generate videos from text descriptions
  - Convert static images into dynamic video content
  - Transform existing videos with style changes
  - Create videos with specific camera movements and effects
  - Produce professional-quality video content for various platforms
  - Integrate video generation into automated workflows

# Invocation Context (how to invoke it and when)
invocation_context: |
  This agent should be invoked when:
  - Someone mentions @video-generation or @video-gen in issues/comments
  - A request is made to create or generate video content
  - Image-to-video conversion is needed
  - Video enhancement or style transfer is required
  - Automated video production workflows need to be triggered

# Execution Configuration
model: claude-3-7-sonnet-20250219
max_turns: 15
verbose: false
timeout: 30
prompt_uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/media/video-generation-agent.prompt.md

# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "push"]

# Mention-based activation
mentions: "@video-generation,@video-gen,@generate-video,@create-video,@video-generation-agent"

# File patterns that might trigger this agent
paths:
  - "**/*.mp4"
  - "**/*.mov"
  - "**/*.avi"
  - "**/*.webm"
  - "**/video/**"
  - "**/videos/**"
  - "**/media/**"

# Priority (higher = runs first, media agents in 60-70 range)
priority: 65

# MCP Server Configuration
mcp_servers: ["filesystem", "memory", "mcp-veo", "mcp-luma", "mcp-runway", "mcp-imagen"]

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  max_agents_in_context: 10
  coordination_instructions: |
    This agent coordinates with other media agents:
    - Works with image-generation-agent for image-to-video workflows
    - Collaborates with music-generation-agent for soundtrack integration
    - Integrates with speech-generation-agent for voiceover addition
    - Passes output to video-editing-agent for post-processing
    - Coordinates with all media agents for comprehensive content creation
---
