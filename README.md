# FastAPI with uv on Clever Cloud

You'll need a Clever Cloud account and [Clever Tools](https://github.com/CleverCloud/clever-tools/) to deploy this application, using our Python image [now including](https://developers.clever-cloud.com/changelog/2024-10-01-python-image-changes/) `uv`.

## Clone this repository and deploy

```bash
git clone https://github.com/CleverCloud/python-fastapi-uv-example.git
cd python-fastapi-uv-example

clever create -t python

clever env set CC_PRE_BUILD_HOOK "uv sync"
clever env set CC_RUN_COMMAND ".venv/bin/fastapi run server.py --port 9000 --host 0.0.0.0"

clever deploy && clever open

```
