FROM python:3.15.0-slim-bookworm@sha256:0e019bbdfb5d9874cb2389f1c2884b64aa2ac97c99960b5bc521cef978c0617d

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    PIP_NO_CACHE_DIR=1

WORKDIR /app
COPY services/requirements.lock ./
RUN pip install --no-cache-dir --require-hashes -r requirements.lock \
    && pip check
COPY services/security-tool-gateway/app ./app
COPY services/security-tool-gateway/entrypoint.py ./

RUN useradd --system --uid 10001 --create-home cyberguard \
    && mkdir -p /data \
    && chown -R cyberguard:cyberguard /data /app
USER 10001

EXPOSE 8080
CMD ["python", "entrypoint.py"]
