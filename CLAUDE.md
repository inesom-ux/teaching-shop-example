# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Boutique Couture is an educational e-commerce application for learning DevOps concepts. It features a React frontend and Django backend for selling baby clothing.

## Development Commands

### Running the Full Stack
```bash
# Start both frontend and backend (requires tmux)
./start-dev.sh
```
This runs frontend on http://localhost:8080 and backend on http://localhost:8000.

### Frontend (frontend/)
```bash
npm install           # Install dependencies
npm run dev -- --port 8080  # Development server with HMR
npm run build         # Production build
npm run lint          # Run ESLint
```

### Backend (backend/)
```bash
uv sync                                    # Install dependencies
cd core && uv run python manage.py migrate # Run migrations
uv run python manage.py runserver          # Start on localhost:8000
uv run python manage.py createsuperuser    # Create admin user
```

## Architecture

**Monorepo Structure:**
- `frontend/` - React 19 + Vite + TypeScript + Tailwind CSS SPA
- `backend/` - Django 5 + Django REST Framework API

**Frontend Key Files:**
- `src/main.tsx` - Entry point, wraps App with ProductsContextProvider
- `src/contexts/ProductsContext.tsx` - Global products state management
- `src/api/products.ts` - API client (fetches from `http://localhost:8000/api/products/`)
- `src/App.tsx` - Main component with hero section and product grid

**Backend Key Files:**
- `core/api/models.py` - Product model (name, description, price, imageUrl)
- `core/api/urls.py` - Routes + DRF serializers/viewsets (all in one file)
- `core/api/settings.py` - Django configuration

**API Endpoints:**
- `GET/POST /api/products/` - List/create products
- `GET/PUT/DELETE /api/products/{id}/` - Product detail operations
- `/admin/` - Django admin interface

## Tech Stack

- **Frontend:** React 19, Vite 7, TypeScript, Tailwind CSS 4, Heroicons
- **Backend:** Django 5, Django REST Framework, SQLite
- **Package Managers:** npm (frontend), uv (backend, Python 3.11)

## Development Notes

- CORS is fully open (`CORS_ALLOW_ALL_ORIGINS = True`) for local development
- SQLite database at `backend/core/db.sqlite3` comes pre-populated
- Product images stored in `frontend/public/`
- No tests configured yet
- No Docker or CI/CD pipelines
