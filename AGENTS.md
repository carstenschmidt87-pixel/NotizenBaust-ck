# AGENTS.md

## Cursor Cloud specific instructions

### What this repo is

A **zero-dependency static website** — the German Masonic-themed interactive evening puzzle **"Gesellenstück"**. It is only HTML, CSS, and vanilla JavaScript plus image assets at the repository root. There is **no package manager, no build step, no backend, no database, and no lockfile**. All puzzle logic runs client-side in the browser.

### Running it (development)

Serve the repository root over HTTP and open pages in a browser:

```bash
python3 -m http.server 8000
```

Then open pages directly, e.g. `http://localhost:8000/bauplan.html`.

Non-obvious caveats:

- **There is no `index.html`.** Navigate to a specific page (participant pages like `arno.html`, the master dashboard `bauplan.html`, `schlussstein.html`, `kamera.html`, `orakel.html`). Opening the bare `http://localhost:8000/` just shows a directory listing.
- **Serve over HTTP, not `file://`.** Relative asset paths and the camera page's `getUserMedia` permissions require an HTTP origin (`localhost` counts as a secure context).
- Google Fonts are loaded from a CDN and are cosmetic only; pages fall back to a serif font offline.

### Lint / test / build

There is **nothing to lint, test, or build** — no test suite, linter config, or build tooling exists. "Running the app" means serving the static files and opening pages in a browser.

### Useful facts for testing flows

- `bauplan.html` is the master dashboard; password is `MEISTER`. It documents every puzzle answer, the pair assignments, and hidden bypasses.
- `schlussstein.html` (keystone) expects the 10-letter word **`PYTHAGORAS`** typed across its 10 slots; solving it reveals a link onward to `kamera.html`.
- `kamera.html` uses the webcam to detect 10 colored cans; there is a master bypass (triple-tap on the title) for testing without props.
- `orakel.html` is a rule-based (keyword-matching) oracle — no LLM/API calls.
