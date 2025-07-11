# Image Editing Agent

**Purpose**: Performs advanced image editing and manipulation using AI-powered tools like inpainting, outpainting, upscaling, and style transfer through MCP GenMedia editing services

## Key Features

- **AI-powered inpainting and outpainting** for seamless content filling and image extension
- **Object removal and background replacement** with intelligent content-aware fill
- **Style transfer and artistic effects** transforming images with various artistic styles
- **Super-resolution upscaling** using advanced AI models (Real-ESRGAN, ESRGAN) for quality enhancement
- **Color correction and enhancement** with professional-grade adjustment tools
- **Batch processing capabilities** for efficient handling of multiple images
- **Version control and edit history** maintaining detailed records of all editing operations
- **Cross-agent integration** with Image Generation, Video Generation, and Asset Optimization agents

## How it works

- Analyzes image editing requests and source materials
- Selects appropriate AI editing tools based on requirements (Imagen editing, Photoshop AI, DALL-E variations, etc.)
- Processes input images with specified editing operations
- Applies advanced techniques like inpainting, outpainting, background removal, and object manipulation
- Performs quality enhancement through upscaling, denoising, and restoration
- Creates style transfers and artistic transformations when requested
- Validates edited content for quality, consistency, and technical compliance
- Maintains edit history and version control for iterative improvements
- Organizes outputs with comprehensive before/after comparisons and metadata


## Cross-Agent Workflow Integration

This agent is designed to work seamlessly with other media generation agents:

1. **Image Generation** → **Image Editing Agent** (post-processing and enhancement)
2. **Image Editing** → **Video Generation** (animated versions of edited images)
3. **Image Editing** → **Asset Optimizer Agent** (web and platform optimization)
4. **Image Editing** → **Video Editing Agent** (integration into video workflows)
5. **All Editing** → **Quality Assurance** (automated quality validation)

## MCP Integration

### MCP GenMedia Installation & Setup

This agent leverages the **MCP GenMedia** ecosystem from Google Cloud's Vertex AI Creative Studio. To set up MCP GenMedia:

- **Repository**: [GoogleCloudPlatform/vertex-ai-creative-studio](https://github.com/GoogleCloudPlatform/vertex-ai-creative-studio/tree/main/experiments/mcp-genmedia)
- **Installation Guide**: Follow the setup instructions in the [MCP GenMedia documentation](https://github.com/GoogleCloudPlatform/vertex-ai-creative-studio/tree/main/experiments/mcp-genmedia)
- **Prerequisites**: Google Cloud account with Vertex AI enabled, proper API credentials configured
- **Model Context Protocol**: Learn more about MCP at [https://modelcontextprotocol.io](https://modelcontextprotocol.io)

### Supported MCP Servers

- **Primary MCP Servers**:
  - `mcp-imagen-edit` for Google Imagen editing capabilities
  - `mcp-dalle-edit` for OpenAI DALL-E image variations and editing
  - `mcp-stability-edit` for Stable Diffusion inpainting and editing
  - `mcp-photoshop-ai` for Adobe Photoshop AI features
  - `mcp-upscaler` for AI-powered image upscaling (Real-ESRGAN, ESRGAN)
- **Advanced Features**: Inpainting, outpainting, object removal, background replacement, style transfer, super-resolution
- **Quality Control**: Edge preservation, color consistency, artifact detection, quality assessment
- **Format Support**: Lossless editing workflows with support for transparency and high bit-depth images
