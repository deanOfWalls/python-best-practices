# Python CRUD Monolith (Documentation-Driven Setup)

A clean, maintainable project setup for learning Python the right way—structured, typed, and inspired by best practices from Java/Spring Boot. This guide uses **FastAPI**, **SQLModel**, and **SQLite** for simplicity and scalability.

---

### ✅ Step 1: Create a Project Directory

```bash
mkdir python-crud-monolith && cd python-crud-monolith
```

### ✅ Step 2: Set Up a Virtual Environment

```bash
python -m venv .venv
source .venv/bin/activate  # Use .venv\Scripts\activate on Windows
```

### ✅ Step 3: Create `requirements.txt` with Core Tools

```txt
fastapi
uvicorn[standard]
pydantic
sqlmodel
pytest
black
ruff
mypy
```

> 💡 Optional tools for later:
>
> ```txt
> alembic       # Migrations
> httpx         # API testing
> ```

### ✅ Step 4: Install Dependencies

```bash
pip install -r requirements.txt
```

### ✅ Step 5: Create the Project Structure

```bash
mkdir -p app/{controllers,services,interfaces,models,repositories,static}
mkdir tests
touch app/main.py
```

### ✅ Step 6: Add VS Code Dev Tools (Optional but Recommended)

Create `.vscode/settings.json`:

```json
{
  "python.defaultInterpreterPath": "${workspaceFolder}/.venv/bin/python",
  "python.formatting.provider": "black",
  "editor.formatOnSave": true,
  "python.linting.enabled": true,
  "python.linting.mypyEnabled": true,
  "python.linting.pylintEnabled": false,
  "python.linting.flake8Enabled": false
}
```

### ✅ Step 7: Create the `main.py` Entrypoint

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def root():
    return {"message": "Hello, Python Spring Boot style"}
```

### ✅ Step 8: Use SQLite for Persistence (H2 Equivalent)

SQLite requires no setup. Example DSN:

```python
sqlite_url = "sqlite:///./dev.db"
```

Fully supported by `sqlmodel` and ideal for testing + prototyping.

### ✅ Step 9: Run Your App

```bash
uvicorn app.main:app --reload
```

---

This setup gives you:

* A clean architecture
* Typing and linting from day one
* A dev database (SQLite) with no overhead

From here, you can build out:

* Entities (`models/`)
* Interfaces + services (`interfaces/`, `services/`)
* REST endpoints (`controllers/`)
* Data access (`repositories/`)

You're now ready to scale with Python the same way you would with Java/Spring Boot—**intentionally and cleanly**.
