## CRITICAL NEXT.JS 15 BREAKING CHANGES

### React 19 Required
- Minimum React 19 is required
- Use `useActionState` instead of deprecated `useFormState`
- `useFormStatus` includes additional keys: `data`, `method`, `action`

### Async Request APIs (BREAKING CHANGE)
These APIs are now **asynchronous** and must be awaited:

**cookies()**
```tsx
// ✅ Correct Next.js 15
const cookieStore = await cookies()
const token = cookieStore.get('token')

// ❌ Wrong - Next.js 14 pattern
const cookieStore = cookies()
```

**headers()**
```tsx
// ✅ Correct Next.js 15
const headersList = await headers()
const userAgent = headersList.get('user-agent')
```

**draftMode()**
```tsx
// ✅ Correct Next.js 15
const { isEnabled } = await draftMode()
```

**params & searchParams**
```tsx
// ✅ Correct Next.js 15 - Page
type Params = Promise<{ slug: string }>
type SearchParams = Promise<{ [key: string]: string | string[] | undefined }>

export default async function Page(props: {
  params: Params
  searchParams: SearchParams
}) {
  const params = await props.params
  const searchParams = await props.searchParams
  const { slug } = params
  const { query } = searchParams
}

// ✅ For generateMetadata
export async function generateMetadata(props: { params: Params }) {
  const params = await props.params
  const { slug } = params
}

// ✅ Route handlers
export async function GET(request: Request, { params }: { params: Params }) {
  const resolvedParams = await params
  const { slug } = resolvedParams
}
```

**Client Components - use React's `use()` hook**
```tsx
'use client'
import { use } from 'react'

export default function ClientPage(props: { params: Params }) {
  const params = use(props.params)
  const { slug } = params
}
```

### Caching Changes
- **fetch()** requests are NOT cached by default
- **Route Handlers** GET methods are NOT cached by default

```tsx
// ✅ Explicit caching
const data = await fetch('https://api.example.com', { cache: 'force-cache' })

// ✅ Opt entire layout/page into caching
export const fetchCache = 'default-cache'

// ✅ Cache route handlers
export const dynamic = 'force-static'
export async function GET() { /* ... */ }
```

### Client Router Cache
- Page segments no longer reused by default
- Use `staleTimes` config to opt-in:

```js
// next.config.js
const nextConfig = {
  experimental: {
    staleTimes: {
      dynamic: 30,
      static: 180,
    },
  },
}
```

## ALWAYS USE THESE PATTERNS

### Page Components
```tsx
type Params = Promise<{ id: string }>
type SearchParams = Promise<{ tab?: string }>

export default async function Page(props: {
  params: Params
  searchParams: SearchParams
}) {
  const params = await props.params
  const searchParams = await props.searchParams
  // ... rest of component
}
```

### Layout Components
```tsx
type Params = Promise<{ slug: string }>

export default async function Layout(props: {
  children: React.ReactNode
  params: Params
}) {
  const params = await props.params
  // ... rest of component
}
```

### Server Actions
```tsx
async function submitForm(formData: FormData) {
  'use server'
  const cookieStore = await cookies()
  const headersList = await headers()
  // ... action logic
}
```

## MIGRATION COMMANDS
```bash
# Auto-upgrade
npx @next/codemod@canary upgrade latest

# Manual upgrade
npm i next@latest react@latest react-dom@latest eslint-config-next@latest
```

## CONFIGURATION UPDATES
```js
// next.config.js - Updated config names
const nextConfig = {
  // ✅ Correct - renamed from experimental
  bundlePagesRouterDependencies: true,
  serverExternalPackages: ['package-name'],
  
  // ❌ Wrong - old names
  // experimental: { bundlePagesExternals: true }
  // experimental: { serverComponentsExternalPackages: ['package-name'] }
}
```

## PACKAGE IMPORTS
```tsx
// ✅ Correct
import { Inter } from 'next/font/google'

// ❌ Wrong - package removed
// import { Inter } from '@next/font/google'
```

**CRITICAL**: Always await `cookies()`, `headers()`, `draftMode()`, `params`, and `searchParams` in Next.js 15. The old synchronous patterns will break your application.

# Vercel AI SDK v5 Migration

## CRITICAL AI SDK v5 BREAKING CHANGES

### Package Structure Changes (BREAKING)

**React hooks moved to separate package:**
```tsx
// ❌ AI SDK v4
import { useChat } from 'ai/react';

// ✅ AI SDK v5
import { useChat } from '@ai-sdk/react';
```

