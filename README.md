# Deploy a FastAPI application with uv on Clever Cloud
[![Clever Cloud - PaaS](https://img.shields.io/badge/Clever%20Cloud-PaaS-orange)](https://clever-cloud.com)

This is an example of how to deploy a [FastAPI](https://fastapi.tiangolo.com/) application
on Clever Cloud, using [uv](https://docs.astral.sh/uv/) to manage the Python project and its
dependencies.

This example uses the [Python runtime](https://www.clever.cloud/developers/doc/deploy/applications/python/)
with its [native uv support](https://www.clever.cloud/developers/doc/deploy/applications/python/uv/),
on Python 3.14. The application is a "Hello world" JSON API that listens on `0.0.0.0:8080`.

## How it works

Native uv deployment activates when both conditions are met:

- a `uv.lock` file exists at the root of the project,
- the `CC_PYTHON_UV_RUN_COMMAND` environment variable is set.

During the build, Clever Cloud installs the locked dependencies with
`uv sync --locked --no-progress --no-dev`. At run time, it executes `CC_PYTHON_UV_RUN_COMMAND`
(without shell expansion), here the FastAPI CLI from the virtual environment:
`.venv/bin/fastapi run server.py --port 8080 --host 0.0.0.0`.

No Nginx, uWSGI or Gunicorn is involved: FastAPI (through Uvicorn) serves HTTP itself.

## Project structure

```
.
├── .python-version   # Python version used by uv (3.14)
├── pyproject.toml    # Project metadata and dependencies (fastapi[standard])
├── uv.lock           # Locked dependency tree, required for native uv deployment
└── server.py         # The FastAPI application
```

## Deployment steps

To deploy this application, you need [Clever Tools](https://github.com/CleverCloud/clever-tools), the Clever Cloud CLI.

```bash
git clone https://github.com/CleverCloud/python-fastapi-uv-example.git
cd python-fastapi-uv-example

# Step 1: Create the application
clever create --type python fastapi-uv-example

# Step 2: Configure the Python version and the uv run command
clever env set CC_PYTHON_VERSION 3.14
clever env set CC_PYTHON_UV_RUN_COMMAND ".venv/bin/fastapi run server.py --port 8080 --host 0.0.0.0"

# Step 3: Add your domain (optional but recommended)
clever domain add <YOUR_DOMAIN_NAME>

# Step 4: Deploy
clever deploy
```

And you're done! Your application is deploying and will be available on the `<YOUR_DOMAIN_NAME>` domain
(or on the default `cleverapps.io` domain shown by `clever domain`).

## Running locally

Install [uv](https://docs.astral.sh/uv/getting-started/installation/), then:

```bash
uv sync --locked
uv run fastapi dev server.py   # start the server on http://localhost:8000
```

The interactive API documentation is available at `/docs`.

## Troubleshooting

If you encounter issues:

1. Check the application logs: `clever logs`
2. Verify all environment variables are correctly set: `clever env`
3. Make sure `uv.lock` is committed and up to date (`uv lock --check`), as the build runs `uv sync --locked`.
4. Make sure the application listens on `0.0.0.0:8080`.

## Contributing

Contributions to improve this deployment example are welcome! Please feel free to submit pull requests or open issues for any enhancements or bug fixes.

## License

This example is provided under the terms of the MIT license.
