# Cursor for Product Managers

![Phase](https://img.shields.io/badge/Phase-1%20Planning%20%26%20Setup-blue)
![Status](https://img.shields.io/badge/Status-In%20Progress-yellow)

An AI-native system for product discovery that transforms customer feedback into actionable product requirements, UI proposals, and development tasks—essentially "Cursor for product management."

## 🎯 Mission

Today's AI tools excel at **writing code** once requirements are clear, but the hardest part is **figuring out what to build**. This system bridges that gap by:

- Ingesting customer interviews, usage data, and feedback in any format
- Using AI to synthesize insights and identify patterns
- Generating complete product artifacts (PRDs, UI specs, data models)
- Breaking down features into development tasks ready for coding agents

## 🏗️ Technical Architecture

### Core Technologies
- **Frontend**: Next.js 14 (App Router), TypeScript, Tailwind CSS, Shadcn/ui
- **Backend**: Next.js API Routes, Supabase (PostgreSQL + Auth + Realtime)
- **AI Stack**: OpenAI GPT-4, LangChain, Pinecone (vector database)
- **Infrastructure**: Vercel deployment, GitHub version control

### System Components
```
Upload & Ingest → Embedding & Storage → Semantic Search → AI Analysis → Artifact Generation → Development Handoff
```

For detailed architecture, see [ARCHITECTURE.md](./ARCHITECTURE.md).

## 📋 Project Status

### Phase 1: Planning & Setup
- [x] **Task 1.1**: Define technical architecture and select core technologies
- [ ] Task 1.2: Initialize project repository with Next.js
- [ ] Task 1.3: Set up Supabase project and configure database schema
- [ ] Task 1.4: Create Pinecone indexes for semantic search

### Phase 2: Core AI Analysis Engine
- [ ] Task 2.1: Build multi-format data ingestion system
- [ ] Task 2.2: Implement feedback chunking and embedding pipeline
- [ ] Task 2.3: Develop LLM-powered analysis chain
- [ ] Task 2.4: Create recommendation engine

### Phase 3: Product Artifact Generation
- [ ] Task 3.1: Build PRD generator
- [ ] Task 3.2: Implement UI change suggestion system
- [ ] Task 3.3: Create data model suggestion module
- [ ] Task 3.4: Develop workflow mapping tool

### Phase 4: Integration & Development Handoff
- [ ] Task 4.1: Build task breakdown engine
- [ ] Task 4.2: Implement AI coding agent integration layer
- [ ] Task 4.3: Create VS Code extension
- [ ] Task 4.4: Build collaborative review workflow

## 🚀 Getting Started

### Prerequisites
- Node.js 18+
- Supabase account
- OpenAI API key
- Pinecone account

### Setup Instructions

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd cursor-for-product-managers
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Configure environment variables**
   ```bash
   cp .env.local.example .env.local
   ```
   
   Fill in your API keys in `.env.local`:
   ```
   NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
   NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
   OPENAI_API_KEY=your_openai_key
   PINECONE_API_KEY=your_pinecone_key
   PINECONE_INDEX=your_index_name
   ```

4. **Initialize Supabase**
   - Run the SQL schema from `supabase/schema.sql` in your Supabase project
   - Enable authentication providers as needed
   - Configure storage buckets for file uploads

5. **Set up Pinecone**
   - Create indexes for embeddings (see `PINECONE.md` for configuration)

6. **Run development server**
   ```bash
   npm run dev
   ```
   
   Open [http://localhost:3000](http://localhost:3000) in your browser.

### Testing
```bash
npm test          # Run unit tests
npm run test:e2e  # Run end-to-end tests
```

### Linting & Formatting
```bash
npm run lint      # Check code quality
npm run format    # Auto-format code
```

## 📁 Project Structure

```
src/
├── app/           # Next.js pages (App Router)
├── components/    # React components
├── lib/          # Core utilities and services
├── types/        # TypeScript definitions
└── hooks/        # Custom React hooks

tests/
├── unit/         # Unit tests
└── integration/  # Integration tests
```

## 🔑 Configuration Files

- `ARCHITECTURE.md` - Detailed technical architecture and design decisions
- `TASKS.md` - Development progress and task tracking
- `prompt.txt` - Agent instructions for autonomous development
- `AGENTS.md` - Project context (auto-generated)
- `.envrc` - direnv configuration for local development

## 🧪 Testing Strategy

- **Unit tests**: Jest + React Testing Library for components and utilities
- **Integration tests**: Test API routes and data flows
- **E2E tests**: Playwright for critical user journeys

## 📝 Development Workflow

1. Check `TASKS.md` for current priorities
2. Create feature branch from `main`
3. Write tests first (TDD approach)
4. Implement feature
5. Run tests, lint, and format
6. Commit with conventional commit message
7. Push and create PR

## 🏛️ License

[Add your license here]

## 🙏 Acknowledgments

Built with modern AI/ML tooling:
- [Next.js](https://nextjs.org/)
- [Supabase](https://supabase.com/)
- [OpenAI](https://openai.com/)
- [Pinecone](https://www.pinecone.io/)
- [LangChain](https://langchain.com/)
- [Vercel](https://vercel.com/)
