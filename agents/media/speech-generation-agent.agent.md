---
# Agent Metadata
name: speech-generation-agent
version: 1.1.0
category: media
description: Generates high-quality speech and voice synthesis from text using advanced AI models like Chirp 3, Azure Speech Services, ElevenLabs, OpenAI TTS, AWS Polly and other MCP GenMedia text-to-speech services

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent when you need to:
  - Generate speech from text content with natural intonation
  - Create professional voiceovers for videos, presentations, or e-learning
  - Synthesize speech in 35+ languages with native accents
  - Generate audio content for accessibility and screen readers
  - Create custom voice experiences with specific emotional tones
  - Apply SSML markup for precise speech control
  - Integrate speech generation into automated workflows
  - Create audiobooks or podcast-style content
  - Generate voiceovers with specific emotional qualities
  - Produce accessible audio content for diverse audiences

# Invocation Context (how to invoke it and when)
invocation_context: |
  This agent should be invoked when:
  - Someone mentions @speech-generation, @speech-gen, or @speech-generation-agent in issues/comments
  - A request is made to create or generate speech content
  - Voiceovers or narration are needed for media projects
  - Text-to-speech conversion is required for accessibility
  - Speech with specific emotional qualities is needed
  - Multi-language speech synthesis is required
  - SSML-enhanced speech generation is needed
  - Custom voice creation is requested (with proper authorization)
  - Automated speech generation workflows need to be triggered
  - Voice content needs synchronization with other media

# Execution Configuration
model: claude-3-7-sonnet-20250219
max_turns: 10
verbose: false
timeout: 20
prompt_uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/media/speech-generation-agent.prompt.md

# Trigger Configuration
events: ["issues", "issue_comment", "pull_request", "push"]

# Mention-based activation
mentions: "@speech-generation,@speech-gen,@generate-speech,@text-to-speech,@speech-generation-agent,@voiceover,@voice-synthesis,@tts"

# File patterns that might trigger this agent
paths:
  - "**/*.mp3"
  - "**/*.wav"
  - "**/*.flac"
  - "**/*.m4a"
  - "**/*.ogg"
  - "**/audio/**"
  - "**/speech/**"
  - "**/voice/**"
  - "**/media/**"
  - "**/tts/**"
  - "**/voiceover/**"

# Priority (higher = runs first, media agents in 60-70 range)
priority: 62

# MCP Server Configuration
mcp_servers: ["filesystem", "memory", "mcp-chirp", "mcp-azure-speech", "mcp-elevenlabs", "mcp-openai-tts", "mcp-aws-polly"]

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  max_agents_in_context: 10
  coordination_instructions: |
    This agent coordinates with other media agents:
    - Provides voiceovers for video-generation-agent workflows
    - Works with music-generation-agent for voice integration with background music
    - Collaborates with video-editing-agent for dubbing, voice synchronization, and subtitles
    - Integrates with image-generation-agent for audio-visual content creation
    - Coordinates with content-writer-agent for script creation and refinement
    - Supports project-seeder-agent for initializing media projects with voice components
    - Integrates with all media agents for comprehensive audio content creation
    
    Workflow coordination patterns:
    - Video production: @content-writer-agent writes script → @speech-generation-agent creates voiceover → @video-editing-agent synchronizes
    - Multimedia: @image-generation-agent creates visuals → @speech-generation-agent adds narration → @music-generation-agent adds background music
    - Accessibility: @content-writer-agent creates content → @speech-generation-agent creates accessible audio versions
---
