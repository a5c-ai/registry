---
# Agent Metadata
name: video-editing-agent
version: 1.1.0
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
  - Color grade and correct video footage
  - Convert between video formats with AI enhancement
  - Add special effects and visual enhancements
  - Synchronize audio and video elements

# Invocation Context (how to invoke it and when)
invocation_context: |
  This agent should be invoked when:
  - Someone mentions @video-editing, @video-edit, or @video-editing-agent in issues/comments
  - A request is made to edit or enhance video content
  - Video post-production workflows need to be triggered
  - Object removal or video inpainting is required
  - Professional video editing and effects are needed
  - Video quality enhancement is requested
  - Audio-video synchronization is needed
  - Color grading or correction is requested
  - Timeline editing and compilation is required

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
  - "**/*.mkv"
  - "**/video/**"
  - "**/videos/**"
  - "**/media/**"
  - "**/editing/**"
  - "**/post-production/**"

# Priority (higher = runs first, media agents in 60-70 range)
priority: 64

# MCP Server Configuration
mcp_servers: ["filesystem", "memory", "mcp-veo", "mcp-runway", "mcp-ffmpeg-ai", "mcp-upscaler", "mcp-davinci"]

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
    - Coordinates with content-writer-agent for caption generation
    - Supports project-seeder-agent for initializing video projects
    - Integrates with all media agents for comprehensive video production
    
    Workflow coordination patterns:
    - Video production pipeline: @video-generation-agent creates raw video → @video-editing-agent enhances and edits
    - Audio-visual integration: @music-generation-agent creates soundtrack → @video-editing-agent synchronizes with video
    - Voiceover addition: @speech-generation-agent creates narration → @video-editing-agent integrates with video timeline
    - Complete production: @content-writer-agent writes script → @video-generation-agent creates video → @music-generation-agent adds soundtrack → @speech-generation-agent adds voiceover → @video-editing-agent finalizes
---