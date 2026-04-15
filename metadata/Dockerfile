FROM python:3.12-slim

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    PIP_NO_CACHE_DIR=1

WORKDIR /workshop

RUN apt-get update && apt-get install -y --no-install-recommends \
    # Required for Python packages with native extensions.
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# Build context should be the repository root so requirements.txt is available at this path.
COPY requirements.txt /tmp/requirements.txt
RUN python -m pip install --upgrade pip && \
    python -m pip install -r /tmp/requirements.txt && \
    python -m pip install notebook

RUN useradd --create-home --uid 1000 workshop && chown -R workshop:workshop /workshop
USER workshop

EXPOSE 8888

CMD ["sh", "-c", "NOTEBOOK_FLAGS='--ip=0.0.0.0 --port=8888 --no-browser'; TOKEN=\"${JUPYTER_TOKEN:-$(python -c \"import secrets; print(secrets.token_urlsafe(24))\")}\"; echo \"Starting Jupyter Notebook with token authentication enabled.\"; jupyter notebook ${NOTEBOOK_FLAGS} --IdentityProvider.token=\"${TOKEN}\""]
