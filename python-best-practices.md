# Python Best Practices for Scalable, Maintainable Projects

## 📌 Core Principles

These principles bring Java/Spring Boot discipline into Python development. They prioritize long-term maintainability, testability, and team-scale growth.

### ✅ Project Structure

* Organize code into clear layers:

  * `interfaces/`: Contracts (via `abc.ABC`)
  * `services/`: Business logic implementations
  * `models/`: Domain/data models (`@dataclass`, `Pydantic`, or ORM models)
  * `controllers/`: API layer (e.g., FastAPI routers)
  * `repositories/`: Data access abstractions

### ✅ Interfaces

* Define contracts using `abc.ABC` and `@abstractmethod`.
* Avoid duck typing in critical systems—explicit contracts make testing and architecture stronger.

```python
from abc import ABC, abstractmethod

class PaymentProcessor(ABC):
    @abstractmethod
    def process(self, amount: float) -> bool:
        pass
```

### ✅ Models

* Use `@dataclass` or `pydantic.BaseModel` to represent data.
* Immutable models (`frozen=True`) where appropriate.

```python
from dataclasses import dataclass

@dataclass(frozen=True)
class User:
    id: int
    name: str
```

### ✅ Dependency Injection (Manual)

* Inject dependencies via constructors.
* No global state or magic singletons.

```python
class UserService:
    def __init__(self, repo: UserRepository):
        self.repo = repo
```

### ✅ Avoid Static-like Design

* Avoid `@staticmethod` and module-level functions for logic.
* Prefer class-based design to support testing and extension.

### ✅ Typing and Static Analysis

* Use full type hints across all code.
* Enforce type checks using `mypy` in CI.

```python
def get_user(user_id: int) -> Optional[User]:
    ...
```

### ✅ Testing and Mocking

* Use `pytest` + mocks based on interfaces.
* Avoid testing implementation details—test behavior.

### ✅ Tooling

* **black**: Autoformatter
* **ruff**: Fast linter
* **mypy**: Static typing validator
* **pytest**: Testing framework

Use pre-commit hooks and CI pipelines to enforce standards.

## 📂 Folder Layout Example

```
project_root/
├── interfaces/
│   └── user_service.py
├── services/
│   └── default_user_service.py
├── models/
│   └── user.py
├── controllers/
│   └── user_controller.py
├── repositories/
│   └── user_repository.py
├── main.py
└── tests/
```

---

## 🔁 Core Philosophy

**Write Python like Java with freedom, not laziness.**
Discipline must be intentional. This structure makes Python scalable, testable, and production-grade.

## 🔧 Mentor-Style Architecture for Python

### ✅ The 3 Mentor-Derived Rules

1. **All method implementations go in a mixin.**
   ➤ Keeps logic out of interfaces and avoids inheritance bloat.

2. **Abstracts wire state, concretes wire values.**
   ➤ Optionally use abstract base classes to wire `__init__` state. Concrete classes assemble dependencies.

3. **Interfaces define contracts, mixins define behavior.**
   ➤ `abc.ABC` declares what must exist; mixins declare how it behaves.

### 🧠 Comparison Table

| Concept             | Java                 | Python Equivalent            |
| ------------------- | -------------------- | ---------------------------- |
| Contract            | `interface`          | `abc.ABC`                    |
| Implementation      | default method       | `Mixin`                      |
| State wiring        | `abstract class`     | Optional abstract base class |
| Dependency wiring   | concrete class       | concrete class               |
| Separation of logic | enforced by compiler | enforced by structure        |

### 🔥 Why This Works

* **Interface-first**: Design behavior contractually.
* **Loose coupling**: Keep logic out of concretes/abstracts.
* **Max testability**: Interfaces + mixins = easily mockable and swappable.
* **Alignment with SOLID**: Especially ISP, DIP, SRP.

### 🧾 TL;DR

> **All logic goes in mixins.**
> **Interfaces define contracts.**
> **Concrete classes only wire dependencies.**

That’s the Pythonic path to writing Java-grade architecture.
