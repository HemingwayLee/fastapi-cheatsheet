# FastAPI Hello World

A minimal FastAPI application to get you started.

## Setup with virtualenv

### 1. Create and activate a virtual environment

```bash
python3 -m venv venv
source venv/bin/activate      # macOS / Linux
# venv\Scripts\activate       # Windows
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Run the server

```bash
uvicorn main:app --reload
```

The `--reload` flag auto-restarts the server on code changes (great for development).

## What is Uvicorn?

Uvicorn is an ASGI (Asynchronous Server Gateway Interface) web server for Python. It serves as the runtime that actually listens for HTTP requests and passes them to your FastAPI application.

**Why Uvicorn?**
FastAPI is a framework, not a server — it needs a server to receive and handle network traffic. Uvicorn fills that role, built on `uvloop` and `httptools` for high performance.

**Command breakdown:**
```bash
uvicorn main:app --reload
#        ^    ^   ^
#        |    |   └── auto-reload on file changes (dev only)
#        |    └────── the FastAPI app instance inside main.py
#        └─────────── the Python module (main.py)
```

**Common options:**

| Flag | Description |
|------|-------------|
| `--reload` | Auto-restart on code changes (development only) |
| `--host 0.0.0.0` | Listen on all network interfaces (default: `127.0.0.1`) |
| `--port 8080` | Change port (default: `8000`) |
| `--workers 4` | Run multiple worker processes (production) |

**Development vs production:**
```bash
# Development
uvicorn main:app --reload

# Production (use multiple workers or a process manager like gunicorn)
uvicorn main:app --host 0.0.0.0 --port 8000 --workers 4
```

## Try it out

| What | URL |
|------|-----|
| Root endpoint | http://127.0.0.1:8000/ |
| Item endpoint | http://127.0.0.1:8000/items/42?q=hello |
| Interactive docs (Swagger UI) | http://127.0.0.1:8000/docs |
| Alternative docs (ReDoc) | http://127.0.0.1:8000/redoc |

### Example responses

```bash
curl http://127.0.0.1:8000/
# {"message":"Hello, World!"}

curl "http://127.0.0.1:8000/items/42?q=hello"
# {"item_id":42,"q":"hello"}
```

## Deactivate the virtual environment

```bash
deactivate
```

## Project structure

```
hello/
├── main.py          # FastAPI application
├── requirements.txt # Python dependencies
└── README.md        # This file
```
