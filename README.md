HorribleTown
=============

Short description
-----------------

HorribleTown is a research / demo codebase for generative agents and simulation-oriented systems. It contains a lightweight Django-based frontend server, a simulation backend (the `reverie` package), and utilities for storing and serving generated simulation outputs and assets.

Goals
-----
- Provide an environment to run and inspect agent-based simulations.
- Serve simulation UI and static assets via a minimal Django frontend.
- Offer utilities for compressing, storing and iterating on generated scene data.

Repository layout (important paths)
----------------------------------
- Project root: contains this README and project-level metadata.
- Frontend server: [environment/frontend_server](environment/frontend_server)
	- Entry: [environment/frontend_server/manage.py](environment/frontend_server/manage.py)
	- App code: [environment/frontend_server/frontend_server](environment/frontend_server/frontend_server)
	- Static and storage: [environment/frontend_server/storage](environment/frontend_server/storage)
- Simulation backend: [reverie](reverie)
	- Main simulation logic and tools: [reverie/backend_server](reverie/backend_server)
	- Helpers and persona code: [reverie/persona](reverie/persona)
	- Utilities: [reverie/global_methods.py](reverie/global_methods.py)

Quickstart
----------
Prerequisites

- Python 3.10+ (virtualenv recommended)
- Install pip requirements from the root `requirements.txt` or the `environment/frontend_server/requirements.txt` as appropriate.

Install (recommended)

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
pip install -r environment/frontend_server/requirements.txt
```

Run the frontend (Django)

```bash
# from repository root
cd environment/frontend_server
python manage.py migrate   # if using DB migrations
python manage.py runserver
```

Run the simulation/backend scripts

```bash
# example: run the reverie backend script
python reverie/backend_server/reverie.py
# or run tests / utilities in reverie
python reverie/compress_sim_storage.py
```

High-level components
---------------------

- Frontend (Django): minimal UI and static file serving. Look in [environment/frontend_server/frontend_server](environment/frontend_server/frontend_server) for URL routing and views.
- Storage: pre-populated example outputs live under `environment/frontend_server/storage/` and `environment/frontend_server/compressed_storage/`.
- Reverie backend: contains core simulation code, path finding (`reverie/backend_server/path_finder.py`), simulation loop (`reverie/backend_server/reverie.py`), and persona definitions.

Important files to inspect
-------------------------
- [environment/frontend_server/manage.py](environment/frontend_server/manage.py) — Django CLI entry
- [environment/frontend_server/frontend_server/urls.py](environment/frontend_server/frontend_server/urls.py) — frontend routes
- [reverie/backend_server/reverie.py](reverie/backend_server/reverie.py) — main simulation runner script
- [reverie/backend_server/path_finder.py](reverie/backend_server/path_finder.py) — path planning utilities
- [reverie/global_methods.py](reverie/global_methods.py) — shared utilities used across the repo

Development notes
-----------------

- Static assets and example simulation outputs are large; storage directories under `environment/frontend_server/storage/` and `environment/frontend_server/compressed_storage/` contain pre-generated scenes and may be several hundred MBs.
- The Django frontend uses a simple SQLite DB in development mode: `environment/frontend_server/db.sqlite3`.
- When iterating on simulation code, run `python reverie/backend_server/reverie.py` from the repository root to exercise the backend tools. For web testing, run the Django development server as shown above.

Troubleshooting
---------------
- If a server fails to start, check logs printed to the terminal for stack traces.
- Verify the active Python environment and that the `requirements.txt` files are installed.
- For database errors, try removing `environment/frontend_server/db.sqlite3` and re-running migrations (only in development/test environments).

Contributing
------------

If you want to contribute:

1. Open an issue describing what you'd like to change or improve.
2. Send a PR with focused changes and a short description of why the change helps.

License
-------
See the repository `LICENSE` file for license terms.

Enjoy exploring HorribleTown!


