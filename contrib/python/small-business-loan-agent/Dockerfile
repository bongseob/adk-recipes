FROM python:3.11-slim

RUN pip install --no-cache-dir uv==0.8.13

WORKDIR /code

COPY ./pyproject.toml ./README.md ./uv.lock* ./
COPY ./app ./app
COPY ./.env.example ./.env

RUN uv sync --frozen

RUN useradd --create-home --uid 1000 appuser && \
    chown -R appuser:appuser /code /home/appuser

USER appuser

EXPOSE 8080

CMD ["uv", "run", "adk", "api_server", "--host", "0.0.0.0", "--port", "8080", "."]
