# Live Polling System

A small real-time polling application composed of a TypeScript/Express backend (Socket.IO + Prisma) and a React + Vite frontend (TypeScript + TailwindCSS). Built to demonstrate live polls with teacher and student interfaces, real-time updates via websockets, and a small REST endpoint for poll history.

---

## 🚀 Quick start

Requirements:
- Node.js 18+ (LTS recommended)
- npm (or yarn/pnpm)
- (Optional) PostgreSQL if you want to use Postgres; by default the project may use SQLite via Prisma when `DATABASE_URL` is not provided.

1. Install dependencies

```bash
# from project root
cd backend && npm install
cd ../frontend && npm install
```

2. Environment files

- Backend: copy and edit `backend/.env` (contains `DATABASE_URL`, `API_PORT`, `CORS_ORIGIN`) if needed.
- Frontend: edit `frontend/.env` (contains `VITE_API_URL`) to point to your backend.

3. Database (Prisma)

```bash
# Backend
cd backend
npm run db:generate      # prisma generate
npm run db:migrate       # apply migrations (dev)
# OR to push the schema directly (dev only):
npm run db:push
npm run db:studio        # opens Prisma Studio
```

4. Run development servers

```bash
# Backend
cd backend
npm run dev

# Frontend (new terminal)
cd frontend
npm run dev
# open http://localhost:5173
```

---

## 📁 Project structure (top-level)

- backend/
  - src/
    - index.ts             — Express + Socket.IO server
    - routes/              — REST endpoints (history)
    - sockets/             — socket handlers and setup
    - services/            — poll/session/chat services
    - config/              — Prisma client configuration
    - prisma/              — Prisma schema & migrations
  - package.json
  - .env

- frontend/
  - src/
    - components/          — React UI components
    - hooks/               — custom hooks (timers, session, web socket)
    - pages/               — top-level pages
    - store/               — Redux store and slices
    - services/            — REST helpers
  - index.html
  - package.json
  - tailwind.config.js
  - postcss.config.js

---

## 🧩 Scripts (use from each folder)

- Backend (backend/package.json):
  - `npm run dev` - start dev server with `nodemon`
  - `npm run build` - compile TypeScript
  - `npm run start` - run compiled build
  - `npm run test` - run local test script (after build)
  - `npm run db:*` - Prisma helpers

- Frontend (frontend/package.json):
  - `npm run dev` - run Vite dev server
  - `npm run build` - build production bundle
  - `npm run preview` - preview build
  - `npm run lint` - run ESLint

---

## 🛠️ Notes & Troubleshooting

- Tailwind/CSS not applied?
  - Make sure `frontend/src/index.css` includes Tailwind directives in this order:
    ```css
    @import url("https://fonts.googleapis.com/...");
    @tailwind base;
    @tailwind components;
    @tailwind utilities;
    ```
  - Google font `@import` must appear before any Tailwind directives (PostCSS requires `@import` before other rules besides `@charset` and empty `@layer`).
  - Confirm `src/main.tsx` imports `./index.css`.

- Environment:
  - Backend uses `DATABASE_URL`, `API_PORT` and `CORS_ORIGIN`. If `DATABASE_URL` is missing the server warns and suggests using Prisma `db:push` for a local SQLite DB.
  - Frontend uses `VITE_API_URL` to talk to the backend (set in `frontend/.env`).

- Logs: The repo contains many `console.log` calls for development debugging. Consider adding a small `logger` util that is quiet in production when you prepare for deployment.

- Unused or duplicate files:
  - `backend/src/sockets/index.new.ts` appears to be a duplicate of `backend/src/sockets/index.ts` and can be removed safely. Confirm before deleting.
  - `frontend/src/App.css` appears unused and can be removed safely if you don't need it.

---

## ✅ Recommendations (non-breaking)

- Add a `typecheck` script to the `frontend/package.json` to run `tsc --noEmit` for quick type checks.
- Replace `console.log` with a small `utils/logger` that no-ops in production to keep logs clean.
- Add unit tests for timer hooks and socket middleware to ensure behavior remains stable after refactors.

---

## Contributing

Feel free to open a PR with fixes, improvements, or documentation updates. Keep changes small and add tests for behavioral changes.

---

If you'd like, I can:
- commit this README and open a PR
- remove the duplicate/unused files mentioned above
- add the `typecheck` script and a small `logger` utility and update console calls

Tell me which actions you'd like me to take next. 👇
