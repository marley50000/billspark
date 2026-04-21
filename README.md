# BILLSPARK (MVP)

Local-first POS + Inventory for Ghana (PWA-ready).

## Repo structure

- `backend/`: Node.js + Express + Prisma + PostgreSQL + JWT auth
- `frontend/`: Vite + React + Tailwind + PWA shell
- `render.yaml`: Render Blueprint (DB + API + Web)

## Run locally (no Docker required)

### 1) Start PostgreSQL (pick one)

- **Docker**: `docker compose up -d`
- **Or install PostgreSQL** locally and create a DB + user

### 2) Backend

```powershell
cd backend
copy .env.example .env
npm install
npx prisma migrate dev --name init
npm run dev
```

Backend runs on `http://localhost:4000`.

### 3) Frontend

```powershell
cd ..\frontend
copy .env.example .env
npm install --legacy-peer-deps
npm run dev
```

Frontend runs on `http://localhost:5173`.

## Deploy to Render (recommended)

### 1) Put this code on GitHub

1. Create a new GitHub repo (empty)
2. Upload/push this whole `Sells/` folder to it

### 2) Deploy using the Blueprint

1. In Render Dashboard: **New → Blueprint**
2. Connect your GitHub repo
3. Render detects `render.yaml` and shows 3 resources:
   - `billspark-db` (PostgreSQL)
   - `billspark-api` (Node web service)
   - `billspark-web` (Static site)
4. Click **Apply**

### 3) After first deploy: set the cross-URLs

Render can’t auto-fill these until URLs exist.

1. Open `billspark-api` → **Environment**
   - Set `CORS_ORIGIN` to your frontend URL, e.g. `https://billspark-web.onrender.com`
2. Open `billspark-web` → **Environment**
   - Set `VITE_API_URL` to your API URL, e.g. `https://billspark-api.onrender.com`
3. Trigger a redeploy for both services (or “Manual Deploy”)

### 4) Install on mobile (PWA)

Open your `billspark-web` URL on mobile:

- **Android (Chrome)**: menu → **Install app**
- **iPhone (Safari)**: share → **Add to Home Screen**

## API quick test

- `GET /health`
- `POST /api/auth/signup`
- `POST /api/auth/login`
- `GET /api/me` (Bearer token)

