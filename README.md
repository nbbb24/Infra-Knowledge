<h1 align="center">Infra Knowledge</h1>

<p align="center">A bilingual knowledge base for AI infrastructure</p>

<p align="center">
| <a href="docs/zh/index.md">中文</a> | <a href="docs/en/index.md">EN</a> |
</p>

The first topic explains NPU hardware, memory movement, and cluster networking in plain language.

## Local preview

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements/mkdocs.txt
mkdocs serve
```

On Windows PowerShell, activate the environment with `.venv\Scripts\Activate.ps1`.
Open `http://127.0.0.1:8000` after the server starts.

## Build

```bash
mkdocs build --strict
```

The generated site is written to `site/` and is intentionally ignored by Git.

## Read the Docs deployment

1. Sign in to Read the Docs with the GitHub account that can access this repository.
2. Choose **Add project** and import `nbbb24/Infra-Knowledge`.
3. Keep the default branch as `main`. Read the Docs reads `.readthedocs.yaml` automatically.
4. Trigger the first build and open the generated site URL.
5. Optional: add a custom domain under **Admin → Domains** after the first successful build.

No generated HTML needs to be committed. Future pushes to `main` can trigger documentation builds automatically.

## Writing conventions

- Put Chinese pages under `docs/zh/` and English pages under `docs/en/`.
- Add every new page to `nav` in `mkdocs.yml`.
- Define an acronym on first use, for example `H2D (Host to Device)`.
- State the hardware generation or product model when a fact is not universal.
- Prefer diagrams and observable paths over isolated definitions.
