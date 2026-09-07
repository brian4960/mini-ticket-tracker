# Mini Ticket Tracker

A scaled-down issue/ticket tracker — similar in spirit to Linear or Jira — built as a full-stack CRUD application with a React + JavaScript frontend and a FastAPI + PostgreSQL backend.

The project is scoped around a single core entity (tickets) so the full CRUD loop, a real status lifecycle, and clean data flow between frontend and backend can be built end-to-end rather than left half-finished across too many features.

## Features

- Create tickets with title, description, priority, and initial status
- View all tickets, filterable by status and priority, sortable by creation date or priority
- View full detail for a single ticket
- Update ticket fields, including moving a ticket through a constrained status lifecycle (`open` → `in_progress` → `closed`)
- Delete tickets with confirmation

## Tech Stack

**Frontend**
- React + JavaScript
- React Router
- TanStack Query (React Query) for data fetching, caching, and mutation handling
- Context API for lightweight shared UI state
- Vite

**Backend**
- FastAPI (Python)
- Pydantic for request/response validation
- SQLAlchemy ORM

**Database**
- PostgreSQL

## Data Model

### Ticket

| Field | Type | Notes |
|---|---|---|
| `id` | integer | Primary key, DB-generated |
| `title` | string | Required |
| `description` | string | Optional |
| `status` | enum: `open`, `in_progress`, `closed` | Defaults to `open` |
| `priority` | enum: `low`, `medium`, `high` | Required |
| `created_at` | timestamp | Server-set |
| `updated_at` | timestamp | Server-set, updated on edit |

## API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/tickets` | List tickets, supports `?status=` and `?priority=` filters |
| `GET` | `/tickets/{id}` | Fetch a single ticket |
| `POST` | `/tickets` | Create a ticket |
| `PATCH` | `/tickets/{id}` | Partially update a ticket, including status |
| `DELETE` | `/tickets/{id}` | Delete a ticket |

## Getting Started

> Setup instructions will be filled in once the project scaffolding is in place.

### 1. Environment variables

Each service has its own `.env`, based on the checked-in `.env.example` in that folder.

```bash
cd backend
cp .env.example .env
# fill in DATABASE_URL, etc.

cd ../frontend
cp .env.example .env
# fill in VITE_API_URL, etc.
```

### 2. Run the backend

```bash
cd backend
python -m venv .venv
source .venv/bin/activate   # .venv\Scripts\activate on Windows
pip install -r requirements.txt
uvicorn main:app --reload
```

### 3. Run the frontend

```bash
cd frontend
npm install
npm run dev
```

## Project Structure

```
.
├── backend/
│   ├── main.py
│   ├── models.py
│   ├── schemas.py
│   ├── database.py
│   ├── .env.example
│   └── .env              # gitignored
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   └── api/
│   ├── vite.config.js
│   ├── .env.example
│   └── .env              # gitignored
├── .gitignore
└── README.md
```

## Roadmap

- User accounts / authentication / ticket assignees
- Real-time updates across clients (WebSockets)
- Comments or activity history per ticket
- Soft delete with audit trail
- Pagination for larger datasets

## License

MIT