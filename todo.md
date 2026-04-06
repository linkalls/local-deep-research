# Migration TODO Checklist (Python -> TS/Bun/Hono)

## Phase 1: Project Setup
- [ ] Initialize Bun project (`bun init` or update existing package.json)
- [ ] Configure `tsconfig.json` for Bun & strict typing
- [ ] Install dependencies: `hono`, `@langchain/*`, Drizzle/Prisma, socket.io, playwright
- [ ] Configure linting (ESLint) and formatting (Prettier)

## Phase 2: Database & Models (replacing `src/local_deep_research/database/`)
- [ ] Port SQLAlchemy models to Drizzle or Prisma schema.
- [ ] Migrate `alembic` setup to Drizzle/Prisma migrations.
- [ ] Implement database connection singleton/module.
- [ ] Implement CRUD utilities for library, settings, notifications, etc.

## Phase 3: Web Server & API (replacing `src/local_deep_research/web/`)
- [ ] Setup Hono application structure.
- [ ] Implement middleware (Auth, Rate Limiting, Error Handling).
- [ ] Port `app.py` and `server_config.py` to `index.ts`.
- [ ] Port `routes/` (API endpoints) from Flask blueprints to Hono Routers.
- [ ] Setup WebSocket (socket.io) for real-time progress updates.

## Phase 4: LLM & Search Logic (replacing `src/local_deep_research/search_system.py`, `advanced_search_system/`, `llm/`)
- [ ] Map Python LangChain models to `@langchain/openai`, `@langchain/anthropic`, etc.
- [ ] Port the `SearchSystem` and `AdvancedSearchSystem` logic.
- [ ] Port `ReportGenerator` and Markdown formatting logic.
- [ ] Port `CitationHandler` logic.
- [ ] Implement web scraping with Node Playwright and Cheerio/JSDOM.

## Phase 5: Utilities & Tools (replacing `src/local_deep_research/utilities/`, `document_loaders/`)
- [ ] Port document parsing (PDF, text extraction).
- [ ] Port chunking/embedding logic.
- [ ] Port error handling and logging utilities.

## Phase 6: CLI & Benchmarks (replacing `cli/`, `benchmarks/`)
- [ ] Re-implement `ldr` CLI commands using a Bun CLI library (e.g., `commander` or `cleye`).
- [ ] Port benchmark scripts if required.

## Phase 7: Testing (replacing `tests/`)
- [ ] Setup `bun test`.
- [ ] Port unit tests.
- [ ] Port integration tests.

## Phase 8: Cleanup
- [ ] Remove all `.py` files.
- [ ] Remove `pyproject.toml`, `pdm.lock`, `requirements.txt`.
- [ ] Update `Dockerfile`, `docker-compose.yml` to use Bun instead of Python.
- [ ] Update `README.md` and documentation to reflect the new stack.