**RSC functions moved:**
```tsx
// ❌ AI SDK v4
import { createStreamableValue } from 'ai/rsc';

// ✅ AI SDK v5
import { createStreamableValue } from '@ai-sdk/rsc';
```

**Install required packages:**
```bash
npm install ai @ai-sdk/react @ai-sdk/rsc zod@3.25.0
```

### Core Type Renames (BREAKING)

**Message types:**
```tsx
// ❌ AI SDK v4
import { CoreMessage, Message, convertToCoreMessages } from 'ai';

// ✅ AI SDK v5
import { ModelMessage, UIMessage, convertToModelMessages } from 'ai';
```

**Provider interfaces:**
```tsx
// ❌ AI SDK v4
import { LanguageModelV2 } from 'ai';

// ✅ AI SDK v5
import { LanguageModelV2 } from '@ai-sdk/provider';
```

### Message Structure Changes (BREAKING)

**UIMessage content → parts array:**
```tsx
// ❌ AI SDK v4
const message: Message = {
  id: '1',
  role: 'user',
  content: 'Hello!',
};

// ✅ AI SDK v5
const message: UIMessage = {
  id: '1',
  role: 'user',
  parts: [{ type: 'text', text: 'Hello!' }],
};
```

**File attachments restructured:**
```tsx
// ❌ AI SDK v4
{
  message.experimental_attachments?.map(attachment => (
    <img src={attachment.url} alt={attachment.name} />
  ))
}

// ✅ AI SDK v5
{
  message.parts.map(part => {
    if (part.type === 'file' && part.mediaType?.startsWith('image/')) {
      return <img src={part.url} />;
    }
  })
}
```

### Tool Definition Changes (BREAKING)

**parameters → inputSchema:**
```tsx
// ❌ AI SDK v4
const weatherTool = tool({
  description: 'Get weather',
  parameters: z.object({
    city: z.string(),
  }),
  execute: async ({ city }) => {
    return `Weather in ${city}`;
  },
});

// ✅ AI SDK v5
const weatherTool = tool({
  description: 'Get weather',
  inputSchema: z.object({
    city: z.string(),
  }),
  execute: async ({ city }) => {
    return `Weather in ${city}`;
  },
});
```

**Tool properties renamed:**
```tsx
// ❌ AI SDK v4 - Tool calls used "args" and "result"
for await (const part of result.fullStream) {
  if (part.type === 'tool-call') {
    console.log('Tool args:', part.args);
  }
  if (part.type === 'tool-result') {
    console.log('Tool result:', part.result);
  }
}

// ✅ AI SDK v5 - Now use "input" and "output"
for await (const part of result.fullStream) {
  if (part.type === 'tool-call') {
    console.log('Tool input:', part.input);
  }
  if (part.type === 'tool-result') {
    console.log('Tool output:', part.output);
  }
}
```

### useChat Hook Changes (MAJOR BREAKING)

**Transport architecture:**
```tsx
// ❌ AI SDK v4
const { messages, input, handleInputChange, handleSubmit } = useChat({
  api: '/api/chat',
  headers: { 'Custom-Header': 'value' },
});

// ✅ AI SDK v5 - Manual input management + transport
import { DefaultChatTransport } from 'ai';
import { useState } from 'react';

const [input, setInput] = useState('');
const { messages, sendMessage } = useChat({
  transport: new DefaultChatTransport({
    api: '/api/chat',
    headers: { 'Custom-Header': 'value' },
  }),
});

const handleSubmit = (e) => {
  e.preventDefault();
  sendMessage({ text: input });
  setInput('');
};
```

**Message sending:**
```tsx
// ❌ AI SDK v4
const { append } = useChat();
append({ role: 'user', content: 'Hello' });

// ✅ AI SDK v5
const { sendMessage } = useChat();
sendMessage({ text: 'Hello' });
```

**Tool result submission:**
```tsx
// ❌ AI SDK v4 - Automatic by returning value
const { messages } = useChat({
  async onToolCall({ toolCall }) {
    return await executeToolCall(toolCall); // Automatic submission
  },
});

// ✅ AI SDK v5 - Explicit with addToolResult
import { lastAssistantMessageIsCompleteWithToolCalls } from 'ai';

const { messages, addToolResult } = useChat({
  sendAutomaticallyWhen: lastAssistantMessageIsCompleteWithToolCalls,
  
  async onToolCall({ toolCall }) {
    const result = await executeToolCall(toolCall);
    
    // Don't await inside onToolCall to avoid deadlocks
    addToolResult({
      tool: toolCall.toolName,
      toolCallId: toolCall.toolCallId,
      output: result,
    });
  },
});
```

