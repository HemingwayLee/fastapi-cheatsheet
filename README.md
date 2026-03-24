# fastapi-cheatsheet

## Django vs Flask vs FastAPI

| Feature | Django | Flask | FastAPI |
|---|---|---|---|
| **Type** | Full-stack framework | Micro-framework | API framework |
| **Interface** | WSGI (sync) | WSGI (sync) | ASGI (async) |
| **Server** | Gunicorn / uWSGI | Gunicorn / uWSGI | Uvicorn / Hypercorn |
| **Async support** | Limited (views can be async, but ORM is sync) | No native async | First-class async/await |
| **ORM** | Built-in (Django ORM) | None (use SQLAlchemy etc.) | None (use SQLAlchemy, Tortoise, etc.) |
| **Admin panel** | Built-in | None | None |
| **Auto API docs** | No (django-rest-framework adds some) | No | Built-in (Swagger UI + ReDoc) |
| **Data validation** | Django forms / DRF serializers | Manual or WTForms | Built-in via Pydantic |
| **Routing** | URL patterns (urls.py) | Decorators (`@app.route`) | Decorators (`@app.get`, `@app.post`, etc.) |
| **Learning curve** | Steep (many conventions) | Low | Low–Medium |
| **Best for** | Full web apps, CMS, admin-heavy projects | Simple apps, prototypes | High-performance APIs, microservices |
| **Performance** | Moderate | Moderate | High (async + Starlette core) |

### Why Flask and Django don't use Uvicorn

Flask and Django are **WSGI** (Web Server Gateway Interface) frameworks — a synchronous, blocking interface. Uvicorn is an **ASGI** (Asynchronous Server Gateway Interface) server designed for async frameworks.

- **Django/Flask servers**: Gunicorn, uWSGI, or the built-in `flask run` / `manage.py runserver` (dev only)
- **FastAPI server**: Uvicorn (or Hypercorn), because FastAPI is built on Starlette which requires ASGI

> Note: Django 3.0+ added *some* ASGI support (via `django.core.asgi`), so it *can* run on Uvicorn, but its ORM and middleware stack remain largely synchronous — you don't get the full async benefit. Flask has no ASGI support.