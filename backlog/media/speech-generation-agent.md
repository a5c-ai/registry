# Speech Generation Agent

**Purpose**: Generates high-quality speech and voice synthesis from text using advanced AI models like Chirp 3, Azure Speech Services, and other MCP GenMedia text-to-speech services

## Key Features

- **Text-to-speech synthesis** using advanced AI voice models like Chirp 3, Azure TTS, ElevenLabs
- **Custom voice cloning** (with proper authorization) for personalized voice experiences
- **Multiple languages and accents** with support for 35+ languages and natural pronunciation
- **SSML markup support** for advanced speech control (pauses, emphasis, tone)
- **Emotional tone control** and speaking style variations (conversational, newscast, audiobook)
- **Professional audio quality** with multiple output formats and bitrates
- **Safety filtering and content validation** ensuring appropriate speech generation
- **Cross-agent integration** with Video Generation, Music Generation, and Audio Processing agents

## How it works

- Analyzes speech generation requests and text content
- Selects appropriate AI voice model based on requirements (Chirp 3, Azure TTS, ElevenLabs, etc.)
- Processes text content with SSML markup for enhanced control
- Generates speech with specified voice characteristics, language, and emotional tone
- Applies audio post-processing like normalization, enhancement, and format optimization
- Creates custom voice clones when requested and authorized
- Supports multiple languages and accents with natural pronunciation
- Validates generated content for quality, accuracy, and technical compliance
- Organizes outputs with comprehensive metadata and transcription verification

## Cross-Agent Workflow Integration

This agent is designed to work seamlessly with other media generation agents:

1. **Speech Generation** → **Video Generation** (voiceover addition and narration)
2. **Speech Generation** → **Music Generation** (voice integration and vocal additions)
3. **Speech Generation** → **Audio Processing Agent** (audio enhancement and mastering)
4. **Speech Generation** → **Video Editing Agent** (dubbing and voice synchronization)
5. **All Generation** → **Asset Optimization** (platform-specific audio optimization)

## MCP Integration

### MCP GenMedia Installation & Setup

This agent leverages the **MCP GenMedia** ecosystem from Google Cloud's Vertex AI Creative Studio. To set up MCP GenMedia:

- **Repository**: [GoogleCloudPlatform/vertex-ai-creative-studio](https://github.com/GoogleCloudPlatform/vertex-ai-creative-studio/tree/main/experiments/mcp-genmedia)
- **Installation Guide**: Follow the setup instructions in the [MCP GenMedia documentation](https://github.com/GoogleCloudPlatform/vertex-ai-creative-studio/tree/main/experiments/mcp-genmedia)
- **Prerequisites**: Google Cloud account with Vertex AI enabled, proper API credentials configured
- **Model Context Protocol**: Learn more about MCP at [https://modelcontextprotocol.io](https://modelcontextprotocol.io)

### Supported MCP Servers

- **Primary MCP Servers**:
  - `mcp-chirp` for Google Chirp 3 HD voices and custom voice generation
  - `mcp-azure-speech` for Azure Cognitive Services Speech
  - `mcp-elevenlabs` for ElevenLabs voice synthesis
  - `mcp-openai-tts` for OpenAI text-to-speech models
  - `mcp-aws-polly` for Amazon Polly voice synthesis
- **Advanced Features**: Custom voice cloning, SSML support, emotional tone control, speaking style variations
- **Quality Control**: Pronunciation accuracy validation, audio quality checks, content appropriateness filtering
- **Language Support**: 35+ languages with native pronunciation and cultural adaptation
