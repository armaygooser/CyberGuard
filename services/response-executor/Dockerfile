FROM python:3.14.7-slim-bookworm@sha256:23c59390fc717bf09f9336908199a0ae75d9c4264bf296123f94ad772fea3b52

ENV PYTHONDONTWRITEBYTECODE=1 PYTHONUNBUFFERED=1 PIP_NO_CACHE_DIR=1
WORKDIR /app
COPY services/requirements.lock ./
RUN pip install --no-cache-dir --require-hashes -r requirements.lock \
    && pip check
COPY services/response-executor/app ./app
COPY services/response-executor/entrypoint.py ./
RUN useradd --system --uid 10002 --create-home cyberguard \
    && mkdir -p /data \
    && chown -R cyberguard:cyberguard /data /app
USER 10002
EXPOSE 8080
CMD ["python", "entrypoint.py"]
