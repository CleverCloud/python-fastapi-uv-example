# FastAPI with uv on Clever Cloud

You'll need a Clever Cloud account and [Clever Tools](https://github.com/CleverCloud/clever-tools/) to deploy this application, using our Python image [now including](https://developers.clever-cloud.com/changelog/2024-10-01-python-image-changes/) `uv`.

## Clone this repository and deploy

```bash
git clone https://github.com/CleverCloud/python-fastapi-uv-example.git
cd python-fastapi-uv-example

clever create -t python

# If these environment variables and a `uv.lock` file are found, `uv` is used for deployment
clever env set CC_PYTHON_UV_SYNC_FLAGS -- "--locked --no-progress"
clever env set CC_PYTHON_UV_RUN_COMMAND ".venv/bin/fastapi run server.py --port 8080 --host 0.0.0.0"

clever deploy
```
