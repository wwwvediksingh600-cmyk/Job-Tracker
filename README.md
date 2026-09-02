# Job Application Tracker

![CI](https://github.com/YOUR_USERNAME/job-tracker/actions/workflows/ci.yml/badge.svg)
![License](https://img.shields.io/badge/license-MIT-blue.svg)

Full-stack job application tracker: React (Vite) frontend, Node/Express API, PostgreSQL for persistence.

> Replace `YOUR_USERNAME` above with your GitHub username once pushed, so the CI badge resolves.

## Features

- Add/edit/delete job applications — company, role, location, salary, date applied
- Status pipeline: `Applied → Interview → Offer/Rejected`
- Search and filter by company, role, location, or status
- Sort by date, status, company, or role
- Dashboard with totals, response rate, offer rate, and a status breakdown chart
- Individual application detail view
- Persistent PostgreSQL storage
- Responsive, mobile-friendly UI

## Structure

```
job-tracker/
├── .github/           issue/PR templates + CI workflow
├── backend/           Express API + PostgreSQL
│   ├── db/
│   │   ├── pool.js       connection pool
│   │   ├── schema.sql    table + trigger definitions
│   │   └── migrate.js    run schema.sql against your DB
│   ├── routes/
│   │   └── applications.js   CRUD + /stats endpoint
│   ├── server.js
│   └── .env.example
├── frontend/          React (Vite) UI
│   └── src/
│       ├── pages/         Dashboard, Applications list, Detail, Add/Edit form
│       ├── components/    StatusBadge, StatCard, FilterBar, ApplicationRow
│       ├── api.js         fetch wrapper for the backend
│       └── index.css
└── docker-compose.yml  optional local Postgres
```

## Quick start

### 1. Clone

```bash
git clone https://github.com/YOUR_USERNAME/job-tracker.git
cd job-tracker
```

### 2. Database

**Option A — Docker (fastest):**

```bash
docker compose up -d
```

Spins up Postgres on `localhost:5432` with database `job_tracker` / user `postgres` / password `postgres`, matching `backend/.env.example` out of the box.

**Option B — local install:**

```bash
createdb job_tracker
```

### 3. Backend

```bash
cd backend
cp .env.example .env      # edit if you're not using the Docker defaults
npm install
npm run migrate           # creates the applications table
npm run dev                # http://localhost:5000
```

### 4. Frontend

In a second terminal:

```bash
cd frontend
npm install
npm run dev                # http://localhost:5173
```

Vite proxies `/api/*` to `http://localhost:5000` in dev, so no extra config is needed. Open http://localhost:5173.

## API reference

| Method | Endpoint                  | Description                                    |
|--------|-----------------------------|-------------------------------------------------|
| GET    | `/api/applications`         | List, with `?search=&status=&sortBy=&order=`    |
| GET    | `/api/applications/stats`   | Dashboard aggregate stats                       |
| GET    | `/api/applications/:id`     | Single application                              |
| POST   | `/api/applications`         | Create                                          |
| PUT    | `/api/applications/:id`     | Update                                          |
| DELETE | `/api/applications/:id`     | Delete                                          |

`status` is constrained at the DB level to: `Applied`, `Interview`, `Offer`, `Rejected`.

## Deployment

- **Backend:** Render, Railway, or Fly.io. Set `DATABASE_URL` (and `PGSSL=true` for most managed Postgres providers).
- **Frontend:** Vercel or Netlify. Set `VITE_API_URL` to your deployed backend's `/api` URL.
- **Database:** any managed Postgres — Supabase, Neon, Railway, or Render all have free tiers.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Issues and PRs welcome.

## License

[MIT](LICENSE)
