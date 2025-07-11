# Image Generation Agent

**Status**: ✅ IMPLEMENTED - Agent created and added to registry

**Purpose**: Generates high-quality images from text prompts using advanced AI models like Imagen, Flux, and other MCP GenMedia services

**Implementation**: Available at `/agents/media/image-generation-agent.agent.md`

## Key Features

- **Text-to-image generation** with multiple model options (Imagen 3/4, Flux, DALL-E, Stability AI)
- **Style control** (photorealistic, cartoon, watercolor, abstract, and more artistic styles)
- **Custom dimensions and aspect ratios** with platform-specific optimizations
- **Batch generation with variations** to provide multiple creative options
- **Quality optimization and format conversion** for different use cases
- **Safety filtering and content validation** ensuring appropriate content generation
- **Cross-agent integration** with Video Generation, Image Editing, and other media agents

## How it works

- Analyzes image generation requests and specifications
- Selects appropriate AI model based on requirements (Imagen 3/4, Flux, DALL-E, etc.)
- Processes text prompts and optional style parameters
- Generates multiple image variations when requested
- Applies post-processing like upscaling, format conversion, or optimization
- Validates generated content against safety and quality guidelines
- Organizes outputs with proper metadata and versioning

## MCP Integration

### MCP GenMedia Installation & Setup

This agent leverages the **MCP GenMedia** ecosystem from Google Cloud's Vertex AI Creative Studio. To set up MCP GenMedia:

- **Repository**: [GoogleCloudPlatform/vertex-ai-creative-studio](https://github.com/GoogleCloudPlatform/vertex-ai-creative-studio/tree/main/experiments/mcp-genmedia)
- **Installation Guide**: Follow the setup instructions in the [MCP GenMedia documentation](https://github.com/GoogleCloudPlatform/vertex-ai-creative-studio/tree/main/experiments/mcp-genmedia)
- **Prerequisites**: Google Cloud account with Vertex AI enabled, proper API credentials configured
- **Model Context Protocol**: Learn more about MCP at [https://modelcontextprotocol.io](https://modelcontextprotocol.io)

### Supported MCP Servers

- **Primary MCP Servers**: 
  - `mcp-imagen` for Google Imagen 3/4 models
  - `mcp-flux` for Black Forest Labs Flux models  
  - `mcp-dalle` for OpenAI DALL-E models
  - `mcp-stability-ai` for Stable Diffusion models
- **Fallback Options**: Multiple model providers for reliability
- **Quality Control**: Automatic content filtering and safety checks
- **Format Support**: PNG, JPEG, WebP, SVG generation capabilities

