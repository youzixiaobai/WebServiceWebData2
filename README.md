# COMP3011 Coursework 2 — Search engine tool (quotes.toscrape.com)

Individual coursework: crawl the target site, build an inverted index with per-page word statistics, and query it from a small command-line shell.

## Setup

Requires **Python 3.8+**. From the repository root:

```bash
python -m venv .venv
.venv\Scripts\activate          # Windows
pip install -r requirements.txt
```

If `pip` fails with a proxy error on Windows, try clearing proxy variables for that shell, for example in PowerShell: `$env:HTTP_PROXY=''; $env:HTTPS_PROXY=''; pip install -r requirements.txt`.

### `build` fails with `ProxyError` / “Unable to connect to proxy”

The crawler **ignores `HTTP_PROXY` / `HTTPS_PROXY` by default** so a broken system proxy does not block `quotes.toscrape.com`. After pulling the latest code, run `build` again.

If you **must** use a corporate proxy, set `CWK2_USE_SYSTEM_PROXY=1` in the environment **and** configure valid `HTTP_PROXY` / `HTTPS_PROXY` values.

## Run the shell

From the repository root:

```bash
python -m src.main
```

Commands:

- `build` — crawl https://quotes.toscrape.com/, build the inverted index, save to `data/index.json` (waits **at least 6 seconds** between HTTP requests).
- `load` — load `data/index.json` into memory.
- `print <word>` — show postings (frequency and token positions on each page) for one word (case-insensitive).
- `find <word> [more words...]` — list pages that contain **all** given words (AND).
- `quit` — exit.

Examples:

```text
search> build
search> load
search> print friends
search> find good friends
```

## Tests

```bash
pytest
```

## Dependencies

See `requirements.txt` (`requests`, `beautifulsoup4`, `pytest`).

## Index file for Minerva

Run `build` once, then submit the generated `data/index.json` (or attach as instructed in the brief).