### Core Function Changes (BREAKING)

**maxTokens → maxOutputTokens:**
```tsx
// ❌ AI SDK v4
const result = await generateText({
  model: openai('gpt-4'),
  maxTokens: 1024,
  prompt: 'Hello!',
});

// ✅ AI SDK v5
const result = await generateText({
  model: openai('gpt-4'),
  maxOutputTokens: 1024,
  prompt: 'Hello!',
});
```

**providerMetadata → providerOptions (input only):**
```tsx
// ❌ AI SDK v4
const result = await generateText({
  model: openai('gpt-4'),
  providerMetadata: {
    openai: { store: false },
  },
});

// ✅ AI SDK v5
const result = await generateText({
  model: openai('gpt-4'),
  providerOptions: {
    openai: { store: false },
  },
});

// Result still uses providerMetadata:
console.log(result.providerMetadata?.openai);
```

### Caching Changes (BREAKING)

**fetch() and Route Handlers no longer cached by default:**
```tsx
// ❌ AI SDK v4 - Cached by default
const data = await fetch('https://api.example.com');

export async function GET() {
  return Response.json({ data: 'cached by default' });
}

// ✅ AI SDK v5 - Explicit caching required
const data = await fetch('https://api.example.com', { cache: 'force-cache' });

export const dynamic = 'force-static';
export async function GET() {
  return Response.json({ data: 'now cached' });
}
```

### Streaming Architecture Changes (BREAKING)

**Stream response helpers renamed:**
```tsx
// ❌ AI SDK v4
return result.toDataStreamResponse();

// ✅ AI SDK v5
return result.toUIMessageStreamResponse();
```

**Media type standardization:**
```tsx
// ❌ AI SDK v4
{
  type: 'image',
  image: data,
  mimeType: 'image/png',
}

// ✅ AI SDK v5
{
  type: 'image',
  image: data,
  mediaType: 'image/png',
}
```

### Step Control Changes (BREAKING)

**maxSteps → stopWhen:**
```tsx
// ❌ AI SDK v4
const result = await generateText({
  model: openai('gpt-4'),
  messages,
  maxSteps: 5,
});

// ✅ AI SDK v5
import { stepCountIs } from 'ai';

const result = await generateText({
  model: openai('gpt-4'),
  messages: convertToModelMessages(messages),
  stopWhen: stepCountIs(5), // Only triggers when last step has tool results
});
```

## MIGRATION COMMANDS

**Automatic migration:**
```bash
npx @ai-sdk/codemod upgrade
```

**Specific v4→v5 codemods:**
```bash
npx @ai-sdk/codemod v5
```

## COMMON PATTERNS

### Server Action Pattern
```tsx
// ✅ AI SDK v5 Server Component
import { convertToModelMessages, streamText } from 'ai';
import { openai } from '@ai-sdk/openai';

export async function POST(req: Request) {
  const { messages }: { messages: UIMessage[] } = await req.json();

  const result = streamText({
    model: openai('gpt-4'),
    messages: convertToModelMessages(messages),
    tools: { weatherTool },
  });

  return result.toUIMessageStreamResponse();
}
```

### Client Component Pattern
```tsx
// ✅ AI SDK v5 Client Component
'use client';
import { useChat } from '@ai-sdk/react';
import { DefaultChatTransport } from 'ai';
import { useState } from 'react';

export default function Chat() {
  const [input, setInput] = useState('');
  
  const { messages, sendMessage } = useChat({
    transport: new DefaultChatTransport({ api: '/api/chat' }),
  });

  return (
    <div>
      {messages.map(m => (
        <div key={m.id}>
          {m.role}: {m.parts.map(part => 
            part.type === 'text' ? part.text : null
          )}
        </div>
      ))}
      
      <form onSubmit={(e) => {
        e.preventDefault();
        sendMessage({ text: input });
        setInput('');
      }}>
        <input 
          value={input} 
          onChange={(e) => setInput(e.target.value)} 
        />
        <button type="submit">Send</button>
      </form>
    </div>
  );
}
```

## PACKAGE VERSIONS
- `ai`: `5.0.0`
- `@ai-sdk/react`: `2.0.0` 
- `@ai-sdk/rsc`: `2.0.0`
- `zod`: `3.25.0+`

**CRITICAL**: Always use `import { z } from 'zod/v3'` for better TypeScript performance with AI SDK v5.

When migrating AI SDK code, focus on these breaking changes first: package imports, type renames, message structure, tool definitions, and useChat restructuring.
