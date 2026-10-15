# Changelog

## [2026-10-15]

### Changed
- Engine: Python 3.12 → 3.14 (`.python-version`, `requires-python`)
- Dependencies: `fastapi[standard]` floor 0.115.0 → 0.142.2 (locked 0.115.14 → 0.142.2, 0.x minor bumps may break)
- Transitive dependencies refreshed in `uv.lock`, including starlette 0.46 → 1.7 (MAJOR), rich 14 → 15 (MAJOR), markdown-it-py 3 → 4 (MAJOR), websockets 15 → 17 (MAJOR), pydantic 2.11 → 2.13, uvicorn 0.35 → 0.54
- README normalized to the Clever Cloud example format; removed the no longer used `CC_PYTHON_UV_SYNC_FLAGS` variable and added `CC_PYTHON_VERSION`

### Added
- `.gitignore`, `CHANGELOG.md`, `.last-checked`, Clever Cloud logo asset

### Notes
- Python held at 3.14; 3.15.0 was released on 2026-10-09 (< 14 days ago)
- Dependencies resolved with a 2026-10-01 cutoff: fastapi 0.143.x, starlette 1.8.0, pydantic 2.14.x, websockets 17.2 are too fresh
