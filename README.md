# Deep Agent - AI Chat Assistant

A modern, streaming AI chat application built with Next.js 15, TypeScript, and OpenAI-compatible APIs. Features a clean, ChatGPT-style interface with support for multiple LLM providers.

## Features

- 🚀 **Streaming Chat Interface** - Real-time streaming responses with Server-Sent Events (SSE)
- 🎨 **Modern UI** - Clean, ChatGPT-style interface with dark/light theme support
- 🔌 **Multi-Provider Support** - Supports OpenAI and Qwen (通义千问) APIs
- 📝 **Markdown Rendering** - Rich markdown support with syntax highlighting
- 🎯 **Type-Safe** - Built with TypeScript for better developer experience
- ⚡ **Fast** - Built with Next.js 15 and Turbopack for optimal performance

## Getting Started

### Prerequisites

- Node.js 18+ 
- npm or yarn
- API key for at least one LLM provider (OpenAI or Qwen)

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd deep-agent
```

2. Install dependencies:
```bash
npm install
```

3. Create a `.env.local` file in the root directory:
```env
# Required: At least one provider API key
OPENAI_API_KEY=your_openai_api_key_here
# OR
QWEN_API_KEY=your_qwen_api_key_here

# Optional: Provider selection (defaults to 'openai' or 'qwen' based on available keys)
PROVIDER=openai

# Optional: Custom model names
OPENAI_MODEL=gpt-4o-mini
QWEN_MODEL=qwen-max

# Optional: Custom API URLs
OPENAI_API_URL=https://api.openai.com/v1
QWEN_API_URL=https://dashscope.aliyuncs.com/compatible-mode/v1

# Optional: Authentication headers (for production)
DEFAULT_INTERNAL_USER_ID=dev-user
DEFAULT_TENANT_ID=dev-tenant
ALLOWED_ORIGINS=http://localhost:3000

# Optional: Debugging
PROMPT_TRACE=false
PROMPT_DEBUG=false
```

4. Run the development server:
```bash
npm run dev
```

5. Open [http://localhost:3000](http://localhost:3000) in your browser.

## Available Scripts

- `npm run dev` - Start the Next.js development server with Turbopack
- `npm run build` - Create an optimized production build
- `npm run start` - Run the production server
- `npm run lint` - Lint all source files with ESLint

## Project Structure

```
deep-agent/
├── src/
│   ├── app/
│   │   ├── api/
│   │   │   └── chat/          # Chat API route (SSE streaming)
│   │   ├── page.tsx           # Main chat page
│   │   └── layout.tsx         # Root layout
│   ├── components/
│   │   ├── ChatWindow/        # Main chat interface component
│   │   ├── MessageBubble.tsx  # Message display component
│   │   ├── MarkdownRenderer.tsx # Markdown rendering with syntax highlighting
│   │   └── ...                # Other UI components
│   ├── hooks/
│   │   ├── useChat.ts         # Chat state management hook
│   │   ├── useAutoScroll.ts   # Auto-scroll functionality
│   │   ├── useDarkMode.ts     # Dark mode detection
│   │   └── useTheme.ts        # Theme management
│   └── lib/
│       ├── providers/         # LLM provider abstraction (OpenAI, Qwen)
│       └── prompts/           # Prompt building utilities
└── public/                    # Static assets
```

## API Endpoints

### POST `/api/chat`

Streaming chat endpoint that accepts messages and returns SSE stream.

**Request:**
```json
{
  "messages": [
    { "role": "user", "content": "Hello!" }
  ],
  "provider": "openai" // optional
}
```

**Response:** Server-Sent Events (SSE) stream with:
- `metadata` - Request metadata (requestId, model, provider)
- `content` - Streaming text chunks
- `done` - Completion signal
- `error` - Error messages

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `OPENAI_API_KEY` | Yes* | OpenAI API key |
| `QWEN_API_KEY` | Yes* | Qwen (通义千问) API key |
| `PROVIDER` | No | Default provider: `openai` or `qwen` |
| `OPENAI_MODEL` | No | OpenAI model (default: `gpt-4o-mini`) |
| `QWEN_MODEL` | No | Qwen model (default: `qwen-max`) |
| `DEFAULT_INTERNAL_USER_ID` | No | Default user ID for dev (default: `dev-user`) |
| `DEFAULT_TENANT_ID` | No | Default tenant ID for dev (default: `dev-tenant`) |
| `ALLOWED_ORIGINS` | No | Comma-separated list of allowed CORS origins |
| `PROMPT_TRACE` | No | Enable prompt tracing for debugging |

*At least one provider API key is required.

## Features in Detail

### Multi-Provider Support

The application supports multiple LLM providers through a unified interface:
- **OpenAI** - Full OpenAI API compatibility
- **Qwen** - Alibaba Cloud's Qwen models

You can switch providers in the UI or via the `provider` parameter in API requests.

### Streaming Responses

All responses are streamed using Server-Sent Events (SSE) for real-time user experience. The chat interface updates as tokens are received.

### Theme Support

- Light mode
- Dark mode  
- System preference (auto-detect)

Theme preference is saved in localStorage and persists across sessions.

### Markdown Rendering

Full markdown support including:
- Headers, lists, links
- Code blocks with syntax highlighting
- Tables, blockquotes
- Inline code

## Development

### Tech Stack

- **Framework:** Next.js 15 (App Router)
- **Language:** TypeScript
- **Styling:** Tailwind CSS
- **Markdown:** react-markdown with remark/rehype plugins
- **LLM SDK:** OpenAI SDK (compatible with Qwen)

### Code Style

- ESLint for linting
- TypeScript strict mode
- Functional components with hooks
- Server Components where appropriate

## License

[Add your license here]

## Contributing

[Add contributing guidelines here]
