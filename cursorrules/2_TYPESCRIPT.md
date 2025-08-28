# TypeScript Development Standards

## Overview
These rules must be strictly followed when working with TypeScript projects. They ensure consistency, performance, security, and maintainability across all codebases.

## Package Management
- **Always use `bun`** as the package manager unless explicitly told otherwise
- Use `bunx` instead of `npx` for all CLI commands
- Lock file: Commit `bun.lockb` to version control
- Common commands:
  - `bun test` - Run Vitest unit tests (only when required)
  - `bun run dev` - Start development server (**ONLY RUN WHEN EXPLICITLY REQUESTED**)
  - `bun run build` - Build project and check for compilation errors
  - `bun run lint` - Run ESLint with auto-fix
  - `bun run format` - Format code with Prettier
  - If build errors occur: fix them, then run `bun run build` again to confirm

## Code Quality & Formatting
- **ESLint**: Use `@next/eslint-config-next` with TypeScript rules
- **Prettier**: Enforce consistent code formatting
  - Single quotes for strings
  - Trailing commas where valid
  - 2-space indentation
  - 80-character line length
- **Import Organization**:
  - External packages first
  - Internal modules second
  - Relative imports last
  - Use import type for type-only imports
- **Naming Conventions**:
  - PascalCase for components, classes, types, interfaces
  - camelCase for variables, functions
  - SCREAMING_SNAKE_CASE for constants
  - kebab-case for file names (except components)

## Next.js Projects
- **Version**: Use Next.js 15+ with App Router
- **Structure**: Implement `./src` directory structure
- **Deployment**: Assume Vercel deployment target
- **File Organization**:
  ```
  src/
  ├── app/                    # App Router pages and layouts
  ├── components/
  │   ├── ui/                # shadcn/ui components
  │   └── [feature]/         # Feature-specific components
  ├── lib/
  │   ├── ai/                # AI / LLM layer with subdirectories for different agents, tools, etc.
  │   ├── db/                # Database layer
  │   ├── store/             # State management
  │   ├── utils/             # Utility functions
  │   └── validations/       # Zod schemas
  └── types/                 # Global type definitions
  ```
- **Components**:
  - Prefer Server Components by default
  - Use Client Components only when interactivity is required
  - Implement React Server Actions for form submissions
  - Use `"use client"` directive only when necessary
- **Encoding**: Always use HTML entities (e.g., `&apos;`) instead of single quotation marks
- **SEO**: Implement proper metadata, OpenGraph tags, and structured data
- **Performance**: Use `next/image`, `next/font`, and proper caching strategies

## UI Components (shadcn/ui)
- **Installation**: Always use `shadcn@latest` for component installation
- **Never use**: `shadcn-ui@latest` (deprecated)
- **Commands**: `bunx shadcn@latest add [component]`
- **Customization**: 
  - Customize theme in `tailwind.config.ts`
  - Extend components in `src/components/ui`
- **Accessibility**: Ensure all custom components follow WCAG 2.1 AA standards
- **Styling**: Use CSS variables for consistent theming

## Database (Drizzle ORM + PostgreSQL)
- **ORM**: Prefer Drizzle ORM with PostgreSQL
- **File Structure**:
  - Database connection: `src/lib/db/index.ts`
  - Schema definitions: `src/lib/db/schema.ts`
  - DAO helper functions: `src/lib/db/<table_name>.ts`
  - Migration files: `drizzle/migrations/`
- **Operations**:
  - Use migrations for all schema changes
  - Implement connection pooling (pg-pool)
  - Handle database errors gracefully with proper logging
  - Use transactions for multi-step operations
  - Push schema changes: `bun run db:push:dev`
- **Security**: Use parameterized queries, validate inputs with Zod

## State Management (Zustand)
- **Library**: Prefer Zustand for state management
- **File Structure**: Create Zustand files in `src/lib/store/`
- **Persistence**: Enable localStorage persistence where appropriate
- **Patterns**:
  - Use immer for complex state updates
  - Implement proper TypeScript typing for stores
  - Avoid storing sensitive data in client-side state

