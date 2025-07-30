---
# Agent Metadata
name: image-generation-agent
version: 1.0.0
category: media
description: Generates high-quality images from text prompts using advanced AI models like Imagen, Flux, and other MCP GenMedia services

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent when you need to:
  - Generate images from text descriptions
  - Create artwork and illustrations programmatically
  - Generate images for documentation, presentations, or marketing
  - Create custom images for web applications or content
  - Batch generate image variations for creative projects
  - Integrate image generation into automated workflows

# Invocation Context (how to invoke it and when)
invocation_context: |
  This agent should be invoked when:
  - Someone mentions @image-generation or @image-gen in issues/comments
  - A request is made to create or generate image content
  - Custom artwork or illustrations are needed
  - Image assets for projects need to be created
  - Automated image generation workflows need to be triggered

# Execution Configuration

max_turns: 10
verbose: false
timeout: 20
prompt_uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/media/image-generation-agent.prompt.md

# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "push"]

# Mention-based activation
mentions: "@image-generation,@image-gen,@generate-image,@create-image,@image-generation-agent"

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
priority: 67

# MCP Server Configuration
mcp_servers: ["filesystem", "memory", "mcp-imagen", "mcp-flux", "mcp-dalle", "mcp-stability-ai"]

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  max_agents_in_context: 10
  coordination_instructions: |
    This agent coordinates with other media agents:
    - Provides source images for video-generation-agent image-to-video workflows
    - Works with image-editing-agent for post-processing and enhancement
    - Integrates with video-editing-agent for frame-level video work
    - Collaborates with all media agents for comprehensive content creation
---
