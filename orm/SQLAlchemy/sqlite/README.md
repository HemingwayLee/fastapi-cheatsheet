# SQLAlchemy + FastAPI Hello World

A minimal example of using SQLAlchemy ORM with FastAPI. Creates a SQLite database with an `Item` model and exposes basic CRUD endpoints.

## Setup

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Run

```bash
uvicorn main:app --reload
```

## Endpoints

| Method | Path | Description |
|--------|------|-------------|
| `POST` | `/items` | Create an item |
| `GET` | `/items` | List all items |
| `GET` | `/items/{id}` | Get item by ID |

## Example Usage

**Create an item:**
```bash
curl -X POST http://localhost:8000/items \
  -H "Content-Type: application/json" \
  -d '{"name": "hello", "description": "world"}'
```

**List all items:**
```bash
curl http://localhost:8000/items
```

**Get item by ID:**
```bash
curl http://localhost:8000/items/1
```

## Interactive Docs

Visit http://localhost:8000/docs for the auto-generated Swagger UI.

## Key Concepts

- **`Base`** — `DeclarativeBase` subclass; all ORM models inherit from it
- **`SessionLocal`** — factory that creates DB sessions
- **`get_db`** — FastAPI dependency that opens a session per request and closes it after
- **`Base.metadata.create_all`** — creates tables on startup if they don't exist
- SQLite file `hello.db` is created automatically in the project directory
