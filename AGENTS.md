# Repository Guidelines

This guide helps contributors work effectively on AiNiee, a Python 3.12 + PyQt5 application for AI translation and batch file processing.

## Project Structure & Module Organization
- `AiNiee.py` – GUI entrypoint and application bootstrap.
- `ModuleFolders/` – core logic: `FileReader/`, `FileOutputer/`, `Translator/`, `LLMRequester/`, `PromptBuilder/`, `Cache/`, `RequestTester/`.
- `UserInterface/`, `Widget/`, `DRWidget/` – pages and custom widgets.
- `PluginScripts/` – extensions; each plugin subclasses `PluginBase` and registers events.
- `Resource/` – configuration, icons, localization (user config: `Resource/config.json`).
- `Tools/` – tooling (e.g., PyInstaller script).
- `StevExtraction/` – extraction helpers; `Example image/` – documentation assets.

## Build, Test, and Development Commands
- Prereqs: Python 3.12.
- Setup (Unix): `python -m venv .venv && . .venv/bin/activate && pip install -r requirements.txt`  (Windows: `\.venv\\Scripts\\activate`).
- Run locally: `python AiNiee.py`.
- Package (one-file): `python Tools/pyinstall.py` → binary in `dist/`; copy `Resource/`, `PluginScripts/`, `StevExtraction/` next to it (CI mirrors this in `.github/workflows/main.yml`).
- Alternative env: `pixi install` then `pixi run python AiNiee.py`.

## Coding Style & Naming Conventions
- PEP 8; 4‑space indentation; prefer type hints and docstrings.
- snake_case for files/functions; PascalCase for classes; UPPER_CASE for constants.
- Readers/Writers end with `Reader`/`Writer`; UI pages end with `Page`; requesters end with `Requester`.
- Plugins: subclass `PluginScripts/PluginBase.py`, set `name/description`, register events via `add_event`.
- No enforced linter; keep formatting consistent. Optional locally: `black`, `ruff`.

## Testing Guidelines
- Framework: pytest (recommended). Place tests in `tests/` named `test_*.py`.
- Include sample fixtures under `tests/data/` for reader/writer I/O.
- Cover new logic in readers/writers and plugin event handling.
- Run: `pytest -q` (add as needed; repo has no default suite).

## Commit & Pull Request Guidelines
- Use a lightweight Conventional Commits style when possible: `feat:`, `fix:`, `perf:`, `docs:`, `chore:` (English or Chinese acceptable). Keep subject ≤ 72 chars; reference issues (e.g., `Fixes #123`).
- PRs include: purpose, summary of changes, risks/impact, screenshots/GIFs for UI, steps to verify (`python AiNiee.py` and `python Tools/pyinstall.py`), and doc updates (`PluginScripts/README.md`, `ModuleFolders/FileAccessor/README.md`) when relevant.
- Do not commit secrets; `Resource/config.json` is gitignored. Use environment variables or local files for API keys.

