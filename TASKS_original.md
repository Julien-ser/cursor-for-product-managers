# cursor-for-product-managers
**Mission:** Over the last few years, we've seen an explosion of AI tools for writing code. Cursor and Claude Code are great at helping teams build software once it's clear what needs to be built.

But writing code is only part of building a product people want. The most important part is figuring out what to build in the first place!

Every successful product requires product management: talking to users, understanding markets, synthesizing feedback, and deciding what problems are worth solving and how the product should work. Whether this process is done by founders, engineers, or product managers, the activity is the same. Historically, the output has been product requirements docs, Figma mocks, and Jira tickets — artifacts designed to communicate intent to human engineers.

Today, teams use AI in isolated parts of this process, but there's no system that supports the full loop of product discovery.

Imagine a tool where you upload customer interviews and product usage data, ask "what should we build next?", and get the outline of a new feature complete with an explanation based on customer feedback as to why this is a change worth making. The tool would also propose specific changes to your product's UI, data model, and workflows, and would break down the development tasks so they could be handled by your favorite coding agent.

We think there's an opportunity to build a "Cursor for product management": an AI-native system focused on helping teams figure out what to build, not just how to build it.

As agents increasingly take the first pass at implementation, the way we define and communicate "what to build" needs to change.

## Phase 1: Planning & Setup
- [ ] **Task 1.1:** Define technical architecture and select core technologies (Next.js 14, TypeScript, Tailwind CSS, Supabase, OpenAI API, LangChain, Pinecone)
  - *Deliverables:* Architecture diagram, tech stack documentation, project structure plan
- [ ] **Task 1.2:** Initialize project repository with Next.js, configure TypeScript, ESLint, and Prettier
  - *Deliverables:* Working Next.js project with linting, formatting, and basic folder structure
- [ ] **Task 1.3:** Set up Supabase project and configure database schema for interviews, feedback, product specs, and user data
  - *Deliverables:* Database schema SQL, Supabase connection configured, authentication setup
- [ ] **Task 1.4:** Create vector database (Pinecone) indexes for semantic search over customer feedback
  - *Deliverables:* Pinecone indexes created, embedding pipeline design, sample data ingested

## Phase 2: Core AI Analysis Engine
- [ ] **Task 2.1:** Build multi-format data ingestion system (video transcripts, audio, text notes, CSV usage logs, JSON logs)
  - *Deliverables:* File upload UI, parsing service for each format, validation layer, storage integration
- [ ] **Task 2.2:** Implement feedback chunking and embedding pipeline using OpenAI embeddings (text-embedding-ada-002)
  - *Deliverables:* Chunking strategy code, embedding service, Pinecone storage with metadata, batch processing
- [ ] **Task 2.3:** Develop LLM-powered analysis chain using GPT-4 to identify patterns, pain points, and opportunities
  - *Deliverables:* LangChain chain with prompts for synthesis, pattern extraction logic, confidence scoring
- [ ] **Task 2.4:** Create recommendation engine that prioritizes features based on feedback frequency, user impact, and strategic alignment
  - *Deliverables:* Scoring algorithm, feature prioritization matrix, explanation generator with evidence citations

## Phase 3: Product Artifact Generation
- [ ] **Task 3.1:** Build PRD generator that creates structured requirements docs with user stories, acceptance criteria, and success metrics
  - *Deliverables:* PRD template system, GPT-4 generation with validation, export to Markdown/PDF
- [ ] **Task 3.2:** Implement UI change suggestion system that generates component descriptions and layout proposals
  - *Deliverables:* Component library reference, UI diff descriptions, Figma-like mock specifications (JSON), wireframe generator
- [ ] **Task 3.3:** Create data model suggestion module that proposes schema changes, API endpoints, and database migrations
  - *Deliverables:* Schema diff tool, Prisma/TypeORM migration generator, API spec generator (OpenAPI)
- [ ] **Task 3.4:** Develop workflow mapping tool that identifies affected user journeys and process changes
  - *Deliverables:* Flowchart generator (Mermaid.js), step-by-step change documentation, edge case analysis

## Phase 4: Integration & Development Handoff
- [ ] **Task 4.1:** Build task breakdown engine that decomposes features into engineering tasks with complexity estimates
  - *Deliverables:* Task tree generator, effort estimation model, dependency mapping, Jira/Linear export format
- [ ] **Task 4.2:** Implement AI coding agent integration layer for cursor/claude-code compatibility
  - *Deliverables:* Export to agent-friendly format (instructions + context), context packaging service, API for agent queries
- [ ] **Task 4.3:** Create editor/IDE extension (VS Code) to access analysis directly from codebase
  - *Deliverables:* VS Code extension with commands, side panel for artifact review, click-to-navigate to relevant files
- [ ] **Task 4.4:** Build collaborative review workflow with commenting, version history, and stakeholder approval tracking
  - *Deliverables:* Real-time collaboration (Supabase Realtime), commenting system, audit log, approval workflows
