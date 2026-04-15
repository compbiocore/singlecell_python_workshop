# Container automation assets

This directory contains the workshop Docker build context used by CI.

- `Dockerfile`: minimal workshop image with Python 3.12, Jupyter Notebook, and all packages listed in `requirements.txt`.

Build locally from the repository root:

```bash
docker build -f metadata/Dockerfile -t singlecell-python-workshop .
```
