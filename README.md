# Artificial Ink - AI PDF Chat SaaS - Undeployed

Portfolio project showcasing a production-style AI application built with the modern Next.js ecosystem.

Users can upload PDFs, process them into vector embeddings, and chat with their documents through a streaming AI interface.

## Why This Project Stands Out

- End-to-end product thinking: auth, billing, storage, AI retrieval, and polished UX.
- Real SaaS architecture: user plans, Stripe checkout/portal, webhook-driven subscription sync.
- Retrieval-augmented generation workflow: PDF parsing -> embeddings -> vector search -> grounded chat responses.
- Full-stack TypeScript with typed APIs (tRPC + Zod) and a clean componentized frontend.

## Core Features

- PDF upload flow with drag-and-drop UI via UploadThing.
- Server-side PDF parsing and ingestion pipeline using LangChain + OpenAI embeddings.
- Vector search with Pinecone for contextual Q&A over document content.
- Streaming AI answers (OpenAI + `ai` SDK) with persistent conversation history.
- Auth-protected dashboard using Kinde.
- Usage plans and upgrades with Stripe billing.
- Document workspace with upload status states (`PENDING`, `PROCESSING`, `FAILED`, `SUCCESS`).
- In-app PDF reader with page navigation, zoom, rotation, and fullscreen mode.

## System Design (High Level)

1. User uploads a PDF from dashboard UI.
2. UploadThing stores the file and triggers server processing.
3. Server loads PDF pages and creates embeddings.
4. Embeddings are indexed in Pinecone.
5. User asks a question in chat.
6. App retrieves relevant chunks from vector search.
7. OpenAI generates a streamed response using retrieved context + recent chat history.
8. Messages are persisted in MySQL via Prisma.

## Tech Stack

- Framework: Next.js 14 (App Router), React 18, TypeScript
- API Layer: tRPC, Zod
- Database/ORM: MySQL, Prisma
- Auth: Kinde
- AI/RAG: OpenAI, LangChain, Pinecone
- File Uploads: UploadThing
- Billing: Stripe + webhooks
- UI: Tailwind CSS, Radix UI, Lucide icons

## Screenshots

- Landing + product preview: `public/dashboard-preview.jpg`
- Upload experience: `public/file-upload-preview.jpg`

## Local Development

### 1. Install dependencies

```bash
npm install
```

### 2. Configure environment variables

Create `.env` in the project root with:

```bash
KINDE_CLIENT_ID=
KINDE_CLIENT_SECRET=
KINDE_ISSUER_URL=
KINDE_SITE_URL=
KINDE_POST_LOGOUT_REDIRECT_URL=
KINDE_POST_LOGIN_REDIRECT_URL=

DATABASE_URL=

UPLOADTHING_SECRET=
UPLOADTHING_APP_ID=

PINECONE_API_KEY=
OPENAI_API_KEY=

STRIPE_SECRET_KEY=
STRIPE_WEBHOOK_SECRET=
```

### 3. Set up database

```bash
npx prisma generate
npx prisma db push
```

### 4. Run the app

```bash
npm run dev
```

Open `http://localhost:3000`.

## Notable Portfolio Signals

- Demonstrates integration-heavy engineering across 6+ third-party platforms.
- Shows practical AI product implementation, not just prompt-only usage.
- Includes user lifecycle essentials: onboarding, gated routes, billing, and account-level data.
- Balances UX polish with backend architecture and data modeling.

## Future Improvements

- Namespace vector indexes per file for stricter retrieval boundaries.
- Add robust quota enforcement per plan during upload/chat flows.
- Improve test coverage (unit + integration + e2e).
- Add observability around ingestion latency and response quality.

## Author

Built by Hichem Hamza as a portfolio project to explore AI-powered product engineering with modern web tooling.
