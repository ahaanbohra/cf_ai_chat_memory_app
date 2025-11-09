# AI Chat Memory App

A conversational AI chatbot built on Cloudflare's platform using Llama 3.3 (70B) via Workers AI. This application demonstrates stateful AI agents with persistent memory, real-time chat capabilities, and seamless deployment on Cloudflare's edge network.

## 🚀 Live Demo

**Try it now**: [https://agents-starter.ahaanbohra03.workers.dev](https://agents-starter.ahaanbohra03.workers.dev)

The chatbot is deployed on Cloudflare's edge network and ready to chat!

## Features

- **Conversational AI**: Powered by Llama 3.3 70B model running on Cloudflare Workers AI
- **Persistent Memory**: Chat history and context stored using Durable Objects
- **Real-time Communication**: WebSocket-based streaming responses for instant feedback
- **State Management**: Built-in state persistence and synchronization
- **Modern UI**: Clean, responsive React interface with dark/light theme support
- **Edge Deployment**: Runs globally on Cloudflare's edge network for low latency

## Architecture

This application fulfills all Cloudflare AI assignment requirements:

1. **LLM**: Llama 3.3 70B Instruct (FP8 Fast) via Workers AI
2. **Workflow/Coordination**: Cloudflare Workers + Durable Objects for orchestration
3. **User Input**: Real-time chat interface with streaming responses
4. **Memory/State**: Persistent conversation history via Durable Objects SQLite storage

### Tech Stack

- **Frontend**: React 19, TypeScript, Tailwind CSS
- **Backend**: Cloudflare Workers (serverless)
- **State**: Durable Objects with SQLite
- **AI**: Workers AI (Llama 3.3 70B)
- **Build Tool**: Vite
- **Package Manager**: npm

## Getting Started

### Prerequisites

- Node.js 18+ installed
- Cloudflare account (for deployment)

### Local Development

1. **Clone the repository**

```bash
git clone https://github.com/ahaanbohra/cf_ai_chat_memory_app.git
cd cf_ai_chat_memory_app/agents-starter
```

2. **Install dependencies**

```bash
npm install
```

3. **Start the development server**

```bash
npm start
```

4. **Open your browser**

Navigate to `http://localhost:5173/` to interact with the chatbot.

### Project Structure

```
agents-starter/
├── src/
│   ├── server.ts          # Durable Object agent implementation
│   ├── app.tsx            # React chat UI
│   ├── client.tsx         # Frontend entry point
│   ├── tools.ts           # Tool definitions (currently minimal)
│   ├── utils.ts           # Helper functions
│   └── components/        # React UI components
├── wrangler.jsonc         # Cloudflare Workers configuration
├── package.json           # Dependencies and scripts
└── vite.config.ts         # Vite build configuration
```

## How It Works

### 1. LLM Integration

The application uses Workers AI to run Llama 3.3 locally within Cloudflare's infrastructure:

```typescript
const workersai = createWorkersAI({ binding: this.env.AI });
const model = workersai("@cf/meta/llama-3.3-70b-instruct-fp8-fast");
```

### 2. Memory & State

Durable Objects provide persistent storage for each chat session:

- Each chat session has its own Durable Object instance
- Conversation history is automatically saved
- SQLite database stores messages and metadata
- State syncs automatically between client and server

### 3. Real-time Communication

WebSocket connections enable streaming responses:

- Client connects via WebSocket to Durable Object
- AI responses stream token-by-token
- UI updates in real-time as tokens arrive

### 4. Natural Conversation

The chatbot is designed for general-purpose conversation:

- No specialized tools or functions
- Answers questions using Llama 3.3's knowledge
- Maintains context throughout conversation
- Remembers information shared by users

## Deployment

Deploy to Cloudflare Workers:

```bash
npm run deploy
```

This will:
1. Build the application
2. Upload to Cloudflare Workers
3. Configure Durable Objects bindings
4. Provide a public URL

## Testing the Application

Try these example interactions:

```
User: "What's the capital of France?"
Bot: "The capital of France is Paris..."

User: "My name is Ahaan"
Bot: "Nice to meet you, Ahaan!..."

User: "What's my name?"
Bot: "Your name is Ahaan. I remember you told me earlier!"
```

## Configuration

### Wrangler Configuration

The `wrangler.jsonc` file configures:

- **AI Binding**: Access to Workers AI models
- **Durable Objects**: Persistent chat sessions
- **Compatibility Date**: Runtime features and APIs

### Model Selection

To use a different model, modify `src/server.ts`:

```typescript
const model = workersai("@cf/meta/llama-3.3-70b-instruct-fp8-fast");
// Change to any supported Workers AI model
```

## Performance Considerations

- **Edge Deployment**: Runs close to users for low latency
- **Streaming**: Token-by-token responses for better UX
- **Durable Objects**: Each session has dedicated compute
- **SQLite**: Efficient local storage without external databases

## Development Notes

### Why No Tools?

This implementation deliberately avoids specialized tools to showcase:
- Pure LLM capabilities without function calling overhead
- Natural conversation flow
- General-purpose question answering

### Memory Implementation

Memory is handled automatically by:
- Durable Objects state persistence
- Message history stored in SQLite
- Context passed to LLM on each request

## Troubleshooting

**Issue**: Blank screen on load
**Solution**: Hard refresh (Ctrl+Shift+R) or clear browser cache

**Issue**: Old responses appearing
**Solution**: Delete `.wrangler` folder and restart dev server

**Issue**: Model not responding
**Solution**: Check AI binding in `wrangler.jsonc` and ensure Workers AI is enabled

## License

MIT License - see LICENSE file for details

## Acknowledgments

Built for Cloudflare AI application assignment, demonstrating:
- Workers AI integration
- Durable Objects for state management
- Real-time chat with streaming responses
- Edge-native AI application architecture
