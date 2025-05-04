# Fusion 10 Context Pack

## What is a Context Pack?
A **Context Pack** is a curated set of files, docs, and configuration sources that you (or your AI agents) should always ingest, chunk, or reference for robust, context-aware development. It ensures every agent, workflow, or dev tool (like Cursor) has the full project picture—no matter the stack, scale, or team.

---

## 📦 Core Context Sources

### 1. **Project Planning & Tasks**
- `/docs/planning.md` – High-level goals, architecture, and roadmap.
- `/docs/task.md` – Current and historical tasks, with completion status.
- `/docs/decision_ai.md` – Key architectural and design decisions.
- `/docs/journey.md` – (Recommended) Project journey, pivots, and lessons learned.

### 2. **Global Rules & Conventions**
- `/docs/global_rules.md` – Your full global rules (as finalized above).
- `/README.md` – Always up-to-date, with stack, usage, and architecture.
- `/docs/security.md` – Security policies, secrets management, and compliance notes.

### 3. **Directory Structure & Codebase**
- Full directory tree (auto-generated or in `/docs/structure.md`).
- Key config files: `.env.example`, `pyproject.toml`, `package.json`, `turbo.json` (if monorepo), `docker-compose.yml`, etc.

### 4. **API & Client Generation**
- `/backend/openapi.json` or `/backend/docs` – FastAPI OpenAPI schema for auto-generating clients.
- `/frontend/lib/` and `/mobile/lib/` – Auto-generated API clients (TypeScript, Python, etc.).
- Reference: [FastAPI: Generate Clients](https://fastapi.tiangolo.com/advanced/generate-clients/)

### 5. **Testing & Reliability**
- `/tests/` – All test suites, with mirrored structure.
- `/docs/testing.md` – Testing strategy, coverage, and CI/CD integration.

### 6. **Workflow & Automation**
- `/workflows/` – n8n flows, custom nodes, and integration scripts.
- `/docs/workflows.md` – Workflow patterns, triggers, and best practices.

### 7. **Frontend & Mobile**
- `/frontend/` – Next.js, Bolt, Tamagui, shared UI components.
- `/mobile/` – Expo/React Native, Tamagui, code sharing notes.
- `/docs/frontend.md`, `/docs/mobile.md` – UI/UX, code sharing, and platform-specific notes.

### 8. **Database & Auth**
- `/supabase/` – Schema, migrations, RLS policies, edge functions.
- `/docs/db.md` – Data model, migration strategy, and Supabase setup.

### 9. **Deployment & CI/CD**
- `/docs/deployment.md` – Deployment strategies (Vercel, Docker, self-hosted, etc.).
- `/docs/infra.md` – Infra as code, cloud vs. local, scaling, and monitoring.

### 10. **References & External Docs**
- Links to all major tools (FastAPI, n8n, Supabase, Tamagui, LangChain, Pydantic, Expo, Bolt, etc.).
- [Context7 Docs](https://github.com/upstash/context7) for up-to-date context management and agent best practices.

---

## 🛠️ How to Use This Context Pack

- **For Agents:**  
  Always ingest, chunk, or reference these files before acting. Use semantic search (RAG) for relevant context.
- **For Cursor/AI IDEs:**  
  Add these files to your context window or “context pack” settings.
- **For Onboarding:**  
  New devs should read these docs in order, starting with planning, global rules, and README.

---

## 🧬 Example: Context7 Integration

- Add Context7 MCP to Cursor or your IDE for live, up-to-date context:
  ```json
  {
    "mcpServers": {
      "context7": {
        "command": "npx",
        "args": ["-y", "@upstash/context7-mcp@latest"]
      }
    }
  }
  ```
- Use prompts like:  
  `use context7`  
  or  
  `Summarize the architecture and global rules for this project. use context7`

---

## 🔗 References

- [Context7 MCP Server](https://github.com/upstash/context7)
- [FastAPI: Generate Clients](https://fastapi.tiangolo.com/advanced/generate-clients/)
- [n8n Docs](https://docs.n8n.io/)
- [Supabase Docs](https://supabase.com/docs)
- [Tamagui Docs](https://tamagui.dev/docs/intro)
- [Expo Docs](https://docs.expo.dev/)
- [LangChain Docs](https://python.langchain.com/docs/)
- [Pydantic Docs](https://docs.pydantic.dev/)
- [Bolt.new](https://bolt.new/)

---

**Tip:**  
Update your context pack as your project evolves. This is your “source of truth” for agents, devs, and automation.
