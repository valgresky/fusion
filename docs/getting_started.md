# 🚀 Fusion 10 – Getting Started Manual

Welcome to the **Fusion 10 Hybrid AI App Template**! This manual will walk you through setting up, developing, and scaling your agentic, multi-method app using Archon, Supabase, n8n, Bolt, and more. It's designed for AI-first workflows, robust agent collaboration, and seamless content/documentation generation.

---

## 1. 🛠️ Environment Setup & Prerequisites

- **OS:** macOS, Linux, or Windows (WSL2 recommended)
- **Required Tools:**
  - [Git](https://git-scm.com/)
  - [Node.js (LTS)](https://nodejs.org/)
  - [Python 3.10+](https://www.python.org/)
  - [Docker](https://www.docker.com/) (for n8n, optional for local Supabase)
  - [Cursor](https://www.cursor.so/) (recommended IDE)
  - [Lovable](https://lovable.so/) (optional, for rapid prototyping)
  - [Expo CLI](https://docs.expo.dev/get-started/installation/) (for mobile)
  - [Supabase account](https://supabase.com/) (hosted)
  - [Gresky](https://github.com/valgresky/gresky) (local knowledge engine)

---

## 2. 📦 Project Initialization

```bash
# Clone your template repo
 git clone [https://github.com/valgresky/fusion.git]
 cd fusion10

# Install frontend dependencies
 cd frontend
 npm install

# Install backend dependencies
 cd ../backend
 python -m venv .venv
 source .venv/bin/activate
 pip install -r requirements.txt

# (Optional) Install mobile dependencies
 cd ../mobile
 npm install
```

- **Copy `.env.example` to `.env`** in each relevant directory and fill in secrets (see Supabase, n8n, FastAPI docs).
- **Reference:** [docs/context_pack.md](context_pack.md) for all required context files.

---

## 3. 🧠 Using Gresky for Context & Agentic Workflows

- **Start Gresky locally** (see Gresky docs for setup):
  - Ingest `/docs/context_pack.md`, `/docs/planning.md`, `/docs/task.md`, and your codebase for robust context.
  - Use Gresky's RAG/knowledge features to power agentic workflows in Cursor or Windsurf.
- **Best Practice:** Keep a local Gresky instance for private dev, and a cloud instance for team/production if needed.

---

## 4. 🔐 Using Supabase (Hosted)

- **Set up your project on [Supabase](https://supabase.com/)**
- **Configure:**
  - Auth (email, OAuth, etc.)
  - Database schema (see `/supabase/schema.sql` or `/supabase/migrations/`)
  - Edge functions/secrets as needed
- **Update `.env` files** with Supabase keys and URLs
- **Reference:** [Supabase Quickstart](https://supabase.com/docs/guides/with-nextjs)

---

## 5. 🔄 Using n8n for Workflow Automation

- **Start n8n:**
  - `docker run -it --rm -p 5678:5678 n8nio/n8n`
  - Or use [n8n cloud](https://n8n.io/)
- **Connect n8n to Supabase, FastAPI, and external APIs**
- **Build workflows:**
  - Use n8n's visual editor to automate triggers, data flows, and agent calls
  - Example: Scrape data, call FastAPI agent, store results in Supabase
- **Reference:** [n8n Docs](https://docs.n8n.io/)

---

## 6. ⚡ Using Bolt (Next.js) for Frontend

- **Start frontend dev server:**
  - `cd frontend && npm run dev`
- **Connect to Supabase and FastAPI via auto-generated API clients**
- **Use Tamagui/React Native Web for shared UI (if desired)**
- **Reference:** [Next.js Docs](https://nextjs.org/docs), [Tamagui](https://tamagui.dev/)

---

## 7. 📱 Using Expo for Mobile (Optional)

- **Start mobile dev server:**
  - `cd mobile && npx expo start`
- **Share code with web via Tamagui/React Native Web**
- **Connect to Supabase and FastAPI via generated clients**
- **Reference:** [Expo Docs](https://docs.expo.dev/)

---

## 8. 🤖 Using Agents (Pydantic AI, LangChain)

- **Develop agents in `/backend/agents/`**
- **Use Pydantic for type-safe agent schemas**
- **Integrate LangChain for advanced chains, tools, and RAG**
- **Expose agent endpoints via FastAPI**
- **Call agents from frontend, mobile, or n8n workflows**
- **Test with Pytest (see `/tests/` directory)**
- **Reference:** [Pydantic](https://docs.pydantic.dev/), [LangChain](https://python.langchain.com/)

---

## 9. 🤝 Collaborating with Cursor, Lovable, and GitHub

- **Use Cursor for AI-powered code navigation, refactoring, and agentic workflows**
- **Use Lovable for rapid prototyping and UI scaffolding**
- **Sync changes via GitHub (push/pull/PRs)**
- **Document your journey in `/docs/journey.md`**
- **Reference:** [Cursor Docs](https://www.cursor.so/docs), [Lovable Docs](https://lovable.so/docs)

---

## 10. 📝 Documenting Your Journey & Generating Docs

- **Start with just the README and global rules**
- **Let your IDE/agents scaffold new docs as you build (planning.md, task.md, etc.)**
- **Use `/docs/context_pack.md` as the canonical context for onboarding agents and new devs**
- **Update docs after every major change**

---

## 11. 🚦 Initial Run-Through & Starter Prompts

1. **Clone the repo and install dependencies** (see above)
2. **Start Gresky and ingest context**
3. **Start Supabase (hosted) and configure env vars**
4. **Start n8n, Bolt, and (optionally) Expo**
5. **Open the project in Cursor**
6. **Use starter prompts in Cursor/Lovable:**
   - "Generate a new agent for [feature] using Pydantic AI and expose via FastAPI."
   - "Scaffold a new n8n workflow to automate [business logic]."
   - "Create a shared UI component for web/mobile using Tamagui."
   - "Document this feature in planning.md and update context_pack.md."
7. **Let agents/IDE auto-generate docs, tests, and code stubs as you go**

---

## 12. 📚 References & Best Practices

- [Global Rules](../README.md#global-user-rules)
- [Context Pack](context_pack.md)
- [Fusion 10 README](../README.md)
- [Supabase Docs](https://supabase.com/docs)
- [n8n Docs](https://docs.n8n.io/)
- [Next.js Docs](https://nextjs.org/docs)
- [Expo Docs](https://docs.expo.dev/)
- [Pydantic](https://docs.pydantic.dev/)
- [LangChain](https://python.langchain.com/)

---

## 🏁 You're Ready!

You now have a robust, AI-first workflow for building, scaling, and documenting agentic apps with Fusion 10. Iterate, collaborate, and let your agents help you build the future! 
