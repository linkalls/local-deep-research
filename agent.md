# Python to TypeScript/Hono/Bun Migration Guide

This file provides the architectural guidelines and instructions for agents to migrate the `local-deep-research` codebase from Python to a pure TypeScript implementation using Hono and Bun.

## Goal
Completely remove Python dependencies and migrate the entire backend, CLI, and LLM processing logic to TypeScript.

## Stack
- **Runtime:** Bun (`bun run`, `bun test`, etc.)
- **Web Framework:** Hono (replacing Flask)
- **Language:** TypeScript
- **Database ORM:** Drizzle ORM or Prisma (replacing SQLAlchemy / Alembic)
- **LLM SDK:** `@langchain/core`, `@langchain/openai`, `@langchain/anthropic`, etc. (replacing Python LangChain)
- **Web Scraping:** Playwright for Node.js (replacing Python Playwright / BeautifulSoup / trafilatura)

## Migration Strategy

1. **Setup & Initialization:**
   - Initialize the bun project (`bun init`).
   - Setup `tsconfig.json` for modern Node/Bun modules.

2. **Database & Models:**
   - Map Python SQLAlchemy models in `src/local_deep_research/database/models` to Drizzle/Prisma schemas.
   - Re-implement database connection logic and migrations (replacing Alembic).

3. **Core LLM & Search Logic (`src/local_deep_research/search_system.py`, etc.):**
   - Translate LangChain Python chains/agents to LangChain.js.
   - Rewrite the advanced search system, report generator, and citation handlers using TypeScript classes and async/await.

4. **Web API & Endpoints (`src/local_deep_research/web/`):**
   - Replace Flask routes with Hono endpoints.
   - Implement Hono middleware for authentication, rate limiting, and database injection.
   - Replace Flask-SocketIO with standard WebSocket or Socket.io for Node.js.

5. **Utilities & File Processing:**
   - Translate document loaders (PDF, TXT, etc.) using Node.js equivalents (e.g., `pdf-parse`).
   - Rewrite embeddings logic and vector storage integration.

6. **Tests:**
   - Migrate `pytest` tests in `tests/` to `bun test`.
   - Ensure mocking uses `bun:test` utilities.

## Agent Instructions
- Do **NOT** add any Python code.
- When porting a module, mark it as completed in `todo.md`.
- Ensure strict TypeScript typing (`noImplicitAny`, etc.).
- Preserve the exact API contracts and WebSocket event names where possible so the frontend (`package.json` in the root) continues to function.
