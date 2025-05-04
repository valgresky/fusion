# 🚀 Fusion 10 – Hybrid AI App Template (Monorepo)

A production-ready, multi-tenant template for rapidly building AI-powered web and mobile apps with robust agent orchestration, workflow automation, and modern UI.

---

## 🛠️ Requirements

- **Python** 3.10+
- **Node.js** 18+
- **npm** 9+ or **yarn**
- **Docker** (for n8n, recommended for local/prod deployment)
- **Docker Compose** (for multi-service orchestration)
- **Turborepo** or **Nx** (for monorepo management)
- See `requirements.txt` and `package.json` for library versions

---

## 🧱 Stack Overview

- **Frontend:** Next.js (via bolt.new), Tailwind, shadcn, GSAP, Three.js
- **Mobile (optional):** Expo/React Native (EAS for builds, OTA updates)
- **Backend:** FastAPI (Python) for agent orchestration and context loaders
- **AI Agents:** Pydantic AI, LangChain, modular agent structure
- **Workflow Automation:** n8n (visual workflow engine)
- **Database/Auth:** Supabase (Postgres, Auth, secrets, edge functions)
- **Optional:** Lovable (AI UX), UX Pilot (user testing), or React Native bridge for advanced mobile integration

---

## 🏗️ Monorepo Directory Structure

```bash
/fusion10/
├── apps/
│   ├── web/           # Next.js (Bolt) app
│   └── mobile/        # Expo/React Native app
├── packages/
│   ├── ui/            # Shared Tamagui/React Native components
│   ├── lib/           # Shared logic, hooks, API clients
│   └── types/         # Shared TypeScript types/interfaces
├── backend/           # FastAPI/Archon agentic backend
│   ├── main.py
│   ├── loaders/
│   ├── agents/
│   ├── models/
│   ├── schemas/
│   ├── config.py
│   └── tests/
├── workflows/         # n8n HTTP endpoints & flows (for backup/examples)
├── supabase/          # Auth, db schema, edge functions, migrations
├── docs/              # planning.md, task.md, decision_ai.md, users.md, journey.md, deployment.md, testing.md
├── tests/             # (root-level) Example test structure for all surfaces
├── requirements.txt
├── package.json
├── yarn.lock / package-lock.json
└── .env.example
```
> _Mobile support is fully integrated but optional—remove `/apps/mobile/` if not needed. Add or remove `/tests` as your project grows._

---

## 🧠 Architecture: Multi-Method, Hybrid-Ready

```text
+-------------------+         +-------------------+         +-------------------+
|   Next.js Frontend| <-----> |      n8n          | <-----> |   FastAPI Backend |
|   (bolt.new, etc) |         | (Workflow Engine) |         |   (Python Agents) |
+-------------------+         +-------------------+         +-------------------+
         |                            |                              |
         |                            |                              |
         |                            v                              v
         |                  +-------------------+         +-------------------+
         |                  |   Supabase        | <-----> |   Database/Auth   |
         |                  | (Auth, Secrets)   |         |   (Postgres)      |
         |                  +-------------------+         +-------------------+
         |
         v
+-------------------+
|   Expo Mobile App |
|   (optional)      |
+-------------------+
```
- **n8n:** Orchestrates workflows, triggers, and integrations. Can call FastAPI endpoints for advanced logic.
- **FastAPI:** Hosts Python agents (Pydantic AI, LangChain), exposes APIs for frontend/n8n.
- **Supabase:** Auth, secrets, RLS, and DB.
- **Frontend/Mobile:** Calls n8n or FastAPI as needed.

---

## 🧭 Usage Modes

- **n8n-Driven:** Visual workflow automation, business logic, integrations.
- **Python Agent-Driven:** Robust, type-safe, testable agent logic (LLM orchestration, validation, chaining).
- **Hybrid:** Combine both for complex SaaS, multi-tenant, or advanced AI workflows.

---

## 🔗 API Client Generation & Type Safety

- Use FastAPI’s built-in OpenAPI schema to auto-generate API clients for:
  - Next.js (TypeScript)
  - Expo (TypeScript)
  - n8n custom Python nodes (if needed)
