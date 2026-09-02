# Contributing

Thanks for considering a contribution!

## Getting set up

1. Fork and clone the repo
2. Follow the setup steps in `README.md` (Docker Compose is the fastest path for the database)
3. Create a branch: `git checkout -b feature/your-feature-name`

## Development workflow

- Backend lives in `backend/`, frontend in `frontend/` — they run as separate processes locally (see README)
- Keep API changes backward compatible where possible, or update `frontend/src/api.js` alongside them
- Run `npm run build` in `frontend/` before opening a PR to catch build errors
- Match the existing code style (plain JS, no TypeScript, functional React components)

## Commit messages

Keep them short and descriptive: `fix: handle empty search query`, `feat: add CSV export`.

## Opening a PR

- Fill out the PR template
- Link any related issue
- Describe what you tested manually, since there's no automated test suite yet — adding one is a welcome contribution!

## Reporting bugs / requesting features

Use the issue templates under **Issues → New Issue**.
