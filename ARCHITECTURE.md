# Technical Architecture

## Overview
"Cursor for Product Management" is an AI-native system that analyzes customer feedback and generates product artifacts. The architecture follows a modern full-stack approach with AI/ML capabilities.

## Tech Stack

### Frontend
- **Next.js 14** - React framework with App Router for optimal performance and SEO
- **TypeScript** - Type-safe development
- **Tailwind CSS** - Utility-first CSS framework
- **Shadcn/ui** - Component library for rapid UI development

### Backend & Database
- **Supabase** - Backend-as-a-Service (PostgreSQL, authentication, realtime)
- **Pinecone** - Vector database for semantic search over feedback
- **OpenAI API** - GPT-4 for analysis and generation, text-embedding-ada-002 for embeddings

### AI/ML Stack
- **LangChain** - LLM orchestration framework
- **Vercel AI SDK** - Streaming AI responses
- **Pinecone** - Vector similarity search

### Infrastructure & Tools
- **GitHub** - Version control
- **Vercel** - Deployment platform
- **ESLint + Prettier** - Code quality and formatting
- **Jest + React Testing Library** - Testing framework

## System Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         Client Layer                            │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  Next.js 14 App (App Router)                            │  │
│  │  - Upload UI                                            │  │
│  │  - Analysis Dashboard                                  │  │
│  │  - Artifact Review                                     │  │
│  │  - Collaboration Features                              │  │
│  └──────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                      API Layer (Next.js API Routes)             │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  - File Upload & Processing                            │  │
│  │  - Query & Analysis Endpoints                          │  │
│  │  - Artifact Generation                                 │  │
│  │  - Export Services                                     │  │
│  └──────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
                              │
              ┌───────────────┼───────────────┐
              ▼               ▼               ▼
┌──────────────────┐ ┌─────────────┐ ┌──────────────┐
│     Supabase     │ │  Pinecone   │ │   OpenAI     │
│                  │ │   Vector    │ │     API      │
│ • PostgreSQL     │ │   Database  │ │              │
│ • Auth           │ │             │ │ • GPT-4      │
│ • Storage        │ │ • Embeddings│ │ • Embeddings │
│ • Realtime       │ │ • Search    │ │              │
└──────────────────┘ └─────────────┘ └──────────────┘
```

## Data Flow

1. **Ingestion Pipeline**: User uploads files → Server validates → Parse content → Chunk text → Generate embeddings → Store in Pinecone + Supabase
2. **Analysis Pipeline**: User query → Semantic search (Pinecone) → Context assembly → LangChain chain → GPT-4 analysis → Store results in Supabase
3. **Generation Pipeline**: Analysis results + templates → GPT-4 generation → Validation → Store artifacts in Supabase → Return to UI
4. **Collaboration**: Supabase Realtime subscriptions for live updates

## Project Structure

```
cursor-for-product-managers/
├── src/
│   ├── app/                    # Next.js App Router pages
│   │   ├── (auth)/            # Auth group routes
│   │   │   ├── login/
│   │   │   └── signup/
│   │   ├── dashboard/         # Main dashboard
│   │   │   ├── page.tsx
│   │   │   └── upload/
│   │   ├── analysis/
│   │   │   └── [id]/
│   │   ├── artifacts/
│   │   │   └── [type]/
│   │   ├── api/              # API routes
│   │   │   ├── upload/
│   │   │   ├── analyze/
│   │   │   ├── generate/
│   │   │   └── search/
│   │   ├── layout.tsx
│   │   └── page.tsx
│   ├── components/           # React components
│   │   ├── ui/              # Shadcn/ui components
│   │   ├── layout/
│   │   ├── upload/
│   │   ├── analysis/
│   │   └── artifacts/
│   ├── lib/                 # Core utilities
│   │   ├── supabase/
│   │   ├── pinecone/
│   │   ├── openai/
│   │   ├── langchain/
│   │   ├── parsers/         # File parsers
│   │   ├── chunkers/        # Text chunking strategies
│   │   └── embeddings/
│   ├── types/               # TypeScript definitions
│   ├── hooks/               # Custom React hooks
│   └── styles/              # Global styles
├── tests/
│   ├── unit/
│   ├── integration/
│   └── fixtures/
├── .env.local.example
├── .envrc
├── next.config.js
├── tailwind.config.js
├── tsconfig.json
├── package.json
└── README.md
```

## Database Schema (Supabase)

### Tables
- `users` - Extended user profiles (Supabase auth integration)
- `interviews` - Uploaded interview records with metadata
- `feedback_items` - Individual feedback chunks with embeddings reference
- `analyses` - AI analysis sessions and results
- `recommendations` - Generated feature recommendations
- `artifacts` - Product artifacts (PRDs, specs, etc.)
- `comments` - Collaborative feedback
- `versions` - Version history for artifacts

## Key Design Decisions

1. **Monorepo with Next.js**: Full-stack app in single repository, simplifies deployment and development
2. **Server-side processing**: Heavy computation (embeddings, analysis) happens server-side to protect API keys and manage rate limits
3. **Vector search first**: Pinecone for fast semantic retrieval before LLM processing
4. **Real-time collaboration**: Supabase Realtime for live commenting and updates
5. **Streaming responses**: Vercel AI SDK for progressive artifact generation
6. **Type-safe throughout**: TypeScript across frontend and backend (API routes)

## Security Considerations

- API keys stored in environment variables, never exposed to client
- Row-level security (RLS) in Supabase for data isolation
- File upload validation for MIME types and size limits
- Authentication required for all protected routes
- Rate limiting on API endpoints

## Scalability Considerations

- Horizontal scaling via Vercel serverless functions
- Pinecone handles vector search at scale
- Supabase database with connection pooling
- Background job queue (e.g., BullMQ) for async embedding generation
- CDN caching for static assets

## Monitoring & Observability

- Vercel Analytics for performance
- Supabase logs for database queries
- OpenAI usage tracking
- Error tracking (Sentry or similar)
- Custom metrics for analysis success rates
