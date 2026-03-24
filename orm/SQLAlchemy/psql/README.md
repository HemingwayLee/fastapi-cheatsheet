# FastAPI + SQLAlchemy + PostgreSQL

A minimal "hello world" CRUD API using **FastAPI**, **SQLAlchemy 2**, and **PostgreSQL**, containerised with Docker Compose.

## Project structure

```
.
├── main.py          # FastAPI routes
├── database.py      # SQLAlchemy engine + session + Base
├── models.py        # ORM model (Item)
├── schemas.py       # Pydantic request/response schemas
├── init_db.py       # Creates tables on startup
├── requirements.txt
├── Dockerfile
└── docker-compose.yml
```

## Run with Docker Compose

```bash
docker compose up --build
```

The API will be available at **http://localhost:8000** once the `api` container prints `Application startup complete`.

Stop everything (and keep the database volume):

```bash
docker compose down
```

Stop and **wipe the database**:

```bash
docker compose down -v
```

## API endpoints

| Method | Path | Description |
|--------|------|-------------|
| GET | `/` | Health check |
| POST | `/items` | Create an item |
| GET | `/items` | List all items |
| GET | `/items/{id}` | Get one item |
| DELETE | `/items/{id}` | Delete an item |

Interactive docs: **http://localhost:8000/docs**

## Quick demo (curl)

```bash
# Create
curl -s -X POST http://localhost:8000/items \
  -H "Content-Type: application/json" \
  -d '{"name": "apple", "description": "a fruit"}' | jq

# List
curl -s http://localhost:8000/items | jq

# Get by id
curl -s http://localhost:8000/items/1 | jq

# Delete
curl -s -X DELETE http://localhost:8000/items/1 -o /dev/null -w "%{http_code}\n"
```

## Run locally (without Docker)

1. Start a PostgreSQL instance and export the connection string:

```bash
export DATABASE_URL=postgresql://postgres:postgres@localhost:5432/appdb
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. Create tables and start the server:

```bash
python init_db.py
uvicorn main:app --reload
```

## Key concepts

| File | What it shows |
|------|---------------|
| `database.py` | `create_engine`, `sessionmaker`, `declarative_base`, `get_db` dependency |
| `models.py` | `Column`, `Integer`, `String`, `Text`, primary key, index |
| `schemas.py` | Pydantic v2 `BaseModel`, `model_config = {"from_attributes": True}` |
| `main.py` | `Depends(get_db)`, `db.add/commit/refresh/delete`, 404 handling |