## Validation & Type Safety
- **Runtime Validation**: Use Zod for all API inputs, forms, and external data
- **Type Generation**: Generate types from Zod schemas using `zod-to-typescript`
- **Form Handling**: Use react-hook-form with Zod resolvers
- **API Validation**: Validate all API route inputs and outputs

## AI/LLM Integration (Vercel AI SDK)
- **Library**: Use Vercel AI SDK v5+ (https://sdk.vercel.ai/docs/reference/ai-sdk-core)
- **Configuration**:
  - Store API keys securely in environment variables
  - Default OpenAI model: `gpt-5-mini` (or `gpt-5-nano` if cost is a concern) but do not change existing code unless explicitly requested
  - Default temperature: `0.2` for consistent responses
  - Implement proper rate limiting and error handling
  - Use streaming responses where appropriate

## Error Handling & Monitoring
- **Client-Side**: Implement React Error Boundaries
- **Server-Side**: Use proper HTTP status codes and error responses
- **Logging**: Implement structured logging (consider Pino or Winston)
- **Monitoring**: Set up error tracking (Sentry recommended for production)
- **Types**: Create custom error classes with proper typing

## Testing Strategy
- **Unit Tests**: Use Vitest for unit testing
- **Component Tests**: Use React Testing Library with Vitest
- **E2E Tests**: Consider Playwright for critical user flows (optional)
- **Test Structure**: Follow AAA pattern (Arrange, Act, Assert)
- **Mocking**: Mock external dependencies and APIs
- **Coverage**: Aim for 80%+ coverage on critical business logic

## Security Best Practices
- **Environment Variables**: Use `.env.local` for development, never commit secrets
- **Input Validation**: Validate all user inputs on both client and server
- **CORS**: Configure proper CORS policies for API routes
- **CSP**: Implement Content Security Policy headers
- **Authentication**: Use secure session management and CSRF protection
- **Dependencies**: Regularly audit dependencies with `bun audit`

## Performance Optimization
- **Bundle Analysis**: Use `@next/bundle-analyzer` to monitor bundle size
- **Code Splitting**: Implement dynamic imports for large components
- **Caching**: Use appropriate caching strategies (ISR, SSG where applicable)
- **Images**: Always use `next/image` with proper optimization
- **Fonts**: Use `next/font` for optimal font loading

## Documentation Standards
- **README**: Include setup, development, and deployment instructions
- **Code Comments**: Use JSDoc for functions and complex logic
- **API Documentation**: Document all API routes with OpenAPI/Swagger
- **Component Documentation**: Use Storybook for component documentation (optional)

## Development Workflow
- **Git Conventions**: Use conventional commits (feat:, fix:, docs:, etc.)
- **Branch Naming**: Use feature/, fix/, hotfix/ prefixes
- **Code Reviews**: Require PR reviews for all changes to main branch
- **Deployment**: Use preview deployments for all PRs on Vercel

## TypeScript Best Practices
- **Configuration**: Use strict TypeScript configuration with all strict flags enabled
- **Type Definitions**: Create comprehensive type definitions in `src/types/`
- **Avoid `any`**: Use `unknown` instead of `any`, implement proper type guards
- **Utility Types**: Leverage TypeScript utility types (Pick, Omit, etc.)
- **Generic Constraints**: Use generic constraints for reusable components
- **Error Handling**: Implement typed error handling with Result/Either patterns
- **Type Assertions**: Use type assertions sparingly, prefer type guards
- **Interface vs Type**: Use interfaces for object shapes, types for unions/computed types

## Environment Management
- **Development**: `.env.local` for local overrides
- **Production**: Use platform environment variables (Vercel)
- **Validation**: Validate environment variables at startup using Zod
- **Documentation**: Document all required environment variables in README
