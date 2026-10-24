# SQLite Core

*An educational project showcasing how to use SQLite with Python, covering both synchronous and asynchronous approaches.*

## Project Structure

```
sqlite-core/
├── app/                   # Main application code
├── .env.example           # Example environment variables file
├── pixi.lock              # Locked dependency versions for reproducible environments
├── pixi.toml              # Pixi project configuration: environments, dependencies, 
│                          # platforms and project-specific commands
└── playground-testing/    # Jupyter notebooks for playground testing
```

Each directory includes its own `README.md` with detailed information about its contents and usage, and every file contains comprehensive inline comments to explain the code.

## Dependencies Overview

| Dependency | Repository | What it is |
| :--- | :--- | :--- |
| **CPython** | [python/cpython](https://github.com/python/cpython) | The de facto standard implementation of the Python programming language. |
| **pydantic-settings** | [pydantic/pydantic-settings](https://github.com/pydantic/pydantic-settings) | Pydantic-powered library for managing application configuration and environment variables with strong typing, validation, and seamless `.env` support. |
| **SQLAlchemy** | [sqlalchemy/sqlalchemy](https://github.com/sqlalchemy/sqlalchemy) | The Python SQL toolkit and Object-Relational Mapper (ORM) used as the foundation for database modeling, querying, and transaction management in both synchronous and asynchronous contexts. |
| **Alembic** | [sqlalchemy/alembic](https://github.com/sqlalchemy/alembic) | A lightweight database migration tool for SQLAlchemy, enabling structured, version-controlled evolution of the SQLite schema over time. |
| **sqlite3** | - | Python’s built-in module for working with SQLite databases — no extra installation required. |
| **aiosqlite** | [omnilib/aiosqlite](https://github.com/omnilib/aiosqlite) | An asynchronous wrapper around Python’s built-in `sqlite3` module, enabling non-blocking SQLite database operations. |
| **JupyterLab** *(Dev)* | [jupyterlab/jupyterlab](https://github.com/jupyterlab/jupyterlab) | Next-generation web-based interactive development environment for Jupyter notebooks; used here to create interactive documents for testing and verifying code execution. |
| **sqlite** *(Dev)* | [mackyle/sqlite](https://github.com/mackyle/sqlite) | The official SQLite engine CLI tool. [^1] |

[^1]: While Python’s built-in `sqlite3` module handles all runtime database operations, it lacks the ability to connect to the database via a command-line interface to inspect or query data using SQL-like commands. Installing the full SQLite engine provides a CLI tool that allows direct inspection, querying, and manipulation of the SQLite database file from the terminal (e.g., to verify schema structure or examine raw data).

## Quick Start

### I. Prerequisites

| Component | Requirement |
| :--- | :--- |
| **Operating System** | GNU/Linux-based system |
| **Architecture** | `x86_64` |
| **Package Manager** | [`Pixi`](https://pixi.prefix.dev/latest/) |

> **Note:**  
> These are not strict requirements, but rather the baseline environment where the code is 
> guaranteed to run out of the box. Alternative setups are possible but may require manual 
> configuration.

### II. Environment Setup

1. **Clone the repository**

    ```bash
    git clone https://github.com/snegoviol/sqlite-core.git
    cd sqlite-core
    ```

2. **Install dependencies**
    
    ```bash
    pixi install --all
    ```

3. **Setup environment configuration**
    
    ```bash
    pixi run copy-env
    ```

4. **Create a database migration & Apply it**
    
    ```bash
    pixi run alembic-revision
    pixi run alembic-upgrade
    ```

### III. Testing

Once a database is ready, you can run and test the SQLite implementation with interactive Jupyter notebooks in `playground-testing/`:

1. **Launch JupyterLab**

    ```bash
    pixi run -e test jupyter lab
    ```

2. **Test the SQLite implementation**
    - JupyterLab should open automatically in your browser at the default address.
    - In JupyterLab, navigate to the `playground-testing/` folder.
    - Open and execute the notebooks interactively.

3. **(Optional) Verify database manually**  
You can open a SQLite shell to manually verify that everything is working correctly:

    ```bash
    pixi run sqlite-shell
    ```

### IV. Cleanup

When you finish testing, stop JupyterLab by pressing `Ctrl+C` in the terminal where it's running.

## License

Each file in this repository is licensed under the [MIT No Attribution License](LICENSE.txt).
