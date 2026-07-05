# base docker image that we will build on
FROM python:3.13.11-slim

# copy uv binary from official uv image (multi-stage build)
COPY --from=ghcr.io/astral-sh/uv:latest /uv /bin/

# set the working directory in the image
WORKDIR /app

# Add virtual environment to PATH so we can use installed packages
ENV PATH="/app/.venv/bin:$PATH"

# copy dependency files first (better layer caching)
COPY "pyproject.toml" "uv.lock" ".python-version" ./

# install dependencies from lock file (ensures reporoducible builds)
RUN uv sync --locked

# copy the pipeline.py file into the image
COPY pipeline.py pipeline.py

# set entry point
ENTRYPOINT ["python", "pipeline.py" ]