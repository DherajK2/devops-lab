# ---------- STAGE 1 (Builder) ----------
FROM python:3.12-slim AS builder

WORKDIR /build

COPY requirements.txt .

RUN pip install --no-cache-dir --prefix=/install -r requirements.txt


# ---------- STAGE 2 (Final) ----------
FROM python:3.12-slim

WORKDIR /app

# Copy only installed packages
COPY --from=builder /install /usr/local

# Copy app code
COPY app.py .

ENV FLASK_ENV=production
ENV REDIS_HOST=redis

EXPOSE 5000

CMD ["gunicorn", "--bind", "0.0.0.0:5000", "--workers", "2", "app:app"]
