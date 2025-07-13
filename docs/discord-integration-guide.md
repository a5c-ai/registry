# Discord Integration Guide for A5C

This guide explains how to integrate A5C agents with Discord to enable seamless interaction through Discord channels and direct messages.

## Overview

The A5C Discord integration provides:

1. Two-way communication between Discord and A5C agents
2. Command processing through Discord channels
3. Event handling for Discord activities
4. User authentication and permissions management
5. Thread and channel management capabilities

## Setup Instructions

### Prerequisites

- Node.js (v16+)
- npm or yarn
- A Discord server with administrative permissions
- A Discord Developer account

### Step 1: Create a Discord Application

1. Go to the [Discord Developer Portal](https://discord.com/developers/applications)
2. Click "New Application" and give it a name
3. Navigate to the "Bot" tab and click "Add Bot"
4. Under the "Privileged Gateway Intents" section, enable:
   - SERVER MEMBERS INTENT
   - MESSAGE CONTENT INTENT
   - PRESENCE INTENT
5. Copy your bot token (keep this secure!)

### Step 2: Add Bot to Your Server

1. Go to the "OAuth2" tab in the Developer Portal
2. Select "bot" under the "SCOPES" section
3. Select the following permissions:
   - Manage Channels
   - Manage Roles
   - Manage Messages
   - Read Messages/View Channels
   - Send Messages
   - Embed Links
   - Attach Files
   - Create Public Threads
   - Manage Threads
   - Read Message History
   - Add Reactions
4. Copy the generated URL and paste it in your browser
5. Select your server and authorize the bot

### Step 3: Configure Environment Variables

Add the following variables to your environment or .env file:

```
DISCORD_TOKEN=your_bot_token_here
DISCORD_GUILD_ID=your_server_id_here
```

To find your server ID:
1. Enable Developer Mode in Discord (Settings > Advanced)
2. Right-click on your server icon and select "Copy ID"

### Step 4: Install Discord.js

Install discord.js globally or in your project:

```bash
# Global installation
npm install -g discord.js

# Project installation
npm install discord.js
```

## Using the Discord Manager Agent

The Discord Manager Agent handles all Discord integration activities. You can use it by:

1. Mentioning it in commit messages, PR descriptions, or comments using: `@discord-manager`
2. Configuring it in your A5C setup to respond to specific events

### Example Agent Communication

To have an agent interact with Discord:

1. Mention the Discord Manager Agent: `@discord-manager`
2. Specify the action and target Discord channel: `Please send a message to #announcements with the latest build status`

## Integration Code Examples

### Basic Bot Setup

```javascript
const { Client, GatewayIntentBits, Partials } = require('discord.js');

const client = new Client({
  intents: [
    GatewayIntentBits.Guilds,
    GatewayIntentBits.GuildMessages,
    GatewayIntentBits.MessageContent,
    GatewayIntentBits.GuildMembers
  ],
  partials: [Partials.Channel]
});

client.once('ready', () => {
  console.log(`Logged in as ${client.user.tag}`);
});

client.on('messageCreate', async (message) => {
  // Ignore messages from bots
  if (message.author.bot) return;
  
  // Process commands or mentions here
  if (message.content.includes('@a5c')) {
    // Handle A5C agent requests
    await message.reply('Processing your request...');
    // Forward to appropriate agent
  }
});

client.login(process.env.DISCORD_TOKEN);
```

### Sending Messages to Channels

```javascript
async function sendMessageToChannel(channelId, message) {
  try {
    const channel = await client.channels.fetch(channelId);
    if (!channel) throw new Error('Channel not found');
    
    await channel.send(message);
    return true;
  } catch (error) {
    console.error('Error sending message:', error);
    return false;
  }
}
```

### Creating Threads for Discussions

```javascript
async function createThread(channelId, threadName, message) {
  try {
    const channel = await client.channels.fetch(channelId);
    if (!channel) throw new Error('Channel not found');
    
    // Send initial message and create thread from it
    const sentMessage = await channel.send(message);
    const thread = await sentMessage.startThread({
      name: threadName,
      autoArchiveDuration: 1440 // Archive after 24 hours of inactivity
    });
    
    return thread.id;
  } catch (error) {
    console.error('Error creating thread:', error);
    return null;
  }
}
```

## Best Practices

1. **Rate Limiting**: Be mindful of Discord API rate limits
2. **Error Handling**: Implement robust error handling for all Discord interactions
3. **Permissions**: Check permissions before attempting operations
4. **User Experience**: Keep responses clear and concise
5. **Security**: Never expose your bot token or sensitive information
6. **Testing**: Test interactions in a dedicated testing channel before deploying

## Troubleshooting

### Common Issues

1. **Bot not responding**: Verify token and intents configuration
2. **Permission errors**: Check bot permissions in your server
3. **Rate limiting**: Implement backoff strategies when hitting rate limits
4. **Missing mentions**: Ensure MESSAGE_CONTENT intent is enabled

### Diagnostic Tools

1. Check the Discord Developer Portal for error messages
2. Enable debug logs in your Discord.js implementation
3. Use the Discord API debugging tools to trace requests

## Additional Resources

- [Discord.js Documentation](https://discord.js.org/)
- [Discord Developer Portal](https://discord.com/developers/docs)
- [A5C Discord Agent Repository](https://github.com/a5c-ai/registry/tree/main/agents/communication)

For further assistance, please contact the A5C support team or open an issue in the GitHub repository.