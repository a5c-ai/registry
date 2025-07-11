# Music Generation Agent

**Status**: ✅ IMPLEMENTED - Agent created and added to registry

**Purpose**: Generates high-quality music and audio compositions from text prompts using advanced AI models like Lyria, MusicLM, and other MCP GenMedia audio services

**Implementation**: Available at `/agents/media/music-generation-agent.agent.md`

## Key Features

- **Text-to-music composition** using advanced AI models like Lyria, MusicLM, AIVA, Mubert
- **Genre and style control** across classical, electronic, jazz, rock, ambient, and more
- **Instrumentation specification** with detailed control over instruments and arrangements
- **Tempo and key control** for precise musical structure and harmony
- **Stem separation** providing individual instrument tracks for mixing
- **Professional audio formats** (MP3, WAV, FLAC, MIDI) with high-quality output
- **Safety filtering and copyright compliance** ensuring original compositions
- **Cross-agent integration** with Video Generation, Speech Generation, and Audio Processing agents

## How it works

- Analyzes music generation requests and creative specifications
- Selects appropriate AI model based on requirements (Lyria, MusicLM, AIVA, etc.)
- Processes text descriptions of musical style, mood, instrumentation, and structure
- Generates music compositions with specified duration, tempo, and genre parameters
- Applies audio post-processing like mastering, format conversion, and optimization
- Creates multiple variations and stems when requested
- Validates generated content for quality, copyright, and technical compliance
- Organizes outputs with comprehensive metadata and licensing information



## Cross-Agent Workflow Integration

This agent is designed to work seamlessly with other media generation agents:

1. **Music Generation** → **Video Generation** (soundtrack integration and synchronization)
2. **Music Generation** → **Speech Generation** (voice integration and vocal additions)
3. **Music Generation** → **Audio Processing Agent** (mastering and final enhancement)
4. **Music Generation** → **Video Editing Agent** (timeline synchronization)
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
  - `mcp-lyria` for Google Lyria text-to-music model
  - `mcp-musiclm` for MusicLM composition capabilities
  - `mcp-aiva` for AIVA AI music composition
  - `mcp-mubert` for Mubert generative music
  - `mcp-amper` for Amper Music AI composition
- **Advanced Features**: Multi-track composition, tempo control, key signature specification, dynamic arrangement
- **Quality Control**: Audio quality validation, copyright scanning, technical specification compliance
- **Format Support**: MP3, WAV, FLAC, MIDI with various bitrates and sample rates

