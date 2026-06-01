FROM python:3.12.13-trixie
WORKDIR /workshop
RUN /bin/sh -c apt-get update && apt-get install -y --no-install-recommends     build-essential     && rm -rf /var/lib/apt/lists/* # buildkit
COPY requirements.txt /tmp/requirements.txt
RUN /bin/sh -c python -m pip install --upgrade pip &&     python -m pip install -r /tmp/requirements.txt &&     python -m pip install notebook # buildkit
RUN /bin/sh -c useradd --create-home --uid 1000 workshop && chown -R workshop:workshop /workshop # buildkit
USER workshop
EXPOSE map[8888/tcp:{}]
CMD ["sh", "-c", "NOTEBOOK_FLAGS='--ip=0.0.0.0 --port=8888 --no-browser'; TOKEN=\"${JUPYTER_TOKEN:-$(python -c \"import secrets; print(secrets.token_urlsafe(24))\")}\"; echo \"Starting Jupyter Notebook with token authentication enabled.\"; jupyter notebook ${NOTEBOOK_FLAGS} --IdentityProvider.token=\"${TOKEN}\""]
