---
# Agent Metadata
name: image-editing-agent
version: 1.0.0
category: media
description: Performs advanced image editing and manipulation using AI-powered tools like inpainting, outpainting, upscaling, and style transfer through MCP GenMedia services

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent when you need to:
  - Edit and enhance existing images
  - Remove objects or backgrounds from images
  - Apply artistic effects and style transfers
  - Upscale images for higher resolution
  - Perform batch image processing operations
  - Create image variations and modifications

# Invocation Context (how to invoke it and when)
invocation_context: |
  This agent should be invoked when:
  - Someone mentions @image-editing or @image-edit in issues/comments
  - A request is made to edit or enhance image content
  - Image manipulation or enhancement workflows need to be triggered
  - Object removal or background replacement is required
  - Professional image editing and effects are needed

# Execution Configuration
model: claude-3-7-sonnet-20250219
max_turns: 10
verbose: false
timeout: 20
prompt_uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/media/image-editing-agent.prompt.md

# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "push"]

# Mention-based activation
mentions: "@image-editing,@image-edit,@edit-image,@enhance-image,@image-editing-agent"

# File patterns that might trigger this agent
paths:
  - "**/*.png"
  - "**/*.jpg"
  - "**/*.jpeg"
  - "**/*.webp"
  - "**/*.svg"
  - "**/images/**"
  - "**/img/**"
  - "**/assets/**"
  - "**/media/**"

# Priority (higher = runs first, media agents in 60-70 range)
priority: 66

# MCP Server Configuration
mcp_servers: ["filesystem", "memory", "mcp-imagen", "mcp-dalle", "mcp-stability-ai", "mcp-upscaler"]

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  max_agents_in_context: 10
  coordination_instructions: |
    This agent coordinates with other media agents:
    - Processes output from image-generation-agent for enhancement
    - Works with video-editing-agent for frame-level video editing
    - Collaborates with all media agents for comprehensive image processing
    - Provides enhanced images for video-generation-agent workflows
---
