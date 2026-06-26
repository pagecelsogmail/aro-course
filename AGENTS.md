# AGENTS.md

## Cursor Cloud specific instructions

This repository (`aro-course`) is **course material**, not a deployable application. It is mostly
OpenShift/Kubernetes YAML manifests, Azure CLI/`oc` command transcripts (`*-commands.txt`), and
Azure deploy scripts grouped into numbered `Section NN: ...` folders. None of that runs locally —
those commands target real Azure / OpenShift clusters.

The **only locally runnable code** is a small Flask demo web app in
`Section 02: Understanding containers/1. Create a container app (web app), run it and push it to Docker Hub/`
(`app.py`, `requirements.txt`, `Dockerfile`).

### Running the Flask demo app

- A Python virtualenv is provisioned at `/workspace/.venv` by the update script (dependency: `flask`).
- Run it (the app hard-codes `host=0.0.0.0`, `port=8080`):
  - `cd "Section 02: Understanding containers/1. Create a container app (web app), run it and push it to Docker Hub"`
  - `/workspace/.venv/bin/python3 app.py`
- Routes: `/`, `/header`, `/url`, `/delay` (sleeps 15s), `/healthz`, `/images`, `/videos`.

### Gotchas

- **Section folder names contain colons (`:`)**. `python3 -m venv` refuses to create a venv inside a
  path containing `:`, so the venv lives at the repo root (`/workspace/.venv`), not inside the section
  folder. Always reference that interpreter explicitly.
- There are no tests, no linter config, and no build system in this repo. "Build" for the demo app is
  just the `Dockerfile` (`docker build`), and "run" is `python3 app.py`.
- The system `python3` is externally managed (Debian/Ubuntu), so always use the `/workspace/.venv`
  interpreter rather than `pip install` into the system Python.
