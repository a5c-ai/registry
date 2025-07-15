---
# Agent Metadata
name: video-editing-agent
version: 1.0.0
category: media
description: Performs advanced video editing and post-production using AI-powered tools like video inpainting, object tracking, effects application, and automated editing through MCP GenMedia services

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent when you need to:
  - Edit and enhance existing video content
  - Remove objects or apply inpainting to video frames
  - Apply professional video effects and transitions
  - Perform automated video editing and post-production
  - Stabilize and enhance video quality
  - Create complex multi-track video projects

# Invocation Context (how to invoke it and when)
invocation_context: |
  This agent should be invoked when:
  - Someone mentions @video-editing or @video-edit in issues/comments
  - A request is made to edit or enhance video content
  - Video post-production workflows need to be triggered
  - Object removal or video inpainting is required
  - Professional video editing and effects are needed

# Execution Configuration
model: claude-3-7-sonnet-20250219
max_turns: 15
verbose: false
timeout: 30
prompt_uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/media/video-editing-agent.prompt.md

# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "push"]

# Mention-based activation
mentions: "@video-editing,@video-edit,@edit-video,@video-post,@video-editing-agent"

# File patterns that might trigger this agent
paths:
  - "**/*.mp4"
  - "**/*.mov"
  - "**/*.avi"
  - "**/*.webm"
  - "**/video/**"
  - "**/videos/**"
  - "**/media/**"
  - "**/editing/**"

# Priority (higher = runs first, media agents in 60-70 range)
priority: 64

# MCP Server Configuration
mcp_servers: ["filesystem", "memory", "mcp-veo", "mcp-runway", "mcp-ffmpeg-ai", "mcp-upscaler"]

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  max_agents_in_context: 10
  coordination_instructions: |
    This agent coordinates with other media agents:
    - Receives output from video-generation-agent for post-processing
    - Works with music-generation-agent for soundtrack integration
    - Integrates with speech-generation-agent for dubbing and voiceover
    - Collaborates with image-editing-agent for frame-level enhancements
    - Coordinates with all media agents for comprehensive video production
---
