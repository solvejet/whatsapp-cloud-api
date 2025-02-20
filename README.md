# WhatsApp Cloud API Wrapper

A powerful, type-safe, and feature-rich wrapper for the WhatsApp Cloud API, built with TypeScript.

[![npm version](https://img.shields.io/npm/v/whatsapp-cloud-api.svg)](https://www.npmjs.com/package/whatsapp-cloud-api-wrapper)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.3.3-blue.svg)](https://www.typescriptlang.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Features

- 📝 **Type Safety**: Full TypeScript support with strict type checking
- 🚀 **Performance**: Built-in caching and rate limiting
- 🔒 **Security**: Input validation and comprehensive error handling
- 📨 **Complete API Coverage**: Support for all WhatsApp message types
- 🎣 **Webhook Support**: Easy-to-use webhook handling
- 📁 **Media Management**: Simple media upload, download, and deletion
- 📦 **Zero Dependencies**: Minimal core with optional enhancements
- 📚 **Extensive Documentation**: Detailed guides and examples

## Installation

```bash
npm install @solvejet/whatsapp-cloud-api
```

## Quick Start

```typescript
import { WhatsAppClient } from '@solvejet/whatsapp-cloud-api';

// Initialize the client
const client = new WhatsAppClient({
  accessToken: 'your-access-token',
  phoneNumberId: 'your-phone-number-id',
});

// Send a message
await client.sendMessage({
  to: '1234567890',
  type: 'text',
  text: { body: 'Hello from WhatsApp API!' },
});
```

## Package Architecture

The package is structured for maximum modularity and extensibility:

[Package Architecture Diagram]

## Message Handling

### Outbound Messages

```typescript
// Text Message
await client.sendMessage({
  to: '1234567890',
  type: 'text',
  text: { body: 'Hello World!' },
});

// Image Message
await client.sendMessage({
  to: '1234567890',
  type: 'image',
  image: {
    url: 'https://example.com/image.jpg',
    caption: 'Check this out!',
  },
});

// Template Message
await client.sendTemplate({
  to: '1234567890',
  template: {
    name: 'hello_world',
    language: {
      code: 'en_US',
    },
    components: [
      {
        type: 'body',
        parameters: [
          {
            type: 'text',
            text: 'John',
          },
        ],
      },
    ],
  },
});
```

### Inbound Messages (Webhooks)

```typescript
import express from 'express';
import { createWebhookHandler } from '@solvejet/whatsapp-cloud-api';

const app = express();
const webhookHandler = createWebhookHandler({
  verifyToken: 'your-verify-token',
});

// Handle incoming messages
webhookHandler.onMessage((message) => {
  console.log('Received:', message);
});

app.post('/webhook', webhookHandler.middleware());
```

## Message Flow

Here's how messages flow through the system:

[Message Flow Diagram]

## Media Management

The wrapper provides comprehensive media handling capabilities:

[Media Handling Diagram]

### Media Upload

```typescript
// Upload from URL
const mediaId = await client.uploadMedia({
  url: 'https://example.com/image.jpg',
  type: 'image/jpeg',
});

// Upload from Buffer
const mediaId = await client.uploadMedia({
  buffer: imageBuffer,
  type: 'image/jpeg',
  filename: 'image.jpg',
});
```

### Media Download

```typescript
// Get media URL
const mediaUrl = await client.getMediaUrl('media-id');

// Download media
const mediaBuffer = await client.downloadMedia('media-id');
```

### Media Deletion

```typescript
// Delete media
await client.deleteMedia('media-id');
```

## Error Handling

The wrapper provides detailed error information:

```typescript
try {
  await client.sendMessage({
    to: 'invalid-number',
    type: 'text',
    text: { body: 'Hello' },
  });
} catch (error) {
  if (error instanceof WhatsAppError) {
    console.error('Code:', error.code);
    console.error('Message:', error.message);
    console.error('Details:', error.details);
  }
}
```

## Advanced Configuration

### Rate Limiting

```typescript
const client = new WhatsAppClient({
  accessToken: 'your-token',
  phoneNumberId: 'your-phone-id',
  rateLimit: {
    maxRequests: 200,
    windowMs: 60000, // 1 minute
    strategy: 'sliding',
  },
});
```

### Caching

```typescript
const client = new WhatsAppClient({
  accessToken: 'your-token',
  phoneNumberId: 'your-phone-id',
  cache: {
    type: 'redis',
    config: {
      host: 'localhost',
      port: 6379,
    },
    ttl: 3600, // 1 hour
  },
});
```

## TypeScript Support

The package includes comprehensive type definitions:

```typescript
interface MessageOptions {
  to: string;
  type: MessageType;
  text?: TextMessage;
  image?: ImageMessage;
  video?: VideoMessage;
  document?: DocumentMessage;
  template?: TemplateMessage;
}

interface TextMessage {
  body: string;
  preview_url?: boolean;
}

// ... more type definitions
```

## Contributing

We welcome contributions! Here's how you can help:

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m 'Add amazing feature'`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

## Development

```bash
# Install dependencies
npm install

# Run tests
npm test

# Build
npm run build

# Lint
npm run lint
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

- 📘 [Documentation](https://github.com/solvejet/whatsapp-cloud-api/wiki)
- 🐛 [Issue Tracker](https://github.com/solvejet/whatsapp-cloud-api/issues)
- 💬 [Discussions](https://github.com/solvjejetwhatsapp-cloud-api/discussions)

## Credits

Developed and maintained by [Your Name/Organization]

---

Made with ❤️ by @karansxa, for developers