- Tools: [openapi-typescript-codegen](https://github.com/ferdikoomen/openapi-typescript-codegen), [openapi-generator](https://openapi-generator.tech/)
- Place generated clients in `/apps/web/lib/` or `/apps/mobile/lib/` as appropriate.
- To update: re-run codegen after backend API changes and commit updated clients.
- Example command:
  ```bash
  npx openapi-typescript-codegen --input http://localhost:8000/openapi.json --output apps/web/lib/api
  ```

---

## 🔄 Code Sharing (Monorepo)

- For maximum code reuse, use [Tamagui](https://tamagui.dev/) or [React Native Web](https://necolas.github.io/react-native-web/) to share UI components between Expo and Next.js.
- Place all shared components in `/packages/ui/` and import them in both web and mobile apps.
- Use `/packages/lib/` for shared logic/hooks, `/packages/types/` for shared types/interfaces.

---

## 🚦 Quick Start

1. **Clone the repo**
   ```bash
   git clone [https://github.com/valgresky/fusion.git]
   cd fusion10
   ```

2. **Set up Supabase**
   - Create a project at [supabase.com](https://supabase.com)
   - Run migrations or apply schema from `/supabase/` if provided.
   - Set up Auth and enable Row Level Security (RLS) as needed.
   - Copy your API keys to `.env` (see `.env.example` for all required variables).

3. **Start Backend**
   ```bash
   cd backend
   uvicorn main:app --reload
   ```

4. **Start n8n**
   ```bash
   docker run -it --rm -p 5678:5678 n8nio/n8n
   # or see [n8n docs](https://docs.n8n.io/) for advanced/local setup
   ```

5. **Start Web Frontend**
   ```bash
   cd apps/web
   npm install
   npm run dev
   ```

6. **(Optional) Start Mobile**
   ```bash
   cd apps/mobile
   npx expo start
   ```
   > _Mobile is optional. Only run this step if you want to develop or test the mobile app._

---

## 🧪 Testing

- All Python code: `pytest`
  ```bash
  cd backend
  pytest
  ```
- All JS/TS code: `jest`
  ```bash
  cd apps/web
  npm test
  ```
- Mobile: `jest` + `detox`
  - See `/docs/testing.md` or [Detox docs](https://wix.github.io/Detox/docs/introduction/getting-started/) for setup.
- Tests should be placed in a `/tests` directory that mirrors the source structure.
- Include one success, one failure, and one edge case per function.
- Example:
  ```
  /backend/tests/
  /apps/web/tests/
  /apps/mobile/tests/
  /packages/ui/tests/
  ```

---

## 🔒 Security

- All secrets in Supabase or EAS dashboard (never committed to VCS/hardcoded in code).
- RLS enabled for all user data (see Supabase docs for [Row Level Security](https://supabase.com/docs/guides/auth/row-level-security)).
- HTTPS enforced everywhere (use Vercel, Nginx, or Caddy for SSL).
- Webhook URLs and API keys are never exposed in frontend code.
- Example `.env.example`:
  ```
  SUPABASE_URL=your-url
  SUPABASE_SERVICE_KEY=your-service-key
  SUPABASE_ANON_KEY=your-anon-key
  # Add other required variables for FastAPI, n8n, etc.
  ```

---

## 📄 Documentation Files

- `/docs/planning.md`: Project goals, roadmap, and high-level architecture.
- `/docs/task.md`: Current and completed tasks, with dates and owners.
- `/docs/decision_ai.md`: Key architectural and technical decisions, with rationale.
- `/docs/users.md`: User roles, permissions, and data policies.
- `/docs/deployment.md`: (Recommended) Deployment strategies and environment setup.
- `/docs/testing.md`: (Recommended) Testing setup and best practices.
- `/docs/journey.md`: (Recommended) Document your build journey, milestones, and lessons learned.

---

## 🚀 Deployment

- **Docker Compose:** Recommended for local development and production.
- **Vercel:** For frontend (Next.js) deployment.
- **Supabase:** Managed Postgres, Auth, and edge functions.
- **Mobile:** Use EAS (Expo Application Services) for builds and OTA updates.
- See `/docs/deployment.md` for step-by-step guides (add this file if needed).

---

## 🧠 References

- [Next.js](https://nextjs.org/)
- [Expo](https://docs.expo.dev/)
- [FastAPI](https://fastapi.tiangolo.com/)
- [n8n](https://n8n.io/)
- [Supabase](https://supabase.com/)
- [Pydantic AI](https://ai.pydantic.dev/)
- [LangChain](https://python.langchain.com/)
- [openapi-typescript-codegen](https://github.com/ferdikoomen/openapi-typescript-codegen)
- [openapi-generator](https://openapi-generator.tech/)
- [Detox](https://wix.github.io/Detox/docs/introduction/getting-started/)
- [Tamagui](https://tamagui.dev/)
- [React Native Web](https://necolas.github.io/react-native-web/)
- [Turborepo](https://turbo.build/)
- [Nx](https://nx.dev/)

---

## 🏆 Why Fusion 10?

**Fusion 10** is named for the “invisible default” that powers modern Python and AI development:

- **10** is the default for API pagination (`limit=10`), batch sizes, worker concurrency, and more—across FastAPI, Django, Pytest, Celery, and ML frameworks.
- It’s a best-practice, human-friendly chunk size for lists, dashboards, and previews.
- Using 10 as a subtle signature signals your stack is built on robust, industry-aligned defaults—making it fast, safe, and scalable out of the box.

---

## 🏆 Why This Template?

- **Separation of concerns:** Cleanly splits workflow, agent logic, and UI.
- **Multi-tenant ready:** Secure, scalable, and easy to extend.
- **Modern AI stack:** Best-in-class tools for rapid, reliable AI app development.
- **Hybrid flexibility:** Use n8n, Python agents, or both—your choice.
- **Type-safe integration:** Auto-generate API clients for all surfaces.
- **Optional code sharing:** Share UI between web and mobile for maximum efficiency.

---

## 🤝 Contributing & Community

- PRs, issues, and feedback welcome!
- Please see `CONTRIBUTING.md` and `CODE_OF_CONDUCT.md` (add these files for production-readiness).
- Follow [semantic versioning](https://semver.org/) for breaking changes.
- Add CI/CD (e.g., GitHub Actions) for automated testing and deployment.

---

## 📝 Glossary

- **n8n:** Visual workflow automation tool (see [n8n docs](https://docs.n8n.io/)).
- **Lovable, UX Pilot:** Optional tools for AI UX and user testing (add links or clarify if these are internal/proprietary).
- **EAS:** Expo Application Services for mobile builds and OTA updates.
- **RLS:** Row Level Security (Supabase feature for data access control).
- **Tamagui/React Native Web:** Libraries for cross-platform UI code sharing.
- **Turborepo/Nx:** Monorepo management tools for JS/TS projects.
